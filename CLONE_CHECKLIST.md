# Horse Property Network — City Site Clone Checklist

**Template source:** `aiagent322/wickenburg-horse-property`  
**Last updated:** June 2026  
**Applies to:** All city horse property sites cloned from this template

---

## Pre-Clone Setup — Gather These Before You Start

| Item | Where to get it | Example (Wickenburg) |
|---|---|---|
| New domain | GoDaddy / purchase | `cavecreekhorseproperty.com` |
| New GitHub repo name | Create in aiagent322 org | `cave-creek-horse-property` |
| Cloudflare zone ID | CF dashboard → zone overview | `ff0e36cb4fcf4b9cb6275ce2ddbc9726` |
| Google Analytics tag | analytics.google.com → new property | `G-XXXXXXXXXX` |
| City name (exact) | — | `Cave Creek` |
| City name (slug/lowercase) | — | `cave-creek` |
| City, State short | — | `Cave Creek, AZ` |
| Postal code | USPS | `85331` |
| County | county records | `Maricopa` |
| Lat / Lng (city center) | Google Maps | `33.8328, -111.9498` |
| Elevation | Google / Wikipedia | `2,100 feet` |
| Miles from Phoenix | Google Maps | `34 miles` |
| Distance descriptor | write this | `34 miles northeast of Phoenix` |
| HPA search URL param | — | `?q=cave+creek` |
| City equestrian identity | research | `Arabian horse capital of the Southwest` |
| Price range low | MLS research | `$450K` |
| Price range high | MLS research | `$4M+` |
| Acreage range | MLS research | `1–40` |
| Pages.dev project name | CF Pages deploy | `cave-creek-horse-property` |

---

## Step 1 — Clone the Repo

```bash
# Clone template
git clone https://github.com/aiagent322/wickenburg-horse-property
cd wickenburg-horse-property

# Rename remote to new repo
git remote set-url origin https://github.com/aiagent322/cave-creek-horse-property

# Create new repo in GitHub org first, then push
git push -u origin main
```

---

## Step 2 — Global Find/Replace

Run these in order. Every replace is case-sensitive where noted.

### 2A — Domain (case-sensitive)

| Find | Replace with |
|---|---|
| `wickenburghorseproperty.com` | `cavecreekhorseproperty.com` |
| `wickenburg-horse-property.pages.dev` | `cave-creek-horse-property.pages.dev` |
| `aiagent322/wickenburg-horse-property` | `aiagent322/cave-creek-horse-property` |

**Files affected:** All `.html` files, `sitemap.xml`  
**Count to verify:** ~10 occurrences in homepage, 11–13 in inner pages

---

### 2B — City Name (case-sensitive, do BOTH)

| Find | Replace with |
|---|---|
| `Wickenburg` | `Cave Creek` |
| `wickenburg` | `cave-creek` |

**Files affected:** All `.html` files, `sitemap.xml`  
**Count to verify:** ~73 in homepage, 35–55 in inner pages  
⚠️ **Do NOT replace inside image URLs** (Unsplash URLs contain `fit=crop` etc — not affected, but double-check)

---

### 2C — State References (only replace if moving outside Arizona)

| Find | Replace with |
|---|---|
| `Arizona` | `[State]` |
| `, AZ` | `, [ST]` |
| `addressRegion": "AZ"` | `addressRegion": "[ST]"` |

**Note:** If staying in Arizona, skip this block entirely. All Arizona-specific content (BLM access, Maricopa/Yavapai zoning, ag exemptions, well permits) is still accurate and should be kept or adapted.

---

### 2D — HPA Agent Search URL

| Find | Replace with |
|---|---|
| `?q=wickenburg` | `?q=cave+creek` |

**Files affected:** All `.html` files (5–6 occurrences per file)  
**Verify:** Nav, sticky CTA bar, hero CTAs, agent module, footer

---

### 2E — Google Analytics Tag

| Find | Replace with |
|---|---|
| `G-PHFSS5JZ36` | `G-XXXXXXXXXX` (new GA4 property) |

**Files affected:** All `.html` files (appears twice in `<head>` — gtag script + config call)  
**Count:** 2 per file × 37 files = 74 replacements

---

### 2F — Cloudflare Web Analytics Token

| Find | Replace with |
|---|---|
| `e8b33bc79099427393f57bf292a402b7` | `[new CF analytics token]` |

