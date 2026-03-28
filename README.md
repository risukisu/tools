# Tools

A collection of single-file HTML tools — each tool is one `.html` file with inline CSS and JavaScript. No build steps, no frameworks, no dependencies beyond CDN-loaded libraries.

Inspired by [Simon Willison's "Useful patterns for building HTML tools"](https://simonwillison.net/2025/Mar/17/useful-patterns-for-building-html-tools/).

## Principles

1. **One file = one tool.** Everything (HTML, CSS, JS) lives in a single `.html` file. This makes deployment trivial — just serve static files.
2. **No build step.** No React, no Webpack, no npm. If you need a library, load it from a CDN (cdnjs, jsdelivr, unpkg).
3. **Keep it small.** A few hundred lines is ideal. If a tool grows too large, it's probably two tools.
4. **Deploy = copy the file.** GitHub Pages, any static host, or just open locally with `file://`. Zero infrastructure.
5. **Secrets stay client-side.** API keys go in `localStorage`, never in the HTML. Use `prompt()` or a settings panel to collect them.

## Current tools

| File | Description |
|------|-------------|
| `triage.html` | Decision Canvas — a triage/prioritization board for sorting items |
| `firestore.html` | Firestore Recovery Tool — backup and restore Firestore data |
| `ga4-traffic-analyzer.html` | GA4 Traffic Analyzer — drop GA4 CSV exports, get YoY comparison, algorithm impact analysis, and SERP event overlays |

## Creating a new tool

When building a new tool for this repo:

- Start from a blank HTML file with inline `<style>` and `<script>` tags
- Use CDN links for any external libraries (e.g. `https://cdn.tailwindcss.com`, `https://cdn.jsdelivr.net/npm/...`)
- No React or JSX — vanilla JS, or lightweight libs only
- Include `<meta charset="UTF-8">` and `<meta name="viewport" ...>` for mobile support
- Name the file descriptively: `tool-name.html`
- Keep the UI clean and functional — these are utility tools, not marketing pages

## Useful patterns

These patterns from the Simon Willison article apply directly to how we work here:

- **Copy/paste as I/O** — tools that accept pasted content, transform it, and offer a "Copy to clipboard" button
- **Persist state in the URL** — use URL hash/params so users can bookmark or share a specific state
- **localStorage for secrets** — API keys stored client-side only, never exposed in source
- **CORS-friendly APIs** — collect and reuse APIs that support cross-origin requests (GitHub raw content, PyPI, Bluesky, etc.)
- **Remix existing tools** — reference other tools in this repo as working examples when building new ones
- **Debug tools** — build small utilities that help you understand browser capabilities (clipboard formats, CORS support, keyboard events)

## Design system

The visual style is "Productivity Minimalist" — inspired by Linear, Superhuman, and Vercel. Every tool must follow these rules strictly to maintain a cohesive, premium feel.

### Color palette

Use CSS custom properties defined in `:root`:

```css
:root {
    --bg-body: #FFFFFF;        /* or very subtle off-white #F9FAFB */
    --bg-subtle: #F9FAFB;     /* secondary backgrounds, cards */
    --bg-element: #FFFFFF;     /* inputs, interactive elements */
    --text-main: #111827;      /* headings, primary text — never use pure #000000 */
    --text-secondary: #6B7280; /* labels, helper text, timestamps */
    --border-color: #E5E7EB;   /* all borders — thin, 1px */
    --accent-color: #2563EB;   /* ONE accent color for primary actions only */
    --focus-ring: #111827;     /* input focus borders — dark, high contrast */
    --radius: 6px;             /* subtle curve, not pill-shaped */
    --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
    --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}
```

Rules:
- **Never use `#000000` for text** — it causes eye strain. Use `#111827` (dark slate).
- **One accent color only** — used solely for primary action buttons and active links. Everything else is grayscale.
- **Borders are always `#E5E7EB`, 1px** — never thicker, never darker.

### Typography

```css
font-family: -apple-system, BlinkMacSystemFont, "Inter", "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
```

- **Headings**: weight 600, `letter-spacing: -0.025em` (tight tracking for premium feel)
- **UI elements** (buttons, labels, nav): weight 500
- **Body text**: weight 400
- **Never use decorative or serif fonts**

### Components

**Buttons:**
- Flat color or subtle 1px border — **no gradients ever**
- `border-radius: 6px` (not pill-shaped)
- Hover: subtle opacity change (`opacity: 0.85`) or slight darken — no dramatic transforms
- Primary buttons use `--accent-color` bg + white text
- Secondary buttons: transparent bg + `--border-color` border + `--text-main` text

**Inputs:**
- White background, `--border-color` border
- On focus: `--focus-ring` border (dark gray/black), high contrast
- No colored focus rings, no glows

**Cards / containers:**
- `--shadow-sm` only — avoid large fuzzy drop shadows
- 1px `--border-color` border
- `--radius` border-radius

**Spacing:**
- Generous padding is mandatory — whitespace is a primary design element
- Prefer `padding: 16px 20px` or more, never cramped
- Vertical rhythm: consistent gaps between sections (use `gap` in flex/grid)

### CSS custom properties template

Every new tool should start with these variables in `:root` and reference them throughout. Never hardcode color values in individual rules — always use the variables.
