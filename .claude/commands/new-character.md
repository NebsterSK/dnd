---
description: Create a D&D 5e player character (full sheet) and lightly weave them into the campaign
argument-hint: "[optional concept, e.g. 'grizzled dwarf cleric']"
---

# /new-character — Character Creator

Build a complete D&D 5e player character through a guided interview, write the full sheet to `public/characters/`, and — if a campaign exists — lightly weave the character into the world.

If `$ARGUMENTS` is given, treat it as a concept seed (race/class/vibe) and pre-fill where it fits.

## Asking questions — two methods
- Use **AskUserQuestion** for any question whose choices fit in **four options** (the auto "Other" covers custom answers). Mark optional questions with a sensible default.
- For questions with **more than four options — Race, Class, Spells, and Equipment** (and any subclass or spell list that exceeds four) — do **not** use AskUserQuestion. Instead present the available options as a clear, numbered **out-of-game list** and let the player reply in plain text. List options appropriate to the campaign's genre/setting.

## Step 0 — Pre-flight
- **Read `private/campaign.md`** if it exists. Pull: **starting level** (build the sheet at that level), **genre & setting** (reskin race/class/gear flavor — e.g. sci-fi names, custom species), **party size**, and **tone/lethality** (HP: max at 1st level, class average or rolled for higher levels).
- If **no campaign exists**, proceed **standalone** with default 5e fantasy assumptions (level 1 unless the player says otherwise). Note that running `/new-adventure` later will integrate this character.
- **Existing characters:** if `public/characters/` already holds a PC, use AskUserQuestion to ask whether to **add another** or **replace** one. If the campaign's party size is >1, offer to build the party **one character at a time**.

## Step 1 — Interview

**Batch A — Concept & identity**
- **Class** *(plain-text list)* — list the classes available for the setting (the 12 core, Artificer optional; reskinned names for sci-fi/custom). Player replies with their pick.
- **Race / species** *(plain-text list)* — list the setting-appropriate species; player replies.
- **Background** *(plain-text list)* — present the fitting backgrounds and let the player reply with their pick (or name their own): Acolyte · Sage · Soldier · Criminal/Spy · Charlatan · Folk Hero · City Watch / Investigator · Urchin · Guild Artisan · Hermit · Noble · Outlander (reskinned to the setting).
- **Name** — ask in plain text (or via Other).

**Batch B — Ability scores** *(AskUserQuestion)*
- **Method** — Standard array / Point buy / Roll 4d6 drop lowest / Manual entry.
- **Assignment** — Optimize for my class (you assign) / I'll assign (player gives the layout).
- **No fudging — show the work.** Use exactly the six values the chosen method produces — the standard array's numbers (15, 14, 13, 12, 10, 8), the point-buy spend, or the dice as rolled — and never quietly inflate them. Roll openly per the dice rules. Then show the **base assignment → racial ability score increases → final scores** so the player can verify nothing was padded.

**Batch C — Class details & proficiencies**
- **Subclass** — if granted at the starting level: AskUserQuestion if ≤4 options, else plain-text list.
- **Class choice** if any (Fighting Style, Patron, Draconic Ancestry, Favored Enemy, etc.) — AskUserQuestion or plain-text list as the option count dictates.
- **Skill proficiencies** *(AskUserQuestion, multiSelect)* — the class's "choose N from …".

**Batch D — Spells** *(casters only; skip for non-casters)*
- *(plain-text / DM-assist)* — propose a sensible loadout (cantrips + prepared/known spells) for the class/subclass **at the campaign's starting level**, and **always list the full set of available cantrips and spells of every level the character can cast at that starting level** so the player can see every option and swap freely (by name). Scale spell count, spell slots, and known/prepared totals to the starting level — don't assume 1st. Honor known/prepared rules.

**Batch E — Personality & alignment** *(AskUserQuestion)*
- **Trait / Ideal / Bond / Flaw** — offer background-flavored picks + Other (split across two calls if needed).
- **Alignment** — two quick axes: Lawful / Neutral / Chaotic, then Good / Neutral / Evil.

**Batch F — Appearance & details** *(plain-text — gather specifics)*
- Ask the player to describe their character's looks in detail, prompting for each item so the sheet is precise: **age**, **height & build**, **hair** (color, length, style), **eye color**, **skin tone / complexion**, **distinctive features** (scars, tattoos, birthmarks, etc.), and **dress / personal style**. The player can give as much or as little as they like — fill any skipped details with fitting choices and read the result back for approval.

**Batch G — Equipment** *(plain-text list)*
- Take the class+background starting package, or roll for starting gold and buy. List the package contents / available gear (reskinned to setting); player replies.

**Batch H — Backstory & ties** *(AskUserQuestion: evocative options + Other — these feed integration)*
- Origin (where/what you're from)
- A defining past deed / formative event
- Allies, family, or a mentor
- Enemies or rivals

## Step 2 — Build the sheet
Compute everything at the campaign's starting level (strict 5e): ability scores & mods, proficiency bonus, saving throws, skills, passive Perception, initiative, speed, AC, HP (max at 1st level), hit dice, attacks, spell save DC / spell attack, features & traits, proficiencies & languages, equipment, and the personality / appearance / backstory blocks.

Write **`public/characters/<name>.md`** — the full, player-facing sheet (it's the player's own character, so it lives in `public/`). Clean sheet sections; no DM/meta notes.

## Step 3 — Light campaign integration *(only if a campaign exists)*
Keep it **light** — it will deepen naturally in play.
- Write or update the **opening hook** (deferred by `/new-adventure`) so it pulls *this* character in specifically.
- Plant **1–3 ties** from their backstory into the world: things the player legitimately knows (a hometown, a living ally, a known rival) go in `public/` (e.g. `public/npcs/`, `public/areas/`); any **secret truth** (an ancestor bound to the villain, a past deed with hidden fallout, a rival who's secretly an agent) goes in `private/` per spoiler discipline.
- Lightly note the character's existence in any directly-relevant `private/` quest / NPC / timeline file. Do not rework the campaign.
- Any NPC file you create here follows the same tiered template as `/new-adventure` (always: name · race · role/class · alignment · appearance · personality/voice · agenda/secret · reactions · graduation note; plus a combat-stat reference if they might fight — full custom block only for a unique foe). `public/npcs/` entries stay observational — only what the player has seen.
- If **standalone (no campaign)**, skip this and note that `/new-adventure` will integrate the character when run.

## Step 4 — Report
Out-of-game: a short summary of the finished character (name, race, class & level, headline stats), confirmation the sheet was written to `public/characters/`, and — if integrated — a spoiler-free note that the world now carries a few of their ties. If the party size calls for more characters, offer to build the next one.

## Step 5 — Free editing (ongoing)
The character isn't locked once written. After creation, the player is free to keep adjusting it in plain chat — rename, swap spells / skills / equipment, retune ability scores, rewrite appearance or backstory, or change any earlier choice. Apply each change to `public/characters/<name>.md` (recompute any derived stats it affects), and update integration files if a backstory tie changes.
