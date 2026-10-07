# random-headgear-box

Monsters can drop a **Random Headgear Box** (0.05% by default) or tickets that Prontera NPCs trade for boxes of
headgears and costumes. One mod for both eras: it uses the pool and costume list that fit whichever era is running.

| | Pre-renewal | Renewal |
|---|---|---|
| Headgear pool (nothing else drops or sells them) | **417**, Snake Head and Skull Cap among them ([list](POOL-pre-renewal.md)) | **1,207** ([list](POOL-renewal.md)) |
| Costume collection (one-slot costumes) | **1,203**, the collection of costume-collector | **2,965**, the stock costume items |
| Headgears the Costume Tailor can convert | 755 | 2,443 |

## Drops

Every monster kill rolls twice:

- **Headgear item**, chance = *Box drop chance* (0.05%). The setting **Monsters drop the Random Headgear Box** decides what
  falls: the **Random Headgear Box** (on, default) or a **Headgear Exchange Ticket** (off).
- **Costume Exchange Ticket**, chance = *Costume Exchange Ticket drop chance* (0.05%, 0 = off). It uses the One-way Ticket icon.

Ground drop and `@autoloot` work for both items (see Settings).

## NPCs in Prontera

| NPC | Where | What |
|---|---|---|
| **Costume Tailor** | 181,190 | Turns any unequipped headgear into a costume that looks the same. Cards come back, refine, enchantments and bonus options are lost. Fee 10,000 zeny. |
| **Headgear Exchange** | 183,190 | Headgear Exchange Tickets for boxes (below). |
| **Costume Exchange** | 185,190 | Costume Exchange Tickets for boxes from the costume collection (below). |
| **Ticket Swap** | 188,193 | Headgear Exchange Tickets <-> Costume Exchange Tickets, in both directions. **1:1 by default, each direction's rate is a setting** (for example make costume -> headgear cost 2 or 3 tickets). |

### Headgear Exchange (headgear tickets)

| You pay (default) | You get |
|---|---|
| **10** tickets | a **Lower / Middle / Upper Headgear Costume Box**: one random costume copy of a headgear of that slot |
| **20** tickets | a **Lower / Middle / Upper Headgear Box**: one random headgear of that slot from the pool |
| **30** tickets | the **Random Headgear Box**: one random headgear from the pool, any slot |

### Costume Exchange (costume tickets)

| You pay (default) | You get |
|---|---|
| **10** tickets | an **Upper / Middle / Lower Costume Box**: one random costume of that slot from the costume collection |
| **15** tickets | a **Random Costume Box**: one random costume from the collection, any head slot or garment |

Both exchanges and the Ticket Swap ask **how many** you want when you can afford more than one: 1, 5, 10 (when affordable), the maximum
you can afford, or any amount you type. All prices are settings. Do not confuse the two kinds of costume boxes: a *Headgear Costume Box* gives a costume copy of a
headgear (see the Tailor), a *Costume Box* gives a costume from the collection.

## Costumes

**Costume Tailor.** Each headgear has a costume twin: a normal item in a costume slot with the headgear's view id, so it draws
the same sprite. Twins are named `Costume <headgear name>` and have no stats. A headgear that fills several slots (for example
Dark Basilium: upper, middle and lower) comes as **one costume per slot**, because the server only hides a costume with the
"view costume" option when it fills a single slot.

**Costume collection.** The boxes of the Costume Exchange draw from a list of costumes that fill **one slot** (for the same
reason, multi-slot costumes are not in the boxes).
- *Pre-renewal:* the collection of the **costume-collector** mod by Thomas, 1,203 single-slot costumes (838 upper, 165 middle, 196
  lower, 4 garments). Their item ids are moved to 70000-71301, see Item ids.
- *Renewal:* the costumes already in the stock renewal item database, with no item redefined (2,965 single-slot costumes
  and garments). 731 of them have no entry in the client's item table and are named by this mod with a generic icon.

Odette's shop and the Lucky Trunk of costume-collector-extended-prerenewal are not part of this mod. Do not run this mod together with
`headgear-to-costume`, `costume-collector` or `costume-collector-extended-prerenewal`: they place or define the same things.

## Settings (Settings -> Mods, then Apply)

| Setting | Default | |
|---|---|---|
| Box drop chance | 5 | Units of 0.01%: 5 = 0.05%, 100 = 1%, 0 = off. Rolled once per monster kill, any monster. |
| Monsters drop the Random Headgear Box | on | Off = they drop a Headgear Exchange Ticket instead. |
| Drop the box on the ground | off | Off: straight into the inventory. On: it falls where the monster died like a normal drop, unless your `@autoloot` would pick it up (see below). |
| Tickets for a Headgear Costume Box | 10 | Lower, middle or upper. |
| Tickets for a one-slot Headgear Box | 20 | Lower, middle or upper. |
| Tickets for the Random Headgear Box | 30 | Any slot. |
| Costume Exchange Ticket drop chance | 5 | Units of 0.01%, 0 = off. |
| Costume tickets for an Upper / Middle / Lower Costume Box | 10 | |
| Costume tickets for a Random Costume Box | 15 | |
| Ticket Swap: headgear tickets for 1 costume ticket | 1 | Raise it to make headgear -> costume more expensive. |
| Ticket Swap: costume tickets for 1 headgear ticket | 1 | Raise it to make costume -> headgear more expensive. |
| Costume Tailor fee | 10000 | Zeny per costume. 0 = free. |

