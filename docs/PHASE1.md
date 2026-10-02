# Phase 1: Become Sora

**Goal:** equip "Sora's Outfit" and the "Kingdom Key", then roam Velen and do
quests looking like Sora. Geralt's animations are used for everything for now.

**Done when:** Sora's model replaces Geralt's in gameplay *and* cutscenes, the
Keyblade is drawn and swung in combat, and unequipping the outfit brings Geralt back.

> File names and paths marked **(verify)** come from KH2 and Witcher 3 modding
> knowledge from before patch 5.0. Check each one when you get to it and fix
> this doc if it's wrong.

---

## Step 0: Install tools

1. Witcher 3 on 5.0. Launch it once **without mods** to confirm it runs clean.
2. **REDkit** from Steam (Library → Tools, or search "The Witcher 3 REDkit"). Create
   a new mod project named `modKH2Sora` and confirm it opens the 5.0 game files.
3. **OpenKh**: download the latest release from github.com/OpenKH/OpenKh.
4. **Blender 4.x**.
5. **Script Merger – Remastered**: not needed yet, but install it before adding other mods.

## Step 1: Extract Sora and the Kingdom Key from KH2

KH2's PC files are packed archives (`.hed` + `.pkg`) in the KH 1.5+2.5 install
folder (`.../KINGDOM HEARTS -HD 1.5+2.5 ReMIX-/Image/en/kh2_*.hed`) **(verify)**.

1. Use OpenKh's archive extractor (`OpenKh.Command.IdxImg`, `hed extract` command) **(verify)**
   to unpack the `kh2_first` … `kh2_sixth` archives into `assets/kh2_extract/`.
2. Find the models:
   - Sora (base KH2 outfit): `obj/P_EX100.mdlx` **(verify)**
   - Kingdom Key: `obj/W_EX010.mdlx` **(verify)**
   - Later: Drive Form models are named `P_EX100_*` (e.g. `_BTLF` = Valor) **(verify)**, Donald is `P_EX020`, Goofy is `P_EX030` **(verify)**
3. Use OpenKh's model tools to export both to FBX/DAE with textures, into
   `assets/kh2_converted/`. Open them in Blender to make sure the mesh and textures look right.

## Step 2: Export Geralt's skeleton from REDkit

Sora has to use **Geralt's skeleton** so he can use all of Witcher 3's
animations (combat, horse riding, climbing, swimming, cutscenes).

1. In REDkit's Asset Browser, find the base male skeleton (`characters/base_entities/man_base/man_base.w2rig`) **(verify)**
   and a Geralt body mesh under `characters/models/geralt/` **(verify)**.
2. Export the body mesh **with its skeleton** to FBX in `assets/w3_reference/`.

## Step 3: Re-rig Sora to Geralt's skeleton (Blender)

This is the main art task in Phase 1.

1. Import Geralt's FBX (skeleton + body) and Sora's model into one Blender scene.
2. Scale and pose Sora to match Geralt's skeleton. Witcher 3's rest pose is a
   T-pose. Line up shoulders, elbows, hips, knees.
3. **Proportions:** Sora is short with a large head. Two options:
   - **A (recommended to start):** scale Sora up to roughly Geralt's height and fit him
     to the skeleton as-is. Animations will just work, and he'll look somewhat lanky.
   - **B:** keep Sora's proportions and adjust the bone lengths. Truer to KH2, but this
     risks broken cutscenes, IK and climbing. Try it after A works.
4. Delete Sora's KH2 skeleton, parent the mesh to Geralt's armature, and **weight paint**
   to Geralt's bones (start with automatic weights, then fix shoulders, hips and the large shoes).
5. Split the mesh into parts that match Witcher armor slots:
   - `sora_torso` (jacket, shirt, head + hair; see Step 5)
   - `sora_gloves`, `sora_pants`, `sora_boots`
6. Separately, set up the Kingdom Key so its grip lines up with the bone Geralt's sword attaches to (the right hand's weapon bone).
7. Export each part to FBX into `assets/export/`.

## Step 4: Import into REDkit

1. Import each FBX as a mesh (`.w2mesh`) into the `modKH2Sora` project and set
   up materials/textures (start from a Geralt armor material and swap the textures).
2. Create the item entities (outfit pieces and the Keyblade) by copying an existing
   vanilla armor/sword entity and swapping in the meshes.
3. Add item definitions:
   - `Sora's Outfit`: 4 pieces (chest/gloves/pants/boots)
   - `Kingdom Key`: steel sword (silver version later), scabbard hidden
4. Pack the mod and install it from REDkit. Use the console (`additem('<item name>')`) to
   spawn the items and test.

## Step 5: Hide Geralt's head and hair

The outfit covers the body, but Geralt's head and hairstyle are separate pieces
that still show. Approaches, simplest first:

1. **Sora's head inside the chest piece**, plus a small script that hides Geralt's
   hair and head while the outfit is equipped, and shows them again when it's removed.
2. Replace Geralt's head with a custom Sora head (more work, but cutscene
   facial animation may partly carry over).

Option 1 needs a WitcherScript. **This is where I come in:** once Steps 1–4
work, send me the relevant 5.0 vanilla scripts (your local copy of the game's
script folder) and I'll write the hide/show logic against the real 5.0 API.
Vanilla scripts are never committed. Keep them in the git-ignored `reference/` folder.

## Step 6: Test checklist

- [ ] Outfit equips/unequips; Geralt returns when removed
- [ ] No Geralt head/hair visible on Sora
- [ ] Walking, sprinting, combat, dodge, roll
- [ ] Keyblade draws, sheathes, swings; scabbard hidden
- [ ] Riding Roach, swimming, climbing
- [ ] A dialogue scene (e.g. any White Orchard NPC)
- [ ] A cutscene (e.g. Griffin fight start)
- [ ] Loading a save with the outfit equipped
- [ ] Meditation, then save and reload

Report anything that looks wrong (stretched mesh, clipping, missing parts) with a screenshot.
