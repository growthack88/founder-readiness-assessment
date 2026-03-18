# 🤝 Contributing Guide

Thank you for your interest in contributing to the **Founder Readiness Assessment**!

---

## Getting Started

```bash
git clone https://github.com/growthack88/founder-readiness-assessment.git
cd founder-readiness-assessment
python3 -m http.server 8080
# Open http://localhost:8080
```

---

## Project Architecture

The entire application lives in a single file: `index.html`.

```
index.html
├── <head>            — Meta, fonts, CDN scripts, base styles
├── <div id="root">   — React mount point
└── <script type="text/babel">
    ├── dimensions[]  — Assessment content (questions, colors, icons)
    ├── levelConfig   — Archetype definitions & advice
    ├── getLevel()    — Score → archetype mapping
    ├── RadialChart   — Animated circular score component
    ├── DimensionBar  — Animated dimension progress bar
    └── FounderReadiness — Main app (3 screens: landing, quiz, results)
```

---

## Customizing Questions

Find the `dimensions` array near the top of the `<script>` block:

```javascript
const dimensions = [
  {
    id: "mindset",
    title: "عقلية المؤسس",       // Arabic title
    titleEn: "Founder Mindset",  // English subtitle
    icon: "🧠",
    color: "#E8A838",            // Hex color for this dimension
    questions: [
      "Question text in Arabic...",
      // Add or remove questions here
    ]
  },
  // ... more dimensions
];
```

**Rules:**
- Keep questions as first-person statements, not yes/no questions
- Ideal range: 6–10 questions per dimension
- Colors should be distinct and visible against the `#0a0a0f` dark background

---

## Customizing Archetypes

```javascript
const levelConfig = {
  explorer: { title: "مستكشف", range: "0-25%", emoji: "🌱", ... },
  builder:  { title: "بانٍ",    range: "26-50%", emoji: "🔨", ... },
  launcher: { title: "منطلق",   range: "51-75%", emoji: "🚀", ... },
  master:   { title: "مؤسس جاهز", range: "76-100%", emoji: "👑", ... }
};

function getLevel(pct) {
  if (pct <= 25) return levelConfig.explorer;
  if (pct <= 50) return levelConfig.builder;
  if (pct <= 75) return levelConfig.launcher;
  return levelConfig.master;
}
```

Edit thresholds in `getLevel()` or text/color/advice in `levelConfig` freely.

---

## Scoring System

Each question is rated on a **0–3 scale**:

| Value | Arabic | English |
|-------|--------|---------|
| 0 | لا ينطبق | Not at all |
| 1 | قليلاً | Slightly |
| 2 | غالباً | Mostly |
| 3 | تماماً | Absolutely |

Overall score: `(total points) / (max possible points) × 100%`

With 8 dimensions × 8 questions × 3 max = **192 max points**.

---

## Branding / White-Label

To customize the tool for your accelerator or program:

1. Update `<title>` tag in the `<head>`
2. Update the landing page badge text (`Founder Readiness Assessment`)
3. Update the footer book attribution line
4. Replace primary gold color `#E8A838` with your brand color
5. Update the book quote in the results screen

---

## Pull Request Guidelines

1. Fork the repository
2. Create a branch: `git checkout -b feature/your-feature-name`
3. Make your changes
4. Test in at least Chrome (latest)
5. Submit a PR with a clear description

**Commit format:**
```
type: short description

feat: add new dimension questions
fix: correct score calculation
docs: update deployment guide
style: improve mobile layout
```

---

## Reporting Issues

Open a GitHub Issue with:
- Browser name and version
- Device type (desktop / mobile)
- Screenshot if possible
- Steps to reproduce

---

*Made with ❤️ by [Mahmoud Omar](https://mahmoudomar.com)*
