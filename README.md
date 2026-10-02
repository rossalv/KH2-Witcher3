# KH2 × Witcher 3: Sora on the Path

A Witcher 3 mod that lets you play the whole game as **Sora from Kingdom Hearts II**:
his look, Keyblade, magic, HUD, Drive Forms and Donald & Goofy as companions. All
of Witcher 3's quests, world and enemies stay as they are.

**Target:** The Witcher 3: Wild Hunt **Remastered (patch 5.0)**, Steam, PC.
**Source assets:** Kingdom Hearts HD 1.5+2.5 ReMIX (Steam), extracted by each user from their own copy.

> This repo holds **only** scripts, item data files, REDkit project files, tools
> and instructions. Assets from KH2 or Witcher 3 are never committed (see
> `.gitignore`). Everyone building the mod extracts them from games they own.

---

## Core design rule

**Under the hood the player stays Geralt. Only how he looks changes.**

Witcher 3 quests, cutscenes and dialogue are built around Geralt. Replacing him
with a new playable character (the way the Ciri sections work) breaks the story.
So Sora is applied as a look over Geralt:

- Sora's body is an **outfit**: a full armor set that, when equipped, shows Sora's model and hides Geralt's head and hair.
- The Keyblade is a **sword**: a new steel/silver sword item with the Kingdom Key model.
- KH abilities are **built on top of** Witcher systems (Signs, stamina, buffs).

Known trade-off: Sora has Geralt's voice in cutscenes.

---

## Roadmap

| Phase | Goal | Main work | Status |
|---|---|---|---|
| **1. Become Sora** | Sora's model + Kingdom Key; roam and do quests as Sora | KH2 extraction, Blender re-rig, REDkit import, outfit & sword items | ⬜ Next |
| **2. Magic** | Fire / Blizzard / Thunder / Aero / Reflect / Cure with an MP pool | WitcherScript, Sign reskins, effects | ⬜ |
| **3. KH2 HUD** | Round HP/MP gauge, command menu, Drive gauge | Flash (.redswf) HUD edits + scripts | ⬜ |
| **4. Donald & Goofy** | Companions who follow, fight and cast Cure | Custom characters, AI behavior, spawn logic | ⬜ |
| **5. Drive Forms & Limits** | Valor/Wisdom/Master/Final, Limits, Reaction Commands | Buffs, look swaps, button-prompt system, animations | ⬜ |
| **6. KH Loot** | Keyblades, accessories, KH-themed gear in the world | Item data, loot tables, shops | ⬜ |
| **Stretch** | Sora's own KH2 combat animations | Converting KH2 animations to Geralt's skeleton | ⬜ |

Start with [`docs/PHASE1.md`](docs/PHASE1.md).

---

## Repo layout

```
docs/                     guides (setup, per-phase steps)
mod/modKH2Sora/           the installable mod (content/scripts, content/xml)
redkit/                   REDkit project files (no cooked/packed output)
tools/                    helper scripts for the asset pipeline
assets/                   LOCAL ONLY, git-ignored: extracted/converted assets
```

## Toolchain

- **The Witcher 3** (Steam, patch 5.0)
- **The Witcher 3 REDkit** (Steam, free for owners): CDPR's official mod editor. As of 5.0 it's required for script mods that should also work on consoles.
- **Kingdom Hearts HD 1.5+2.5 ReMIX** (Steam)
- **OpenKh** (github.com/OpenKH/OpenKh): KH2 file extraction and model export
- **Blender** (4.x)
- **Script Merger – Remastered**: version 5.0 changed how scripts and item data files combine across mods, so the old Script Merger is not safe to use

## Patch 5.0 caveats

5.0 shipped on 2026-09-29. Its script and item data changes are new, so
guides and mods from before 5.0 (anything for 4.04 or 1.32) may not apply. When
something here disagrees with how 5.0 actually behaves, 5.0 wins. Update the docs.
