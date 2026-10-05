# random-headgear-box

Every monster kill has a small chance to drop a **Random Headgear Box**. Opening it gives one random
headgear that nothing in the stock item database drops, sells or hands out as a reward. One mod for
both eras: it uses the pool that fits whichever era is running.

| Era | Pool | List |
|---|---|---|
| Pre-renewal | **417** headgears, Snake Head and Skull Cap among them | [POOL-pre-renewal.md](POOL-pre-renewal.md) |
| Renewal | **1,207** headgears | [POOL-renewal.md](POOL-renewal.md) |

## Settings (Settings -> Mods, then Apply)

| Setting | Default | |
|---|---|---|
| Box drop chance | 5 | Units of 0.01%: 5 = 0.05%, 100 = 1%, 0 = off. Rolled once per monster kill, any monster. |
| Drop the box on the ground | off | Off: straight into the inventory. On: it falls where the monster died like a normal drop, unless your `@autoloot` would pick it up (see below). |

**Autoloot.** With the ground drop on, the box goes into your inventory anyway when your `@autoloot` would have taken it: the box is on your `@autolootitem` list, or its drop chance (0.05% by default) is within your `@autoloot` rate and the item type is allowed. Same test as extended-arpg-eq-mod. There is no chat message when the box drops.

## How the pools were built

For every headgear in the era's stock database (costume slots are not counted) I searched the stock
item groups, monster drops, quests, produce, pets and every NPC script (shops by item id too), plus
barters, packages and enchant/reform tables in renewal. An item that matched anything, however
obscure, is not in the box. Items sold only through the cash shop are in it, since the cash shop is
not part of the stock database.

- **Pre-renewal:** 758 headgears, 424 with no source, minus 7 test or event leftovers (`RTC_*`,
  `Solo_Play_Box1/2`, `Spare_Card`, `Wit_Pumpkin_Hat`, `Mosquito_Coil_1Use`) = 417.
- **Renewal:** 2,465 headgears, 1,225 with no source, minus 18 leftovers (the `RTC` trophies,
  `Mosquito_Coil_1Use`, `Wit_Pumpkin_Hat`, `Spider_Temp_TW`, `Solo_Play_Box1/2`, `Spare_Card`) = 1,207.
  480 of them have no entry in the client's item table, so `renewal/System/itemInfo-headgears.lua` names them (English name,
  defense, weight and slots from the server database, a generic icon per slot). Their worn sprite is not affected.
  Snake Head and Skull Cap sit in a stock renewal item group, so they are not in this pool.

## Layout

- `db/item_db.yml`: the box, item id 72001. `System/itemInfo.lua`: its client name and Gift Box icon.
- `npc/box_drop.txt`: the drop roll, shared by both eras.
- `pre-renewal/npc/headgear_box_pool.txt` and `renewal/npc/headgear_box_pool.txt`: the pool as
  `setarray` lines of item ids. The app applies the folder for the running era over the mod, so only
  one is ever loaded. Add or remove ids and the script adapts to the length.

## Install

Copy the `random-headgear-box` folder to `%APPDATA%\Ragnarok Offline\state\mods`, or use
Settings -> Mods -> Add mod from folder, then restart the server. Needs app >= 1.4.3.

## Changelog

- **1.1.0**: the 480 renewal headgears the client has no item name for are named by the mod (they showed as "Unknown Item"), so the renewal pool is the full 1,207. They use generic icons.
- **1.0.0**: first release, pre-renewal and renewal. Optional ground drop with autoloot support.

## License

MIT, see [LICENSE](LICENSE).
