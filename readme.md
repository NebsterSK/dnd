# 🎲 AI Dungeon Master - D&D 5e

Play a solo game of Dungeons & Dragons 5th Edition with an AI Dungeon Master. This repo turns Claude into a DM that generates a complete hidden campaign, builds your character, and runs the whole adventure - you just play.

No prep, no rulebooks required. The AI handles the world, the NPCs, the dice, and the story; you make the choices.

---

## What you need

- **[Claude Cowork](https://claude.com/product/cowork)** (or Claude Code) - this is where you'll play.
- A copy of this repo - either clone it with **git**, or just **download it as a ZIP** from GitHub (green **Code** button → **Download ZIP**) and unzip it. No git required.

## Getting started

1. **Get the repo** - either clone it:
   ```
   git clone <this-repo-url>
   ```
   …or on GitHub click the green **Code** button → **Download ZIP**, then unzip it. (No git needed.)
2. **Open the folder in Claude Cowork.**
3. **Generate your campaign** - run:
   ```
   /new-adventure
   ```
   Answer the setup questions (genre, tone, length, themes, and so on). The AI builds an entire hidden campaign - world, villain, NPCs, quests, monsters - behind the scenes.
4. **Create your character** - run:
   ```
   /new-character
   ```
   A guided walkthrough builds a full D&D 5e character sheet and quietly weaves them into the world.
5. **Just start playing** - type what your character does or says, in plain chat. The DM describes the world and reacts to you. That's it.

## ⚠️ Do NOT open the `private/` folder

`private/` holds the **hidden campaign** - the villain's real plans, plot twists, secret identities, undiscovered places, and the ending. **Reading it spoils the entire game for you.** Leave it closed and let the story reveal itself through play.

✅ The **`public/`** folder is safe to read - it's *your* stuff: your character sheet, the people and places you've actually met, your quests, and a journal of what you've done.

## How to talk to the DM

- **Just type what you do or say** - everything is in-character by default. *("I push open the tavern door and scan the room.")*
- **`oog:`** - out-of-game. For questions or instructions to the DM. *("oog: how much HP do I have left?")*
- **`inner:`** - your character's private thoughts. *("inner: I don't trust this guy one bit.")*

## Your game saves itself

There's no separate save file - the game **is** the files. As you play, the AI keeps everything current: your character sheet (HP, gear, level, XP), the NPCs and places you discover, your quests, and the running **journal** (`public/journal.md`) you can read any time to recap *"previously…"*.

## Starting over

- **`/clear-adventure`** - wipe the current campaign and world but **keep your character**, ready for a fresh `/new-adventure`.
- **`/clear-characters`** - remove a character (and scrub them from the story).

---

*Have fun, roll well, and don't peek in `private/`.* 🗺️
