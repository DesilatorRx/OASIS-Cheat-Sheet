# OASIS-E M & GG Cheat Sheet

A single-file HTML scoring aid for home health nurses completing the OASIS-E (Outcome and Assessment Information Set, home-health edition) assessment.

Built as a paper-replacement working sheet with click-to-select pills, real-time conflict detection, and browser-local persistence — no server, no install, no build step.

## What's in it

**GG section — Functional Abilities & Goals**
- **GG0100** Prior Functioning: Self-Care, Indoor Mobility, Stairs, Functional Cognition
- **GG0130** Current Self-Care (7-item table): Eating, Oral Hygiene, Toileting Hygiene, Shower, Upper/Lower Body Dressing, Footwear
- **GG0170** Current Mobility (17-item table): rolling, sit/stand transfers, walking distances, stair climbing, picking up objects, wheeling

**M section — Clinical Record Items M1033 through M2030**
- Risk for hospitalization (M1033)
- Pain & dyspnea (M1242, M1400)
- Skin/wound risk (M1300, M1302)
- Continence (M1610, M1615, M1620, M1630)
- Cognition & behavior (M1700, M1710, M1720, M1730, M1740, M1745)
- ADL / functional status (M1800–M1860)
- Medications (M2003, M2005, M2010, M2015, M2020, M2030)

## Conflict detection engine

A real-time engine flags inconsistent or implausible scoring as you click. Roughly 70 rules across three severity tiers:

- 🔴 **Errors** — direct contradictions (e.g. *M1850=4 Bedbound* with *M1860≤1 Independent ambulation*)
- 🟡 **Warnings** — clinically unusual combinations that warrant verification
- 🔵 **Soft checks** — gray-area suggestions to review at your discretion

Findings appear in a sticky panel at the top of the page. Affected item cards get a colored ring; the panel expands to list each conflict with rule name and rationale. When an item is hit by multiple rules, the highest severity wins the visual.

Coverage areas include:
- Bedbound / immobility consistency across M1850 / M1860 / M1840 / M1830
- Cognition and behavior (M1700 vs M1710 / M1740 / M1745)
- M ↔ GG cross-section consistency (M1810 vs GG0130F, M1850 vs GG0170E, etc.)
- GG sequencing (toileting hygiene ⇄ bathing, upper/lower dressing, walking distance progression, stair-step progression)
- Continence + catheter / ostomy logic
- Medication management vs cognition
- Pressure injury risk vs immobility
- Prior (GG0100) vs current functional status — flags clinically unusual improvement
- Multi-check exclusivity ("None of the above" with other options)

## Persistence

Scores, patient demographics, and multi-check selections persist via `localStorage` automatically — refresh-safe within the same browser/origin. Three keys: `oasis_state`, `oasis_fields`, `oasis_checks`.

## Print / Standalone export

- **Print / Save PDF** — uses the browser's print dialog. Auto-routes through *Open in New Tab* when the page is embedded in an iframe (otherwise printing prints the parent page).
- **Open in New Tab** — pops out a standalone snapshot of the filled cheat sheet with current state seeded inline. The new tab is self-contained — `Ctrl+S` to save a single HTML file with all current data baked in.
- **Clear All** — wipes scores, patient demographics, and checkboxes (with confirmation).

## Running it

Open `OASIS-E_Cheat_Sheet.html` in any modern browser. That's it — no server, no dependencies beyond Google Fonts (loaded over the network for typography).

## Project structure

```
OASIS-E_Cheat_Sheet.html   — the entire app (HTML, CSS, JS inline)
.gitignore
README.md
```

Single-file architecture is intentional. The cheat sheet can be emailed, saved to a thumb drive, or dropped on a tablet without any tooling.

## Disclaimer

This tool is a working aid, not a clinical record. Do not enter PHI/PII unless your environment permits browser `localStorage` for the data sensitivity involved. The conflict engine flags common scoring inconsistencies but does not replace clinical judgment, agency QA review, or official OASIS-E guidance from CMS.
