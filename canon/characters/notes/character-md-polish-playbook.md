# Character Dossier Full-Migration Playbook (LLM + Human)

Use this playbook to convert a badly formatted, legacy character `.md` into the new canonical schema.

## Objective
Transform legacy dossiers (including malformed `E###`/`Q###` sections, duplicate entries, and filler analysis) into a **source-grounded, scene-catalog-first, inference-auditable** format.

---

## What "Full Migration" Means
A full migration is **not** just editing the latest section. It includes all of the following end-to-end changes:
1. Remove obsolete `E###` analytical-note entries.
2. Replace/retire obsolete standalone `Q###` quote snippets.
3. Fold useful quote evidence into line-numbered scene blocks.
4. Remove duplicate or near-duplicate entries.
5. Remove non-character-relevant entries.
6. Enforce the six-question per-scene schema.
7. Sync top-level character categories with scene-derived evidence.

---

## Inputs Required
- Target character markdown file.
- Corpus dumps (e.g., `ffxv_part1_clean.txt` … `ffxv_part4_clean.txt`, `ffxv_misc_clean.txt`, `ffxv_ultimania_clean.txt`).
- Repository style/format instructions.

---

## Target Schema (Required End State)
1. **Top dossier synthesis** (appearance, biography, personality, voice, relationships, skills, likes/dislikes).
2. **Single comprehensive scene catalog** grouped by source file and scene blocks, covering **every scene where the character is named, directly appears, or is explicitly referenced** within corpus scope.
3. **Each scene block contains full quoted corpus lines with `L####` references**, not selective fragments that omit context.
4. **Each scene block has six structured interpretation prompts** with scene-specific answers.
5. **If no meaningful new evidence for a prompt in that scene, use `-`.**
6. No orphaned `E###`/`Q###` sections and no stale references to removed IDs.

7. **Appearance prompt is strictly physical**: include only visible physical descriptors (e.g., body features, age/age cues, hair, eyes, build, clothing if explicitly appearance-relevant). Do **not** use appearance to discuss demeanor, behavior, social staging, or personality.

---

## Non-Negotiable Rules
1. No canned filler (e.g., “contributes to dossier”).
2. Every claim is either direct corpus evidence or explicitly bounded inference.
3. Prefer contiguous scene context over isolated one-line quote fragments.
4. Voice analysis is linguistic style (diction/register/grammar/rhetoric), not vocal timbre.
5. Keep entries unique; remove repetition unless each repetition adds new evidence.
6. Do not preserve legacy IDs (`E###`, `Q###`) as primary schema once migrated.

---

## Full Migration Workflow

### Phase 0) Legacy inventory pass
Before rewriting, inventory the file:
- Count `E###` entries.
- Count `Q###` entries.
- Identify duplicated blocks.
- Identify placeholder/filler phrases.

### Phase 1) Remove obsolete legacy structures
- Delete all `E###` entries and their references.
- Remove standalone `Q###` sections **after** extracting any useful evidence.
- Replace old references (`See Q###`) with scene-block/L-number references or remove if stale.

### Phase 2) Build evidence catalog from corpus (exhaustive)
For each source file:
1. Find **all** character mentions/appearances (name variants, titles, aliases).
2. Build a complete mention index first; do not skip low-drama references.
3. Merge adjacent lines into coherent scene windows.
4. Quote full relevant lines under scene blocks with `L####` numbering.
5. Group blocks under source headings.
6. Add per-source coverage counts (e.g., `N scene blocks; M matching lines`) to make completeness auditable.

Format:

```md
### <source_file>
#### Scene block N (Lstart-Lend)
> L####: ...
> L####: ...
```

### Phase 3) Deduplicate and relevance prune
- Remove exact duplicates and near-duplicates.
- Do **not** remove scenes just because they look minor if they contain an explicit mention; exhaustive coverage has priority.
- Mark low-signal scenes with `-` in non-evidentiary prompts rather than deleting mention evidence.
- If a scene is context-critical but low-signal, keep it but mark non-evidentiary prompt answers as `-`.

### Phase 4) Add six-question scene interpretation
Under **every** scene block, answer:
- What can I glean about his physical appearance?
- What can I glean about his personality?
- What can I glean about his relationships?
- What can I glean about his skills?
- What can I glean about his likes/dislikes/hobbies?
- What can I glean about the way he speaks aka his "voice"?

Rules:
- Tailor answer text to that specific scene.
- Avoid copy-paste phrasing across many blocks.
- Use `-` when no meaningful new evidence exists for that category.
- **Appearance answer constraint:** only physical look/age/visible-feature evidence; if absent, write `-`.

