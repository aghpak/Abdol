# EM Mastery Academy Non-Destructive Redesign Audit and Plan

Source reviewed: https://emmastery.academy, indexed public pages, public search excerpts, and visible page text. This audit is intentionally read-only and does not modify the live WordPress/Elementor site.

## Phase 1: Audit

### Page inventory observed

| Existing URL | Current role | Preserve requirements | Key findings |
|---|---|---|---|
| `/` | Homepage | URL, SEO metadata, forms, images, comments state, analytics | Current hero says “Master Emergency Medicine, Through Real Cases. For Real Practice.” Navigation is limited to Home, Learning Hub, Who We Are, Join. Homepage shows unsupported counters at zero, duplicated newsletter areas, footer category duplication, and “Blog” labels for clinical content. |
| `/learning-hub/` | Article archive / learning index | URL, query behavior, article links, filters if present | Needs heading changed from “What I’m Learning” to “Emergency Medicine Learning Hub”; requires robust search, filters, count, sort, pagination/load-more, and empty state. |
| `/who-we-are/` | About page | URL unless renamed with redirect; page content; faculty details | Contains useful mission/founder content but also broad promotional claims around community, mentorship, study groups, networking, and programs that should not appear unless operational. |
| `/join/` | Contribution form | URL, form fields, submissions, integrations | Destination should be labeled “Contribute,” not “Join.” Contains unsupported “world’s most comprehensive” claim and insufficient publication policy details. Preserve form data and submission handling. |
| `/privacy-policy/` | Public policy page currently showing publication-policy content in search | URL, legal/policy content, metadata | Public search shows “publication-policy” content under Privacy Policy URL, creating policy/SEO mismatch risk. Validate in WordPress before editing. |
| `/category/em-core/` | Category archive | URL, slug, category assignment | Footer shows category duplication and inconsistent brand capitalization. |
| `/category/pocus/` | Category archive | URL, slug, category assignment | Preserve archive URL; improve archive template. |
| `/category/case-study/` | Category archive | URL, slug, category assignment | Preserve archive URL; map to Clinical Cases navigation. |
| `/category/blog/` | Generic category archive | URL, slug, category assignment | Avoid using “Blog” as the visible label for all clinical content. Keep existing category until taxonomy migration is approved. |
| Article URLs, e.g. `/optimizing-airway-management-five-key-plans/`, `/essential-steps-for-treating-toxicology-emergencies/`, `/understanding-brash-syndrome-causes-and-effects/`, `/step-by-step-guide-to-safe-ventilation-techniques-in-the-emergency-room/`, `/2025-hypertension-guidelines-updates-for-emergency-care/` | Long-form medical education articles | URL, slug, title, author, publication date, modified date, category, tags, featured image, alt text, references, comments, SEO fields, schema | Article template needs consistent evidence metadata, one H1, table of contents, references, disclaimer, biographies, related resources, callouts, and accessible comments only if moderated. |
| Date archives, e.g. `/2026/06/23/` | WordPress date archive | URL/indexing decision | Preserve if indexed; evaluate noindex policy only after SEO review. |

A complete production inventory must be exported from WordPress before implementation using WP-CLI or a read-only database export. Required fields: `ID`, `post_type`, `post_status`, `post_title`, `post_name`, `post_date`, `post_modified`, `post_author`, `author_display_name`, permalink, parent, template, excerpt, content hash, featured image ID, featured image URL, image alt, categories, tags, custom taxonomies, comments count/status, SEO title, SEO description, canonical, Open Graph image/title/description, schema settings, redirects, form IDs, newsletter integration IDs, and analytics/verification snippets.

### Content-type inventory

- WordPress pages: homepage, learning hub, about/who-we-are, join/contribute, privacy/policy pages.
- WordPress posts: clinical articles, practical guides, case studies, POCUS content, resuscitation/critical care content, pitfalls, evidence updates.
- Category archives: EM Core, POCUS, Case Study, Blog, and likely Critical Care/Pitfalls where linked in footer snippets.
- Author archives: at least Dr. Abdolghader Pakniyat; verify Dr. Sabrina Berdouk and additional contributors.
- Forms: contribution form and newsletter signup forms; preserve submission storage and integrations.
- Comments: visible comment/loading UI appears on homepage; audit where comments are intentionally enabled.
- Media: featured images and article images with existing alt text.
- Policy/legal content: publication policy, privacy policy, disclaimer, terms, conflict-of-interest policy, contributor guidelines.

### Category and taxonomy review

Current visible categories include EM Core, POCUS, Case Study, Blog, Critical Care, and Pitfalls. Recommended future taxonomy model is non-destructive:

- Preserve existing categories and slugs.
- Add parent/child structure only after export and redirect review.
- Add `content_type` taxonomy: Clinical Review, Case Study, Practical Guide, Evidence Update, Procedure Guide, Algorithm, Commentary.
- Add optional `clinical_topic` taxonomy if current categories are too broad: Airway, Toxicology, Cardiology, Neurology, Trauma, Procedures, POCUS, Resuscitation, Critical Care, Pitfalls.
- Do not bulk rename “Blog” until each post is mapped and a redirect/indexing plan exists.

