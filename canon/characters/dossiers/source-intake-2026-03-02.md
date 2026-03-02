# Source Intake Log — 2026-03-02

## User-provided sources processed

### Accessible
1. Google Doc export:
   - `https://docs.google.com/document/d/1RU-oxisOexwzyHS8jOVSS6Rj2IWO2z1iIvH2gUMVaHY/export?format=txt`
   - Contained: Eos historical chronology, Cosmogony excerpts, chapter quote excerpts including Ardyn identity lines and "Accursed" framing.

2. Supplemental accessible references used for cross-check:
   - Wikipedia raw: `Noctis_Lucis_Caelum`
   - Wikipedia raw: `Ardyn_Izunia`
   - Wikipedia raw: `Characters_of_Final_Fantasy_XV`
   - Wikipedia page HTML: `Final_Fantasy_XV`

### Blocked during this run
1. All listed TheLifestream URLs (Cloudflare challenge page).
2. Fandom wiki pages (403/Cloudflare).
3. FinalFantasyWiki direct pages (Cloudflare challenge).

## Practical impact on dossiers
- We upgraded codename/title handling for Ardyn using accessible text: **Ardyn Lucis Caelum**, **Ardyn Izunia**, **the Accursed**.
- We retained open-research tags for unresolved micro-facts (e.g., Gladio books/flirt specifics) rather than asserting uncertain details.


## Root-file check
- I checked repository root for a file explicitly named `ffxv part 1 clean` and did not find a file with that exact name in this environment.
- In this pass, I used the already-ingested chronology/cosmogony data that had been exported and logged previously, then propagated that data into canon location/item/supporting-character files.


## Re-check requested by user (second pass)
- Re-ran filename discovery across repo and `/workspace` using broad glob patterns for `ffxv`, `part`, `1`, and `clean`.
- Result: no file with matching name pattern was present at scan time.
- Note: current root-level files are: `final fantasy xv research`, `ffxv ao3 research`, `name`, `novel`, `vhujik`, and `README.md`.
