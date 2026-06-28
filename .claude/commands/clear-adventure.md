---
description: Delete all campaign/world files from private/ and public/, keeping player characters
---

# /clear-adventure - Wipe the current campaign

Delete the current campaign and world state from `private/` and `public/` so a fresh `/new-adventure` can be run - but **keep the player characters** (`public/characters/`). This is the "I want a new adventure, but my character carries over" reset. To wipe characters too, use `/clear-characters`.

## Step 0 - Warn & confirm (destructive)

- First check whether any campaign files exist (anything under `private/` or `public/` other than `public/characters/`). If there's nothing to clear, say so and stop.
- Otherwise, warn the user **out-of-game** that this permanently deletes the current campaign, world, NPCs, areas, and quests (player characters are kept), then use **AskUserQuestion** to confirm: **"Wipe the campaign (keep characters)"** vs **"Cancel"** (frame Cancel as the safe default).
- If the user cancels, stop immediately and change nothing.

## Step 1 - Delete (only after confirmation)

- Delete **all files under `private/`** (recursively) - campaign, villain, timeline, factions, and everything in `npcs/`, `areas/`, `quests/`.
- Delete **all files under `public/` EXCEPT everything in `public/characters/`** - i.e. remove `public/world.md`, `public/npcs/`, `public/areas/`, `public/quests/`, journals, etc., but never touch `public/characters/` or its contents.
- **Keep the directory skeleton** (leave the now-empty subdirectories in place). Do not delete `public/characters/`.

Suggested commands (verify paths first; never delete outside this project):
- `find private -type f -delete`
- `find public -type f -not -path 'public/characters/*' -delete`

## Step 2 - Report

Finish with a brief summary: confirmation that player characters in `public/characters/` were kept, and a note that the player can now run `/new-adventure` to generate a new campaign.
