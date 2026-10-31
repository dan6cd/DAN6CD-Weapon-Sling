# DAN6CD Weapon Sling — STOCK Framework & Clothing Edition

**Version: 2.0.0-clean-test — free, source-readable testing release.**

This is a **clean standalone rebuild** based on the earlier editable Weapon Sling design. It is not a decrypted copy of the Cfx Portal asset and **does not replace your original weapon_sling or physical_equipment** project.

## What's included

- A single GTA V **Assault Rifle (`WEAPON_ASSAULTRIFLE`)** carried on front or back.
- Uses the stock in-game **`w_ar_assaultrifle`** rifle prop, built-in male/female freemode characters, and whatever **stock clothing** the player wears. **No streamed YDD/YTD clothing**, custom textures, shop items, menus, or asset packs.
- Server-validated inventory-to-front/back/world transfers, serial verification, MySQL persistence of slung or dropped weapons, ground pickup with **E**, and lightweight client-only props synced to nearby players.
- No ox_lib requirement; **oxmysql** is required for persistence.
- Vanilla player clothing is **not modified by the script**. There is no visual strap/clothing asset in this edition; the weapon is attached to the ped as a prop.

## Stock framework support

| Framework | Inventory | Notes |
|---|---|---|
| Qbox `qbx_core` | `ox_inventory` | Primary supported adapter |
| QBCore `qb-core` | `qb-inventory` | Refuses ambiguous multiple Assault Rifles |
| QBCore `qb-core` | `ox_inventory` | Requires compatible QB/ox integration |
| ESX Legacy `es_extended` | `ox_inventory` | Preferred ESX integration |
| ESX Legacy `es_extended` | Built-in ESX loadout | Best effort; one rifle per weapon type, serial stored separately |

Only one inventory should be active. Other frameworks/inventories are not implemented. **Live FiveM end-to-end testing is still required** for each combination.

## Installation

1. Back up your database, and **stop** the old `weapon_sling`, `weapon_sling_free`, and any equipment script controlling the same weapon. Never run this beside `physical_core` weapon ownership or `physical_equipment` for the same rifle.
2. Extract `dan6cd_weapon_sling/` to `resources/[standalone]/`.
3. Import **`database.sql`** into your server's database. Creates independent `dan6cd_sling_*` tables; no migration from the old build.
4. Set the **framework and inventory to start first**, then `oxmysql`, then the resource (oxmysql itself may start before the framework):

```cfg
ensure oxmysql
ensure qbx_core        # OR qb-core OR es_extended
ensure ox_inventory   # OR qb-inventory; ESX native needs no inventory resource
ensure dan6cd_weapon_sling
```

Remove the lines for resources you do not use. Start `ox_inventory` in your normal framework-approved order. Do not run both ox_inventory and qb-inventory.

5. Leave `Config.Framework` and `Config.Inventory` at `auto` unless your server has special resource names. Confirm the server console prints the detected pair.
6. Equip a serialized stock Assault Rifle; press `J` or use `/sling` to put it on your front; `/backsling` for your back. Use the same command to return the rifle to inventory. Use `/dropgun` while holding a rifle, or `/dropgun front` / `/dropgun back` to place a slung rifle on the ground. Press **E** near a dropped rifle to pick it up.
7. Test weapon ammo, serial, components, inventory-slot return, relog/restart, full inventory refusal, nearby players, ground pickup contention, and both ped models **before publishing on a live server**.

## Vanilla clothing options

`Config.RequireStockClothing=false` by default. This supports standard male and female freemode ped models with their normal GTA clothing; it never spawns an outfit or adds mod clothing.

If you want to require a specific **stock outfit that looks like it has a strap**, choose that outfit on your own stock server, run `/slingclothes` and read its **component:drawable/texture** values. Enter those numbers into `Config.StockClothing` and set `RequireStockClothing=true`. The sample presets included in the config were inherited from the previous configuration and are **NOT guaranteed to be part of every stock server/DLC build**. Changing clothing validation is client-side/cosmetic; server-side inventory transfers remain authenticated.

## Commands

- `J` or `/sling` — store/return the equipped Assault Rifle on the front.
- `/backsling` — store/return from back.
- `/dropgun` — ground-drop equipped Assault Rifle.
- `/dropgun front` / `/dropgun back` — ground-drop a slung rifle.
- `E` near ground rifle — pick up.
- `/slingclothes` — inspect your current stock clothing indices.
- `/slingstatus` — view your persistent storage entries (including pending / returning rows).

## Data integrity and troubleshooting

This resource is **one-authority-at-a-time**: inventory owns the rifle until the server removes its serial; the MySQL row owns it while slung/dropped; restoring the weapon removes the row. Client props are visual-only. It deliberately refuses to create a second copy of a serial that is already in inventory.

**Important non-atomic boundary:** Inventory APIs and SQL are two different systems. Crashes between them can leave a row in `pending` or `returning`. The script **never auto-retries ambiguous transfers**, which would risk duplication. An administrator must inspect the inventory item and `dan6cd_sling_items` row by serial before repairing it. See `TROUBLESHOOTING.md`.

**No automatic migration:** Do not import the old `weapon_sling_items`, `weapon_sling_transforms` or `physical_core` data. Return weapons with the prior script and remove it before using this edition. Any migration needs a verified one-to-one serial audit.

**No custom sling animation/editor:** The original large editor, stream assets, debugging commands, duplicate hooks and clothing YDD/YTD models are intentionally excluded. Standard weapon draw/equip follows the stock inventory system. This release focuses on essential, stable functionality.

**Not live certified:** The code has been statically checked, but no full server with Qbox, QBCore or ESX is available in this environment. Publish as a test release until each supported path is verified.
