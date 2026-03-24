# Claude instructions for this repo

This repo contains single-file HTML tools. Read `README.md` for full project conventions.

## Key rules when building or modifying tools

- Each tool is a **single `.html` file** — inline CSS and JS, no external files
- **No React, no build steps** — vanilla JS only, load libraries from CDNs
- Keep tools **small** (a few hundred lines)
- Store API keys in **localStorage**, never in source
- Name files descriptively: `tool-name.html`

## Design system (strict)

Follow the "Productivity Minimalist" style described in `README.md` — full spec is there. The non-negotiable rules:

- **Colors**: `#111827` for text (never `#000000`), `#E5E7EB` for borders, ONE accent color (`#2563EB`) for primary actions only
- **Typography**: system font stack, weight 600 + tight letter-spacing for headings, weight 500 for UI, 400 for body
- **Buttons**: flat color, no gradients, `border-radius: 6px`, subtle hover (opacity or slight darken)
- **Inputs**: white bg, light border, dark focus ring (`#111827`) — no glows, no colored rings
- **Shadows**: `0 1px 2px 0 rgba(0,0,0,0.05)` for cards — no large fuzzy shadows
- **Spacing**: generous padding, whitespace is a design element
- **Always use CSS custom properties** from `:root` — never hardcode colors

Start every tool with the `:root` variables block from README.md.
