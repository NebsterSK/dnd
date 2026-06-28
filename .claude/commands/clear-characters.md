---
description: Delete player character(s) and scrub every mention of them and their actions from all public/ and private/ state files
argument-hint: "[optional character name to clear just one; default clears all]"
---

# /clear-characters - Delete characters and erase their footprint

Delete player character(s) from `public/characters/` **and** remove every trace of them from the rest of the game state - their mentions, dialogue, choices, and the actions/consequences they caused - across all `public/` and `private/` files. The campaign and world themselves (villain, factions, areas, the master plan) stay intact; only the removed characters' *presence and progress* are unwound.

If `$ARGUMENTS` names a character, clear only that one. Otherwise clear **all** characters.

## Step 0 - Identify & confirm (destructive)

- List the files in `public/characters/`. If there are none, say so and stop.
- Decide the target set: a single named character if `$ARGUMENTS` was given, else all of them.
- **Read the targeted character file(s)** and note each character's full name, any aliases/nicknames/titles, and their notable deeds - you'll need these to scrub thoroughly.
- Warn the user **out-of-game** that this permanently deletes the character(s) **and rewinds all progress they drove** (quest advancement, NPC relationships, world changes, journal entries) - it cannot be undone. Then use **AskUserQuestion** to confirm: **"Delete character(s) & erase their footprint"** vs **"Cancel"** (frame Cancel as the safe default).
- If the user cancels, stop immediately and change nothing.

## Step 1 - Delete the character file(s)

- Delete the targeted file(s) from `public/characters/`. Leave any non-targeted characters untouched.

## Step 2 - Scrub their footprint (only after confirmation)

This is a **quick reimagining, not a forensic undo.** Remove the obvious traces and rewrite affected passages so the world still reads coherently - don't agonize over perfectly reversing every downstream ripple. A plausible, clean state is the goal, not a provable one.

Search **every** file under `public/` and `private/` for each removed character's name and aliases (use Grep across both trees), then edit in place to remove their footprint:

- Remove the character's name and every mention of them - their dialogue, decisions, and the actions they took.
- **Roll back world state that changed only because of the removed character:** quest progress they made (revert to the pre-character status), NPC attitudes/relationships/debts toward them, areas they altered or cleared, session journal/log entries, `private/timeline.md` world-clock events that their actions triggered, and any villain/faction reactions aimed at them.
- **Goal:** leave a coherent state as if the removed character had never entered the story. When clearing **all** characters, this effectively rewinds the campaign to its freshly-generated, unplayed baseline. When clearing **one of several**, keep the remaining characters' history and only remove the cleared one's footprint - re-attribute or generalize jointly-taken actions to the remaining party.
- **Editing rules:** edit campaign/world files in place - never delete `private/campaign.md`, `villain.md`, `factions.md`, areas, or quest *definitions* (these exist independent of any PC). You may delete a file only if it existed *solely* to record the removed character's interactions (e.g., a public journal, or a `public/npcs/` entry for someone met only by that character and referenced nowhere else).
- As a quick sanity check, re-grep for the name(s) afterward and clean up any obvious stray mentions - no need to chase every subtle implication.

## Step 3 - Report

Finish with a brief **out-of-game** summary: which character(s) were deleted, which files were edited and which (if any) were removed, confirmation that no traces remain and the world state is coherent, and which characters (if any) still exist. Suggest `/new-character` to create a new one.
