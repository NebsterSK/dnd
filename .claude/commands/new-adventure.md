---
description: Generate a full hidden D&D 5e campaign into private/ from a guided Q&A
argument-hint: "[optional one-line premise seed]"
---

# /new-adventure — Campaign Generator

Generate a complete, hidden D&D 5e campaign and write it to `private/`. This builds the **world, story, villain, factions, quests, and NPCs** — it does NOT create player characters (that is `/new-character`).

If `$ARGUMENTS` is non-empty, treat it as an initial premise seed and fold it into the answers.

## Step 0 — Warn & confirm (destructive)

Generating a new campaign **wipes the existing campaign and world state** — but never the player characters in `public/characters/`. Before anything else, check whether any campaign files exist: anything under `private/` or `public/` other than `public/characters/` (and beyond empty subdirectories).

- If existing state is found, warn the user **out-of-game** that proceeding will permanently erase the current campaign, world, NPCs, areas, and quests (player characters are kept), then use **AskUserQuestion** to confirm: "Wipe current campaign and start new" vs **"Cancel"** (make Cancel the safe default framing).
- If the user cancels, stop immediately and change nothing.
- Only after explicit confirmation, delete all files under `private/` and all files under `public/` **except** everything in `public/characters/`, keeping the directory structure. Then continue. (Same deletion as `/clear-adventure`.)
- If no existing state is found, skip the prompt and continue.

## Step 1 — Interview the user (out-of-game)

Ask the questions below using the **AskUserQuestion** tool, batched at most 4 per call. Provide the listed options; AskUserQuestion always adds an "Other" free-text choice, so the user can type a custom answer to any question.

For every question marked **[optional]**, include **"Let the DM decide"** as the first option — selecting it means you invent a fitting value during generation. (Exceptions: the multiSelect questions in **Batch 5 — Themes & motifs** omit it, with "select none" in a question meaning the DM decides that axis; and Party size omits it — pick Solo or type a number via Other.)

**Batch 1 — Setting**
1. **[core] Genre** — Fantasy / Dark fantasy / Sci-fi / Post-apocalyptic *(Other auto-added)*
2. **[core] Theme** — Classic heroic adventure / Intrigue & mystery / Gothic horror / Pirate & seafaring  *(Other: heist, detective, non-combat, etc.)*
3. **[core] Setting** — Sword Coast / Other Forgotten Realms region / Another published world (Eberron, Ravenloft, etc.) / Fully custom world
4. **[optional] Magic & tech level** — Standard / High magic / Low magic *(for sci-fi/other, capture tech tier via Other)*

**Batch 2 — World & powers**
5. **[optional] Geographic scope** — Single locale (one town & nearby sites) / Regional (a cluster of settlements and wilds) / Continental (far-ranging travel across the realm)
6. **[optional] Religion, cults & deities** — Central (gods, clergy, and cults actively drive events and the plot) / Present (temples and worship are a normal part of life, the occasional cult) / Background (gods exist but rarely come up). Calibrate clergy NPCs, temples, divine intervention, and cult threats accordingly.
7. **[optional] Faction politics** — Prominent & central / Present but light / Minimal
8. **[optional] Structure** — Directed (a clear main plot to follow) / Mixed (main plot with room to wander) / Open sandbox (player-driven; the world reacts)

**Batch 3 — Tone & stakes**
9. **[core] Tone** — Heroic & hopeful / Gritty & dark / Comedic & light / Morally gray
10. **[core] Lethality** — Forgiving (death rare) / Standard / Deadly (enemies play to kill, harsh consequences) / Brutal (meatgrinder — TPK is on the table)
11. **[optional] Character death** — Permadeath (death can end the campaign) / Second chances (rescue, resurrection, or a new character keeps the story going) / Narrative saves (death only when story-fitting)
12. **[optional] Lines & veils** — None / Fade-to-black on sensitive themes / Specific limits *(via Other)*

**Batch 4 — Story & secrets**
13. **[core] Spoiler appetite** — Surprise me completely / I'll give a seed, you build the rest / Co-author the premise with me / Tell me everything up-front
14. **[core] Central conflict** — Surprise me *(or Other: type a villain/hook/conflict seed)*
15. **[optional] Twist intensity** — Few (a clear, straightforward story) / Moderate / Many (frequent betrayals and rug-pulls)

