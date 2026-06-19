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

Ask each question using one of two methods:
- **AskUserQuestion** for questions whose choices fit in four options (the auto "Other" covers custom answers). Batch at most 4 per call.
- **Plain-text list** for questions with more than four options — here, **Theme (Q2)** and **Themes & motifs (Q16)**. Don't use AskUserQuestion for these; present the options as a clear, numbered out-of-game list and let the player reply in plain text.

For every AskUserQuestion question marked **[optional]**, include **"Let the DM decide"** as the first option — selecting it means you invent a fitting value during generation. (Exception: Party size omits it — pick Solo or type a number via Other.) The plain-text questions handle "DM decides" in their own wording: naming nothing lets the DM choose.

**Batch 1 — Setting**
1. **[core] Genre** — Fantasy / Dark fantasy / Sci-fi / Post-apocalyptic *(Other auto-added)*
2. **[core] Theme** *(plain-text list)* — present these archetypes and let the player pick one (or name their own): Classic heroic adventure · Intrigue & mystery · Gothic horror · Pirate & seafaring · Heist & crime · Detective / noir · War & military · Exploration & wilderness survival · Political & courtly intrigue · Dungeon crawl · Planar & cosmic · Comedy & lighthearted romp.
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
12. **[optional] Anything off-limits?** — Ask plainly whether there's anything the player wants kept out of the game or handled off-screen. Options: Nothing — anything goes / Keep dark or graphic moments off-screen (fade to black) / There are specific things to avoid *(name them via Other)*

