# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project type

Single static HTML site — one self-contained `index.html` with inline `<style>` and `<script>`. No build step, no package manager, no tests, no dependencies beyond two CDN resources (Google Fonts + Unsplash images). Open `index.html` directly in a browser to preview.

## What it is

A single-page bridal photography booking website (brand: "Eternal Moments"). Lead-gen marketing page where visitors browse packages and submit a booking inquiry form. Inquiries POST as JSON to [formsubmit.co](https://formsubmit.co) (`/ajax/wolfgangs246@gmail.com`), which relays them to email — no backend.

## Where things live in `index.html`

The file is large but linearly organized. Edits should land in the right region:

- `<style>` block at top — CSS custom properties (`:root`), then sections in this order: base/typography, buttons, nav, hero, about, packages, gallery, booking, contact, footer, responsive media queries, `prefers-reduced-motion`.
- `<body>` sections in order, each with a matching `id`: `#hero`, `#about`, `#packages`, `#gallery`, `#booking`, `#contact`, plus `<footer>`.
- `<script>` block at bottom — sticky-nav scroll state, mobile menu toggle, package "Choose" buttons (preselect form dropdown), form submission handler.

## Design tokens (keep edits consistent)

All colors, fonts, shadows, and timings are defined as CSS custom properties on `:root` near the top of `<style>`. Use the variables — don't hardcode new values. Palette is baby blue (`--baby-light/--baby/--baby-deep`) with gold accents (`--gold/--gold-deep`) and a deep navy primary (`--navy`) on an ivory base. Headings use `Cormorant Garamond` (italic-leaning), body uses `Lato`.

Note: shadows and dark-tone overlays use the navy RGB triplet `26, 39, 69` directly (e.g., `rgba(26, 39, 69, 0.10)`) because CSS custom properties can't be interpolated inside `rgba()`. If you change `--navy`, find-and-replace the matching rgb triplet in shadow values, the hero overlay, gallery hover tint, and form-field borders.

## Form submission contract

`POST https://formsubmit.co/ajax/wolfgangs246@gmail.com` with `Content-Type: application/json`. The submit handler builds the body from `FormData` keyed by each input's `name` attribute (which use Title Case strings like `"Full Name"`, `"Preferred Date"` — these become the email field labels, so don't rename casually). Three formsubmit-specific fields are also injected: `_subject`, `_template`, `_captcha`.

**Important gotcha:** formsubmit.co requires a one-time activation. The first submission to a new endpoint email triggers a confirmation email to that address; the link must be clicked once before any inquiry actually relays. This is expected behavior, not a bug.

## Image strategy

All photographs are loaded from Unsplash via the stable CDN pattern `https://images.unsplash.com/photo-{ID}?auto=format&fit=crop&w={W}&q=80`. Hero image is `eager`, all others are `loading="lazy"`. To swap an image, replace the `{ID}` portion only — the URL pattern is intentionally uniform across all `<img>` tags and the hero `background` so a find-and-replace works.

## Placeholder content (must be swapped before going live)

The site reads as finished but is populated with invented content. Single-string find-and-replace candidates: brand name `Eternal Moments`, photographer name `Sophia`, prices `$1,800` / `$2,800` / `$4,200` (each appears in both a package card and the booking-form `<select>`), email `hello@eternalmoments.co`, phone `+1 (555) 555-0199`, studio location `Portland, Oregon`. The booking-endpoint email (`wolfgangs246@gmail.com`) is real and embedded in the `<script>` fetch URL — change it there if the photographer's address changes.

## `.claude/` subdirectories

Empty `agents/`, `commands/`, `hooks/`, `skills/` folders exist for future Claude Code customization but contain nothing yet. They are not part of the deployed site.
