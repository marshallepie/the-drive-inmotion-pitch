# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains the investor pitch deck for **The Drive** — a global automotive asset exchange platform targeting InMotion Ventures for a $5M seed round. It is not an application codebase; it is a presentation artifact.

## Contents

```
pitch/
├── inmotion-pitch-deck.html   # Interactive single-file HTML presentation (~3MB)
└── inmotion-pitch-deck.pdf    # Static PDF export of the same deck
```

## Pitch Deck Architecture

The HTML deck is a **self-contained single-file presentation** with no external dependencies:

- All CSS is inline in a `<style>` block at the top
- All images are embedded as base64 data URIs (accounts for the large file size)
- Navigation logic is in a small `<script>` block at the bottom (~70 lines)
- Each slide is a `<section class="slide" id="sN">` element; the active slide gets `class="slide active"`
- `cur` (0-indexed integer) tracks the current slide; `goTo(idx)` drives all transitions
- Slide navigation: arrow keys, on-screen prev/next buttons, clickable dot indicators, and touch/swipe

### Slide IDs (in order)

| ID | Title |
|----|-------|
| `s1` | Title / Hero |
| `s2` | OEMs Lose Visibility After the First Sale |
| `s-asian` | Strong Asian Demand for UK Premium Vehicles |
| `s3` | Three Converging Forces. One Window. |
| `s-pekema` | PEKEMA: The Gateway to Malaysian Market Distribution |
| `s4` | Three-Layer Architecture for Automotive Assets |
| `s-jlr` | What This Platform Delivers for Jaguar Land Rover |
| `s5` | Phase 1 Is Live. Right Now. |
| `s-uksupply` | Unlocking the UK's Premium Vehicle Supply |
| `s6` | A $2 Trillion Global Opportunity |
| `s7` | Five Revenue Streams. Sustainable Platform Economics. |
| `s8` | The Drive vs The Incumbents |
| `s9` | Institutional Demand. Before We've Launched. |
| `s-token` | From Physical Asset to Financial Instrument |
| `s10` | Four Strategic Phases to Global Exchange |
| `s11` | Automotive Expertise Meets Web3 Infrastructure |
| `s12` | $5M Seed Round |
| `s13` | Perfect Alignment with InMotion's Investment Thesis |
| `s14` | Closing / CTA |

### Design System (CSS variables)

```css
--bg: #000000          /* page background */
--gold: #c9a96e        /* primary accent */
--gold-light: #e8c98a  /* gradient end */
--blue: #3b82f6        /* secondary accent */
--green: #22c55e       /* positive indicators */
--red: #ef4444         /* contrast/warning */
--card-bg: #111111     /* slide card backgrounds */
--muted: rgba(255,255,255,0.72)
--dim:   rgba(255,255,255,0.40)
```

## Editing the Deck

To add or reorder slides: add/move a `<section class="slide" id="sX">` block, then update the dot indicators in `#dots` to match the new total count. The JS reads `slides` and `dots` NodeLists dynamically so slide count is self-updating.

To update images: replace the base64 `src` on the relevant `<img>` tag. Keep images small to avoid bloating the file further.

To preview: open `pitch/inmotion-pitch-deck.html` directly in a browser — no build step required.

## Generating a New PDF

Open the HTML in Chrome, press `Cmd+P` → Save as PDF (background graphics on, margins: none, A4 landscape or match current aspect ratio).
