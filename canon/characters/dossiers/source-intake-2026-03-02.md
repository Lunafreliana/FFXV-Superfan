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


## Re-check requested by user (third pass, exact filename)
- User supplied exact expected filename: `ffxv_part1_clean.txt`.
- Executed exact-name and fuzzy-name scans in both repo root and `/workspace`.
- Enumerated root filenames with Python `repr(...)` to catch hidden characters/whitespace variants.
- Result: no file named `ffxv_part1_clean.txt` (or close variant) was present in this runtime.

### Verification commands (for reproducibility)
- `find . -maxdepth 2 -type f -print`
- `rg --files | rg "ffxv_part1_clean|part1|part 1 clean|clean"`
- `python - <<'PY' ... print(repr(name)) ... PY`
- `find /workspace -maxdepth 4 -type f -iname '*ffxv*' -o -type f -iname '*part1*clean*'`

### Ready-to-ingest checklist once file appears
When `ffxv_part1_clean.txt` is visible in this branch/runtime, next pass should do all of the following in one commit:
1. Extract chapter-by-chapter facts into structured notes under `canon/plot-points/`.
2. Add dedicated files for **locations**, **items/artifacts**, and **side characters** if any new entities appear.
3. Patch all six main-character dossiers with newly sourced hobbies/preferences/relationship intensity details.
4. Expand `superfan-qa-audit.md` with a new “from part1_clean ingestion” section and confidence ratings.
5. Append a source provenance block with line-anchored quotes from the text file.
