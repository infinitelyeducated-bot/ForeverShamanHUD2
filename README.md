<p align="center"><img src="media/banner.jpg" alt="Shaman header art" width="100%"></p>

<img src="media/crest.png" alt="Shaman crest" width="96" align="left">

# ForeverShamanHUD2

A shaman HUD for **World of Warcraft: Forever** (Interface 16001). This is the "2" build: everything in [ForeverShamanHUD](../../../ForeverShamanHUD) plus text fonts and formats, player / target / target-of-target frames and minimap options.

<br clear="left">

> **Status: version 2.0.0, not yet verified in the game client.** It passes a mocked-client test
> suite and boots cleanly in a simulated UI, but nobody has confirmed it in the real game. Expect
> rough edges and please report them.

## Install

1. Download this repository (Code -> Download ZIP) or clone it.
2. Put the folder in `World of Warcraft/_forever_/Interface/AddOns/` and make sure it is named exactly `ForeverShamanHUD2`.
3. Restart the game or `/reload`. Type `/fs2` to open the menu.

Optional companions (the HUD works without them):
- **ForeverArt** - menu artwork: a painted backdrop, a header picture and a class crest.
- **ForeverFonts** - extra typefaces for the Text options.

Do not enable `ForeverShamanHUD` at the same time: you would get two HUDs.

## How you use it

Open the menu with `/fs2`. **While the menu is open** (and Lock is off), point at any bar or icon:

| Do this | Result |
|---|---|
| Hold **CTRL**, then hold the **left** mouse button | The item sticks to the cursor until you let go |
| Hold **CTRL** and roll the **mouse wheel** | Bigger or smaller |
| Hold **CTRL**, then hold the **right** mouse button and drag | Turns the item; it stays as you leave it |
| **Double-click the right** mouse button | Back to its original orientation |

Icons turn to any angle. Bars and the recent-actions row turn in quarter turns, because the
client cannot draw a status bar at an angle. With the menu closed nothing can be clicked or moved.
Because the mouse does all of this, the menu has no position, scale or orientation controls.
The **Help** tab in the menu explains all of it in game.

## What it shows

- **Mana bar** - mana. Its number has its own on/off switch.
- **Regeneration bar** - what is actually arriving per second.
- **Swing timer** - with its own Show switch, colour, spark, text mode, ticks and ready flash.
- **Combo points** - present but off by default; this class has none.
- **Recent actions** - the last four spells you cast, newest first.
- **Ability icons** - 37 abilities, switched on one by one. On cooldown an icon goes dark and
  grey, a clock sweep runs round it, and the time left counts down to the hundredth of a second in
  its bottom-right corner, drawn above everything else. It also flashes when ready, glows while its
  effect is on you, and dims or turns red when you cannot use it. Every one of these has a switch.
- **Unit frames** - player, target and target-of-target, with cast bar, buffs and debuffs. Opening
  the menu puts all three on screen (switched-off ones dimmed) so each can be moved and sized.
- **Text** - typeface, size, place and number format for each text, beside the thing it labels.
- **Map** - minimap shape, size and clutter.

On by default: Earth Shock, Chain Lightning, Grounding Totem, Earthbind Totem.

## Look

- **40 colour skins**, plus **custom colours**: on the Skins tab click any colour in the strip for a
  colour wheel (with an Opacity slider for the see-through parts), then save your set under a name.
- **Menu artwork** (needs ForeverArt): High resolution, Low resolution or Off, and a choice of header picture.
- **Named profiles**: save, load and delete whole setups. Reset to default keeps them.

## Commands

| Command | What it does |
|---|---|
| `/fs2` | Open or close the menu |
| `/fs2 help` | Open the Help tab |
| `/fs2 abilities`, `skins`, `profiles`, `text`, `frames`, `map` | Open that tab |
| `/fs2 show` / `hide` | Whole HUD on or off |
| `/fs2 energy|regen|swing|combo|trail on|off` | One element on or off ("energy" is the resource bar) |
| `/fs2 cooldown on|off` | Countdown numbers |
| `/fs2 lock` / `unlock`, `sticky`, `grid` | Editing aids |
| `/fs2 skin <name>`, `save <name>`, `load <name>`, `reset` | Skins and profiles |

## Abilities

IDs are rank 1 and only a fallback: at login the addon asks the client for the ID behind each
spellbook name, so an icon follows the rank you actually know.

| Ability | Fallback ID | Default |
|---|---|---|
| Earth Shock | 8042 | on |
| Chain Lightning | 421 | on |
| Grounding Totem | 8177 | on |
| Earthbind Totem | 2484 | on |
| Flame Shock | 8050 | off |
| Frost Shock | 8056 | off |
| Purge | 370 | off |
| Tremor Totem | 8143 | off |
| Stoneclaw Totem | 5730 | off |
| Fire Nova Totem | 408341 | off |
| Magma Totem | 8190 | off |
| Searing Totem | 3599 | off |
| Chain Heal | 1064 | off |
| Healing Stream Totem | 5394 | off |
| Mana Spring Totem | 5675 | off |
| Windfury Totem | 8512 | off |
| Grace of Air Totem | 8835 | off |
| Lightning Shield | 324 | off |
| Lava Burst | 408490 | off |
| Riptide | 408521 | off |
| Astral Recall | 556 | off |
| Reincarnation | 20608 | off |
| Stormstrike | 17364 | off |
| Elemental Mastery | 16166 | off |
| Nature's Swiftness | 16188 | off |
| Mana Tide Totem | 16190 | off |
| Lightning Bolt | 403 | off |
| Healing Wave | 331 | off |
| Lesser Healing Wave | 8004 | off |
| Strength of Earth Totem | 8075 | off |
| Stoneskin Totem | 8071 | off |
| Water Shield | 408510 | off |
| Cure Disease | 2870 | off |
| Cure Poison | 526 | off |
| Totemic Recall | 36936 | off |
| Call of the Elements | 66842 | off |
| Totemic Projection | 437009 | off |

## How it stays within the client's rules

Public API only. No protected calls, no combat automation, no combat log, nothing written outside
its own SavedVariables. Values the client marks secret are handed to widgets and never compared or
calculated with; a cooldown the addon may not read simply shows no number.

## Known limits

- Not verified in game (see Status).
- Bars turn in quarter turns only; a turned icon's border, sweep and number stay upright. Unit frames move and size but do not turn.
- Glow, dim and red tint depend on what the client will tell an addon; in combat it may withhold
  those answers and the icon then stays plain.
- A few fallback spell IDs are unconfirmed on this client; the name lookup normally corrects them.

## How it is built

This file and the addon are generated: one generator produces all nine class HUDs from a single
reference, so they stay identical in behaviour. A mocked-client suite (722 assertions for this
class), a Lua 5.1 limits check and a simulated UI run are part of every build.
