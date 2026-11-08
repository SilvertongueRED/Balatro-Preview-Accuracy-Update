<h1 align="center">Divvy's Preview for Balatro (Accuracy Update)</h1>

<p align="center">
<b>Preview the score and the dollars you will get by playing the selected cards, for vanilla and modded content alike.</b>
</p>

Fork of [DivvyCr/Balatro-Preview](https://github.com/DivvyCr/Balatro-Preview). Version 5.0.5.

## What changed in 5.0.0

The original mod re-implemented every joker and card effect by hand, so anything it did not know about (modded jokers, enhancements, editions, seals, consumable effects, boss blinds) previewed wrongly. 5.0.0 adds the **accurate engine**:

 - It copies the relevant game state, runs the **real Play Hand flow** of your installed game and mods in a private sandbox with animations, sounds, saving and unlocks switched off, reads the score the game itself computes, and then puts the state back exactly as it was.
 - Because it runs the code that actually scores your hand, modded content is included automatically, including new mods and new versions, with no per-joker support code.
 - The state is checked with a fingerprint after every run. If it is ever not restored exactly, the engine switches itself off for the session and the original engine takes over.
 - If a simulated play fails for any reason (a mod throws an error, an unknown mechanic), the preview falls back to the original engine for that hand. After 3 failures in a row it pauses for a short while.
 - Scoring done in coroutines (Talisman, balatro-utils/futil async scoring) is run to completion, and futil's async scoring options are turned off only while a simulated play runs.
 - Min and max are found by re-running the sandbox with every dice roll forced to its extremes.

## Installation

 0. Install [Lovely](https://github.com/ethangreen-dev/lovely-injector) (Steamodded installs it for you).
 1. Download the latest zip from [Releases](https://github.com/SilvertongueRED/Balatro-Preview-Accuracy-Update/releases/latest).
 2. Unzip it into `%AppData%\Balatro\Mods` so that you have `...\Mods\Balatro-Preview\metadata.json`.
 3. Launch the game.

## Settings

Open the mod settings (Mods menu, Preview) for:

 - **Accurate engine**: use the sandbox described above (on by default). Turn it off to use only the original engine.
 - **Accuracy audit log**: after every real hand, write the previewed score and the actual score to `DVPreview_audit.log` in the Balatro save folder (`%AppData%\Balatro`). Lines say OK or MISMATCH, which engine was used, and the jokers and consumables involved. Useful for reporting a mod that still previews wrongly.
 - The original options (min and max preview, etc.) still work.

## Limits

 - The preview is only as exact as the game's own scoring code is repeatable. Effects that depend on real time, other players or outside state cannot be previewed.
 - Random effects are previewed using the game's real next random numbers when that is what would happen. Min and max cover the extremes.
 - A mod that changes the Play Hand flow in unusual ways may make the sandbox fail; the preview then uses the original engine and the failure is written to the Lovely console.
 - Each preview costs about a millisecond or two on small tables of cards; very large setups cost more.

## Credits

Original mod by Divvy C. Accuracy engine by SilvertongueRED.

## Troubleshooting

If a line in `DVPreview_audit.log` says `engine=legacy`, the accurate engine was not used for that hand. The line ends with `why=` and the reason. The same reason is written once to the Lovely console log as `[DVPreview] accurate engine not used: ...`.

---

<!-- other-mods:start -->
## More from SilvertongueRED

**Fit to Screen (Menu Resizer) is now on Nexus Mods:** [nexusmods.com/balatro/mods/1001](https://www.nexusmods.com/balatro/mods/1001). It stops tall pause menus and sidebars from being cut off at the top and bottom of your screen.

### See my other mods and forks of other people's mods

- [Balatro-Fit-To-Screen-Menu-Resizer-](https://github.com/SilvertongueRED/Balatro-Fit-To-Screen-Menu-Resizer-) ([Nexus Mods](https://www.nexusmods.com/balatro/mods/1001)) - stops tall pause menus and sidebars from being cut off at the top and bottom of your screen
- [Balatro-Mod-Search-and-Sort](https://github.com/SilvertongueRED/Balatro-Mod-Search-and-Sort) ([Nexus Mods](https://www.nexusmods.com/balatro/mods/984)) - search, filter and sort the Mods menu without messing up the load order
- [Balatro-Mod-Updater](https://github.com/SilvertongueRED/Balatro-Mod-Updater) - keeps your mods, Steamodded and Lovely up to date, with backups and a rescue screen when an update breaks the game
- [Balatro-SaveRewinder-Config-Fix](https://github.com/SilvertongueRED/Balatro-SaveRewinder-Config-Fix) - Save Rewinder fork with a config fix: automatic save points and one key to rewind (a fork of [liafonx/Balatro-SaveRewinder](https://github.com/liafonx/Balatro-SaveRewinder))
- [Trance-Active-and-Updated](https://github.com/SilvertongueRED/Trance-Active-and-Updated) - colour and font manager that recolours the whole game, maintained fork (a fork of [SpectralPack/Trance](https://github.com/SpectralPack/Trance))
- [BalatroMods-HoldForFinalHandScore-Update](https://github.com/SilvertongueRED/BalatroMods-HoldForFinalHandScore-Update) - holds the final hand score on screen long enough to read it (a fork of [pumpncode/BalatroMods](https://github.com/pumpncode/BalatroMods), original mod by [Wiwiweb/BalatroMods](https://github.com/Wiwiweb/BalatroMods))
- [Main-Menu-Theme-Selector](https://github.com/SilvertongueRED/Main-Menu-Theme-Selector) - choose your main menu colours, background theme and title logo (a fork of [EmperorGesar/Balatro-Colour-Selector](https://github.com/EmperorGesar/Balatro-Colour-Selector))
- [Better Mouse and Gamepad (bmag)](https://github.com/SilvertongueRED/bmag) - bind any key or button to quick actions like multiselect, easier on your hands (a fork of [uptudev/bmag](https://github.com/uptudev/bmag))
- [Balatro-Music-Selector-Fixes-and-Features](https://github.com/SilvertongueRED/Balatro-Music-Selector-Fixes-and-Features) - pick extra soundtracks or your own music without installing all of Cardsauce (a fork of [DZAladan/Balatro-Music-Selector](https://github.com/DZAladan/Balatro-Music-Selector))
<!-- other-mods:end -->