### Existing user journeys

- Google-arriving clinician can reach articles but article cards and templates do not yet prioritize rapid clinical scanning.
- Regular reader sees recent articles on the homepage but needs clearer “Latest Learning” and archive filters.
- Topic browser has category archives but needs stronger pathway cards and filters.
- Programs/workshops user journey is not currently confirmed; do not advertise dates, prices, CME, or active courses.
- Contributor journey exists at `/join/` but needs clearer eligibility, de-identification, AI disclosure, review, attribution, and rights language.
- Partnership journey is weak; add a restrained education partnership CTA without claiming active partnerships.
- Newsletter journey is duplicated on homepage and footer; consolidate to one homepage section plus footer link/signup if required.

### Issues and risks

- Broken/mismatched calls to action: homepage “Explore Cases” points to Join rather than Clinical Cases; “Join” is ambiguous.
- Duplicate sections: public homepage text shows repeated nav blocks, duplicate category groups, and duplicate newsletter/signup areas.
- Inconsistent branding: “EM Mastery Academy,” “Em Mastery Academy,” and “Emmastery Academy” appear in public text.
- Unsupported claims: homepage counters display zero values; Join page claims “world’s most comprehensive emergency medicine learning resource”; About page references mentorship, study groups, community, and programs that may not exist.
- Accessibility issues: repeated navigation text, ambiguous image labels, generic links, potential comments loading text, form labels/consent requiring validation, and likely focus/keyboard issues in mobile menu.
- Mobile issues: repeated mobile navigation blocks and potential Elementor duplication suggest risk of screen-reader noise and layout bloat.
- SEO risks: generic “Blog” labeling, duplicate footer categories, possible privacy/publication-policy mismatch, unclear schema, and unsupported publication/review labels.
- Data-preservation risks: renaming pages, categories, or rebuilding Elementor templates can accidentally alter slugs, dates, authors, SEO fields, form records, and comments unless implementation is staged and field-mapped.

## Phase 2: Proposed Structure

### Revised sitemap

- Home `/`
- Learning Hub `/learning-hub/`
  - Topic archive filters: EM Core, Resuscitation, Critical Care, POCUS, Trauma, Airway, Toxicology, Cardiology, Neurology, Procedures, Clinical Pitfalls
  - Content-type filters: Clinical Review, Case Study, Practical Guide, Evidence Update, Procedure Guide, Algorithm, Commentary
- Clinical Cases: existing Case Study category archive or `/clinical-cases/` only if created with redirects/internal links validated
- POCUS: existing `/category/pocus/`
- Resuscitation and Critical Care: existing category archive or curated landing page if content exists
- Programs: restrained “Programs are being developed” or hide until confirmed
- About: preserve `/who-we-are/` or create `/about/` only with 301 from old URL after approval
- Contribute: preserve `/join/` destination, relabel in navigation as “Contribute”; optionally create `/contribute/` later with 301 plan
- Footer: Contact, Editorial and Peer-Review Policy, Medical Disclaimer, Privacy Policy, Terms of Use, Conflict-of-Interest Policy, Contributor Guidelines, active social links only

### Navigation model

Primary header: Home, Learning Hub, Clinical Cases, POCUS, Resuscitation and Critical Care, Programs, About, Contribute. Utility: search icon and “Explore the Learning Hub” button. Mobile: single accessible menu button, search, then stacked navigation with 44px minimum targets.

### Homepage wireframe

1. Sticky header.
2. Hero: “Emergency Medicine Education for Decisions That Cannot Wait,” supporting text, Explore Learning Hub, Browse Clinical Cases, Subscribe link, and restrained POCUS/decision-pathway visual.
3. Learning pathways: six cards for EM Core, Resuscitation and Critical Care, POCUS, Clinical Cases, Procedures, Clinical Pitfalls.
4. Featured clinical resource: one selected article with real metadata and review badge only if documented.
5. Latest Learning: six recent articles, no generic Blog label.
6. Why EM Mastery Academy: Frontline relevance, Evidence-informed teaching, Case-based learning, Independent clinical education.
7. Faculty and Editorial Leadership: verified structured profiles.
8. Programs/Education Partnerships: future services, no dates/prices/CME unless confirmed.
9. Contributor CTA: “Share Your Clinical Experience.”
10. Single newsletter section with consent and privacy link.
11. Footer with mission, navigation, clinical categories, policies, contact, social, dynamic year.

### Learning Hub wireframe

- Header: Emergency Medicine Learning Hub and concise positioning text.
- Search bar with label and submit button.
- Filters: topic, content type, author, publication year, sort; clear filters.
- Results summary: “Showing X resources.”
- Cards: image, category/topic, title, summary, author, date, reading time, review status if documented.
- Pagination or accessible Load More.
- Empty state: “No resources match these filters. Clear filters or try a broader topic.”

### Article-template wireframe

