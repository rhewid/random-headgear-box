# random-headgear-box

Monsters can drop a **Random Headgear Box** (0.05% by default). Opening it gives one random headgear that
nothing in the stock item database drops, sells or hands out as a reward. One mod for both eras: it uses the
pool that fits whichever era is running. It also brings a **Headgear Exchange** and a **Costume Tailor**.

| Era | Pool | List |
|---|---|---|
| Pre-renewal | **417** headgears, Snake Head and Skull Cap among them | [POOL-pre-renewal.md](POOL-pre-renewal.md) |
| Renewal | **1,207** headgears | [POOL-renewal.md](POOL-renewal.md) |

## Drops: box or ticket

The **Monsters drop the Random Headgear Box** setting decides what a kill can drop:

- **On (default):** the Random Headgear Box, as before.
- **Off:** a **Headgear Exchange Ticket** (it uses the event ticket icon) that the Headgear Exchange trades for boxes.

## Headgear Exchange (Prontera 183,190)

| You pay (default) | You get |
|---|---|
| **10** tickets | a **Lower / Middle / Upper Headgear Costume Box**: one random costume of that slot, taken from the Costume Tailor's list |
| **20** tickets | a **Lower / Middle / Upper Headgear Box**: one random headgear of that slot from the pool |
| **30** tickets | the **Random Headgear Box**: one random headgear from the pool, any slot |

A headgear or costume with several slots (for example upper and middle) is in the list of each of its slots.
All three prices are settings.

## Costume Tailor (Prontera 181,190)

The same NPC as in the `headgear-to-costume` mod, bundled here. It turns a headgear into a costume that looks
exactly like it: **cards come back, refine, enchantments and bonus options are lost.** Fee 10,000 zeny by
default (setting). Only unequipped headgear in your inventory is listed, 30 per page. 755 headgears in
pre-renewal and 2,443 in renewal can be converted; those without a view id or AegisName are skipped (3 and 22).

Each headgear has a **costume twin**: a normal item in a costume slot with the headgear's view id, so it draws
the same sprite. Twins are named `Costume <headgear name>` and have no stats.

Do not run this mod together with `headgear-to-costume`: both place the same NPC and define the same items.

## Settings (Settings -> Mods, then Apply)

| Setting | Default | |
|---|---|---|
| Box drop chance | 5 | Units of 0.01%: 5 = 0.05%, 100 = 1%, 0 = off. Rolled once per monster kill, any monster. |
| Monsters drop the Random Headgear Box | on | Off = they drop a Headgear Exchange Ticket instead. |
| Drop the box on the ground | off | Off: straight into the inventory. On: it falls where the monster died like a normal drop, unless your `@autoloot` would pick it up (see below). |
| Tickets for a Headgear Costume Box | 10 | Lower, middle or upper. |
| Tickets for a one-slot Headgear Box | 20 | Lower, middle or upper. |
| Tickets for the Random Headgear Box | 30 | Any slot. |
| Costume Tailor fee | 10000 | Zeny per costume. 0 = free. |

**Autoloot.** With the ground drop on, the dropped box or ticket goes into your inventory anyway when your
`@autoloot` would have taken it: it is on your `@autolootitem` list, or its drop chance (0.05% by default) is
within your `@autoloot` rate and the item type is allowed. There is no chat message when it drops.

## Item ids

This mod reserves two id blocks. Stock items do not use 70000-99999.

| Ids | What |
|---|---|
| 72001 | Random Headgear Box |
| 72011-72013 | Upper / Middle / Lower Headgear Costume Box |
| 72021-72023 | Upper / Middle / Lower Headgear Box |
| 72031 | Headgear Exchange Ticket |
| **73000-75999** | **costume twins** (pre-renewal 73000-73754, renewal 73000-75442) |

A twin's id is its position in the era's sorted headgear list, so if an app update adds a headgear the table
must be regenerated with new headgears *appended* at the end, otherwise costumes players already own would
turn into different items. Other mods in this repository use 50000-50071, 55000-56999 (ARPG Equipments),
70000-71301 (costume-collector-extended-prerenewal) and 92001-92010 (endow-sage).

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
  Snake Head and Skull Cap sit in a stock renewal item group, so they are not in this pool.

## Item names and descriptions (renewal)

The renewal client has no item name for 480 of the 1,207 headgears, so they would show as "Unknown Item"
(the worn sprite is fine). `renewal/System/itemInfo.lua` names and describes them:

- **33** use the name, icon and description of the iRO client table, only where its record matches the
  server's item name.
- **447** are generated. Name, defense, weight, slots, level, job and class limits come from the server item
  database. The item script is turned into plain text: stat and percent bonuses, damage against race, size and
  element, resistances, skill damage / cooldown / cast bonuses, autocasts and chance effects, refine, skill-level,
  stat and base-level conditions, and per-refine or per-level scaling. Checked against the 1,958 headgears that
  do have a real description: 94.8% of the generated lines carry numbers that also appear in the real text.
  116 items still end with "Has additional effects that are not listed here", where the script uses something
  not translated. They use a generic icon per slot.

## Layout

The app applies the folder of the running era over the mod, and a file at the same path replaces the mod's copy,
so everything era-specific lives in the era folders and only the scripts are shared.

- `npc/box_drop.txt`: the drop roll. `npc/exchange.txt`: the Headgear Exchange. `npc/headgear_costume.txt`: the Costume Tailor.
- `<era>/db/item_db.yml`: the boxes, the ticket and the costume twins. `<era>/System/itemInfo.lua`: their client names
  and icons (renewal also names the 480 headgears the client lacks).
- `<era>/npc/headgear_box_pool.txt`: the headgear pool per slot (`F_RndHeadgearBox`). `<era>/npc/htc_table.txt`: the
  headgear -> costume twin table and the costume lists per slot (`F_RndCostumeBox`). Add or remove ids freely.

## Install

Copy the `random-headgear-box` folder to `%APPDATA%\Ragnarok Offline\state\mods`, or use
Settings -> Mods -> Add mod from folder, then restart the server. Needs app >= 1.4.3.

## Changelog

- **1.3.0**: Headgear Exchange Ticket drop (new setting), the Headgear Exchange NPC with costume boxes, one-slot
  headgear boxes and the Random Headgear Box, and the Costume Tailor from headgear-to-costume bundled. Exchange ticket idea by BlaXun, costume exchange idea by faust.layout.
- **1.2.0**: item descriptions for the 480 renewal headgears the client has no entry for (see above), including skill bonuses and conditions.
- **1.1.1**: fixed the box showing as "Unknown Item" in renewal. The app links one item table per mod and the renewal table replaced the box's, so the renewal table now includes the box.
- **1.1.0**: the 480 renewal headgears the client has no item name for are named by the mod (they showed as "Unknown Item"), so the renewal pool is the full 1,207. They use generic icons.
- **1.0.0**: first release, pre-renewal and renewal. Optional ground drop with autoloot support.

## Credits

- **BlaXun**: the idea of dropping an exchange ticket instead of the box itself.
- **faust.layout**: the idea of the costume exchange (tickets for headgear costume boxes).

## License

MIT, see [LICENSE](LICENSE).
