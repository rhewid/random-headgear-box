# random-headgear-box

Pre-renewal only. Every monster kill has a small chance to drop a **Random Headgear Box**.
Opening it gives one random headgear from a pool of **417** that nothing in stock pre-renewal
drops, sells or hands out as a quest reward. Snake Head and Skull Cap are two of them.
The full list is in [POOL.md](POOL.md).

## Settings (Settings -> Mods, then Apply)

| Setting | Default | |
|---|---|---|
| Box drop chance | 5 | Units of 0.01%: 5 = 0.05%, 100 = 1%, 0 = off. Rolled once per monster kill, any monster. |

## How the pool was built

The stock pre-renewal database has 758 headgear items. For each one I searched the stock item
groups, monster drop lists, quests, produce, pets and every NPC script (shops by item id too).
424 had no source at all. I removed 7 that look like test or event leftovers (the `RTC_*`
trophies, `Solo_Play_Box1/2`, `Spare_Card`, `Wit_Pumpkin_Hat`, `Mosquito_Coil_1Use`), which leaves 417.

Items the search did match to something (a shop, a drop, a quest) are not in the box, even if
that source is obscure. Items sold only through the cash shop are in the box, since the cash shop
is not part of the stock database.

## Editing

`npc/headgear_box_pool.txt` holds the pool as `setarray` lines of item ids. Add or remove ids,
the script adapts to the length. The drop itself is `npc/box_drop.txt`, the box is
`db/item_db.yml` (id 72001) and its client name and icon are in `System/itemInfo.lua`.

Modelled on the chests of ARPG Equipments Mod (container item plus an OnNPCKillEvent roll).

## Install

Copy the `random-headgear-box` folder to `%APPDATA%\Ragnarok Offline\state\mods`, or use
Settings -> Mods -> Add mod from folder, then restart the server. Needs app >= 1.4.3, pre-renewal.

## Changelog

- **1.0.0**: first release.

## License

MIT, see [LICENSE](LICENSE).