**Batch 4 — Story & secrets**
13. **[core] Spoiler appetite** — Surprise me completely / I'll give a seed, you build the rest / Co-author the premise with me / Tell me everything up-front
14. **[core] Want to shape what the story is about?** — Ask whether the player wants to suggest the main story, or leave it to the DM. Options: Surprise me — you come up with it / I have an idea *(choose Other and describe it — a bad guy, a mystery to solve, or a situation you'd like to start in)*.
15. **[optional] Twist intensity** — Few (a clear, straightforward story) / Moderate / Many (frequent betrayals and rug-pulls)
16. **[optional] Themes & motifs** *(plain-text list)* — present the 16 motifs below grouped under their headings; the player names any they want (or none, which lets the DM decide). **Soft cap ~6:** let about six emphasized motifs meaningfully shape the story; treat extras as light seasoning so generation stays coherent.
    - *Conflict & reckoning:* Betrayal · Revenge · Justice & law · War and its cost
    - *Fall & redemption:* Redemption · Corruption & temptation · Sacrifice · Power & ambition
    - *Discovery & the unknown:* Exploration & lost places · Hidden history & secrets · Forbidden knowledge · Survival against the wild
    - *Heart & identity:* Love & loss · Found family & loyalty · Identity & belonging · Freedom vs. tyranny

**Batch 5 — Progression & tempo**
17. **[core] Campaign length** — One-shot / Short arc (3–6 sessions) / Medium (7–15 sessions) / Long campaign (level 1 → high)
18. **[core] Leveling** — XP per encounter (combat, social, exploration) / Milestone (level on major story beats) / Hybrid (milestone for story, XP for combat) / Session-based (level every N sessions)
19. **[core] Starting level** — Level 1 / Level 3 / Level 5 / Higher *(via Other)*
20. **[optional] Pacing & urgency** — Urgent (a ticking clock drives events) / Moderate / Relaxed (explore at your own pace)

**Batch 6 — Challenge & encounters**
21. **[optional] Difficulty** — Easy / Standard / Hard  *(encounter balance — distinct from lethality, which is consequence severity)*
22. **[optional] Encounter mix** — Combat-heavy (fights dominate) / Balanced (even split of combat, social, exploration) / Social & exploration-heavy (intrigue, discovery, and roleplay over fighting). Shape the quest chain and the three-act arc to match.
23. **[optional] Survival & realism** — Gritty (track rations, encumbrance, ammo, exhaustion) / Standard (light logistics) / Cinematic (hand-wave logistics, focus on story)
24. **[optional] Party size** — Solo / Enter a number *(no "Let the DM decide" option here; pick Solo or choose Other and type the party size. Used only for encounter math; actual PCs come from /new-character)*

**Batch 7 — Rewards & play style**
25. **[optional] Magic-item abundance** — Sparse / Standard / Generous
26. **[optional] Romance & relationships** — Romance welcome (subplots can develop) / Player-initiated only (NPCs won't push) / Keep it platonic (no romance)
27. **[optional] Player guidance** — Hands-off (never suggest actions; the player drives entirely) / Light nudges (occasional hints when stuck) / Offer choices (present possible actions). Default if undecided: hands-off.
28. **[optional] NPC name style** — Regular roleplay fantasy names (full, immersive) / Simple fantasy names (first name only, easy to remember) / Simple real-world names (easiest to remember). Apply the chosen style to every NPC you generate and name in play.

Respect spoiler appetite when interviewing: if the user chose "Surprise me completely," do NOT ask follow-up plot questions — invent silently in Step 2.

## Step 2 — Generate the campaign in one pass

Using all answers (filling every "Let the DM decide" / unanswered optional with a fitting invention), generate the entire campaign at once. Be coherent: villain motive, factions, quest chain, and twists must interlock. Also assemble a **threat roster** (the bestiary) themed to the genre/setting and calibrated to the campaign's level range, difficulty, and party size, so encounters are buildable from the start. Likewise assemble an **items catalog** — the magic items the campaign offers (per the magic-item-abundance setting) and the plot items the story needs (maps, letters, artifacts), each with its place in the world and any hidden properties. Honor the CLAUDE.md rules (strict 5e, coherent villains, world that moves on its own).

## Step 3 — Write files to private/ (DM eyes only)

Do not add "DM EYES ONLY" banners or similar headers to private files — CLAUDE.md already establishes that everything under `private/` is DM/AI-only. A short file-specific note is fine; the redundant banner is not.

Create:
- `private/campaign.md` — master doc: title, **all 28 settings** (genre, theme, setting, magic/tech, geographic scope, religion, structure, pacing, tone, **lethality**, character death, lines & veils, faction politics, length, leveling, starting level, difficulty, encounter mix, survival & realism, magic-item abundance, party size, twist intensity, romance, **player guidance**, NPC name style, plus spoiler appetite/central conflict and the selected **themes & motifs**), premise, three-act arc, win/lose conditions, secret core theme
- `private/villain.md` — BBEG: true identity, motive, master plan, timeline, resources, weaknesses, how they react to interference; plus a **combat block** — a stat-block reference (MM/SRD) scaled to the party, or, since the villain is usually a unique foe, a hand-built block with the combat essentials (AC, HP, speed, attacks, saves, key abilities, CR)
- `private/timeline.md` — planned story beats, plot twists, planned betrayals, and a "world clock" of events that happen whether or not the player is present
- `private/factions.md` — each faction's public face, hidden agenda, and ties to the villain
- `private/npcs/<name>.md` — each seeded key NPC, using a tiered template:
  - **Always:** name · race · role/class · **alignment** · **appearance** · **personality** (manner, voice, a tell) · the hidden truth (real identity, agenda, secrets) · how they react to the player · the public-graduation note (what `public/npcs/` shows once the player meets them). Add **languages** only if it matters whether they can talk to the party, and **notable gear** only if it's story- or loot-relevant — skip PC-style proficiency lists.
  - **Combat-capable NPCs also get a combat block:** a stat-block reference (MM/SRD — e.g. "Assassin," "Veteran," "Mage"), its CR and how to scale it to the party, any signature ability, and notable equipment. Hand-build a full custom block (AC, HP, speed, attacks, saves, CR — combat essentials only) only for a unique central foe where no existing block fits. **Social-only NPCs need no combat stats.**
- `private/areas/<name>.md` — seeded key locations not yet discovered; list the creatures/encounters here by **reference to `bestiary.md`**, and any notable loot or plot items by **reference to `items.md`** (don't restate stat blocks or item details)
- `private/quests/<name>.md` — the main quest chain plus a few side quests, each with hidden objectives and rewards (reference notable rewards/items in `items.md`)
- `private/bestiary.md` — the campaign's **threat roster**, calibrated to its level range, difficulty, and party size. Tiered like NPCs:
  - **Standard creatures:** name + **stat-block reference** (SRD/MM) + CR + one-line role/where-used + a **reskin note** if the genre needs it (e.g. sci-fi: "Zombie reskinned as a reanimated crewman").
  - **Signature/custom creatures** (no good MM match): a full custom block — AC, HP, speed, attacks, saves, traits, CR.
  - This is the **single source of truth** for monster stats; areas and quests reference it rather than restating blocks. DM-only — creatures graduate to player knowledge only through play.
- `private/items.md` — the campaign's **notable items** (not mundane gear), in two kinds:
  - **Mechanical items** (weapons, armor, wondrous items): name · rarity · attunement · mechanics — a **reference** (DMG/SRD, e.g. "+1 cutlass") where one exists, a short custom block only for a bespoke item; plus which area/quest holds it. Calibrate quantity to the magic-item-abundance setting and level.
  - **Story/plot items** (letters, maps, artifacts): what it appears to be · its role in the plot · and its **hidden truth/secret**.
  - **Single source of truth** — areas and quests reference items by name. DM-only; an item's player-known form moves to a character's inventory only once it's found or identified, with its secrets staying here until discovered in-game.

## Step 4 — Public side & report

- Do **not** reveal `private/` contents to the player or copy them into `public/`.
- **Integrate existing characters:** check `public/characters/`. If one or more PCs already exist (i.e. `/new-adventure` is being run after `/new-character`), then after generating, **lightly weave them in** — write a tailored opening hook that pulls *those* characters in, and plant 1–3 of each PC's backstory ties into the world (player-known facts in `public/`, secret truths in `private/`), exactly as in `/new-character` Step 3. Keep it light; don't rework the campaign around them. If **no characters exist yet**, do **not** write a hook — defer it to `/new-character`.
- Optionally write `public/world.md` with ONLY common-knowledge setting facts any inhabitant would know (geography, well-known cities, current year) — zero plot, zero secrets. Skip if the setting is fully custom and nothing is "common knowledge" yet.
- Public files are read by the player: write them as in-world content only. No DM/meta notes, no "player-facing" headers, no "DM eyes only" banners, no parenthetical instructions. (Those belong only in `private/` files.)
- Finish with a brief **out-of-game** confirmation: campaign title, the chosen settings (no plot spoilers), and the list of files written. If no characters exist yet, tell the user to run `/new-character` next; if characters were integrated, note they've been woven in and play can begin.
