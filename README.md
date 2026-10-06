# Clinic Call List Dashboard

A lightweight, mobile-first, zero-dependency single-page web application designed for clinic owners and healthcare staff to track, search, and manage incoming patient calls and appointment inquiries.

Built with **vanilla HTML, CSS, and modern JavaScript in a single self-contained file (`index.html`)**. No build tools, package managers, or external libraries required.

---

## 🚀 Quick Start

### Option 1: Direct File Access (No Server Required)
Simply double-click [`index.html`](./index.html) in your file explorer, or open it directly in any browser:
```powershell
Start-Process "index.html"
```

### Option 2: Local HTTP Server (Optional)
If you prefer running via a local HTTP server:
```bash
# Using Python
python -m http.server 3000

# Using Node.js npx
npx serve .
```
Then visit: `http://localhost:3000`

---

## 📱 Features

- **Mobile-First Responsive Layout**: Optimized for 375px phone viewports (iPhone SE / standard smartphones) with zero horizontal scrolling, extending smoothly up to desktop widths (centered `640px` max-width).
- **Instant Name Search**: Real-time filtering across caller names on every keystroke (case-insensitive substring match).
- **Smart Sticky Header**: Clean header with frosted glass backdrop blur (`backdrop-filter: blur(10px)`) that anchors the title, search box, and counter as you scroll through calls.
- **Dynamic Content Clamping**: Summaries that exceed 3 lines are clamped and automatically display an accessible `<button>` toggle (**"Show more"** / **"Show less"**) using real DOM measurement.
- **Accessible Design (WCAG AA)**:
  - Touch targets sized to at least `44px` height.
  - Form inputs set to `16px` font size to eliminate iOS auto-zoom on focus.
  - High-contrast clinical color palette.
  - Semantic markup (`<header>`, `<main>`, `<ul role="list">`, `<article>`).
  - Screen reader support with `aria-live="polite"` regions for dynamic count updates and empty state alerts.
  - Full support for `prefers-reduced-motion`.

---

## 🛡️ Edge Cases Handled

| Edge Case | Description | Handled Implementation |
| :--- | :--- | :--- |
| **Duplicate Records** | Record `id: 7` appears twice in source data. | Automatically deduplicated by unique `id` prior to rendering so it displays once. Total counts accurately reflect unique callers (7 items). |
| **Missing Caller Name** | Record `id: 3` has `name: null`. | Rendered as *"Unknown caller"* in muted italic style. Searching for `"unknown"` reliably finds this record. |
| **Inconsistent Casing** | Record `id: 5` is `"priya nair"` in lowercase. | Normalized to proper Title Case (*"Priya Nair"*) without mutating the underlying data. |
| **Long Names & Summaries** | Record `id: 4` has a long multi-part name and lengthy summary text. | Text breaks and wraps neatly without layout overflow. Clamps to 3 lines with dynamic Show more/Show less expansion. |
| **HTML Injection in Data** | Record `id: 6` contains raw `<b>very</b>` tags. | Safely rendered as literal text characters using `textContent`, preserving clinic records and preventing XSS. |
| **Empty Summary Text** | Records `id: 2` and `id: 5` have empty summaries (`""`). | Displays a muted *"No summary"* label instead of empty blank space. |
| **Duration Formatting** | Raw seconds converted to human-readable strings. | `137s` &rarr; `2m 17s`, `64s` &rarr; `1m 4s`, `59s` &rarr; `59s`, `3725s` &rarr; `1h 2m 5s`. For `0s` on failed/no-answer calls, displays an em dash (`—`). |
| **Status Mapping** | Raw status identifiers mapped to visual badges. | `answered` &rarr; Green (*Answered*), `failed` &rarr; Red (*Failed*), `no_answer` &rarr; Amber (*No answer*), Unknown &rarr; Neutral badge. Badges use both colored dots and visible text for accessibility. |
| **Zero Search Matches** | Query returns no records (e.g. `"zzz"`). | Displays friendly empty state (`No calls match "xyz"`) and updates count to `Showing 0 of 7 calls`. |

---

## 📂 Repository Structure

```text
Logictap/
├── index.html       # Single self-contained application (HTML + CSS + JS)
├── .gitignore       # Git ignore rules for editor files and artifacts
└── README.md        # Project documentation and architectural overview
```

---

## 🛠️ Tech Stack

- **HTML5**: Semantic document structure.
- **Vanilla CSS**: Custom properties (CSS variables), Flexbox, CSS line clamp, backdrop filters.
- **Vanilla JavaScript (ES6+)**: Pure functional data normalization, DOM manipulation, and event handling.
- **Zero Dependencies**: No React, Vue, jQuery, Tailwind, CDN links, or build tools.

---

## 📄 License

MIT License. Open for personal and commercial clinic management use.
