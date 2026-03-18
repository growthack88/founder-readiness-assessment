# 🧭 Founder Readiness Assessment

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![No Build Required](https://img.shields.io/badge/build-none%20required-orange?style=flat-square)
![Arabic RTL](https://img.shields.io/badge/language-Arabic%20%2B%20English-purple?style=flat-square)
![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react)

**A bilingual Arabic/English interactive assessment tool for startup founders**
*مبني على كتاب "طريقك لبناء Startup" — محمد حميدة*

[🚀 Live Demo](#) · [📖 Deployment Guide](./DEPLOYMENT.md) · [🤝 Contributing](./CONTRIBUTING.md)

</div>

---

## 📌 Overview

The **Founder Readiness Assessment** is a single-file web application that helps startup founders measure their real readiness across 8 critical dimensions. Built as a lightweight, zero-dependency tool that runs directly in any modern browser — no backend, no database, no build step required.

The tool is based on the book **"طريقك لبناء Startup"** (Your Path to Building a Startup) by **Mohamed Hamida**.

### ✨ What It Does

- Walks founders through **64 carefully crafted questions** across 8 dimensions
- Calculates a readiness score and assigns one of 4 founder archetypes
- Provides visual analytics: radial chart, dimension bars, strength/weakness breakdown
- Gives personalized advice tied to each archetype
- Fully bilingual (Arabic RTL + English labels)
- Mobile-first, responsive design

---

## 🏗️ The 8 Assessment Dimensions

| # | Icon | Dimension (AR) | Dimension (EN) | Questions |
|---|------|----------------|----------------|-----------|
| 1 | 🧠 | عقلية المؤسس | Founder Mindset | 8 |
| 2 | 💡 | وضوح الفكرة | Idea Clarity | 8 |
| 3 | 👥 | الفريق والثقافة | Team & Culture | 8 |
| 4 | 🚀 | المنتج والسوق | Product & Market | 8 |
| 5 | ⚡ | القيادة واتخاذ القرار | Leadership & Decisions | 8 |
| 6 | 💰 | نموذج العمل والتمويل | Business Model & Funding | 8 |
| 7 | ⚖️ | التوازن والاستدامة | Balance & Sustainability | 8 |
| 8 | 🤖 | الجاهزية للذكاء الاصطناعي | AI Readiness | 8 |

---

## 🎯 Founder Archetypes

Based on the final score, founders are placed into one of four levels:

| Score | Archetype (AR) | Archetype (EN) | Description |
|-------|----------------|----------------|-------------|
| 0–25% | 🌱 مستكشف | Explorer | Early awareness stage — focus on self and market understanding |
| 26–50% | 🔨 بانٍ | Builder | Good foundation with critical gaps to fill |
| 51–75% | 🚀 منطلق | Launcher | Ready to launch — sharpen the weakest dimensions |
| 76–100% | 👑 مؤسس جاهز | Ready Founder | Strong position — the market is waiting |

---

## 🖥️ Tech Stack

This is intentionally a **zero-build, zero-dependency** tool:

| Technology | Version | Purpose |
|------------|---------|----------|
| HTML5 | — | Single file, no bundler needed |
| React | 18.2.0 | UI components (loaded via CDN) |
| ReactDOM | 18.2.0 | DOM rendering |
| Babel Standalone | 7.23.9 | JSX transformation in-browser |
| Google Fonts | — | Outfit + Noto Kufi Arabic |
| CSS-in-JS | — | All styles embedded in component |

> **No npm. No build step. No server-side code. Just drop the file and serve.**

---

## 🚀 Quick Start

### Option 1: Direct File Open (Instant Preview)

```bash
git clone https://github.com/growthack88/founder-readiness-assessment.git
cd founder-readiness-assessment
open index.html   # macOS
# or double-click index.html in your file explorer
```

> ⚠️ Some browsers restrict local file fonts. For best results, serve via a web server.

### Option 2: Python Local Server (Recommended for Dev)

```bash
git clone https://github.com/growthack88/founder-readiness-assessment.git
cd founder-readiness-assessment

# Python 3
python3 -m http.server 8080

# Python 2
python -m SimpleHTTPServer 8080
```

Then open `http://localhost:8080` in your browser.

### Option 3: Node.js Local Server

```bash
npx serve .
# or
npx http-server . -p 8080
```

---

## 🌐 Production Deployment

See the full **[Deployment Guide](./DEPLOYMENT.md)** for step-by-step instructions for:

- ✅ Apache / Nginx web server
- ✅ cPanel shared hosting
- ✅ GitHub Pages (free)
- ✅ Vercel / Netlify (free)
- ✅ Docker container
- ✅ Custom subdirectory deployment

---

## 📁 Project Structure

```
founder-readiness-assessment/
│
├── index.html          # The entire application (single file)
├── README.md           # This file
├── DEPLOYMENT.md       # Server deployment instructions
├── CONTRIBUTING.md     # Contribution guidelines
├── CHANGELOG.md        # Version history
├── SECURITY.md         # Security policy
└── LICENSE             # MIT License
```

---

## 🎨 Customization

All content is defined in the `dimensions` array near the top of `index.html`. You can easily:

- **Add/remove questions** — edit the `questions` arrays inside each dimension object
- **Change dimension colors** — update the `color` hex values
- **Update archetype thresholds** — edit the `getLevel()` function
- **Change branding/copy** — update the landing page text and book reference
- **Add a new dimension** — push a new object into the `dimensions` array

See [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed customization guidelines.

---

## 🔒 Privacy & Data

This tool is **100% client-side**. All assessment answers:
- Are stored only in browser memory (React state)
- Are **never sent to any server**
- Are **erased** when the page is refreshed or the session ends
- Require no user accounts, emails, or cookies

This makes it ideal for privacy-sensitive deployments in accelerators, universities, and corporate innovation labs.

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](./LICENSE) for details.

The assessment content is inspired by the book **"طريقك لبناء Startup"** by **Mohamed Hamida**.

---

## 🤝 Built By

Developed by **[Mahmoud Omar](https://mahmoudomar.com)** — Growth & E-commerce Consultant, MENA.

---

<div align="center">

*If you find this useful, consider giving it a ⭐ on GitHub!*

</div>
