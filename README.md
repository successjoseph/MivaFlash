# MivaFlash — Miva Techies Flashcards

![HTML](https://img.shields.io/badge/HTML-Static%20Web%20App-orange)

## Table of Contents
- [About](#about)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Testing](#testing)
- [Contributing](#contributing)
- [Authors and License](#authors-and-license)

## About

MivaFlash is a two-page client-side flashcard study app built for "Miva Techies" students. `index.html` is the student-facing app: a typewriter-animated landing screen introducing a guide character named "NYMO", a Cohort/Level and Course selector, and a swipeable flashcard carousel with next/prev navigation and touch-swipe support. `admin.html` is a companion content-management console for adding, editing, and deleting cohort folders, courses, and individual flashcards, plus an AI-assisted "batch generate" feature that sends pasted notes to the Google Gemini API to extract flashcards automatically, and an "Enhance" button that asks Gemini to clean up a single card's wording. Both pages share the same data model, persisted entirely in browser `localStorage` under the key `mivaDB` (no backend/server component exists). The admin page gates access with a simple client-side check against a base64-encoded password string, which is a convenience gate rather than real authentication since it runs entirely in the browser and the encoded password is visible in the page source.

## Prerequisites

- A modern web browser with `localStorage` support.
- For the AI features in `admin.html` to work, a Google Gemini API key must be supplied — the `apiKey` constant in `admin.html` is currently left blank (`const apiKey = "";`), so AI generation/enhancement will fail until a key is added.

## Installation

```bash
git clone https://github.com/successjoseph/MivaFlash.git
cd MivaFlash
```

No package manager or build step is used; both pages load Tailwind CSS from the CDN (`https://cdn.tailwindcss.com`) at view time.

## Configuration

| Location | Setting | Notes |
|---|---|---|
| `admin.html`, `const apiKey` | Google Gemini API key | Currently empty; required for the AI flashcard extraction/enhancement features to function. |
| `admin.html`, `targetHash` | Base64-encoded admin password | Hardcoded client-side gate; not a secure authentication mechanism. |
| Browser `localStorage['mivaDB']` | The flashcard database | Seeded with a small default dataset (`200lvl_sem2` / CSC 204, `100lvl_sem1` / MTH 101) on first load if not already present. |

## Usage

Serve or open the files directly:
```bash
python -m http.server 8000
```
- Visit `index.html` to browse/study flashcards as a student.
- Visit `admin.html` (linked from the heart icon in the footer of `index.html`) to log in and manage the cohort/course/flashcard data. The "Clear Cache" action is triggered by clicking the "MT" logo, which resets `localStorage['mivaState']` and reloads.

## Testing

No automated tests are currently included.

## Contributing

This is a personal/community utility project (for the Miva Techies student group) rather than an open contribution target. Notes above are for future-you when revisiting the code.

## Authors and License

- **Author:** successjoseph ([github.com/successjoseph](https://github.com/successjoseph))
- **License:** No license file included in this repository — all rights reserved by default.
