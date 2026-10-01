# HistoryCorrections

A Europa Universalis IV mod that corrects the game's starting history. Target
version 1.37.5.0.

Two jobs. The first is fixing province and country data that is wrong or
anachronistic at any start date. The second is making EU4's **later start dates
actually playable** — vanilla puts most of its care into 1444, so a 1556 start
inherits a world that is subtly frozen in 1444: no buildings anywhere, rulers who
would be 180 years old, great powers that own land their vassals should hold.

## How it works

EU4 merges province and country history additively: any file whose name begins
with a province ID merges into that province, and any file whose first three
characters are a country tag merges into that country. Almost everything here is
therefore a small overlay rather than a replaced vanilla file, which survives
patches and conflicts with other mods far less.

Overlays are named by what they do:

| Suffix | Count | What it does |
| --- | --- | --- |
| `ZZHistCorr` | 864 | Province development, terrain and trade-good corrections |
| `ZZTradition` | 280 | Starting army and navy tradition by country |
| `ZZBuildings` | 230 | Buildings for late start dates, placed by development threshold |
| `ZZUnion` | 36 | Bohemia and Royal Hungary carved out of Austria as personal unions |
| `ZZRulers` | 4 | Replaces rulers who would be absurdly old at a late start |
| `ZZEstates` | 4 | Retires estate privileges no longer true, and fixes one lost on a tag change |
| `ZZHeir` | 2 | Heirs vanilla omits, for Russia and Spain |

Overlays meant only for later starts are dated after 1444, since history is only
applied up to the start date — a 1444 game never reads them.

Beyond the overlays: `common/countries/` revises `historical_idea_groups` for 111
notable countries, `map/terrain.txt` carries the attrition changes, mission trees
are edited for Toungoo and the Ottomans, and `common/on_actions/` seeds things
that cannot be expressed in history at all — baseline military tradition,
monument tiers, and accumulated age splendor for a late start.

## Install

Copy this folder into

    Documents/Paradox Interactive/Europa Universalis IV/mod/

and create a sibling `HistoryCorrections.mod` next to it containing the same lines
as `descriptor.mod` plus an absolute path, forward slashes:

    path="C:/Users/<you>/Documents/Paradox Interactive/Europa Universalis IV/mod/HistoryCorrections"

EU4 ignores the launcher's load order and resolves conflicts by mod *name*, with
the earlier-sorting name winning.

## Conventions

Every line changed in a copied vanilla file carries an `@` in its trailing comment
with the previous value, so a plain text search for `@` lists everything this mod
touches. Deleted lines are commented out rather than removed. Each copied vanilla
file is committed unmodified first, so `git diff` against that commit is the
authoritative list of changes.

Script files are CP-1252 with LF endings and no BOM; localisation is UTF-8 with
BOM. Both matter — EU4 fails quietly on the wrong one.

## Note

A small number of files here are Paradox Interactive's, copied because the
directory in question overrides by filename rather than merging, with edits marked
as above. This is an unofficial personal mod, not affiliated with or endorsed by
Paradox Interactive.