**Batch 5 — Themes & motifs** *(all four are multiSelect; no "Let the DM decide" option — selecting none in a question means the DM decides that axis. **Soft cap ~6:** across all four questions, lean on the player's emphasized themes and let about 6 meaningfully shape the story — treat any extras as light seasoning so generation stays coherent.)*
16. **[optional] Conflict & reckoning** *(multiSelect)* — Betrayal / Revenge / Justice & law / War and its cost
17. **[optional] Fall & redemption** *(multiSelect)* — Redemption / Corruption & temptation / Sacrifice / Power & ambition
18. **[optional] Discovery & the unknown** *(multiSelect)* — Exploration & lost places / Hidden history & secrets / Forbidden knowledge / Survival against the wild
19. **[optional] Heart & identity** *(multiSelect)* — Love & loss / Found family & loyalty / Identity & belonging / Freedom vs. tyranny

**Batch 6 — Progression & tempo**
20. **[core] Campaign length** — One-shot / Short arc (3–6 sessions) / Medium (7–15 sessions) / Long campaign (level 1 → high)
21. **[core] Leveling** — XP per encounter (combat, social, exploration) / Milestone (level on major story beats) / Hybrid (milestone for story, XP for combat) / Session-based (level every N sessions)
22. **[core] Starting level** — Level 1 / Level 3 / Level 5 / Higher *(via Other)*
23. **[optional] Pacing & urgency** — Urgent (a ticking clock drives events) / Moderate / Relaxed (explore at your own pace)

**Batch 7 — Challenge & encounters**
24. **[optional] Difficulty** — Easy / Standard / Hard  *(encounter balance — distinct from lethality, which is consequence severity)*
25. **[optional] Encounter mix** — Combat-heavy (fights dominate) / Balanced (even split of combat, social, exploration) / Social & exploration-heavy (intrigue, discovery, and roleplay over fighting). Shape the quest chain and the three-act arc to match.
26. **[optional] Survival & realism** — Gritty (track rations, encumbrance, ammo, exhaustion) / Standard (light logistics) / Cinematic (hand-wave logistics, focus on story)
27. **[optional] Party size** — Solo / Enter a number *(no "Let the DM decide" option here; pick Solo or choose Other and type the party size. Used only for encounter math; actual PCs come from /new-character)*

**Batch 8 — Rewards & play style**
28. **[optional] Magic-item abundance** — Sparse / Standard / Generous
29. **[optional] Romance & relationships** — Romance welcome (subplots can develop) / Player-initiated only (NPCs won't push) / Keep it platonic (no romance)
30. **[optional] Player guidance** — Hands-off (never suggest actions; the player drives entirely) / Light nudges (occasional hints when stuck) / Offer choices (present possible actions). Default if undecided: hands-off.
31. **[optional] NPC name style** — Regular roleplay fantasy names (full, immersive) / Simple fantasy names (first name only, easy to remember) / Simple real-world names (easiest to remember). Apply the chosen style to every NPC you generate and name in play.

Respect spoiler appetite when interviewing: if the user chose "Surprise me completely," do NOT ask follow-up plot questions — invent silently in Step 2.

## Step 2 — Generate the campaign in one pass

Using all answers (filling every "Let the DM decide" / unanswered optional with a fitting invention), generate the entire campaign at once. Be coherent: villain motive, factions, quest chain, and twists must interlock. Honor the CLAUDE.md rules (strict 5e, coherent villains, world that moves on its own).

## Step 3 — Write files to private/ (DM eyes only)

Do not add "DM EYES ONLY" banners or similar headers to private files — CLAUDE.md already establishes that everything under `private/` is DM/AI-only. A short file-specific note is fine; the redundant banner is not.

Create:
- `private/campaign.md` — master doc: title, **all 31 settings** (genre, theme, setting, magic/tech, geographic scope, religion, structure, pacing, tone, **lethality**, character death, lines & veils, faction politics, length, leveling, starting level, difficulty, encounter mix, survival & realism, magic-item abundance, party size, twist intensity, romance, **player guidance**, NPC name style, plus spoiler appetite/central conflict and the selected **themes & motifs**), premise, three-act arc, win/lose conditions, secret core theme
- `private/villain.md` — BBEG: true identity, motive, master plan, timeline, resources, weaknesses, how they react to interference
- `private/timeline.md` — planned story beats, plot twists, planned betrayals, and a "world clock" of events that happen whether or not the player is present
- `private/factions.md` — each faction's public face, hidden agenda, and ties to the villain
- `private/npcs/<name>.md` — the hidden truth for each seeded key NPC (real identity, agenda, secrets)
- `private/areas/<name>.md` — seeded key locations not yet discovered
- `private/quests/<name>.md` — the main quest chain plus a few side quests, each with hidden objectives and rewards

## Step 4 — Public side & report

- Do **not** reveal anything to the player. Do **not** write a campaign hook — characters don't exist yet, so the hook is deferred to session start / `/new-character`.
- Optionally write `public/world.md` with ONLY common-knowledge setting facts any inhabitant would know (geography, well-known cities, current year) — zero plot, zero secrets. Skip if the setting is fully custom and nothing is "common knowledge" yet.
- Public files are read by the player: write them as in-world content only. No DM/meta notes, no "player-facing" headers, no "DM eyes only" banners, no parenthetical instructions. (Those belong only in `private/` files.)
- Finish with a brief **out-of-game** confirmation: campaign title, the chosen settings (no plot spoilers), and the list of files written. Tell the user to run `/new-character` next.
