# 8th RPO Conference — Live Display & Control App

A single self-contained web app (`index.html`) that drives the projector at the
**8th Annual RPO Conference for Medical Facilities**
(14–17 July 2026 · David Livingstone Safari Lodge · Livingstone, Zambia),
hosted by the Radiation Protection Authority of Zambia (RPA).

It is both the **control hub** (operator view) and the **big-screen display**
(audience view), in one file with no build step, no server and no logins.

---

## Quick start

1. Open `index.html` in Chrome/Edge → this is the **Control Panel**.
2. Click **🖥 Open Display Window** → the projector-output window opens.
   With a projector/second screen attached, Chrome/Edge places it there
   automatically (allow the one-time "manage windows" permission);
   otherwise drag it onto the projector screen yourself.
3. Click **⛶ Go fullscreen** on the banner (or press **F** / double-click).
4. Enter your speakers under **People**, pick a scene, press **▶ Display …** —
   it appears on the projector with a smooth transition.

The preview inside the control panel is a *mirror* of the display window —
your confidence monitor — so every scene shows in both places at once.

> If pop-ups are blocked or you only have one screen, use
> **⛶ Fullscreen preview** on the control panel instead.

The display can also be opened manually: `index.html#display`.

## The five scenes

| Scene | What it shows | Live controls |
|---|---|---|
| **① Title / Welcome** | Event name, theme, dates, venue, conference + RPA logos | wording editable in Settings |
| **② Panel Grid** | Everyone (or one category) as circular gold-ring photos with name, affiliation and topic — IAEA-panel style | group picker + custom heading |
| **③ Speaker Spotlight** | One person full-screen: large photo, name, title, topic, session chip and bio | **◀ Prev / Next ▶** steps the queue (also ← / → keys); every person row has an instant **Spotlight** button |
| **④ Countdown & Stats** | Live countdown to the next session + Day X of 4, session count, speaker count, theme | target time, session label, quick-set buttons (+5/+10/+15/+30 min, top of next hour) |
| **⑤ Slides** | An uploaded presentation, full-screen | **◀ Prev / Next ▶**, ← → / PgUp PgDn keys or a presenter clicker; clickable thumbnail strip; per-deck resume position |

**○ Blackout** fades the display to black instantly (and back).

Every scene change is the same smooth crossfade, so you can cut from a slide
to a Speaker Spotlight (or the Countdown) and back **mid-presentation** and it
reads as one continuous show.

## Presenting a PowerPoint

Browsers cannot render `.pptx` files with perfect fidelity, so the app presents
an **exported copy** of the deck — pixel-identical to what PowerPoint shows.
Under **Presentations → ＋ Add presentation** upload either:

1. **A PDF export** — in PowerPoint: *File → Save As → PDF*. The app converts
   each page to a slide (this one-time conversion fetches the pdf.js engine
   from a CDN, so it needs internet **once**; presenting afterwards is fully
   offline).
2. **Slide images** — in PowerPoint: *File → Export → Change File Type → PNG →
   All Slides*, then upload the whole folder of images in one go (they are
   ordered automatically). No internet needed at any point.

Dropping a raw `.pptx` on the app shows these instructions.

### Attach a deck to a speaker

In the person editor (**People → ✎**) pick the speaker's deck under
**Presentation** — or upload it right there with **⬆ Upload deck**. Then:

- their row in People gets a **▤ Slides** button (pushes their deck live);
- the Spotlight panel gets **🎞 Start presentation** — introduce the speaker,
  one click and their slides are on screen;
- the Slides panel gets **👤 Spotlight ‹name›** — one click back to their
  spotlight when the talk ends.

Notes:

- Slides are stored in the browser's **IndexedDB** (they are too large for the
  JSON export). To move a deck to the event machine, use the **⬇** button on
  the deck (downloads a portable `.rpo8deck.json`) and import it there via
  **＋ Add presentation** — or just re-upload the original PDF/images.
- Each deck remembers its position, so cutting away to a Spotlight and coming
  back resumes on the slide you left.
- A presenter clicker (PageUp/PageDown or arrow keys) works while **either**
  window is focused — control panel or projector window.
- Animations/videos inside PowerPoint become still slides; the app supplies
  the transitions between slides instead.

## People & data

Per person: honorific, full name, organisation, topic, session, time slot,
photo (uploaded locally, auto-resized, shown in a circular gold frame), bio and
a category tag (Keynote, Speaker, Panellist, RPA/RPO Official, Organising
Committee — or type your own). Add / edit / delete / reorder from the People
panel; search and filter by category.

- **Persistence** — everything is saved in the browser (`localStorage`)
  automatically, including photos and logos.
- **Export / Import** — the header buttons download / restore the full dataset
  as JSON (people + photos + settings + logos). Export a backup before the
  event and carry it on a USB stick.
- First run loads a sample line-up so every scene demos immediately —
  delete the samples or **Clear ALL data** in Settings.

## Logos

The app looks for logos in this order:

1. Logos uploaded in **Settings → Logos** (stored with the data, travels with
   JSON export — the most reliable option for the event machine).
2. Files placed next to `index.html`: `logos/conf_logo_transparent.png` and
   `logos/rpa_logo.png` (see `logos/README.md`).
3. A neutral typographic fallback, so nothing ever looks broken.

## Tech notes

- Single file, vanilla JS. Brand tokens from `brand/brand.css`
  (Falls Gold `#C9A227`, Gunmetal `#2B2D2F`, Charcoal `#1A1B1D`,
  Mist White `#F7F4EC`; Cinzel / Playfair Display / Inter / Roboto Mono with
  Cambria/Calibri/Consolas fallbacks when offline).
- The display renders on a fixed **1920×1080 stage** that scales to any window,
  so typography is pixel-consistent on the projector.
- Control ↔ display sync uses `BroadcastChannel` with `localStorage`-event and
  polling fallbacks (works from `file://` too).
- Testing helper: `index.html#display?scene=grid|spotlight|countdown|title`
  forces a scene on the display without touching the live state.

## Repo layout

```
index.html          the whole app
logos/              drop the brand PNGs here (see logos/README.md)
brand/              brand tokens, CSS variables and the asset sheet
```