**Files affected:** All `.html` files (appears in the `<script defer>` beacon at bottom of `<body>`)  
**Get new token:** Cloudflare dashboard → Web Analytics → Add site  
**Note:** This is injected by Cloudflare Pages automatically on some configs — verify whether it needs manual replacement or is auto-injected.

---

### 2G — Sticky CTA Bar Label

| Find | Replace with |
|---|---|
| `Wickenburg Horse<br>Property Specialist` | `Cave Creek Horse<br>Property Specialist` |

**Files affected:** All 35 inner pages (in the `sticky-cta` div before `</body>`)

---

### 2H — Schema — Homepage `index.html` only

Edit these blocks manually (not find/replace — values are unique per city):

**WebSite schema:**
```json
"name": "CavecreekHorseProperty.com",
"url": "https://cavecreekhorseproperty.com/",
"description": "Cave Creek, Arizona horse property guide..."
```

**Place schema:**
```json
"name": "Cave Creek, Arizona",
"description": "[City-specific description of equestrian character]",
"url": "https://cavecreekhorseproperty.com/",
"addressLocality": "Cave Creek",
"postalCode": "85331",
"latitude": 33.8328,
"longitude": -111.9498
```

Also update `additionalProperty` values:
```json
{ "name": "Elevation", "value": "2,100 feet" },
{ "name": "Distance from Phoenix", "value": "34 miles" },
{ "name": "Equestrian Identity", "value": "Arabian horse capital of the Southwest" }
```

---

### 2I — Schema — Neighborhood Pages

Each neighborhood page has a `Place` schema with city-specific `geo` coordinates and `containedInPlace`. These need manual editing per neighborhood — the coordinates are neighborhood-specific, not city-wide.

**Template pattern to update:**
```json
"containedInPlace": {
  "@type": "City",
  "name": "Cave Creek",   ← update
  ...
}
```

The `geo` coordinates on neighborhood pages are already neighborhood-specific and were manually researched for Wickenburg — update them with the new city's neighborhood coordinates.

---

## Step 3 — Stats Bar (Homepage)

The homepage stats bar has 5 hardcoded values. Update all five for the new city:

| Stat | Wickenburg value | Update to |
|---|---|---|
| Corridors | `6` | count of new city's corridors |
| Price Range | `$320K–$3M+` | new city's range |
| Acres Available | `1.5–160` | new city's typical range |
| Days Rideable | `365` | adjust if seasonally limited |
| From Phoenix | `60 mi` | new city's distance |

---

## Step 4 — Hero Section (Homepage)

Update three things in `.hp-hero-content`:

1. **Kicker line:** `Arizona's Horse Country Capital` → `[City's equestrian identity]`
2. **H1:** `Wickenburg Horse Property` → `Cave Creek Horse Property`
3. **Sub:** `60 miles northwest of Phoenix — 2,100 feet elevation — year-round riding — Team Roping Capital of the World` → city-specific tagline

---

## Step 5 — Intro Paragraph (Homepage)

The intro paragraph contains Wickenburg-specific market intelligence (price comparisons to Scottsdale/Temecula, 1863 founding date, etc.). **This must be rewritten for each city** — this is the core of the editorial differentiation.

Do not clone this paragraph. Write a new one with:
- City's distance and direction from Phoenix
- What it's undervalued against (comparable markets)
- The equestrian infrastructure that defines the community
- How long that community has been building

---

## Step 6 — Seasonal Callout (Homepage)

The snowbird section references October–April season, Gold Rush Days rodeo, Wellington comparison, and Colorado/Wyoming/Montana buyers. Rewrite for the new city's seasonal buyer profile.

---

## Step 7 — Six Corridor Cards (Homepage + `/neighborhoods/`)

The six corridor cards and their sub-pages are the most city-specific content. Each requires:
- New corridor names
- New acreage and price specs
- New descriptions (soil type, water history, trail access, proximity to town)
- New geo coordinates in Place schema
- New hero images matched to that corridor's character

**This is editorial work, not find/replace.** Budget 30–60 minutes per corridor.

---

## Step 8 — Page Hero Images

Every inner page uses an Unsplash URL as the hero image background. These are Arizona/desert/equestrian images that work for any Arizona city site. For non-Arizona cities, replace with region-appropriate images.

The image URL pattern is in the inline `style` attribute:
```html
<div class="page-hero" role="img" aria-label="..." 
  style="background-image:linear-gradient(...),url('[IMAGE_URL]')">
```

For Arizona city clones: existing Unsplash images are acceptable placeholders. Replace with real property photography when available.

---

