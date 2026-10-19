# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is a **client project workspace**, not a software codebase. It holds the briefing and design materials for a new website for "Radwerk Mitte" (a regional bike/e-bike dealer and workshop in Kassel/Göttingen, Germany), produced as part of a Business Trends Academy workshop engagement. There is no build system, package manager, test suite, linter, or application source code here — do not look for or invent `npm`/build/test commands.

Top-level contents:
- `PRD – Neue Website Radwerk Mitte.pdf` / `Radwerk_PRD_Kurzfassung.pdf` — the product requirements doc for the new website (full and short versions).
- `Firmensteckbrief-Radwerk-Mitte-BTA.pdf` — company profile/fact sheet for Radwerk Mitte.
- `Übung_Kundengespräch_Protokoll.pdf` — protocol/notes from a client conversation exercise.
- `Radwerk_Mitte_Designvorgaben/` — the design specification for the website (see below). This is the most structured, actionable part of the repo.
- `Radwerk-Mitte.code-workspace` — a VS Code multi-root workspace that also references a sibling folder in `~/Downloads/Radwerk_Mitte_Designvorgaben` (an external copy outside this repo; don't assume it's in sync).

## `Radwerk_Mitte_Designvorgaben/` — the design system spec

This folder defines "Stufe 1" (stage 1) of the website's design and is meant to be handed to Claude for implementation work. No website code exists yet; this is the source of truth future implementation should follow.

- `LIESMICH.txt` — index/README for this folder (German), explains what each file is for.
- `README.md` — the main rulebook: JobRad-style structural orientation (what's borrowed vs. Radwerk-specific), color rules, typography, layout/grid, component quick-rules, imagery/icons, tone of voice, and accessibility requirements.
- `Glow-Akzente.md` — detailed rules for the "Glow" dark accent panels (used only for digital/electric content: leasing calculator results, repair status, e-bike specs). Strict limits: max one per screen height, max two per page, no permanent animation, specific allowed/forbidden uses.
- `Seitenaufbau.md` — the homepage section-by-section layout (11 sections in order: header, hero, trust bar, leasing calculator, "how it works", audience tiles, testimonial, workshop/status, FAQ, contact, footer), each with its background surface and Glow usage.
- `tokens.json` — the full design token set (colors for both "hell"/light and "glow"/dark themes, type scale, spacing, radii, shadows, layout). This is the canonical source for any CSS variables/tokens used in implementation.
- `design-system.json` — metadata/index pointing at a Claude-side design-system artifact (not consumable application config).
- `components/` — per-component spec: each subfolder (`Button`, `AudienceCard`, `GlowPanel`, `Steps`, `Cover`) has a short `README.md` with usage rules and a standalone `preview.html` (self-contained HTML/CSS snippet, no build step — open directly in a browser; references `../../tokens.css`, which is *not yet present* in the folder, and Google Fonts, so previews need internet access and the token CSS file to render correctly).

### Key design constraints to respect in any future implementation

- **Color discipline**: ~80% light surfaces, ~15% `radblau` (house blue), ~5% `koralle` (coral accent) + glow. `koralle` is only ever a filled surface with `nachtblau` (dark) text — never as text color, never with white text. `cyan-strom` is only used on dark (`nachtblau`) backgrounds, never on light.
- **Glow panels** are the "digital" signal and are deliberately rare — never for body text, forms, price lists, legal text, or error messages.
- **Language/tone**: German, formal "Sie", typographic quotes, short factual sentences, no superlatives.
- **Accessibility is a hard requirement**: 4.5:1 text contrast, 3:1 for large text/controls (in both light and glow themes), `prefers-reduced-motion` respected, 44×44px minimum touch targets, status always conveyed with icon + word (never color alone).
- Phone number and both locations (Kassel, Göttingen) must appear on every page (header phone, footer addresses/hours).
- No real logo file yet — until delivered, use the "radwerk mitte" wordmark convention described in `README.md` section 7.

## Working in this repo

- Files are primarily German-language; keep terminology and tone consistent with existing docs when editing or extending them.
- When asked to implement the website itself, treat `Radwerk_Mitte_Designvorgaben/` as the spec to build against, and flag it to the user if a referenced file (e.g. `tokens.css`) is missing rather than inventing its contents.
