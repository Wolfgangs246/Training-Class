# Eternal Moments — Bridal Photography

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Google Fonts](https://img.shields.io/badge/Google_Fonts-4285F4?style=flat&logo=google&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222?style=flat&logo=github)

> **Live site:** [wolfgangs246.github.io/Training-Class](https://wolfgangs246.github.io/Training-Class/)

## About

A single-page bridal photography booking website (brand: *Eternal Moments*). Visitors browse packages, view a portfolio gallery, and submit a booking inquiry that's relayed via [formsubmit.co](https://formsubmit.co) — no backend required. Built as one self-contained `index.html` with inline CSS + JS, styled in a navy / baby-blue / gold palette.

## Screenshot

![Screenshot](./screenshot.png)

## File structure

```
.
├── .github/
│   └── workflows/
│       └── pages.yml          # GitHub Pages deployment workflow
├── .gitignore
├── .mcp.json                  # Playwright MCP server config (Claude Code)
├── CLAUDE.md                  # Guidance for Claude Code in this repo
├── README.md
├── index.html                 # The entire site (HTML + inline CSS + JS)
└── screenshot.png             # Site preview, captured via Playwright
```

## How to use

### Preview locally

The site is a single static file — open it directly in any browser:

```bash
# Windows
start index.html

# macOS
open index.html

# Linux
xdg-open index.html
```

Or serve it over HTTP if you prefer (some browsers behave better with HTTP than `file://`):

```bash
npx -y http-server -p 8000
# then visit http://localhost:8000
```

### Customize before going live

The site ships with placeholder content. Single-string find-and-replace targets:

| Find | Replace with |
|---|---|
| `Eternal Moments` | your brand |
| `Sophia` | photographer name |
| `$1,800` / `$2,800` / `$4,200` | your package prices (each appears in a card *and* the booking form `<select>`) |
| `hello@eternalmoments.co` | real contact email |
| `+1 (555) 555-0199` | real phone |
| `Portland, Oregon` | real studio location |

The booking form's submission endpoint is hardcoded near the bottom of `<script>` in `index.html`:

```js
fetch('https://formsubmit.co/ajax/wolfgangs246@gmail.com', { ... })
```

Update the email there to point inquiries to your inbox. **Note:** [formsubmit.co](https://formsubmit.co) requires a one-time activation — the first submission to a new endpoint email triggers a confirmation email; the link must be clicked once before any inquiry actually relays.

### Deploy

This repo auto-deploys to GitHub Pages via [`.github/workflows/pages.yml`](.github/workflows/pages.yml) on every push to `main`.
