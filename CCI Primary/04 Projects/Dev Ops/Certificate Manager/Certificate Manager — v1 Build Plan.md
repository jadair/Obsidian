
## The gap you're filling

Free tools that monitor certificates **on the wire** are everywhere. Free tools that find certificates **on disk across a fleet** — in nginx configs pointing at `/opt`, inside Java keystores, in PKCS#12 bundles — essentially don't exist. [Keyfactor does it commercially](https://software.keyfactor.com/Core-OnPrem/v11.5/Content/ReferenceGuide/Certificate%20Store%20Discovery.htm); nothing free does it well.

**The one thing this app does that others cannot:**

> Find every certificate on a fleet of internal Linux servers — including ones in non-standard paths and non-file containers — and tell you which are about to expire, and which were renewed on disk but never actually loaded by the service.

---

## Non-goals for v1

Explicit, so they don't creep back:

- **No writes to managed servers.** Read-only. This deletes approval gating, maintenance windows, rollback, job queues, and most of §5 — ~60 of the original 98 requirements exist only to make writes safe.
- **No patching.**
- **No ACME / renewal.** Blocked on unanswered questions (your CA, DNS API access, key custody).
- **No Windows.** You don't yet know if you have any.
- **No filesystem scan.** Layers 1–3 find ~98% of certs without an I/O storm.

---

## Stack — all free, all permissive

