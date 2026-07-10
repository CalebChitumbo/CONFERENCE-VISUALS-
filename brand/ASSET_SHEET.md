# 8th RPO Conference — Display App Asset Pack

Everything here is sampled from `/rpo-conference-brand` and `/rpa-brand`. Feed the
logos, `brand.css` and `brand_tokens.json` into the build.

---

## 1. Logos (in `/logos`)

| File | Size | Where to use |
|---|---|---|
| `conf_logo_transparent.png` | 1024² | **Default for the display** — sits on the dark (Charcoal/Gunmetal) projector scenes |
| `conf_logo_transparent_small.png` | 512² | Corner watermark / control-panel header on dark |
| `conf_logo_primary.png` | 1024² | Only on white / near-white surfaces (e.g. a light control panel) |
| `conf_logo_small.png` | 512² | Inline, light backgrounds, where file size matters |
| `rpa_logo.png` | 412² | RPA institutional mark — pair with the conference logo on the Title/Welcome scene |
| `rpa_logo_2x.png` | 824² | Hi-res RPA mark for large screens |
| `rpa_logo_on_dark.png` | 412² | Reference only — shows how the RPA logo reads on dark (place `rpa_logo.png`, its bg is transparent) |

**Rules:** never recolour, rotate, skew, or add shadows/glows to either logo.
Minimum on screen: conference logo **200px** wide, RPA logo **64px** wide.
Keep clearspace around each equal to the height of the "8th" (conference) / one electron dot (RPA).
Use the **transparent** conference logo on every coloured/dark surface — never the white-BG version on dark.

## 2. Palette

**Conference (primary):**
- Falls Gold `#C9A227` — the one accent. Headline highlights, rules, photo rings. *One gold moment per scene.*
- Falls Gold Highlight `#F0DC8C` — gradient/shine support only.
- Gunmetal `#2B2D2F` — dark surfaces & text.
- Charcoal `#1A1B1D` — deepest dark; the default display background.
- Mist White `#F7F4EC` — warm off-white canvas (**not** pure white).
- Pure White `#FFFFFF` — reverse type on dark only.
- Falls Mist `#A8B5BD` — cool grey-blue secondary (captions, taglines).

**RPA atom accents — only when the RPA logo/branding is co-shown:**
- RPA Green `#3A8B3A`, RPA Yellow `#E5C100`
- (RPA institutional-brand versions, if the RPA logo appears standalone: Green `#00A050`, Yellow `#F0F000`.)

**Contrast rules:** Charcoal/Gunmetal text on Mist White for light surfaces; Mist White text on
dark for the display. **Never** set body text in Falls Gold on a light background — gold is for
display sizes (24px+) and thick strokes only. Never use RPA Yellow for paragraph text.

## 3. Typography

| Role | Web font | Fallback | Use for |
|---|---|---|---|
| Display / headers | **Cinzel** | Cambria, Georgia | Speaker names, scene titles. All-caps for ≤4 words, +5% tracking |
| Subhead / tagline | **Playfair Display** *(italic)* | Cambria | Theme line, pull-quotes |
| Body / UI | **Inter** | Calibri, Arial | Bios, affiliations, control-panel UI. Min 16px on screen |
| Mono / labels | **Roboto Mono** | Consolas | Countdown timer, dates, "DAY 2 OF 4", badge-style labels. UPPERCASE +10–15% tracking |

Never set body in Cinzel or in italic. Max three families per surface.
The Google Fonts import line is already in `brand.css`.

## 4. Fixed conference facts (for Title / holding scenes)

- **Full name:** 8th Annual Radiation Safety Conference (shorthand: 8th RPO Conference)
- **Theme:** *Sustaining Excellence in Radiation Safety: From Compliance to Culture*
- **Sector focus:** Medical Facilities
- **Dates:** 14–17 July 2026  ·  mono form: `14–17 JULY 2026`
- **Venue:** Livingstone, Zambia (David Livingstone Safari Lodge)
- **Host:** Radiation Protection Authority of Zambia (RPA)
- **Contact (confirm before locking):** www.rpa.org.zm · conference@rpa.gov.zm · +260 211 254 254
- **Hashtags:** #RPOConference2026 #8thRPOConference #RadiationSafety
  #MedicalRadiationSafety #RadiationProtectionAuthority #RPA #Livingstone #ZambiaHealthcare

## 5. Look & feel

- Default the **display view to dark** (Charcoal background, Mist White text, Falls Gold accent).
- Circular speaker photos with a thin Falls Gold ring — matches the IAEA panel reference.
- Gold used sparingly: one gold moment per scene (a rule, a name highlight, the countdown digits).
- Subtle Victoria Falls / mist motif is on-brand; avoid AI-cliché gradients, glows, glassmorphism.

---

*Files: `brand.css` (drop-in CSS variables + font import), `brand_tokens.json` (machine-readable
tokens for any build script), `/logos` (all marks).*
