# LLM Handoff Handbook — FFXV Superfan Canon Project

## 1) Mission You Are Inheriting
Your job is to maintain and expand this repository into a **high-confidence Final Fantasy XV superfan knowledge base** that can answer deep lore questions without bluffing.

Primary expectations:
- Provide richly detailed, character-accurate, continuity-aware answers.
- Distinguish canon tiers (base game, DLC, Royal, cross-media, novel route).
- Preserve provenance and confidence labels.
- Prefer explicit “unknown / open research” over fabricated claims.


## 2) User Criticisms of Prior Agent Work (Important)
The previous agent was criticized for:
- Being **too superficial** in early character dossiers.
- Missing specific high-value details (example from user: Ardyn + Somnus/Aera/fall progression/Ifrit daemonization framing).
- Failing to ingest a user-claimed local source file quickly enough (`ffxv_part1_clean.txt`) and repeatedly responding with “not found.”

Takeaway:
- Assume user requests are specific and detail-sensitive.
- When something is “missing,” add denser micro-facts, arc mechanics, and niche-QA handling.
- If a source is not found, record exact checks once, then pivot to a concrete ingestion plan.


## 3) What Has Already Been Built
The repository now includes:
- A canon structure under `canon/` with timeline, lore, characters, locations, factions, terms, and plot points.
- Main-character dossiers:
  - `canon/characters/dossiers/noctis-lucis-caelum.md`
  - `canon/characters/dossiers/ignis-scientia.md`
  - `canon/characters/dossiers/gladiolus-amicitia.md`
  - `canon/characters/dossiers/prompto-argentum.md`
  - `canon/characters/dossiers/lunafreya-nox-fleuret.md`
  - `canon/characters/dossiers/ardyn-izunia.md`
- QA/support docs:
  - `canon/characters/dossiers/superfan-qa-audit.md`
  - `canon/characters/dossiers/source-intake-2026-03-02.md`
  - `canon/characters/dossiers/part1-clean-ingestion-template.md`
- Supporting files enriched previously:
  - `canon/locations/key-sites.md`
  - `canon/lore/items-and-regalia.md`
  - `canon/characters/supporting-cast.md`
  - `canon/terms/glossary.md`
  - `canon/plot-points/eos-historical-chronology.md`


## 4) Current Known Friction Point
The user insists `ffxv_part1_clean.txt` exists (or should exist) and wants its contents ingested deeply.

Known runtime history:
- Multiple prior scans did not find the file in this environment at those moments.
- A dedicated intake log now records those checks and a ready-to-run ingestion workflow.

Your operating stance:
1. Check for `ffxv_part1_clean.txt` first.
2. If found, ingest immediately and update dossiers/canon in one coherent pass.
3. If not found, document exact command + timestamp once, then continue with best available sources.


## 5) Non-Negotiable Working Standards
When writing or editing lore docs:
- **No hallucinations**: mark uncertain facts as open research.
- Keep a high signal-to-noise ratio: dense, practical, answer-ready content.
- Include “superfan-style” micro-facts:
  - hobbies/routines
  - likes/dislikes with intensity framing
  - trauma triggers
  - arc turning points
  - ending-state trajectory
- Add contradiction handling where canon branches diverge.

When answering user questions from docs:
- Provide a docs-only answer first when requested.
- Then provide internet-checked answer (if requested and accessible).
- Explain what was newly learned and patch docs so the same gap does not recur.


## 6) Suggested Handoff Workflow (Execute in Order)
1. **Source discovery pass**
   - Confirm presence/absence of `ffxv_part1_clean.txt` and other root text sources.
2. **Ingestion pass**
   - Use `canon/characters/dossiers/part1-clean-ingestion-template.md`.
3. **Canon patch pass**
   - Update dossiers + locations/items/side-cast/chronology + glossary as needed.
4. **Superfan stress-test pass**
   - Add high-difficulty Q/A to `superfan-qa-audit.md`.
5. **Provenance pass**
   - Append source intake notes and confidence levels.
6. **Navigation pass**
   - Ensure `canon/index.md` and dossier README link new files.


## 7) Definition of “Good Enough” for This Repo
A change is high quality only if:
- It materially improves answerability for niche fan questions.
- It is transparent about certainty and source boundaries.
- It reduces future ambiguity (better structure, indexing, and intake logs).
- It does not force future agents to rediscover project context from scratch.


## 8) Practical Next Task for You (If File Exists)
If `ffxv_part1_clean.txt` is present now, prioritize:
- extracting chapter-level facts,
- enriching all six main dossiers with new micro-facts,
- adding side-character/location/item entries discovered in the text,
- expanding the superfan QA bank with difficult questions,
- updating source intake with concrete provenance notes.

If done correctly, the user should feel the docs can power believable “superfan-level” responses without improvisation.