**Autoloot.** With the ground drop on, a dropped box or ticket goes into your inventory anyway when your `@autoloot` would
have taken it: it is on your `@autolootitem` list, or its drop chance is within your `@autoloot` rate and the item type is
allowed. There is no chat message when it drops.

## Item ids

Stock items do not use 70000-99999. This mod uses:

| Ids | What |
|---|---|
| 70000-71301 | pre-renewal costume collection (1,203 of the ids are used; ids moved from costume-collector's 19500-31495, which overwrote stock items) |
| 72001 | Random Headgear Box |
| 72011-72013 | Upper / Middle / Lower Headgear Costume Box |
| 72021-72023 | Upper / Middle / Lower Headgear Box |
| 72031 | Headgear Exchange Ticket |
| 72032 | Costume Exchange Ticket |
| 72041-72043 | Upper / Middle / Lower Costume Box |
| 72044 | Random Costume Box |
| **73000-75999** | **costume twins of headgears** (pre-renewal 73000-73881, renewal 73000-75661) |

A twin's id is its position in the era's sorted headgear list (73000 + i, the headgear's first slot); the extra pieces of
multi-slot headgears follow after that block. If an app update adds a headgear the table must be regenerated with new
headgears *appended* at the end, otherwise costumes players already own would turn into different items. Other mods in
this repository use 50000-50071, 55000-56999 (ARPG Equipments) and 92001-92010 (endow-sage).

## How the headgear pools were built

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

## Item names and descriptions

`<era>/System/itemInfo.lua` names only the mod's own items: the boxes and tickets (72001-72044) and the costume
twins (73000+). Official items are left to the client's own tables. The app reads a mod's item table before the
client's, so an entry for an official item would replace its real iRO name and icon with a generic one (issue #1).
Headgears or costumes that the client has no name for show as "Unknown Item" (the worn sprite is fine).

## Layout

The app applies the folder of the running era over the mod, and a file at the same path replaces the mod's copy,
so everything era-specific lives in the era folders and only the scripts are shared.

- `npc/box_drop.txt`: the drops. `npc/exchange.txt`: Headgear Exchange. `npc/costume_exchange.txt`: Costume Exchange.
  `npc/ticket_swap.txt`: Ticket Swap. `npc/exchange_quantity.txt`: the "how many" menu of the exchanges and the swap.
  `npc/headgear_costume.txt`: Costume Tailor.
- `<era>/db/item_db.yml`: the boxes, tickets, costume twins (and, in pre-renewal, the costume collection).
  `<era>/System/itemInfo.lua`: their client names and icons.
- `<era>/npc/headgear_box_pool.txt`: the headgear pool per slot. `<era>/npc/htc_table.txt`: the headgear -> costume
  twin table and the headgear costume lists. `<era>/npc/costume_lists.txt`: the costume collection per slot.
  Add or remove ids freely.

## Install

Copy the `random-headgear-box` folder to `%APPDATA%\Ragnarok Offline\state\mods`, or use
Settings -> Mods -> Add mod from folder, then restart the server. Needs app >= 1.4.3.

## Changelog

- **1.4.1**: renewal `itemInfo.lua` now holds only the mod's own items (boxes, tickets, costume twins), so official iRO items keep their real names and icons (issue #1). The renewal Costume Exchange Ticket and costume boxes (72032, 72041-72044) now have client names.
- **1.4.0**: Costume Exchange Ticket drop (new setting), Costume Exchange NPC with one-slot and random costume boxes from a
  costume collection (pre-renewal: costume-collector's costumes under new ids; renewal: the stock costumes), Ticket Swap
  NPC (headgear <-> costume tickets, 1:1 by default, both rates adjustable). Both exchanges and the swap ask how many to buy. Costume ids no longer overwrite stock items.
- **1.3.0**: Headgear Exchange Ticket drop (new setting), the Headgear Exchange NPC with costume boxes, one-slot
  headgear boxes and the Random Headgear Box, and the Costume Tailor from headgear-to-costume bundled. A multi-slot headgear
  becomes one costume per slot, so the "view costume" checkbox hides it. Exchange ticket idea by BlaXun, costume exchange idea by faust.layout.
- **1.2.0**: item descriptions for the 480 renewal headgears the client has no entry for (see above), including skill bonuses and conditions.
- **1.1.1**: fixed the box showing as "Unknown Item" in renewal. The app links one item table per mod and the renewal table replaced the box's, so the renewal table now includes the box.
- **1.1.0**: the 480 renewal headgears the client has no item name for are named by the mod (they showed as "Unknown Item"), so the renewal pool is the full 1,207. They use generic icons.
- **1.0.0**: first release, pre-renewal and renewal. Optional ground drop with autoloot support.

## Credits

- **BlaXun**: the idea of dropping an exchange ticket instead of the box itself.
- **faust.layout**: the idea of the costume exchange (tickets for headgear costume boxes).
- **Thomas** (costume-collector): the costume collection used in pre-renewal, built from the game client's item data.

## License

MIT, see [LICENSE](LICENSE).