## Step 9 — Sitemap (`sitemap.xml`)

All `<loc>` URLs will be updated by the domain find/replace in Step 2A. Verify after:

```bash
# Count URLs — should be 42
grep -c '<loc>' sitemap.xml

# Confirm no Wickenburg domain remains
grep 'wickenburg' sitemap.xml
```

Also update `<lastmod>` dates to current date.

---

## Step 10 — `_headers` File

No changes needed — cache control rules are domain-agnostic.

---

## Step 11 — Cloudflare Pages Setup

1. Create new Pages project in CF dashboard
2. Connect to new GitHub repo (`aiagent322/cave-creek-horse-property`)
3. Build settings: none (static HTML, no build command)
4. Add custom domain
5. Verify DNS propagation
6. Get new Web Analytics token and update all HTML files if not auto-injected

---

## Step 12 — Google Search Console

1. Add new domain as URL prefix property
2. Deploy the HTML verification file: `google[token].html` (with and without `.html` extension due to Cloudflare 308 redirect — see Wickenburg setup notes)
3. Submit sitemap: `https://[domain]/sitemap.xml`

---

## Step 13 — Pre-Launch Verification Checklist

Run this audit before announcing the site:

```
□ No "wickenburg" anywhere in page source (grep test)
□ Canonical tag points to new domain on every page
□ OG:URL points to new domain on every page  
□ Schema @id/url values point to new domain
□ GA tag is new property (not Wickenburg's G-PHFSS5JZ36)
□ HPA links use new city's ?q= parameter
□ Sticky CTA bar shows new city name
□ Stats bar has new city values
□ Hero H1 shows new city name
□ Intro paragraph is new city content (not Wickenburg copy)
□ Corridor cards show new city corridors
□ Sitemap submitted to Search Console
□ Site loads on both www and non-www (verify redirect)
□ Mobile nav opens and closes correctly
□ Sticky CTA appears after 300px scroll on mobile
□ Breadcrumbs render correctly on 3 inner pages
□ Page hero images render on 3 inner pages
□ Buy/Sell module shows on homepage
□ Sell Your Property in desktop nav
□ Sell Your Property in mobile menu
```

---

## What Stays Identical (Do Not Change)

These clone verbatim with zero edits:

- `styles.css` — entire stylesheet
- Nav structure and CSS classes
- Breadcrumb logic and CSS
- Page hero CSS (`.page-hero`)
- Sticky CTA bar CSS and JS logic
- Buy/Sell module CSS
- Footer network links (HPA, HorsePropertyFinancing, HorsePropertyGuide, TeamRoping.AI, HorseCalendar.AI, B&B)
- Schema types and structure (only values change)
- `_headers` cache control rules
- Internal link architecture pattern
- All guide page templates (water/zoning/arena/barn/buying) — **rewrite content, keep structure**
- All article page templates — **rewrite content, keep structure**

---

## What Requires Full Rewrite (Not Find/Replace)

These cannot be copied from Wickenburg:

| Page/Section | Why |
|---|---|
| Homepage intro paragraph | City-specific market intelligence |
| Seasonal callout | City-specific buyer season and events |
| All 6 corridor pages | Unique to each city's geography |
| `articles/why-[city].html` | City identity piece — must be original |
| `articles/[city]-to-arizona.html` | City-specific relocation story |
| `market/price-guide.html` body | City-specific price bands |
| Neighborhood index descriptions | City-specific corridor overviews |
| Stats bar values | City-specific market data |
| Hero sub tagline | City-specific identity line |
| `services/sell-your-property.html` local refs | City-specific selling context |
| All schema `description` values | City-specific editorial descriptions |

---

## Time Estimate Per Clone

| Task | Time |
|---|---|
| Global find/replace (Steps 2A–2I) | 15 min |
| Stats bar + hero + intro (Steps 3–5) | 20 min |
| Seasonal callout + buy/sell module | 15 min |
| 6 corridor cards + descriptions | 60–90 min |
| Inner page content rewrites | 3–5 hours |
| Schema manual updates | 30 min |
| CF Pages + DNS + GSC setup | 30 min |
| Pre-launch verification | 20 min |
| **Total** | **~6–8 hours** |

The 6–8 hours is all editorial. The technical scaffolding (nav, breadcrumbs, hero, sticky bar, schema structure, CSS) is zero work — it clones.

---

*Document maintained by Rex Wager / Bridle & Bit Network*  
*Template repo: `aiagent322/wickenburg-horse-property`*