### Phase 5) Rebuild top-level synthesis from scene evidence
Update the opening dossier categories so they summarize repeated, cross-scene patterns:
- Appearance
- Biography/chronology
- Personality
- Relationships
- Skills
- Likes/dislikes/hobbies
- Voice (speech style)

No top-level bullet should assert information unsupported by the scene catalog or corpus references.

### Phase 6) Final integrity checks
Verify:
- No `E###` entries remain.
- No standalone `Q###` sections remain.
- No stale `Q###`/`E###` references remain.
- Every scene block has exactly 6 prompt answers.
- Duplicate answers are minimized.
- Voice lines discuss language style, not physical sound.
- Scene catalog includes every explicit in-scope mention (no silent omissions).
- Appearance lines do not contain personality/behavior language when no physical evidence exists.

---

## Suggested Command Checklist

```bash
# A) Legacy schema leftovers
rg -n '^### E[0-9]+|^### Q[0-9]+|\*\*E[0-9]+' <character_file>

# B) Filler/placeholder detection
rg -n 'Detailed synthesis note|Contribution to dossier|Cross-check adjacent|TODO' <character_file>

# C) Stale legacy refs
rg -n 'See Q[0-9]+|Q[0-9]{3}|E[0-9]{3}' <character_file>

# D) Scene-block and six-prompt coverage validation
python - <<'PY'
import re
p='<character_file>'
lines=open(p).read().splitlines()
blocks=[i for i,l in enumerate(lines) if re.match(r'^#### Scene block',l)]
keys=[
'- **What can I glean about his physical appearance?**',
'- **What can I glean about his personality?**',
'- **What can I glean about his relationships?**',
'- **What can I glean about his skills?**',
'- **What can I glean about his likes/dislikes/hobbies?**',
'- **What can I glean about the way he speaks aka his "voice"?**',
]
print('scene_blocks',len(blocks))
for k in keys:
    print(k, sum(1 for l in lines if l.startswith(k)))
blocks.append(len(lines))
bad=[]
for idx,(a,b) in enumerate(zip(blocks,blocks[1:]),1):
    c=sum(1 for l in lines[a:b] if l.startswith('- **What can I glean about '))
    if c!=6:
        bad.append((idx,c))
print('blocks_not_6',bad)
PY

# E) Voice drift guardrail
rg -n 'vocal timbre|physical voice|voice sounds' <character_file>
# F) Exhaustive mention sanity check against corpus (example pattern; adapt aliases/titles)
rg -n '(Ardyn|Izunia|Chancellor)' ffxv_*_clean.txt

# G) Appearance leakage heuristic (flag likely non-physical wording in appearance answers)
rg -n '^- \*\*What can I glean about his physical appearance\?\*\* .*\b(personality|manipulat|control|relationship|skill|voice|speaks|tone|behavior)\b' <character_file>
```

---

## Definition of Done
A migration is complete only when all are true:
- Legacy `E###`/`Q###` schema is fully retired.
- Duplicates and low-value clutter are removed.
- Scene catalog is comprehensive for corpus scope and includes every explicit mention scene.
- Every scene has six prompt answers; weak/no-evidence categories use `-`.
- Appearance answers contain only physical-feature evidence (or `-`).
- Top-of-file synthesis is aligned with scene evidence.
- File is readable, auditable, and free from filler language.

---

## Reusable Prompt Template (Strict Full-Migration Mode)

```text
You are rewriting <character_file> from legacy format to the new schema.

Execute a FULL migration, not a partial edit.

Required outcomes:
1) Remove all E### entries and references.
2) Remove standalone Q### sections and references.
3) Build a unified scene catalog with source-grouped scene blocks and full L-numbered lines, covering every explicit mention of the character (including alias/title mentions).
4) Deduplicate and prune non-character-relevant entries.
5) Under every scene block, answer six prompts:
   - physical appearance
   - personality
   - relationships
   - skills
   - likes/dislikes/hobbies
   - voice (speech style only: diction/grammar/register/repeated phrasing/rhetoric)
6) If no meaningful evidence for a prompt in that scene, output `-`.
7) Ensure per-scene answers are scene-specific (no repetitive boilerplate).
8) Appearance answers must be strictly physical descriptors (features/age/look); if none, output `-`.
9) Update top-level character categories to reflect repeated scene evidence.
10) Validate final structure: no E/Q leftovers, no stale refs, every scene has exactly six prompt answers, exhaustive mention coverage, and no appearance leakage into personality/behavior.

Output only the final updated markdown.
```