- Breadcrumbs.
- Article header: category, H1, dek/excerpt, author, reviewer, original date, updated date, reading time, evidence/review status.
- Featured image with preserved alt text.
- Key takeaways box.
- Desktop two-column layout: sticky TOC + article body; mobile collapsible TOC.
- Article body with reusable callouts.
- References.
- Medical education disclaimer.
- Author/reviewer biographies.
- Related learning resources.
- Newsletter CTA.
- Comments only where actively moderated.

### About-page wireframe

Mission, What We Teach, Educational Approach, Editorial Standards, Founders and Faculty, Who the Platform Serves, Education Partnerships, Contact.

### Contributor-page wireframe

Contribute to EM Mastery Academy, accepted submission types, eligibility, patient de-identification, originality, references, conflicts, AI disclosure, editorial/peer review, response process, editing/publication rights, authorship/attribution, rejection/revision process, link to full publication policy, existing preserved form.

## Phase 3: Visual Direction

### 1. Clinical Editorial

Deep navy, warm paper background, editorial article typography, restrained teal accents, strong article cards, and clinical callouts. Best for a serious learning platform with long-form evidence-based content.

### 2. Modern Academic

Charcoal/navy base, grid-heavy archive pages, structured metadata, institutional calm, minimal imagery, and policy/editorial emphasis. Best for credibility and partnerships, slightly less warm for daily readers.

### 3. Premium POCUS Education

Dark navy with ultrasound-inspired panels, cyan linework, image-led POCUS cards, and procedural visual language. Best if POCUS becomes the flagship vertical, but may over-narrow the brand.

### Recommendation

Use **Clinical Editorial** as the primary direction with selective POCUS visual motifs. It best balances evidence-based authority, practical bedside learning, calm trust, and broad emergency medicine coverage without looking like a hospital template or generic online course.

## Phase 4: Prototype scope

A responsive, static, clickable prototype is included in `/prototype/index.html` and `/prototype/styles.css`. It uses sample content and existing public article titles only; it does not connect to the live WordPress database and is not deployed.

## Phase 5: WordPress Implementation Plan

### Elementor templates/components

Global header, mobile menu, global footer, article archive card, featured article card, category/pathway card, faculty profile card, newsletter form, contributor CTA, clinical callout boxes, single-post template, category archive template, author archive template, search-results template, 404 page, legal-page template.

### Required dynamic fields

Post title, excerpt, content, permalink, featured image, image alt text, categories, tags, author, reviewer, original publication date, modified date, last clinically reviewed date, reading time, evidence/review status, references, key takeaways, related resources, author credentials, conflict disclosures, schema fields, SEO metadata, canonical URL, Open Graph fields, comments state.

### Plugin requirements

Elementor Pro or equivalent theme builder, SEO plugin with schema controls, ACF or Meta Box for structured fields, faceted search/filter plugin compatible with Elementor, SMTP/form storage plugin, backup plugin, caching/performance plugin, accessibility testing support, redirect manager only if URL changes are approved.

### Migration mapping

No migration before complete inventory. Map old field to new display field one-to-one. Use dynamic fields rather than copying article content into Elementor widgets. Keep slugs, dates, authors, categories, tags, media IDs, alt text, comments, SEO data, and form entries intact.

### Redirect requirements

No redirects expected for the prototype. If `/join/` becomes `/contribute/` or `/who-we-are/` becomes `/about/`, retain the old URLs with 301 redirects and update internal navigation only after verifying indexed URL status.

### Backup and staging procedure

1. Full filesystem backup.
2. Full database backup.
3. Export media library manifest.
4. Export SEO/plugin settings.
5. Export forms and subscribers.
6. Create staging copy on separate URL with noindex and blocked indexing.
7. Validate staging parity before design work.
8. Build Elementor templates on staging.
9. Run acceptance tests.
10. Schedule controlled launch with rollback package ready.

### Testing checklist

URL crawl, content parity, metadata parity, authors/dates, categories/tags, images/alt text, forms, newsletter, comments, search, filters, mobile, keyboard, screen reader spot checks, WCAG contrast, schema validation, sitemap, analytics, redirects, performance, legal pages, disclaimers.

### Rollback plan

Keep pre-launch database and filesystem backups, document all template/plugin changes, maintain old theme/template versions, avoid destructive migrations, and restore previous templates/database if launch validation fails.

## Phase 6: Acceptance Testing

- Verify every existing URL from sitemap and Search Console export.
- Verify every article and page renders with unchanged title, slug, author, publication date, modified date, category, tag, image, alt text, references, comments, and SEO fields.
- Verify forms submit to the same storage/integration and existing submissions remain accessible.
- Verify newsletter consent and unsubscribe language.
- Verify search, filters, pagination/load more, and empty states.
- Verify mobile layouts at common breakpoints.
- Verify accessibility: keyboard, focus, menu, modals, filters, accordions, labels, errors, contrast, reduced motion.
- Verify metadata, schema, canonicals, Open Graph, sitemap, analytics, redirects, and Search Console verification.
- Verify performance: LCP, CLS, INP, image optimization, lazy loading, and third-party script control.
- Verify medical disclaimers and legal/policy pages are accurate and accessible.
