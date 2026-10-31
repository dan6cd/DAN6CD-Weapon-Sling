# DAN6CD-Weapon-Sling
DAN6CD Weapon Sling is a FREE FiveM script for Qbox, QBCore, and ESX. Features realistic front and back rifle slings, physical weapon drops, MySQL persistence, and inventory compatibility. Includes installation instructions and framework adapters. Free development release for FiveM roleplay servers.
# DAN6CD Weapon Sling — FREE Multi-Framework Edition (v1.0.0)

This is a separate distribution of the uploaded `weapon_sling` v0.3.0. Your original ZIP has **not** been changed. It is **not** a replacement for the ongoing `physical_equipment`/`physical_player` project.

## Supported stock combinations

| Framework | Inventory | Adapter | Notes |
|---|---|---|---|
| Qbox (`qbx_core`) | `ox_inventory` | `qbox`/`ox` | Normal Qbox stack |
| QBCore (`qb-core`) | `qb-inventory` | `qbcore`/`qb` | Standard QB items (`weapon_assaultrifle`, `info.serie`) |
| QBCore | `ox_inventory` | `qbcore`/`ox` | Only where a supported ox/QB integration is installed |
| ESX Legacy (`es_extended`) | Native ESX weapon loadout | `esx`/`esx_native` | One of each weapon type; ESX native slots are virtual |
| ESX Legacy | `ox_inventory` | `esx`/`ox` | Serialized inventory recommended for accuracy |

Other inventories (qs-, lj-, ps-, codem-) are **not** supported. Do not start multiple inventory resources at once. This version is for **one Assault Rifle model (`WEAPON_ASSAULTRIFLE`)**. It is not a universal holster system.

## Requirements

- FiveM current artifact + OneSync
- `ox_lib` (client lib and notifications), `oxmysql` (SQL)
- Exactly one framework and a compatible inventory
- A female/male stock freemode ped with the configured sling clothing (see `config.lua`)
- MySQL server with permissions to create tables (or import `database.sql` manually)

## Install

1. BACK UP the database and original resources. Disable any older `weapon_sling`/`physical_equipment` competing for `/sling` or `/backsling`.
2. Place the folder **`weapon_sling_free`** in `resources/[standalone]/`.
3. Import `weapon_sling_free/database.sql` via your database administration tool.
4. Verify your inventory and framework start before the sling. Example configs:

**Qbox**
```cfg
ensure oxmysql
ensure ox_lib
ensure qbx_core
ensure ox_inventory
ensure weapon_sling_free
```
**QBCore stock**
```cfg
ensure oxmysql
ensure ox_lib
ensure qb-core
ensure qb-inventory
ensure weapon_sling_free
```
**ESX Legacy native**
```cfg
ensure oxmysql
ensure ox_lib
ensure es_extended
ensure weapon_sling_free
```
**ESX + ox_inventory**
```cfg
ensure oxmysql
ensure ox_lib
ensure es_extended
ensure ox_inventory
ensure weapon_sling_free
```
5. In `config.lua`, leave `Config.Framework='auto'` and `Config.Inventory='auto'`, or manually set both values if you have a complex server.
6. Verify the server console prints the detected framework/inventory. Equip an **Assault Rifle** and a matching front sling shirt; press `J` or `/sling`. Use `/backsling` for back slot, `/dropgun` for placement/pickup and `/slingdebug` to inspect serials.
7. Check logout/relog, restart, picking a dropped weapon up, swapping and multiple players. Test with weapons containing ammo and attachments.

## Compatibility differences / precautions

- **Stock QBCore** uses lower-case item names and `info.serie` instead of Ox's upper-case and `metadata.serial`. The adapter normalizes internally without changing stored item names. Serial and metadata are verified by the server on every transfer.
- **QBCore with two Assault Rifles in inventory:** The standard native weapon selection API does not reliably say which identical inventory slot is currently held, so this edition *refuses the ambiguous transfer*. Unequip or store the other rifle first. This avoids moving the wrong serialized weapon.
- **ESX native:** ESX only supports one weapon of each type in its native loadout, not multiple uniquely slotted copies. The adapter uses a persistent metadata sidecar for the one weapon's serial, ammo, tint and components. This is a **best-effort native compatibility path**, not byte-for-byte equivalent to Ox's unique inventory slots. Use ESX + ox_inventory for strongest weapon-identity semantics. Test attachment names: ESX uses framework-specific component names.
- Ground pickup uses server-authoritative `weapon_sling_items` rows, not client item creation. Config requires a serial, and transactions use source locks and serial locks.
- **Database separation:** This free resource owns `weapon_sling_items` / `weapon_sling_transforms` so it does not overwrite `physical_core`'s `physical_items`. Never run both resources to manage the *same* weapon at once.
- **Original data not automatically migrated.** `MIGRATION_OPTIONAL.sql` is an illustrative commented template. Audit duplicates before importing old rows.
- Only weapons configured in `Config.Weapons` have sling prop transforms. The included stream clothing is the uploaded original and must be kept with its original author/license permissions.

## Useful commands

- `J` / `/sling` — front sling equip/unequip/swap
- `/backsling` — back sling
- `/dropgun` — place equipped rifle in the world
- `/slingcheck` — check clothing
- `/slingdebug` — inspect weapon serial ownership (best while testing)

## Testing and free distribution

This release has been **statically adapted** and includes a smoke-test script. It has **not been run against a live Qbox/QBCore/ESX server here**. Test first on a development server and keep backups. In particular check qb-inventory's `useItem` event against your installed version and ESX native component restoration. Do not market it as production-proven without passing the integration tests.

## License / credit

You supplied the base weapon_sling v0.3.0 resource. Preserve attribution to its owner. Only share the custom streamed clothing if you have rights to redistribute those assets. This package is offered free of charge; that does not override any third-party asset licenses.

