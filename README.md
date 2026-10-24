# Keepers

Issue orders to your AI teammates and jokers - a community-maintained fork of
TdlQ's [Keepers](http://pd2mods.z77.fr/keepers.html), updated for
**PAYDAY 2 248.2** (64-bit, SuperBLT).

The mod keeps the original name, options, localization and player-facing
behaviour. Version **239.1** is the first fork release: it merges upstream
revisions r237-r239 (code maintenance by BangL) and adds three fixes that
upstream r239 does not carry.

## Status

- Upstream: TdlQ (original author), BangL (r237-r239 maintenance).
- This repository: fork maintenance by met94.
- Base: upstream r239; first fork release 239.1.
- Verification: static compatibility checks against the 248.2 game Lua; an
  in-game smoke test is still pending.
- Auto-updates come from this repository's GitHub releases, not from
  `pd2mods.z77.fr`. The upstream feed serves the unpatched r239 package and
  would overwrite the fork's fixes.

## Main features

From the original mod page:

> This mod lets you issue various types of order to your NPC teammates,
> including jokers.

- Order modes with icons next to each bot's name: **Stationary**, **Use cover**
  and **Patrol**, plus follow/hold orders for the whole crew.
- Precise positioning: place a mark with GoonMod's Custom Waypoints, shout at a
  bot, and it moves there.
- Stealth: the host can wake a bot with the secondary "Stop AI" control
  (0.5 s hold by default, configurable).
- Bots can be sent to interact with objects and carry bags, at the cost of a
  slower regeneration model.
- Jokers: custom names, health bars, names shared between players, and TeamAI
  movement/suppression settings.
- Shout filtering, so marking cops does not reassign bots by accident.
- Assist revives, stolen-bag retrieval and medic icon colours.

See [MENU_OPTIONS.md](MENU_OPTIONS.md) for every option and mode.

## Requirements

- PAYDAY 2 248.2, 64-bit.
- [SuperBLT](https://superblt.znix.xyz/).
- GoonMod's Custom Waypoints.
- No Duplicated Bullets.

Simple Mod Updater is optional. When present it can install the declared
dependencies; version checks use SuperBLT's own update provider.

## Installation

1. Close PAYDAY 2.
2. Remove or rename an older `Keepers` folder in `...\PAYDAY 2\mods\`.
3. Download `Keepers_v239.1.zip` from
   [Releases](https://github.com/met94/payday2-mod-Keepers/releases/latest)
   and extract it so the result is exactly:
   `...\PAYDAY 2\mods\Keepers\mod.txt`
4. Install GoonMod's Custom Waypoints and No Duplicated Bullets, or let Simple
   Mod Updater prompt for them.
5. Launch the game and open **Mod Options -> Keepers**.

If you download the GitHub source ZIP instead, rename the extracted
`payday2-mod-Keepers-master` folder to `Keepers`.

> Do not install two folders with the same `mod.txt` name. SuperBLT treats the
> name as the dependency key and one copy will win unpredictably.

## Auto-updates and versioning

`mod.txt` points SuperBLT's updater at
`releases/latest/download/meta.json` in this repository.

Versions use `<upstream revision>.<fork release>`:

- `239.1` is the first fork release on top of upstream r239;
- `239.2`, `239.3`, ... are later fork releases on the same upstream base;
- after merging a new upstream revision the base changes (`240.1`).

Upstream integer revisions are never reused, so a future TdlQ/BangL release
cannot collide with a fork build. Release tags mirror the version (`v239.1`).

Upstream's own update endpoint is deliberately not referenced: it only knows
about upstream packages.

## Changes in 239.1

Merged from upstream r237-r239 (code maintenance by BangL):

- Iter and its pathing hooks are no longer required; optional Iter r203 direct
  paths still work.
- Own coarse path distance to interaction positions; each search gets its own
  search data.
- Idle animation no longer restarts while it is already returning to idle.
- `hostage_trade` forwards additional parameters.

Fork-only fixes:

- `PlayerStandard._get_interaction_target` forwards the `secondary` parameter
  (introduced in U240.3), so inspire/long-distance revive targeting no longer
  leaks into team-AI shout filtering.
- Bot bag pickups use `sync_carry_interacted` (introduced in U241), fixing
  multiplayer bag and UI sync.
- Removed a redundant `_debug` toggle in the cover-registration wrapper.

## Compatibility

Keepers hooks 43 game files, mostly AI managers and cop logic. It composes with
mods that wrap different functions, but an AI overhaul that overrides the same
functions can conflict. After changing your load order, check
`...\PAYDAY 2\mods\logs\`; the expected line is
`Setting up mod 'Keepers'` and there should be no `FATAL ERROR`.

Keepers and Monkeepers are separate mods and can be used together.

## Development

Repository layout:

```text
lua/            hooks into game AI, network, HUD and menu code
menu/options.txt  SuperBLT options menu definition
loc/            translations
changelog.txt   release notes / player notes
README.md       this file
MENU_OPTIONS.md player-facing option guide
```

Lua syntax gate (LuaJIT is not shipped in this repository):

```powershell
luajit -bl lua\*.lua
```

When changing code that mirrors a game function body, also check free variables
against the matching 248.2 game file.

Release checklist: bump `version` in `mod.txt`, prepend a `Revision N:` block to
`changelog.txt` (newest first, ending with `Player notes:`), build a zip whose
single root folder is `Keepers`, and publish it with a `meta.json` asset from a
release tagged `v<version>`. The asset is an array containing `ident`
(`Keepers`), `version` (must equal `mod.txt`), `download_url` and optionally
`patchnotes_url`.

## Credits

- Original mod, design and code: **TdlQ**.
- Upstream maintenance r237-r239: **BangL**.
- Translations: chrom[K]a (Russian), NewPJzuza (Thai), LycanCHKN (Italian),
  Arknights (Chinese), Kilowide (Spanish).
- Fork maintenance 239.1: **met94**.

## License

The original Keepers archive (r239) ships no license file, and the original mod
page states none. The fork changes in this repository are released under the
**Unlicense** (public-domain dedication); see [LICENSE](LICENSE).

The original mod name, code, localization files, icons and any retained
original content remain credited to their original authors. No ownership is
claimed over those parts. If you are an original author and want different
terms, open an issue.
