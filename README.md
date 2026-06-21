# DragonUI_NewEra

A support / extension module for **[DragonUI](https://github.com/NeticSoul/DragonUI)** — the World of Warcraft **3.3.5a (WotLK)** port of the Dragonflight UI.

DragonUI ports the Dragonflight **HUD** to 3.3.5a. **DragonUI_NewEra** fills in the rest: it faithfully downports the panel work from **NewEra** (Ashgaroth's Classic Era 1.15 Dragonflight-style addon) to 3.3.5a, rebuilding the panels DragonUI hasn't ported yet so the whole interface matches the modern look — not just the action bars.

> **Requires DragonUI.** This is an add-on *to* DragonUI, not a standalone UI. It reuses DragonUI's textures, atlases, and chrome where possible and only rebuilds what's missing.

## What's inside

### Character panel
A full custom replacement for the 3.3.5a `CharacterFrame`, styled to match Dragonflight:

- Paperdoll (3D model + all equipment slots) with modern model controls (zoom, click-drag rotate / pan)
- **Stats sidebar** (General / Attributes / Melee / Ranged / Spell / Defense / Resistances) with proper tooltips
- Tabs for **Character, Pet, Skills, Honor, Reputation**
- **Titles** picker — set your title from the panel; the window header shows `Name <Title>`
- **Equipment Manager** — a fully client-side gear-set manager (works on any server, no reliance on the native equipment-manager API)

### `/gearset` — equip a saved set by name

Save gear sets in the Equipment Manager, then swap to one from chat or a macro:

```
/gearset "Tank Set"      -- equip the set named "Tank Set" (case-insensitive)
/dnequip "Healer Set"    -- alias of /gearset
```

- Matches by name (quoted or bare); errors and lists your sets if no match.
- If the set is already fully equipped, it does nothing (no redundant request to the server).
- Sets are stored client-side in SavedVariables and applied with a physical item swap.

*(Note: `/equip` and `/equipset` are reserved built-in WotLK macro commands, hence `/gearset` / `/dnequip`.)*

### Spellbook
A standalone War-Within-style two-page spellbook, replacing the 3.3.5a `SpellBookFrame`:

- **Card layout** — every learned spell as a Dragonflight-style card (icon + name + rank), flowing across a two-page evergreen book; a min/max button collapses it to a single page (↗ Expand / ↙ Condense).
- **Category tabs** — General, your class (sectioned by spec), and a live Pet tab, styled to match the Character panel.
- **Active vs passive** — active spells use the gold spellbook frame; passives use the dark square talent-node socket. Passive cells are click-inert (hover for tooltip only); pet cells ignore right-click.
- **Whole-cell interaction** — click anywhere on a cell to cast, drag to place it on a bar, hover anywhere for the tooltip.
- **Search + options** — filter spells by name; a cog menu toggles *Hide Passives* and *Show All Ranks* (off = highest rank only).

Built natively for 3.3.5a's index-based spellbook API (a compat shim maps the Cataclysm `GetSpellBookItem*` family onto it).

## Roadmap

Faithfully downporting the remaining NewEra panels to 3.3.5a:

- [x] ~~**Character panel**~~ — *done* (paperdoll, stats sidebar, Skills / Honor / Reputation / Pet tabs, Titles, Equipment Manager + `/gearset`)
- [x] ~~**Spellbook**~~ — *done* (two-page book, category tabs, active/passive frames, search + Hide Passives / Show All Ranks, single/double-page toggle)
- [ ] **Talents**
- [ ] **Quest Log**
- [ ] **Merchant**
- [ ] **Mail**

## Credits

- **[DragonUI](https://github.com/NeticSoul/DragonUI)** by NeticSoul — the base 3.3.5a Dragonflight UI port this builds on.
- **NewEra** by Ashgaroth — the Classic Era Dragonflight-style addon these panels are downported from.
- Dragonflight UI © Blizzard Entertainment.
