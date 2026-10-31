# galaxycut-skills

AI skills for editing Luke's videos (GalaxyCut). **Feed these to any AI before it edits a video.**

## Skills

| Skill | What it defines | Raw URL (paste this into the AI chat) |
|-------|-----------------|--------------------------------------|
| **Dynamic Shorts Style** — v1.4 | The talking-character Short format: locked 3-zone frame layout (photo 12–45% · caption ~50% universal position · character bottom-anchored, waist cut at the bottom edge), character pose bank (9 files + 1 banned), yellow `#FFD93D` dry captions 2 words per card with thick black stroke and **no background**, **the approval gate** (complete transcription + numbered caption cards shown in the chat for Luke to edit and approve before anything is applied), hard-cut rules, 3-track audio mix, b-roll policy, locked output format (1080×1920 9:16, 30 fps, H.264), and the edit-map output table | `https://raw.githubusercontent.com/lucasgabrieldevgg/galaxycut-skills/main/dynamic-shorts-style.md` |

## How to use

1. Copy the raw URL of the skill you want.
2. Paste it into any AI chat: *"Read this skill and follow it exactly: \<URL\>"*.
3. Send your `[SCRIPT]` and the character pose bank folder.
4. The AI answers with the edit map; if it is operating a real editor (e.g. GalaxyCut-AI in Bridge Mode), it applies the map to the timeline.

## Conventions

- One file per skill, self-contained, English, versioned in the file header.
- Filenames of the character pose bank are the contract — the skill maps emotion → file.
- The skill file is the **source of truth** for its format; app tool names may change, the spec does not.

## Owner

Luke — [lucasgabrieldevgg](https://github.com/lucasgabrieldevgg)
