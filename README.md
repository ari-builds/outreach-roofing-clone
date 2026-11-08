# Outreach Roofing — Static Clone & Analysis

Complete static clone of [outreach-roofing.com](https://outreach-roofing.com) with comprehensive architecture analysis.

## 🏗️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Framework** | React 18.3.1 (production build) |
| **Build Tool** | Vite (ES modules, code-split chunks) |
| **Styling** | Tailwind CSS (utility classes) |
| **Animation** | Framer Motion 11.x |
| **Routing** | React Router v6 (SPA) |
| **Icons** | Inline SVG paths |
| **Analytics** | Plausible.io |
| **Reviews** | Elfsight (external) |

---

## 📁 Project Structure

```
outreach-roofing-clone/
├── index.html                    # SPA entry point
├── assets/
│   ├── index-C4--TScq.css        # Tailwind CSS (115KB)
│   ├── index-aicoXCeA.js         # React app entry
│   ├── framer-motion-OcBjDxyj.js # Framer Motion + React
│   ├── react-vendor-xwh5lo3K.js  # React + Router
│   ├── Services-CAquVrhv.js      # Services listing
│   ├── About-FBCITjZt.js         # About page
│   ├── ResidentialRoofing-BJvYxwJh.js
│   ├── CommercialRoofing-DYORnn9I.js
│   ├── StormDamageRepair-DQQ3PBkm.js
│   ├── Siding-DhRJdXYv.js
│   ├── Gutters-Aju8l2qf.js
│   ├── SolarInstallation-B9LMK2Hr.js
│   ├── TreeRemoval-B-Y-Xk_v.js
│   ├── TurnkeyConstruction-vstit0uR.js
│   ├── Contact-B8BLaQiW.js
│   ├── FAQ-sAIp2lZ7.js
│   ├── ReviewsSection-UrNVN6-a.js
│   ├── NotFound-C8CenBzp.js
│   ├── Success-B-ZsUbZM.js
│   ├── Hero images (mobile/desktop)
│   ├── 8 service hero + thumbnail images
│   ├── Team photos (3)
│   ├── Logo, favicon
│   └── 6 font files (Poppins, Roboto, Montserrat)
└── fonts/ (6 .woff2 files)
```

---

## 🧠 Architecture Analysis

### 1. Route Mapping (Single Source of Truth)
```javascript
// Services-CAquVrhv.js
const services = [
  {name:"Residential Roofing", path:"residential-roofing"},
  {name:"Commercial Roofing", path:"commercial-roofing"},
  {name:"Storm Damage Repair", path:"storm-damage-repair"},
  // ... 5 more
];
```
- `/services` redirects to `/services/residential-roofing`
- Active tab state synced with URL via `useLocation()`

### 2. Animation System (3-Tier Framer Motion)
```javascript
const pageEnter = {hidden:{opacity:0}, visible:{opacity:1,transition:{staggerChildren:.15,duration:.6}}}
const contentUp = {hidden:{opacity:0,y:30}, visible:{opacity:1,y:0,transition:{duration:.5,ease:"easeOut"}}}
const cardScale = {hidden:{opacity:0,scale:.95}, visible:{opacity:1,scale:1,transition:{duration:.8}}}
```
- **Page entrance**: fade + stagger children
- **Content blocks**: slide up 30px
- **Cards/images**: scale from 0.95
- **Viewport trigger**: `whileInView` + `viewport={{once:true, margin:"-100px"}}`

### 3. Schema.org SEO (Every Page)
```json
// Homepage: RoofingContractor + FAQPage + WebSite + VideoObject
// Service pages: Service + BreadcrumbList + VideoObject
// About: Person (×3) + BreadcrumbList
// Rich snippets for local business, services, team, FAQs
```

### 4. Component Composition
```jsx
<Layout>
  <Header />        // Nav, logo, phone CTA
  <Main />          // Page content
  <Footer />        // Links, contact, social
  <Scripts />       // Elfsight, Plausible, YouTube
</Layout>
```

---

## 🎨 Design System

| Token | Value |
|-------|-------|
| Primary | `#3A6ACB` |
| Primary Gradient End | `#1C3D72` |
| Background | `#FAFAFA` |
| Text Primary | `#1C3D72` |
| Text Body | `#475569` |
| Font Headings | Poppins (600/700) |
| Font Body | Roboto (400/500) |
| Font Buttons | Montserrat (600) |
| Container Max | 1280px (7xl) |
| Transition | 150ms cubic-bezier(0.4,0,0.2,1) |

---

## 🚀 Running Locally

### Option 1: Python (simplest)
```bash
cd outreach-roofing-clone
python -m http.server 8000
# Open http://localhost:8000
```

### Option 2: Node `serve` (SPA fallback)
```bash
cd outreach-roofing-clone
npx serve -s . -l 3000
# Open http://localhost:3000
```

### Option 3: Vite Dev Server (if you have source)
```bash
npm install
npm run dev
```

---

## 🌐 Deployment

### GitHub Pages
1. Enable GitHub Pages in repo settings
2. Set source to "GitHub Actions"
2. Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: .
      - uses: actions/deploy-pages@v4
```

### Netlify / Vercel
- Connect repo → Auto-detects SPA → Deploys

---

## ⚠️ Limitations (Static Clone)

| Feature | Status |
|---------|--------|
| HTML/CSS/JS/Fonts/Images | ✅ Complete |
| Client-side Routing | ✅ Works with `serve -s` |
| Elfsight Reviews | ✅ Loads from elfsight.com |
| Plausible Analytics | ✅ Loads from plausible.io |
| YouTube Videos | ✅ Embedded from YouTube |
| Dynamic API calls | ⚠️ Some calls to outreach-roofing.com |
| Service page images | ✅ All 16 images downloaded |

---

## 📋 Service Pages Included

| Service | Hero Image | Thumbnail |
|---------|------------|-----------|
| Residential Roofing | ✅ | ✅ |
| Commercial Roofing | ✅ | ✅ |
| Storm Damage Repair | ✅ | ✅ |
| Siding | ✅ | ✅ |
| Gutters | ✅ | ✅ |
| Solar Installation | ✅ | ✅ |
| Tree Removal | ✅ | ✅ |
| Turnkey Construction | ✅ | ✅ |

---

## 📊 Key Metrics

| Metric | Value |
|--------|-------|
| Total Files | 40+ |
| Total Size | ~15 MB |
| CSS Bundle | 115 KB |
| JS Bundle (gzipped) | ~63 KB |
| Fonts | 6 × .woff2 |
| Images | 25+ .webp/.png |
| Fonts | 6 families |

---

## 🔧 Customization

### Colors (in CSS variables)
```css
:root {
  --primary: #3A6ACB;
  --primary-gradient-end: #1C3D72;
  --background: #FAFAFA;
}
```

### Fonts
Replace `.woff2` files in `/fonts/` and update `index-C4--TScq.css` `@font-face` declarations.

### Content
Edit the JS chunks in `/assets/` or rebuild from source.

---

## 📄 License

Cloned for educational/analysis purposes. Original site © Outreach Roofing and Construction.

---

*Cloned and analyzed on 2026-11-08*