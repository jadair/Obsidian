### Phase 1: Set Up DocuSign API Access

**1. Create a DocuSign Integration Key**

1. Log into your DocuSign account → go to **Settings** (top right)
2. Navigate to **Apps and Keys** (under Integrations)
3. Click **Add App and Integration Key**
4. Give it a name (e.g., "PowerAutomate Flow")
5. Under **Authentication**, select **Authorization Code Grant**
6. Add a **Redirect URI** — use `https://global.consent.azure-apim.net/redirect` (Power Automate's OAuth redirect)
7. Copy and save:
    - **Integration Key** (this is your Client ID)
    - **Secret Key** (generate one and copy it immediately)
    - **API Account ID** (found on the Apps and Keys page)

---

### Phase 2: Get Your OAuth Token (One-Time Setup)

You need to do this manually the first time to get a refresh token.

**1. Build the authorization URL and paste it into your browser:**

```
https://account.docusign.com/oauth/auth?response_type=code&scope=signature%20extended&client_id=YOUR_INTEGRATION_KEY&redirect_uri=https://global.consent.azure-apim.net/redirect
```

**2.** Log in and consent. You'll be redirected to a URL like:

```
https://global.consent.azure-apim.net/redirect?code=XXXXXXXX
```

Copy the `code` value.

**3.** Exchange the code for tokens using Postman or any REST client:

- **Method:** POST
- **URL:** `https://account.docusign.com/oauth/token`
- **Body (x-www-form-urlencoded):**

```
grant_type=authorization_code
code=YOUR_CODE_FROM_ABOVE
client_id=YOUR_INTEGRATION_KEY
client_secret=YOUR_SECRET_KEY
redirect_uri=https://global.consent.azure-apim.net/redirect
```

You'll get back a JSON response with an `access_token` and a `refresh_token`. **Save the refresh_token** — you'll store it in Power Automate.

---

### Phase 3: Store the Refresh Token Securely

The cleanest place to store secrets in Power Automate is **Environment Variables** (if your admin allows it) or a **SharePoint list** with a single row. The SharePoint list approach is simplest:

1. Create a SharePoint list called `DocuSign_Config`
2. Add columns: `refresh_token` (single line text), `access_token` (single line text)
3. Create one item and paste your refresh token in

---

### Phase 4: Build the Power Automate Flow

Go to **make.powerautomate.com → Create → Scheduled Cloud Flow**

---

#### Step 1 — Trigger: Recurrence

- Interval: `30`, Frequency: `Minute`

---

#### Step 2 — Get Refresh Token from SharePoint

- Action: **SharePoint → Get Items**
- Site: your site, List: `DocuSign_Config`
- This retrieves your stored refresh token

---

#### Step 3 — HTTP: Exchange Refresh Token for Access Token

- Action: **HTTP**
- Method: `POST`
- URI: `https://account.docusign.com/oauth/token`
- Headers:

```
  Content-Type: application/x-www-form-urlencoded
```

- Body:

```
  grant_type=refresh_token&refresh_token=REFRESH_TOKEN_FROM_STEP_2&client_id=YOUR_INTEGRATION_KEY&client_secret=YOUR_SECRET_KEY
```

- After this action, add **Parse JSON** on the response body. Schema fields you need: `access_token`, `refresh_token`

---

#### Step 4 — Update Stored Refresh Token

- Action: **SharePoint → Update Item**
- Write the new `refresh_token` from Step 3 back to your config list (tokens rotate on each use)

---

#### Step 5 — Calculate `from_date`

- Action: **Initialize Variable**
- Name: `from_date`, Type: String
- Value (expression):

```
  addMinutes(utcNow(), -35)
```

This gives you a 35-minute lookback window with a little overlap buffer.

---

#### Step 6 — HTTP: List Completed Envelopes

- Action: **HTTP**
- Method: `GET`
- URI:

```
  https://na4.docusign.net/restapi/v2.1/accounts/YOUR_API_ACCOUNT_ID/envelopes?status=completed&from_date=@{variables('from_date')}
```

> **Note:** Replace `na4` with your correct DocuSign server (check your account URL — it may be `na2`, `na3`, `eu1`, etc.)

- Headers:

```
  Authorization: Bearer ACCESS_TOKEN_FROM_STEP_3
  Accept: application/json
```

- Add **Parse JSON** on the response. Key field from schema: `envelopes` (array), each with `envelopeId`, `emailSubject`, `status`

---

#### Step 7 — Apply to Each Envelope

- Action: **Apply to each**
- Input: `envelopes` array from Step 6

Inside the loop:

**Step 7a — HTTP: Download the Completed PDF**

- Method: `GET`
- URI:

```
  https://na4.docusign.net/restapi/v2.1/accounts/YOUR_API_ACCOUNT_ID/envelopes/@{items('Apply_to_each')?['envelopeId']}/documents/combined
```

- Headers:

```
  Authorization: Bearer ACCESS_TOKEN_FROM_STEP_3
```

- **Important:** Set **"Format"** in the HTTP action advanced settings to retrieve binary content (the response will be the raw PDF bytes)

**Step 7b — SharePoint: Create File**

- Action: **SharePoint → Create File**
- Site Address: your SharePoint site
- Folder Path: `/Shared Documents/DocuSign Completed` (or wherever you want)
- File Name expression:

```
  @{items('Apply_to_each')?['emailSubject']}_@{utcNow('yyyyMMdd')}.pdf
```

- File Content: output of the HTTP action from Step 7a (the raw body)

---

### Phase 5: Test It

1. Save the flow and click **Test → Manually**
2. Watch the run history for any failed steps
3. Common issues:
    - Wrong DocuSign server URL (`na4` vs `na2` etc.) — check your DocuSign account URL in the browser
    - Token expiry — make sure the refresh token update in Step 4 is writing back correctly
    - Binary content — if the PDF saves but is corrupted, make sure you're not accidentally passing the body through Parse JSON before writing to SharePoint

---

### Quick Reference: Your DocuSign Base URL

|Account URL you see in browser|Base API URL|
|---|---|
|`app.docusign.com`|`na4.docusign.net`|
|`na2.docusign.com`|`na2.docusign.net`|
|`eu.docusign.com`|`eu1.docusign.net`|

Check your browser URL when logged into DocuSign to confirm which server you're on.

---

That's the full implementation. The most failure-prone parts in practice are the token refresh logic (Step 3/4) and the binary PDF download (Step 7a) — let me know if you hit a snag on either of those.

#docusign #onedrive