# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hospital opening and operating cost calculator (병의원 개원비용 및 운영비용 계산기) for HorangPharm. This is a single-page static web application written entirely in one `index.html` file — no build system, no dependencies, no tests.

## Development

Open `index.html` directly in a browser. No build step or server required. Tailwind CSS is loaded via CDN (`cdn.tailwindcss.com`).

## Architecture

Everything lives in `index.html`: HTML structure, CSS (custom properties + Tailwind), and vanilla JavaScript.

**Data model:** `defaultData` object with two top-level categories:
- `opening` — one-time startup costs (realEstate, equipment, supplies, reserve)
- `operating` — monthly recurring costs (labor, fixed, variable)

Each input field is linked to the data model via `data-category`, `data-section`, and `data-field` attributes.

**Key functions:**
- `calculateOpeningCosts()` / `calculateOperatingCosts()` — sum values per section
- `updateAllTotals()` — recalculates all subtotals/totals and updates the DOM
- `formatKoreanCurrency()` — converts numbers to Korean 억/만원 notation
- `handleInputChange()` — debounced (300ms) input handler that syncs input → data model → totals

**State persistence:** User-modified values are saved to `localStorage` under key `costCalculatorData` and restored on page load.

**PDF export:** Uses `window.print()` with extensive `@media print` CSS rules to produce a clean A4 layout.

## Language

All UI text and code comments are in Korean. Maintain Korean for user-facing strings.
