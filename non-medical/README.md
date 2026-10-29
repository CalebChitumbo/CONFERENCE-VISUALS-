# 8th RPO Conference — Non-Medical Edition · Live Display & Control App

Projector app for the **8th Annual Radiation Safety Conference, Non-Medical
Facilities Edition** (3–6 November 2026 · Livingstone, Zambia), hosted by the
Radiation Protection Authority of Zambia (RPA).

It works the same way as the medical edition (`../index.html`), with the
Non-Medical seal, the confirmed line-up and Programme v12 already loaded, plus
the upgrades below. It keeps its **own saved data**, so both editions can sit
on the same laptop without overwriting each other.

## Quick start

1. Open `index.html` in Chrome/Edge → **Control Panel**.
2. **🖥 Open Display Window** → drag it to the projector (or it jumps there
   automatically), then **⛶ Go fullscreen** / press **F**.
3. Pick a scene and press **▶ Display …**.

`index.html` is fully self-contained: logos, speaker photos and brand fonts
are embedded, so it looks identical **offline** and can be copied or emailed
on its own.

## Scenes

| Scene | What it shows |
|---|---|
| **① Title / Welcome** | Non-Medical seal with radiating rings, event name, edition, theme, dates, venue, RPA host line, optional sponsor row |
| **② Panel Grid** | Everyone, a group (e.g. *Panellist*) or a **session** (e.g. *Session 2*, which also shows each slot time). Suggested headings in the heading box |
| **③ Spotlight** | One person: photo with rings and sweep dial, groups (e.g. *Speaker · Panellist*), topic, bio, session watermark, queue counter (05 / 09) |
| **④ Countdown** | Countdown to any programme item (pick from the list or **Next on programme**), stats, and a **“Then”** strip of the following items |
| **⑤ Agenda** *(new)* | The day's programme. On the day, the current item is highlighted **NOW**, the next is tagged **NEXT** and finished items fade, all automatically |

- **Info bar** *(new)*: a live strip along the bottom of Grid, Spotlight and
  Agenda showing the event, the next programme item, the day and the time.
  Turn it on or off and change its label in Settings.
- **⟳ Holding loop** *(new)*: cycles Title → Grid → Agenda → Countdown every
  20 s (set in Settings) during breaks. Any manual push stops it.
- **○ Blackout**: fades to black.

## Data

- **People**: pre-loaded from the developer pack. A person has one category
  plus optional **“Also show in”** groups, so speakers who are also panellists
  appear in both.
- **Programme**: Settings → Programme, one line per item:
  `2026-11-04 09:00 | Session 2: Know What You Hold`. Lines starting
  `End of` mark when a day finishes (shown on the Agenda, never counted down to).
- **Sponsor logos**: Settings → Logos → *Sponsor / partner logos* → **Add**.
- **Export / Import** JSON for backups (includes photos, logos and the programme).

## Still to confirm (from the developer pack)

- Venue (*David Livingstone Safari Lodge* is in the ED's speech, but Programme
  v12 says "to be confirmed"), so the venue line shows *Livingstone, Zambia* for now.
- Hashtags (using the medical set), MC name, session moderators, sponsor logos.
- **Bios** for every speaker (none collected yet). Add them via ✎ Edit.
- Ms Beatrice Mvula is **TBC** and has no organisation yet. Delete her row
  if she does not present.
- RPA staff presenters are not yet named.
- A larger RPA logo master, if one exists.

## Updating photos, logos or fonts

Replace the files in `photos/` (square JPEGs, named `First_Last.jpg`),
`logos/` or `fonts/`, then run:

```
python3 non-medical/tools/embed_seed.py
```

This re-embeds them into `index.html` (needs Pillow). Photos already saved in
the browser stay as they are. Use ✎ Edit → *Change photo* to swap one live.

Fonts (Cinzel, Inter, Playfair Display, Roboto Mono) are under the SIL Open Font License.

Testing helper: `index.html#display?scene=title|grid|spotlight|countdown|agenda`
(add `&date=2026-11-04` for a specific Agenda day).
