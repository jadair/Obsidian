1. Add real page-level SEO metadata everywhere.  
    Refs: base.html (line 7), base.html (line 26), views.py (line 40)  
    Right now every page inherits the same fixed title, and there is no visible meta description, canonical URL, Open Graph, or Twitter metadata. This is the single biggest low-effort SEO gap. Add template blocks for title, meta description, canonical, og:title, og:description, and og:image, then set them per page. This will help queries like Senior Project, Drexel Senior Project, CCI Senior Project, Senior Project Showcase, and COEC Senior Project far more than cosmetic changes.
    
2. Rewrite the homepage title and hero copy to explicitly target the search phrases.  
    Refs: base.html (line 7), index.html (line 28)  
    The homepage H1 is branded but not keyword-rich: Real Students. Real Problems. Real Solutions. That is good marketing copy, but weak search copy. Keep it if you want, but add crawlable text above or below it that says something like Drexel CCI Senior Project Showcase and naturally mentions Senior Project, Drexel Senior Project, CCI Senior Project, and Senior Project Showcase. If COEC Senior Project matters, that acronym needs to appear in text too, not just in an image alt.
    
3. Add robots.txt and an XML sitemap, then expose them in URL routing.  
    Refs: urls.py (line 42)  
    There is no sitemap or robots route in the main URL config, and I did not find sitemap/robots support in the repo. That makes indexing harder than it needs to be. This is a high-impact, low-effort technical SEO fix.
    
4. Remove user-scalable=0 from the viewport meta tag.  
    Refs: base.html (line 8)  
    Blocking zoom is a clear accessibility problem and hurts mobile usability immediately. Change the viewport to a normal responsive value and allow pinch zoom.
    
5. Add a skip link and stronger visible keyboard focus styles.  
    Refs: base.html (line 29), main.css (line 82), home.css (line 114)  
    There is no skip-to-content link before the nav, and some controls rely on subtle color/background changes instead of a strong focus indicator. The hero slider explicitly removes outline on focus-visible. That is a quick accessibility win with very little implementation cost.
    
6. Replace the JS-only project gallery cards with real links, or at minimum render a server-side fallback.  
    Refs: project/index.html (line 12), project/index.html (line 303), project/index.html (line 593)  
    The gallery is rendered client-side and uses div role="link" plus JS navigation instead of normal anchor tags. That is weaker for SEO, weaker for accessibility, and worse for resilience. This is one of the few medium-effort items here, but it is worth doing because the projects page is likely your strongest long-tail search asset.
    
7. Add structured data on the public pages and project detail pages.  
    Refs: base.html (line 4), project/detail.html (line 30)  
    I did not find any JSON-LD. Add WebSite and EducationalOrganization on the site shell, CollectionPage on the projects page, and CreativeWork or SoftwareApplication-style structured data on project detail pages where appropriate. This is a strong SEO improvement without major design work.
    
8. Make image text alternatives more meaningful.  
    Refs: judges.html (line 80), project/detail.html (line 127)  
    Many judge photos use empty alt="", and screenshots use generic labels like Screenshot 1. If the image is informative, give it a meaningful alt. If it is purely decorative, keep empty alt consistently. This is easy cleanup with immediate accessibility value.
    
9. Use page-specific titles for project detail pages and category-like pages.  
    Refs: project/detail.html (line 30), project/urls.py (line 8)  
    A project detail page should not inherit the same generic site title as every other page. Use titles like Project Name | Drexel Senior Project Showcase. That is low effort and helps click-through from search results.
    

10. Consider adding readable slugs to project URLs after the quick wins are done.  
    Refs: project/urls.py (line 8)  
    UUID-only URLs are functional but not descriptive. This is not the first fix I would do, but project/<uuid>/<slug>/ is better for users and search snippets.
    

Open questions / assumptions:

- I reviewed the repo and public templates, not a live deployed site, so I could not verify Search Console coverage, real crawl behavior, Lighthouse scores, or Core Web Vitals.
- If COEC is still an important term for your audience, you should decide whether it is an active brand term you want intentionally in headings/meta copy, or just a legacy query to capture in supporting text.

If you want the fastest path, I would do these first in order:

1. Dynamic titles + descriptions + canonicals.
2. Homepage copy rewrite for the target terms.
3. robots.txt + XML sitemap.
4. Remove zoom blocking.
5. Skip link + stronger focus styles.

After that, the projects page rendering and structured data are the next best return.