|Piece|Choice|Why|
|---|---|---|
|Language|Python 3.12|Best cert + SSH libraries|
|Web|Django 5 + Django admin|Admin gives you CRUD free; you write two real views|
|DB|PostgreSQL|Free. SQLite fine to start|
|SSH|`asyncssh`|Async, no shell-out, native concurrency|
|Cert parsing|`cryptography`|PEM, DER, PKCS#12 all built in|
|Java keystores|[`pyjks`](https://github.com/kurtbrose/pyjks)|Pure Python, JKS/JCEKS/BKS, no JVM needed|
|Scheduling|`cron` → management command|Not Celery. Not yet.|
|Email|`smtplib` via Django|Already there|

**Deliberately not used:** Celery/Redis (cron is enough at this scale), Docker orchestration, any JS framework, NetBox (it's [free](https://netboxlabs.com/docs/netbox/), but it's a documentation store that [doesn't scan](https://github.com/netbox-community/netbox/discussions/7303) — it'd be a dependency that solves nothing here).

---

## Data model — 6 tables

The two splits worth keeping from the original doc, because retrofitting them means a migration:

```python
Server
  hostname, platform_family, platform_version
  state: ok | unreachable | partial
  last_error, last_seen_at

Service                      # nginx, apache2, postfix...
  server → Server
  name, config_paths[]

Certificate                  # deduped by fingerprint, fleet-wide
  fingerprint_sha256 (unique)
  subject_cn, sans[], issuer, serial
  valid_from, valid_to
  key_algorithm, key_size, signature_algorithm

CertificateInstallation      # one cert, one server, one location
  certificate → Certificate
  server → Server
  location_type: file | pkcs12 | jks
  path, keystore_alias
  discovered_by: conventional | config_parse | admin_path | on_wire
  served_on_ports[]
  status: in_sync | stale_on_disk | mismatch | key_missing | unattributed

SearchPath                   # admin says "also look here"
  server → Server (nullable = global)
  path_or_glob

AlertLog                     # dedup + don't re-send
  dedupe_key, certificate → Certificate
  threshold_days, sent_at
```

**Why `Certificate` ≠ `CertificateInstallation`:** a wildcard on 12 servers is **one** certificate with **twelve** installations. Get this wrong and every wildcard generates 12 duplicate alerts, and you can't answer "where is this cert deployed?"

**Why `location_type`:** a cert in a JKS expires exactly like one in `/etc/ssl`. Bolting keystores on later means migrating every row.

Everything else from the original §7 — `DiscoveredFact` history, tags, groups, jobs, policies, maintenance windows — is gone.

---

## Two protocols, five methods

Only what has a real implementation and a real caller on day one:

```python
class FactProvider(Protocol):
    async def probe(self) -> Platform: ...
    async def discover_facts(self) -> Facts: ...
    async def enumerate_services(self) -> list[Service]: ...

class CertificateStore(Protocol):
    async def find_certificate_paths(self) -> list[CertPath]: ...
    async def read_certificate(self, path: CertPath) -> bytes: ...
```

Two implementations: `DebianAdapter` and `PosixAdapter` (fallback — `uname`, `cat`, `find` only). An unknown OS gets the POSIX adapter and lands as `partial`, never as a failure.

`install_certificate` joins `CertificateStore` when you build installation. `PackageManager` gets defined only if you decide against AWX. Not before.

---

## Discovery — three layers

**Layer 1 — Conventional paths.** `/etc/ssl`, `/etc/pki`, `/etc/letsencrypt`, `/etc/nginx`, `/etc/apache2`, `/etc/httpd`.

**Layer 2 — Config parsing.** ← _the differentiating layer._ Read nginx/Apache/Postfix/Dovecot/HAProxy configs, extract `ssl_certificate` / `SSLCertificateFile` / equivalent directives. This finds certs in `/opt`, `/srv`, app dirs, NFS mounts — wherever they actually point. **This is what free tools don't do.** It also gives you the cert→service mapping for free, which is what makes stale-on-disk detection possible.

**Layer 3 — Admin-defined paths.** An admin who knows a cert lives somewhere odd just says so.

**Plus: on-the-wire.** Connect to listening TLS ports, read what's presented.

**Then the comparison that is the whole point:**

```
on-disk cert  ≠  on-wire cert  →  stale_on_disk
on-wire SANs  ∌  hostname      →  mismatch
disk cert     ∌  any service   →  unattributed  (still alerted, never dropped)
```

---

## Build order

**Week 1 — Connect and identify.** `asyncssh` connect, host key recorded on first contact and verified after, `probe()`, `DebianAdapter` + `PosixAdapter`, Server model, unreachable-state handling with the specific error. _Done when: add a hostname, get back OS and version._

**Week 2 — Find certs on disk.** Layers 1–3, parse PEM/DER/PKCS#12/JKS, dedupe by fingerprint, populate Certificate + Installation. _Done when: point at a real server, get every cert it holds._

**Week 3 — Find certs on the wire + compute status.** TLS port scan, fingerprint comparison, status computation, stale-on-disk detection. _Done when: the app catches a cert you renewed but never reloaded._

**Week 4 — Make it visible and loud.** Dashboard (expiry timeline, counts by status, soonest-first), server detail, cert detail. Email alerts at 60/30/14/7/3/1 days, deduped by `dedupe_key` so a wildcard on 50 servers sends **one** email listing 50 installations. Cron entry for daily discovery + 6-hourly cert checks. _Done when: you get one useful email and no duplicates._

**Week 5 — Make it safe to leave running.** SSO (protocol TBD — the one open question that can actually block you), viewer/admin split, encrypted credential storage, key-material redaction in logs, HTTPS + CSRF.

Five weeks to something genuinely useful. Roughly 24 of the original 98 requirements.

---

## Security — non-negotiable even in a read-only v1

Not YAGNI, because retrofitting means auditing every call site after a compromise:

- SSH private key **encrypted at rest**, key from env/secrets file, never in the DB plaintext or in git
- Host keys recorded on first contact; **later mismatch fails the connection and alerts**
- All remote commands **parameterized** — admin search paths (Layer 3) are untrusted input; a glob is a command argument, and injection here is fleet-wide root
- Key material **redacted** from all logs and output capture
- Uploaded/parsed cert material handled defensively — malformed input fails clean
- HTTPS only, CSRF on, RBAC enforced server-side
- Not exposed to the public internet

Bonus of read-only v1: the sudo allowlist is nearly empty. Discovery mostly needs plain file reads.

---

## What you'll know in 5 weeks that you can't know now

Ship this and real data answers the questions the requirements doc is currently guessing at:

- **Actual OS spread** → which adapter to write next (§10 Q3 predicted exactly this)
- **Whether Windows servers exist and serve TLS** → whether Phase 5 matters at all
- **Which apps hold non-standard certs** → validates Layer 2 against reality
- **Who issues your certs** → whether renewal is ACME, internal CA, or both

Then decide on installation and renewal, with evidence instead of speculation.

---

Want me to scaffold Week 1 — Django project, the two protocols, `DebianAdapter`, and the Server model with real `asyncssh` probing?

**Sources:** [PyJKS](https://github.com/kurtbrose/pyjks) · [NetBox open source](https://netboxlabs.com/docs/netbox/) · [NetBox discovery limits](https://github.com/netbox-community/netbox/discussions/7303) · [Ansible AWX](https://docs.ansible.com/projects/awx/en/24.6.1/userguide/overview.html) · [Keyfactor cert store discovery](https://software.keyfactor.com/Core-OnPrem/v11.5/Content/ReferenceGuide/Certificate%20Store%20Discovery.htm)