# Will Reynolds

Developer with a 20-year USAF background and an MBA in progress. Building production websites, data systems, and self-hosted infrastructure — solo, end-to-end, from architecture through deployment.

## What I've shipped

**[WJR Visuals](https://wjrvisuals.com)** — photography published in The Guardian, U.S. Army, and Photo-Weekly Germany. The portfolio scores 95 mobile / 98 desktop on PageSpeed, all Core Web Vitals green, accessibility 100/100 verified through screen-reader testing. Built across two stacks: an initial Next.js 15 App Router version, then rebuilt on Astro 6 + Cloudflare Workers with Cloudflare D1 for contact lead storage, build-time AVIF/WebP image generation at four widths per image via Sharp, and a scroll-driven essay reader written in vanilla TypeScript — no JS framework, no animation library beyond Lenis.

**[V Goal Visa Service](https://vgoalvisaservice.com)** — a multilingual consultancy site taken from effectively zero organic presence to position 1 on Google and Bing for branded queries, with sitelinks and AI overviews. Site-wide conversion sits at approximately 15%. ChatGPT referral accounts for roughly 9% of traffic and converts at approximately 58% — the highest of any channel, and the direct result of citation-friendly schema, server-rendered HTML, and explicit Author/Organization markup. Not an accident. Traffic grew roughly tenfold year-on-year, underpinned by a comprehensive Search Engine Optimisation (SEO) and analytics pipeline built on Google Analytics 4 (GA4) with Urchin Tracking Module (UTM) tagging for full attribution across channels. Performance is gated by Lighthouse CI running against the live URL via the PageSpeed Insights API on every PR, nightly, and post-merge — regressions open tracked issues with cooldown to avoid alert fatigue.

**[Developed by Will](https://developedbywill.com)** — my agency. Current focus is the trades vertical and small businesses that need a performance-grade web presence and a real leads pipeline, not a Wix or SquareSpace page with a form. The product underneath is an Astro + Cloudflare monorepo where client sites inherit CI/CD, schema infrastructure, and a Cloudflare D1 leads pipeline on day one. Turnstile server-side verification, D1 writes via prepared statements, Biome strict mode, path-filtered GitHub Actions per site, Lighthouse CI as a deploy gate. PSI ≥ 90, LCP ≤ 2.5s, total page weight ≤ 700KB — hard rules, enforced by CI, not by intention.

## Services

Four tiers of service. 

**Paid Site Audit — scope-based.** Forensic audit of an existing site: mobile + desktop PSI, competitor benchmarking against the top three in the operator's market, dollar-loss calculation specific to the trade, written findings report, Loom walkthrough. Credited toward a build within 60 days.

**New Site — one-time.** Up to 8 pages. Three-week build. Mobile-first design, on-site photography, schema markup, sitemap, robots, click-to-call and click-to-text wiring, Cloudflare Web Analytics, free monthly reports for the first 6 months, 30 days of post-launch edits. PSI 90+ mobile is contractual — drop below 90 in year one and I fix it free.

**Site + SEO Setup — one-time.** Everything in New Site plus the local-SEO groundwork most agencies bill monthly for: Google Business Profile rebuild, local schema for every service area, backlink cleanup, citation cleanup across 40+ directories, custom keyword research (~25 terms), 90 days of post-launch edits.

**Ongoing Retainer — optional add-on.** Monthly content updates, two new pages per quarter, quarterly PSI + SEO report, schema + sitemap maintenance, priority response (1 business day). No long-term contract. Most owners run the site themselves after launch — the retainer is the exception, not the default.

Full pricing posted publicly at [developedbywill.com/pricing](https://developedbywill.com/pricing) so prospective clients self-qualify before either of us commits.

## Research and data work

**[Thailand Livability Index](https://thailandliveabilityindex.com)** is a 77-province composite index across seven categories, sourced from public datasets and cited APA 7 from day one. Ingestion pulls from heterogeneous government and civic sources — TMD, MOPH, OpenAQ, ACLED, OSM, NASA FIRMS — through a Python ETL pipeline backed by DuckDB for analysis and Cloudflare R2 for artifact storage. Normalization uses Z-score / percentile-band methods with goalpost methodology; a `check-goalposts` step in CI validates reproducibility before any score can be published. The site is Astro 5 static output: 77 province pages, 82 zone pages, and per-indicator detail pages generated at build from a data fetch step that runs in `predev` and `prebuild` — the site cannot ship without a fresh score pull. Per-route OG images generated at build via resvg. JSON-LD across home, methodology, province, indicator, and FAQ pages. A versioned widget and public API (`/widget/v1/` + `/api/v1/`) with a written partner-embed contract, SRI manifest, and CORS and edge-cache rules designed before launch. Hosted on Cloudflare Pages.

Phase 1 closed April 2026. Phase 2 reached end-to-end production validation in week 1. MVP launch targets late August 2026; the first annual report ships December 2026 as a 15–20 page gated PDF with DOI, deposited to Zenodo and SSRN. Journal submission targets 2028–2029, to *Cities*, *Habitat International*, or *Environment and Planning B*.

**Supporting public repos:**

- **[thailand-livability-index](https://github.com/DevelopedbyWill/thailand-livability-index)** — companion repo: methodology, citations, and reproducible build steps.
- **[thailand-canonical-admin-names](https://github.com/DevelopedbyWill/thailand-canonical-admin-names)** — canonical English and Thai names for Thailand's administrative units at all three levels, with TIS-1099 and ISO 3166-2 codes, an override registry, computed centroids, and bundled polygons. CC BY 4.0, Zenodo DOI.
- **Thailand Wanderer** — a data-driven travel site that helps readers make informed decisions about where to go and when, built on the Thailand Livability Index data layer.

## Infrastructure I run

A VPS runs analytics, error monitoring, contracts, CRM, uptime monitoring, log viewer, and a form-capture API for my own portfolio of sites.

Each service runs in its own container with a dedicated Postgres user against a shared Postgres instance, least-privilege throughout. Plausible and Umami handle analytics; GlitchTip handles error monitoring (deliberately swapped in for Sentry SaaS to consolidate the observability stack onto owned infrastructure); Twenty handles CRM; DocuSeal handles contracts and signatures; Gatus drives public status pages; Caddy handles TLS and routing.

The `leads` service is the custom piece: five of my own sites POST into a single FastAPI + asyncpg endpoint. Per-project CORS allow-lists from a single source of truth. Turnstile server-side verification. IP-hash rate limiting. Postgres advisory locks for migration serialization. Best-effort Twenty CRM + email fan-out — each of the four steps (validation, Turnstile, Postgres write, CRM + email) can fail independently without losing the submission. One service, five sites; one fix, every site benefits.

## Stack

TypeScript + Astro / Next.js on the frontend; Python (FastAPI, asyncpg, DuckDB) on the backend; Postgres + object storage for state; Cloudflare Workers + Hetzner for compute; Caddy and Docker Compose for the platform underneath. pnpm workspaces and Biome for monorepo discipline.

## Background

20-year USAF career, transitioned into web and data engineering post-military. AWS Certified Cloud Practitioner. Microsoft Certified: Azure Administrator Associate. CompTIA Security+, Network+, A+. MBA in progress. Building things that are live and used, not demo repos.

## Connect

Methodology and tooling are public. Client codebases and production infrastructure stay private — happy to walk through architecture, trade-offs, and decision memos on request.

[developedbywill.com](https://developedbywill.com) for inquiries.
