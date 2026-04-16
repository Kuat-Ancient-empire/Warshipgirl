# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Stellaris game mod** ("Warship Girls R And MIST Species" / 舰船少女R和MIST物种). It adds anime-style "ship girl" species, custom leaders, events, factions, and gameplay mechanics to the grand strategy game Stellaris.

**Supported version**: v4.3.* | **Mod ID**: 1747099270

## Project Structure

```
Warshipgirl/
├── common/           # Game customization files (species, tech, governments, traits, etc.)
├── events/           # Event chains and triggered events
├── interface/        # GUI (.gui) and graphics (.gfx) files
├── localisation/     # Bilingual translations (english/, simp_chinese/)
├── gfx/              # Models, portraits, textures
├── sound/            # Sound effects
├── music/            # Music tracks
├── prescripted_countries/  # Pre-defined empire templates
└── descriptor.mod    # Mod metadata file
```

## Major Factions

- **Warship_Girls (wsg)** - Main ship girl species with custom authority `auth_warshipgirls`
- **ShenHai (sh)** - 深海 (Deep Sea) fallen empire faction with `auth_shenhai`
- **United_fleet (uf)** - 联合舰队 with unique crisis mechanics

## Coding Conventions

### Script Language
Paradox Scripting Language (declarative, statement-based). Key patterns:
```
namespace = wsg

event_id = {
    title = "event_key.name"
    desc = "event_key.desc"
    picture = GFX_evt_xxx
    is_triggered_only = yes

    trigger = { ... }
    immediate = { ... }

    option = {
        name = "event_key.option_name"
        effect = { ... }
    }
}
```

### Naming Conventions
| Prefix | Usage |
|--------|-------|
| `wsg_` | Warship Girls core content |
| `sh_` | ShenHai/深海 faction |
| `uf_` | United Fleet content |
| `wgor_` | Cross-mod compatibility content |
| `wsg.` (event namespace) | Event IDs |

### Localization Pattern
Events reference localization keys directly:
- `wsg.3000.name` → title
- `wsg.3000.desc` → description
- `wsg.3000.a` / `.b` → option names

Localization files: `wsg_<feature>_l_english.yml` and `wsg_<feature>_l_simp_chinese.yml`

### File Organization
- `common/scripted_effects/` - Reusable effect blocks (numbered prefix for load order)
- `common/scripted_triggers/` - Reusable condition blocks
- `common/traits/` - Leader/species traits organized by category
- `common/technology/` - Tech tree files by faction

## Key Files

- [descriptor.mod](descriptor.mod) - Mod metadata (name, version, supported version)
- [common/defines/wsg_defines.txt](common/defines/wsg_defines.txt) - Game balance adjustments
- [common/game_rules/wsg_rules.txt](common/game_rules/wsg_rules.txt) - Custom game rules
- [events/wsg_events.txt](events/wsg_events.txt) - Core event chain examples

## Working with this Mod

**No build/test commands** - Stellaris mods are text-based data files. Testing requires:
1. Copy the mod folder to Stellaris mod directory
2. Enable the mod in-game
3. Start a new save to test changes

**Load Order**: Files load alphabetically within directories. Prefix with `00_`, `01_`, `zzz_` to control precedence.

**Localization**: Always update both `english/` and `simp_chinese/` directories when adding text content.
