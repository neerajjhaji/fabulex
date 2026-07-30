# Fab Luxe — SEO & Social Media Strategy

**Domain:** `https://fabluxe.co.in`
**Brand:** Fab Luxe
**Positioning:** Luxury apartments & premium interior execution — Greater Noida West
**Document type:** Production-ready technical SEO + social distribution playbook
**Last updated:** 2026-07-30

> **How to use this doc:** Everything in code fences is copy-paste ready. Values wrapped in `{{DOUBLE_BRACES}}` are placeholders you must replace with real data (phone numbers, coordinates, social URLs, image paths) before shipping. Search the file for `{{` to find every one.

---

## Table of Contents

1. [Technical & On-Page SEO Framework](#1-technical--on-page-seo-framework)
   - [1.1 Meta Tags Strategy](#11-meta-tags-strategy)
   - [1.2 Open Graph & Twitter Cards](#12-open-graph--twitter-cards)
   - [1.3 Canonical URLs & Hreflang](#13-canonical-urls--hreflang)
   - [1.4 Structured Data (JSON-LD)](#14-structured-data-json-ld)
2. [Social Media Integration & Open Graph Audit](#2-social-media-integration--open-graph-audit)
   - [2.1 Social Preview Optimization](#21-social-preview-optimization)
   - [2.2 Cross-Platform Content Distribution](#22-cross-platform-content-distribution)
   - [2.3 Social Profiles Schema (sameAs)](#23-social-profiles-schema-sameas)
3. [Technical SEO Google Indexing Architecture](#3-technical-seo-google-indexing-architecture)
   - [3.1 XML Sitemap Specs](#31-xml-sitemap-specs)
   - [3.2 Robots.txt Optimization](#32-robotstxt-optimization)
   - [3.3 Core Web Vitals Blueprint](#33-core-web-vitals-blueprint)
4. [Claude Code Implementation Script](#4-claude-code-implementation-script)

---

## Global Placeholder Reference

Replace these once and reuse everywhere:

| Placeholder | Meaning | Example |
|---|---|---|
| `{{PHONE_E164}}` | Phone in E.164 | `+91-120-XXXXXXX` |
| `{{EMAIL}}` | Contact email | `sales@fabluxe.co.in` |
| `{{STREET}}` | Street address | `Plot XX, Sector XX` |
| `{{LOCALITY}}` | City/area | `Greater Noida West (Bisrakh)` |
| `{{REGION}}` | State | `Uttar Pradesh` |
| `{{POSTAL}}` | PIN code | `201306` |
| `{{LAT}}` / `{{LNG}}` | Geo coordinates | `28.6100` / `77.4300` |
| `{{IG_URL}}` | Instagram profile | `https://www.instagram.com/fabluxe` |
| `{{FB_URL}}` | Facebook page | `https://www.facebook.com/fabluxe` |
| `{{LI_URL}}` | LinkedIn company page | `https://www.linkedin.com/company/fabluxe` |
| `{{YT_URL}}` | YouTube channel | `https://www.youtube.com/@fabluxe` |
| `{{PIN_URL}}` | Pinterest profile | `https://www.pinterest.com/fabluxe` |
| `{{TWITTER_HANDLE}}` | X/Twitter handle | `@fabluxe` |

---

# 1. Technical & On-Page SEO Framework

## 1.1 Meta Tags Strategy

**Pixel-length rules (enforce, don't just count characters):**

- **Title:** target **≤ 580px** (~50–60 chars). Google truncates titles near 600px. Front-load the primary keyword; put brand last after a `|`.
- **Description:** target **≤ 920px** (~140–155 chars). Include the primary keyword once + one CTA verb + one differentiator (AQI, RERA, possession).
- One `<title>` and one `<meta name="description">` per URL. Never duplicate across pages.

### Homepage

```html
<title>Luxury Apartments in Greater Noida West | Fab Luxe</title>
<meta name="description" content="Fab Luxe offers AQI-managed 3 & 4 BHK luxury residences in Greater Noida West with bespoke interior execution. Book a private site visit today.">
```

### Luxury Apartments — 3 BHK

```html
<title>3 BHK Luxury Apartments in Greater Noida West | Fab Luxe</title>
<meta name="description" content="Own an AQI-managed 3 BHK luxury residence in Greater Noida West. Premium fittings, curated amenities & RERA-ready homes. Enquire for pricing & floor plans.">
```

### Luxury Apartments — 4 BHK

```html
<title>4 BHK Luxury Residences, Greater Noida West | Fab Luxe</title>
<meta name="description" content="Spacious 4 BHK luxury residences with AQI-managed living & designer interiors in Greater Noida West. Limited units. Schedule your walkthrough with Fab Luxe.">
```

### Interior Execution Services

```html
<title>Luxury Interior Execution Services | Fab Luxe</title>
<meta name="description" content="Turnkey luxury interior execution for apartments & villas — design to handover. Premium materials, transparent timelines & site-managed delivery by Fab Luxe.">
```

### Contact

```html
<title>Contact Fab Luxe | Luxury Homes & Interiors, Greater Noida</title>
<meta name="description" content="Talk to Fab Luxe about 3 & 4 BHK luxury apartments and interior execution in Greater Noida West. Call, WhatsApp, or book a private consultation online.">
```

### Dynamic template (server/SSG)

Use this pattern in your templating layer (Next.js `generateMetadata`, Nunjucks, Liquid, etc.):

```txt
TITLE  = {{PrimaryKeyword}} in {{Location}} | Fab Luxe        # ≤ 60 chars
DESC   = {{ValueProp}} {{Location}} with {{Differentiator}}. {{CTA}}.  # ≤ 155 chars

Rules:
- PrimaryKeyword pulled from page taxonomy (e.g., "3 BHK Luxury Apartments")
- Differentiator rotates: "AQI-managed living" | "RERA-ready" | "designer interiors"
- CTA rotates: "Book a site visit." | "Request floor plans." | "Enquire now."
- Never emit an empty description — fall back to the homepage description.
```

**Supporting head tags for every page:**

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="robots" content="index, follow, max-image-preview:large">
<meta name="theme-color" content="#0E0E0E">
<meta name="format-detection" content="telephone=yes">
```

> On staging, thank-you, and filtered/faceted URLs, swap to `<meta name="robots" content="noindex, follow">`.

---

## 1.2 Open Graph & Twitter Cards

Place in `<head>`. `og:image` must be an **absolute HTTPS URL**, ideally **1200×630**, under 5 MB, JPG/PNG (not WebP for maximum scraper compatibility).

### Homepage OG + Twitter

```html
<!-- Open Graph -->
<meta property="og:site_name" content="Fab Luxe">
<meta property="og:type" content="website">
<meta property="og:title" content="Luxury Apartments in Greater Noida West | Fab Luxe">
<meta property="og:description" content="AQI-managed 3 & 4 BHK luxury residences with bespoke interior execution. Book a private site visit.">
<meta property="og:url" content="https://fabluxe.co.in/">
<meta property="og:image" content="https://fabluxe.co.in/assets/og/home-1200x630.jpg">
<meta property="og:image:secure_url" content="https://fabluxe.co.in/assets/og/home-1200x630.jpg">
<meta property="og:image:type" content="image/jpeg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="Fab Luxe luxury residences exterior, Greater Noida West">
<meta property="og:locale" content="en_IN">

<!-- Twitter / X -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="{{TWITTER_HANDLE}}">
<meta name="twitter:creator" content="{{TWITTER_HANDLE}}">
<meta name="twitter:title" content="Luxury Apartments in Greater Noida West | Fab Luxe">
<meta name="twitter:description" content="AQI-managed 3 & 4 BHK luxury residences with bespoke interiors. Book a private site visit.">
<meta name="twitter:image" content="https://fabluxe.co.in/assets/og/home-1200x630.jpg">
<meta name="twitter:image:alt" content="Fab Luxe luxury residences, Greater Noida West">
```

### Property page OG (use `og:type` = `website`; `product` is not valid for real estate listings)

```html
<meta property="og:type" content="website">
<meta property="og:title" content="3 BHK Luxury Apartments in Greater Noida West | Fab Luxe">
<meta property="og:description" content="AQI-managed 3 BHK luxury residence — premium fittings, curated amenities, RERA-ready.">
<meta property="og:url" content="https://fabluxe.co.in/apartments/3-bhk/">
<meta property="og:image" content="https://fabluxe.co.in/assets/og/3bhk-1200x630.jpg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="3 BHK luxury living room render by Fab Luxe">
```

**OG per-page checklist:** unique `og:title`, unique `og:url` (self-referential, absolute), unique `og:image` per template. Never let all pages inherit the homepage image — social CTR collapses when every share looks identical.

---

## 1.3 Canonical URLs & Hreflang

### Canonical policy

- **One true origin:** `https://fabluxe.co.in` (HTTPS, non-www). Everything else 301s to it.
- Every page emits a **self-referential absolute canonical**.
- Canonicalize away trailing-slash duplicates, uppercase paths, and tracking params (`utm_*`, `gclid`, `fbclid`).

```html
<link rel="canonical" href="https://fabluxe.co.in/apartments/3-bhk/">
```

### Server-level redirect rules

**Apache `.htaccess`:**

```apache
RewriteEngine On

# Force HTTPS
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# Force non-www
RewriteCond %{HTTP_HOST} ^www\.fabluxe\.co\.in [NC]
RewriteRule ^ https://fabluxe.co.in%{REQUEST_URI} [L,R=301]

# Force trailing slash on directory-style URLs (optional but be consistent)
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_URI} !(\.[a-zA-Z0-9]{1,5}|/)$
RewriteRule ^(.*)$ /$1/ [L,R=301]

# Strip index.html
RewriteCond %{THE_REQUEST} /index\.html[\s?] [NC]
RewriteRule ^(.*)index\.html$ /$1 [L,R=301]
```

**Nginx:**

```nginx
# Canonical host + HTTPS (put www and http server blocks here)
server {
    listen 80;
    listen 443 ssl;
    server_name www.fabluxe.co.in;
    return 301 https://fabluxe.co.in$request_uri;
}
server {
    listen 80;
    server_name fabluxe.co.in;
    return 301 https://fabluxe.co.in$request_uri;
}
```

### Hreflang

Fab Luxe is a single-market (India, English) brand today, so **full hreflang is not required**. If you later add a Hindi variant or an NRI/`en-gb`, `en-ae` targeted page set, use a reciprocal cluster on every equivalent URL:

```html
<link rel="alternate" hreflang="en-in" href="https://fabluxe.co.in/apartments/3-bhk/">
<link rel="alternate" hreflang="en-ae" href="https://fabluxe.co.in/ae/apartments/3-bhk/">
<link rel="alternate" hreflang="x-default" href="https://fabluxe.co.in/apartments/3-bhk/">
```

> **Rule:** hreflang must be reciprocal (every URL in the set lists every other, including itself) or Google ignores the whole cluster. Until a second locale ships, omit hreflang entirely — a lone tag adds risk with zero benefit.

---

## 1.4 Structured Data (JSON-LD)

Place each block as `<script type="application/ld+json">` in the page it describes. Validate with the [Schema Markup Validator](https://validator.schema.org/) and Google's [Rich Results Test](https://search.google.com/test/rich-results).

### 1.4.1 Property page — `RealEstateListing` + `SingleFamilyResidence`

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "RealEstateListing",
  "name": "3 BHK Luxury Apartment — Fab Luxe, Greater Noida West",
  "url": "https://fabluxe.co.in/apartments/3-bhk/",
  "datePosted": "2026-07-30",
  "image": [
    "https://fabluxe.co.in/assets/listings/3bhk/living-1600x900.jpg",
    "https://fabluxe.co.in/assets/listings/3bhk/floorplan-1600x900.jpg"
  ],
  "description": "AQI-managed 3 BHK luxury residence in Greater Noida West with premium fittings, designer interiors and curated amenities.",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "INR",
    "price": "{{PRICE_INR}}",
    "availability": "https://schema.org/InStock",
    "url": "https://fabluxe.co.in/apartments/3-bhk/"
  },
  "about": {
    "@type": "SingleFamilyResidence",
    "name": "Fab Luxe 3 BHK Luxury Residence",
    "numberOfRooms": 3,
    "numberOfBedrooms": 3,
    "numberOfBathroomsTotal": 3,
    "floorSize": {
      "@type": "QuantitativeValue",
      "value": "{{AREA_SQFT}}",
      "unitCode": "FTK"
    },
    "petsAllowed": true,
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "{{STREET}}",
      "addressLocality": "{{LOCALITY}}",
      "addressRegion": "{{REGION}}",
      "postalCode": "{{POSTAL}}",
      "addressCountry": "IN"
    },
    "geo": {
      "@type": "GeoCoordinates",
      "latitude": "{{LAT}}",
      "longitude": "{{LNG}}"
    },
    "amenityFeature": [
      { "@type": "LocationFeatureSpecification", "name": "AQI-managed indoor air", "value": true },
      { "@type": "LocationFeatureSpecification", "name": "Modular kitchen", "value": true },
      { "@type": "LocationFeatureSpecification", "name": "Clubhouse", "value": true }
    ]
  },
  "broker": {
    "@type": "RealEstateAgent",
    "name": "Fab Luxe",
    "url": "https://fabluxe.co.in/",
    "telephone": "{{PHONE_E164}}"
  }
}
</script>
```

> **Note:** `RealEstateListing.price` is not a Google-supported rich result today; the markup still helps entity understanding and third-party parsers. Keep `price` accurate and RERA-compliant, or omit `offers` entirely and show "Price on request."

### 1.4.2 Interior Execution — `HomeAndConstructionBusiness` (a `LocalBusiness` subtype)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "HomeAndConstructionBusiness",
  "@id": "https://fabluxe.co.in/#business",
  "name": "Fab Luxe",
  "image": "https://fabluxe.co.in/assets/brand/fabluxe-storefront-1200x800.jpg",
  "url": "https://fabluxe.co.in/",
  "logo": "https://fabluxe.co.in/assets/brand/fabluxe-logo.png",
  "telephone": "{{PHONE_E164}}",
  "email": "{{EMAIL}}",
  "priceRange": "₹₹₹",
  "description": "Fab Luxe delivers turnkey luxury interior execution and AQI-managed luxury residences in Greater Noida West.",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "{{STREET}}",
    "addressLocality": "{{LOCALITY}}",
    "addressRegion": "{{REGION}}",
    "postalCode": "{{POSTAL}}",
    "addressCountry": "IN"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "{{LAT}}",
    "longitude": "{{LNG}}"
  },
  "areaServed": [
    { "@type": "City", "name": "Greater Noida" },
    { "@type": "City", "name": "Noida" },
    { "@type": "AdministrativeArea", "name": "Delhi NCR" }
  ],
  "openingHoursSpecification": [{
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],
    "opens": "10:00",
    "closes": "19:00"
  }],
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Interior Execution Services",
    "itemListElement": [
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Turnkey Interior Execution" } },
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Modular Kitchen & Wardrobes" } },
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Luxury Furnishing & Styling" } }
    ]
  },
  "sameAs": [
    "{{IG_URL}}",
    "{{FB_URL}}",
    "{{LI_URL}}",
    "{{YT_URL}}",
    "{{PIN_URL}}"
  ]
}
</script>
```

### 1.4.3 `FAQPage` — high-intent buyer questions

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Where are Fab Luxe luxury apartments located?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Fab Luxe luxury 3 and 4 BHK residences are located in Greater Noida West (Noida Extension), with quick connectivity to Noida, the FNG corridor and Delhi NCR."
      }
    },
    {
      "@type": "Question",
      "name": "What does AQI-managed living mean at Fab Luxe?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "AQI-managed living combines building-level air filtration, ventilation design and green buffers to keep indoor air quality healthy year-round, especially during high-pollution NCR winters."
      }
    },
    {
      "@type": "Question",
      "name": "Are Fab Luxe projects RERA registered?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. Each Fab Luxe project carries a valid UP-RERA registration number, displayed on the respective project page. Always verify the number on the official UP-RERA portal before booking."
      }
    },
    {
      "@type": "Question",
      "name": "Does Fab Luxe provide interior execution for the apartments?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. Fab Luxe offers turnkey luxury interior execution — design, procurement, site management and handover — so buyers can move into a fully finished, styled home."
      }
    },
    {
      "@type": "Question",
      "name": "How can I book a site visit or request pricing?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Call or WhatsApp {{PHONE_E164}}, or submit the enquiry form on the Contact page. The Fab Luxe team schedules private site visits and shares current floor plans and pricing on request."
      }
    }
  ]
}
</script>
```

> Only mark up FAQs that are **visible on the page**. Invisible FAQ markup violates Google's structured-data guidelines and risks a manual action.

### 1.4.4 Site-wide `Organization` + `WebSite` (homepage only)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://fabluxe.co.in/#org",
      "name": "Fab Luxe",
      "url": "https://fabluxe.co.in/",
      "logo": "https://fabluxe.co.in/assets/brand/fabluxe-logo.png",
      "sameAs": ["{{IG_URL}}","{{FB_URL}}","{{LI_URL}}","{{YT_URL}}","{{PIN_URL}}"]
    },
    {
      "@type": "WebSite",
      "@id": "https://fabluxe.co.in/#website",
      "url": "https://fabluxe.co.in/",
      "name": "Fab Luxe",
      "publisher": { "@id": "https://fabluxe.co.in/#org" }
    }
  ]
}
</script>
```

---

# 2. Social Media Integration & Open Graph Audit

## 2.1 Social Preview Optimization

| Platform | Recommended share image | Aspect | Safe zone / notes |
|---|---|---|---|
| **OG master (FB/LinkedIn/WhatsApp link preview)** | **1200 × 630** | 1.91:1 | Keep logo + headline within center 1200×600. WhatsApp needs image **< 300 KB** or it may skip the thumbnail. |
| **Facebook feed post** | 1200 × 630 (link) / 1080 × 1350 (native) | 1.91:1 / 4:5 | Native 4:5 wins more vertical real estate. |
| **LinkedIn link preview** | 1200 × 627 | 1.91:1 | Text overlay ≤ 20% area; crops ~1200×620. |
| **LinkedIn native image** | 1200 × 1500 | 4:5 | Best organic reach format on LI. |
| **Instagram feed** | 1080 × 1350 | 4:5 | Primary render format. |
| **Instagram / FB Story & Reels** | 1080 × 1920 | 9:16 | Keep text within center 1080×1420 (UI safe zone). |
| **Pinterest pin** | 1000 × 1500 | 2:3 | 2:3 is the only ratio Pinterest doesn't crop. |
| **YouTube thumbnail** | 1280 × 720 | 16:9 | Min 640px wide, < 2 MB. |

**Design template rules for share thumbnails:**

- Brand lockup (Fab Luxe logo) bottom-left or top-left, consistent placement across all cards.
- One benefit line max: *"AQI-Managed 3 & 4 BHK Luxury Residences."*
- Dark, high-contrast overlay (`rgba(14,14,14,0.35)`) behind text so it stays legible over renders.
- Use the hero render, never stock. Real 3D renders convert; generic imagery doesn't.
- Export **JPG at ~80% quality**, sRGB color profile. Keep OG under 300 KB for WhatsApp.

**OG audit checklist (run before every launch):**

1. Facebook [Sharing Debugger](https://developers.facebook.com/tools/debug/) — scrape URL, confirm 1200×630 renders, click "Scrape Again" to bust cache.
2. LinkedIn [Post Inspector](https://www.linkedin.com/post-inspector/) — refresh cache.
3. Send the link to a private WhatsApp chat — confirm the thumbnail + title appear.
4. X/Twitter — paste link into a draft, confirm `summary_large_image` renders.

---

## 2.2 Cross-Platform Content Distribution

### Instagram & Pinterest — visual aesthetics roadmap

**Content pillars (rotate weekly):**

| Pillar | Instagram | Pinterest |
|---|---|---|
| 3D renders | Carousel: exterior → living → master → kitchen | Vertical pin per room, board: "Luxury Apartment Interiors" |
| Site progress | Weekly Reel + Story "construction update" | "Project Progress — Greater Noida West" board |
| AQI / wellness | Reel explaining AQI-managed living (30–45s) | Infographic pin: "How AQI-Managed Homes Work" |
| Material textures | Close-up carousel (marble, veneer, brass) | "Luxury Material Palette" board, rich pins |
| Amenities & lifestyle | Golden-hour clubhouse/pool Reels | "Amenities & Lifestyle" board |

- **Instagram cadence:** 4–5 posts/week (≥2 Reels), 1 Story/day. Always geo-tag *Greater Noida West*.
- **Alt text (SEO):** describe render + location, e.g. *"3 BHK luxury living room 3D render, Fab Luxe Greater Noida West."*
- **Pinterest:** enable Rich Pins, verify domain, pin 3–5×/day mixing fresh + evergreen. Pinterest indexes into Google Images — treat pin titles/descriptions as keyword real estate.

### LinkedIn — B2B strategy (architects, interior designers, investors, HNIs)

- **Company page:** complete profile, custom banner, "Products/Services" listing interior execution.
- **Content mix (weekly):**
  - 1 thought-leadership post (market trend, AQI/wellness real estate, NCR luxury demand).
  - 1 project showcase (native 4:5 or 1200×627 render + narrative caption).
  - 1 behind-the-execution post (site management, timelines, craftsmanship) — builds trust with designers/investors.
- **Targeting play:** tag partner architects/designers; publish 1 long-form article/month ("Why AQI-managed luxury is the next NCR standard"); use employee advocacy (founders reshare).
- **Lead gen:** LinkedIn Lead Gen Form for the "Download the Fab Luxe brochure" CTA; retarget site visitors via Insight Tag.

### YouTube & Short-form (Reels/Shorts) — video SEO

**Long-form walkthrough (YouTube) script template:**

```txt
[0:00] Hook — "Step inside a 4 BHK AQI-managed luxury residence in Greater Noida West."
[0:10] Location & connectivity (FNG, Noida, metro)
[0:35] Exterior + amenities walkthrough
[1:20] Interior room-by-room (living → kitchen → master → balcony)
[3:00] AQI-managed living explainer (the differentiator)
[3:45] Interior execution — design-to-handover
[4:20] CTA — "Book a private site visit. Link + number in description."
```

**Optimized video title patterns:**

- `4 BHK Luxury Apartment Tour | AQI-Managed Living in Greater Noida West | Fab Luxe`
- `Inside a ₹— Cr Luxury Home | Fab Luxe Interior Execution Walkthrough`

**Description template (first 150 chars carry SEO weight):**

```txt
Tour a 4 BHK AQI-managed luxury residence in Greater Noida West by Fab Luxe.
Book a site visit: {{PHONE_E164}} | https://fabluxe.co.in

Chapters:
00:00 Intro
00:35 Amenities
01:20 Interiors
03:00 AQI-managed living
04:20 Book a visit

#LuxuryApartments #GreaterNoidaWest #FabLuxe
```

**Hashtag clusters:**

- *Discovery:* `#LuxuryApartments #GreaterNoidaWest #NoidaExtension #DelhiNCRRealEstate #LuxuryHomesIndia`
- *Niche/intent:* `#3BHK #4BHK #AQIManagedLiving #InteriorExecution #TurnkeyInteriors`
- *Brand:* `#FabLuxe #FabLuxeHomes`
- **Reels/Shorts:** 3–5 hashtags max, vertical 9:16, hook in first 2 seconds, on-screen captions always (most watch muted).

---

## 2.3 Social Profiles Schema (sameAs)

Bridges official channels to the Google Knowledge Panel. Put on the homepage inside the `Organization` node (see [1.4.4](#144-site-wide-organization--website-homepage-only)) — don't duplicate a second standalone block. Standalone version if you need it:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Fab Luxe",
  "url": "https://fabluxe.co.in/",
  "logo": "https://fabluxe.co.in/assets/brand/fabluxe-logo.png",
  "sameAs": [
    "{{IG_URL}}",
    "{{FB_URL}}",
    "{{LI_URL}}",
    "{{YT_URL}}",
    "{{PIN_URL}}"
  ]
}
</script>
```

> Keep the exact URLs in `sameAs` identical to the live profile URLs (final canonical form, no `?` params). Mismatches weaken entity consolidation.

---

# 3. Technical SEO Google Indexing Architecture

## 3.1 XML Sitemap Specs

Structure: one sitemap index → per-type sitemaps. Reference from `robots.txt` and submit in Google Search Console.

**Priority & frequency policy:**

| URL type | priority | changefreq |
|---|---|---|
| Homepage | `1.0` | `weekly` |
| Apartment listing pages (3/4 BHK) | `0.9` | `weekly` |
| Interior execution service page | `0.8` | `monthly` |
| Amenities / location / about | `0.7` | `monthly` |
| Contact | `0.6` | `yearly` |
| Blog / insights posts | `0.5` | `monthly` |

> Google largely ignores `priority`/`changefreq` as ranking signals, but they remain valid sitemap fields and help some crawlers/parsers. **`lastmod` is the field Google actually trusts** — keep it accurate (real modification date, W3C format).

**`sitemap-index.xml`:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <sitemap>
    <loc>https://fabluxe.co.in/sitemap-pages.xml</loc>
    <lastmod>2026-07-30</lastmod>
  </sitemap>
  <sitemap>
    <loc>https://fabluxe.co.in/sitemap-listings.xml</loc>
    <lastmod>2026-07-30</lastmod>
  </sitemap>
</sitemapindex>
```

**`sitemap-pages.xml`:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:image="http://www.google.com/schemas/sitemap-image/1.1">
  <url>
    <loc>https://fabluxe.co.in/</loc>
    <lastmod>2026-07-30</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://fabluxe.co.in/apartments/3-bhk/</loc>
    <lastmod>2026-07-30</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.9</priority>
    <image:image>
      <image:loc>https://fabluxe.co.in/assets/listings/3bhk/living-1600x900.jpg</image:loc>
      <image:title>3 BHK luxury living room — Fab Luxe</image:title>
    </image:image>
  </url>
  <url>
    <loc>https://fabluxe.co.in/apartments/4-bhk/</loc>
    <lastmod>2026-07-30</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.9</priority>
  </url>
  <url>
    <loc>https://fabluxe.co.in/interior-execution/</loc>
    <lastmod>2026-07-30</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://fabluxe.co.in/contact/</loc>
    <lastmod>2026-07-30</lastmod>
    <changefreq>yearly</changefreq>
    <priority>0.6</priority>
  </url>
</urlset>
```

**Sitemap hygiene rules:**

- Only include `200`, indexable, canonical URLs. No redirects, `noindex`, or param URLs.
- Max 50,000 URLs / 50 MB uncompressed per file — split beyond that (you won't hit this soon).
- All `loc` values absolute, HTTPS, non-www, matching the canonical exactly.

---

## 3.2 Robots.txt Optimization

Serve at `https://fabluxe.co.in/robots.txt`. Reachable, `200`, `text/plain`.

```txt
# robots.txt — fabluxe.co.in
# Allow all reputable crawlers to index public content.

User-agent: *
Allow: /

# Block backend, staging, and non-public utility paths
Disallow: /admin/
Disallow: /wp-admin/
Disallow: /staging/
Disallow: /dev/
Disallow: /cart/
Disallow: /checkout/
Disallow: /*/thank-you/
Disallow: /search
Disallow: /*?*utm_
Disallow: /*?*gclid
Disallow: /*?*fbclid

# Let crawlers fetch CSS/JS/images so pages render fully
Allow: /wp-admin/admin-ajax.php
Allow: /assets/
Allow: /*.css$
Allow: /*.js$

# Optional: throttle aggressive SEO scrapers (keep Google/Bing at full speed)
User-agent: AhrefsBot
Crawl-delay: 10
User-agent: SemrushBot
Crawl-delay: 10

# Sitemaps
Sitemap: https://fabluxe.co.in/sitemap-index.xml
```

**Cautions:**

- `robots.txt` `Disallow` **blocks crawling, not indexing** — a disallowed URL can still appear in results without a snippet. To keep a page *out of the index*, allow crawling and use `<meta name="robots" content="noindex">` (or an `X-Robots-Tag` header) instead.
- Never `Disallow: /` on production — it de-indexes the whole site. Verify after every deploy.
- Keep staging on a separate host with HTTP auth + `noindex`, not just a `Disallow`.

---

## 3.3 Core Web Vitals Blueprint

Targets (75th percentile, mobile): **LCP ≤ 2.5s · INP ≤ 200ms · CLS ≤ 0.1**. Image-heavy luxury sites live or die on LCP and CLS.

### LCP — Largest Contentful Paint

- [ ] Hero image served as **AVIF/WebP** with JPG fallback; correctly sized per breakpoint via `srcset`/`sizes`.
- [ ] `fetchpriority="high"` on the LCP hero; **do not** lazy-load it.
- [ ] `<link rel="preload" as="image" imagesrcset="…" fetchpriority="high">` for the hero.
- [ ] `preconnect`/`dns-prefetch` to image CDN, fonts, and analytics origins.
- [ ] Self-host fonts, `font-display: swap`, subset to Latin; preload the primary weight.
- [ ] CDN + long-cache (`Cache-Control: public, max-age=31536000, immutable`) on hashed assets.
- [ ] Server response (TTFB) < 600ms — enable caching/SSG for listing pages.

```html
<link rel="preconnect" href="https://cdn.fabluxe.co.in" crossorigin>
<link rel="preload" as="image"
      imagesrcset="/assets/hero-800.avif 800w, /assets/hero-1600.avif 1600w"
      imagesizes="100vw" fetchpriority="high">
<img src="/assets/hero-1600.jpg"
     srcset="/assets/hero-800.avif 800w, /assets/hero-1600.avif 1600w"
     sizes="100vw" width="1600" height="900"
     fetchpriority="high" alt="Fab Luxe luxury residence, Greater Noida West">
```

### CLS — Cumulative Layout Shift

- [ ] **Every** `<img>`/`<video>`/`<iframe>` has explicit `width`+`height` (or `aspect-ratio` CSS).
- [ ] Reserve space for embeds (maps, virtual tours) with a fixed-ratio container.
- [ ] No content injected above existing content after load (sticky banners, cookie bars) — reserve their height.
- [ ] Fonts preloaded to avoid FOIT→FOUT reflow; match fallback metrics with `size-adjust`.
- [ ] Gallery/carousel containers have a defined min-height before JS hydrates.

```css
.gallery-item { aspect-ratio: 16 / 9; }  /* reserves box before image loads */
.map-embed    { aspect-ratio: 4 / 3; width: 100%; }
```

### INP / interactivity & image galleries

- [ ] Lazy-load **below-the-fold** gallery images (`loading="lazy" decoding="async"`).
- [ ] Use a lightweight lightbox; defer its JS (`defer`/dynamic import on first interaction).
- [ ] Break up long JS tasks; avoid heavy hydration on the listing pages.
- [ ] Serve responsive thumbnails in the grid, full-res only in the lightbox.
- [ ] Ship the 3D-tour/`iframe` (Matterport etc.) via **facade** — click-to-load poster, not on initial paint.

**Measurement loop:** PageSpeed Insights + CrUX for field data, Lighthouse CI in the deploy pipeline for lab regressions, Search Console → Core Web Vitals report for URL-group trends.

---

# 4. Claude Code Implementation Script

Validation workflow to automate robots/sitemap checks, HTML tag validation (OG + canonical), and JSON-LD verification. Two forms below: a **portable Bash script** and **PowerShell** (your primary shell on this machine).

> These scripts **validate** existing files/URLs — they don't publish anything. Run them locally or in CI.

### 4.1 Bash — `seo-validate.sh`

```bash
#!/usr/bin/env bash
# seo-validate.sh — validate robots.txt, sitemap, OG/canonical tags, and JSON-LD.
# Usage: ./seo-validate.sh https://fabluxe.co.in
set -euo pipefail

BASE="${1:-https://fabluxe.co.in}"
PAGES=("/" "/apartments/3-bhk/" "/apartments/4-bhk/" "/interior-execution/" "/contact/")
fail=0

echo "== 1. robots.txt =="
if curl -fsSL "$BASE/robots.txt" -o /tmp/robots.txt; then
  grep -qi "^Sitemap:" /tmp/robots.txt && echo "  ✓ Sitemap directive present" \
    || { echo "  ✗ No Sitemap directive"; fail=1; }
  grep -qiE "^Disallow:\s*/\s*$" /tmp/robots.txt \
    && { echo "  ✗ DANGER: site-wide Disallow: /"; fail=1; } \
    || echo "  ✓ No site-wide Disallow"
else echo "  ✗ robots.txt not reachable"; fail=1; fi

echo "== 2. sitemap.xml (well-formed XML) =="
if curl -fsSL "$BASE/sitemap-index.xml" -o /tmp/sitemap.xml; then
  if command -v xmllint >/dev/null; then
    xmllint --noout /tmp/sitemap.xml && echo "  ✓ Valid XML" || { echo "  ✗ Malformed XML"; fail=1; }
  else echo "  ! xmllint not installed — skipping XML lint"; fi
else echo "  ✗ sitemap-index.xml not reachable"; fail=1; fi

echo "== 3. OG + canonical tags per page =="
for p in "${PAGES[@]}"; do
  url="$BASE$p"; html="$(curl -fsSL "$url" || true)"
  echo "  $url"
  grep -qi 'property="og:title"'  <<<"$html" && echo "    ✓ og:title"  || { echo "    ✗ og:title";  fail=1; }
  grep -qi 'property="og:image"'  <<<"$html" && echo "    ✓ og:image"  || { echo "    ✗ og:image";  fail=1; }
  grep -qi 'property="og:url"'    <<<"$html" && echo "    ✓ og:url"    || { echo "    ✗ og:url";    fail=1; }
  grep -qi 'rel="canonical"'      <<<"$html" && echo "    ✓ canonical" || { echo "    ✗ canonical"; fail=1; }
  grep -qi 'name="twitter:card"'  <<<"$html" && echo "    ✓ twitter:card" || echo "    ! twitter:card missing"
done

echo "== 4. JSON-LD extraction + JSON validity =="
for p in "${PAGES[@]}"; do
  url="$BASE$p"
  curl -fsSL "$url" \
    | grep -ozP '(?s)<script type="application/ld\+json">\K.*?(?=</script>)' \
    | tr '\0' '\n' > /tmp/ld.json || true
  if [ -s /tmp/ld.json ]; then
    if command -v jq >/dev/null; then
      jq empty /tmp/ld.json >/dev/null 2>&1 && echo "  ✓ $url — valid JSON-LD" \
        || { echo "  ✗ $url — JSON-LD parse error"; fail=1; }
    else echo "  ! jq not installed — found JSON-LD but not validated ($url)"; fi
  else echo "  ! $url — no JSON-LD block found"; fi
done

echo
[ "$fail" -eq 0 ] && echo "ALL CHECKS PASSED ✓" || { echo "SOME CHECKS FAILED ✗"; exit 1; }
```

Run:

```bash
chmod +x seo-validate.sh && ./seo-validate.sh https://fabluxe.co.in
```

### 4.2 PowerShell — `seo-validate.ps1` (Windows-native)

```powershell
# seo-validate.ps1 — validate robots, sitemap, OG/canonical, JSON-LD.
# Usage: ./seo-validate.ps1 -Base "https://fabluxe.co.in"
param([string]$Base = "https://fabluxe.co.in")
$ErrorActionPreference = "Stop"
$pages = @("/", "/apartments/3-bhk/", "/apartments/4-bhk/", "/interior-execution/", "/contact/")
$fail = $false

Write-Host "== 1. robots.txt =="
try {
  $robots = (Invoke-WebRequest "$Base/robots.txt" -UseBasicParsing).Content
  if ($robots -match "(?im)^Sitemap:") { Write-Host "  OK Sitemap directive" }
  else { Write-Host "  FAIL no Sitemap directive"; $fail = $true }
  if ($robots -match "(?im)^Disallow:\s*/\s*$") { Write-Host "  FAIL site-wide Disallow: /"; $fail = $true }
  else { Write-Host "  OK no site-wide Disallow" }
} catch { Write-Host "  FAIL robots.txt unreachable"; $fail = $true }

Write-Host "== 2. sitemap-index.xml =="
try {
  [xml]$sm = (Invoke-WebRequest "$Base/sitemap-index.xml" -UseBasicParsing).Content
  Write-Host "  OK valid XML ($($sm.sitemapindex.sitemap.Count) sitemaps)"
} catch { Write-Host "  FAIL sitemap missing or malformed"; $fail = $true }

Write-Host "== 3. OG + canonical per page =="
foreach ($p in $pages) {
  $url = "$Base$p"; Write-Host "  $url"
  try {
    $h = (Invoke-WebRequest $url -UseBasicParsing).Content
    foreach ($t in @('og:title','og:image','og:url')) {
      if ($h -match "property=`"$t`"") { Write-Host "    OK $t" } else { Write-Host "    FAIL $t"; $fail = $true }
    }
    if ($h -match 'rel="canonical"') { Write-Host "    OK canonical" } else { Write-Host "    FAIL canonical"; $fail = $true }
    if ($h -match 'name="twitter:card"') { Write-Host "    OK twitter:card" } else { Write-Host "    WARN twitter:card missing" }

    # 4. JSON-LD extraction + validity
    $matches = [regex]::Matches($h, '(?s)<script type="application/ld\+json">(.*?)</script>')
    if ($matches.Count -eq 0) { Write-Host "    WARN no JSON-LD block" }
    foreach ($m in $matches) {
      try { $m.Groups[1].Value | ConvertFrom-Json | Out-Null; Write-Host "    OK JSON-LD valid" }
      catch { Write-Host "    FAIL JSON-LD parse error"; $fail = $true }
    }
  } catch { Write-Host "    FAIL page unreachable"; $fail = $true }
}

Write-Host ""
if ($fail) { Write-Host "SOME CHECKS FAILED"; exit 1 } else { Write-Host "ALL CHECKS PASSED" }
```

Run:

```bash
pwsh ./seo-validate.ps1 -Base "https://fabluxe.co.in"
```

### 4.3 CI integration (GitHub Actions)

```yaml
# .github/workflows/seo-validate.yml
name: SEO Validation
on:
  push: { branches: [main] }
  schedule: [{ cron: "0 3 * * 1" }]   # weekly Monday 03:00 UTC
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install tooling
        run: sudo apt-get update && sudo apt-get install -y jq libxml2-utils
      - name: Run SEO validation
        run: chmod +x seo-validate.sh && ./seo-validate.sh https://fabluxe.co.in
```

### 4.4 External validators (manual, pre-launch gate)

| Check | Tool |
|---|---|
| Rich results / JSON-LD | https://search.google.com/test/rich-results |
| Schema syntax | https://validator.schema.org/ |
| OG (Facebook) | https://developers.facebook.com/tools/debug/ |
| OG (LinkedIn) | https://www.linkedin.com/post-inspector/ |
| Sitemap submission | Google Search Console → Sitemaps |
| Core Web Vitals | https://pagespeed.web.dev/ |
| Mobile rendering | GSC → URL Inspection → "Test live URL" |

---

## Launch Checklist (tl;dr)

- [ ] Fill every `{{PLACEHOLDER}}` (search the file for `{{`).
- [ ] One canonical origin enforced (`https://fabluxe.co.in`, non-www) via 301s.
- [ ] Unique title + description + OG image per template.
- [ ] JSON-LD live on: homepage (Org+WebSite), each listing (RealEstateListing), interior page (HomeAndConstructionBusiness), FAQ page.
- [ ] `robots.txt` + `sitemap-index.xml` reachable; sitemap submitted in GSC.
- [ ] OG previews verified on FB, LinkedIn, WhatsApp, X.
- [ ] LCP ≤ 2.5s / CLS ≤ 0.1 / INP ≤ 200ms on mobile for homepage + listing pages.
- [ ] `seo-validate` passing in CI.
- [ ] All social profile URLs matched exactly in `sameAs`.

> **Compliance note:** For a real estate brand in India, every project page must display the correct **UP-RERA registration number** and standard RERA disclaimer. Keep advertised pricing/area RERA-accurate; use "Price on request" rather than stale figures in schema `offers`.
