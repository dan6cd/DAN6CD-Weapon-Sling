# DAN6CD WEAPON SLING
### FREE EDITION | Multi-Framework FiveM Resource

**Realistic Weapon Carrying • Live Attachment Editor • Outfit-Based Presets • Physical Weapon Drops**

Take weapon realism to the next level with **DAN6CD Weapon Sling**, a free weapon-carrying system designed for FiveM roleplay servers.

Instead of making rifles disappear when unequipped, this resource lets players visibly carry supported weapons across their chest or back, interact with physical weapon drops, and customize weapon positions to match their character's clothing.

Built with support for **Qbox, QBCore, and ESX Legacy**, using GTA V's original weapon models and freemode clothing.

---

## KEY FEATURES

### 🔫 1. Realistic Front & Back Weapon Sling

- Visibly carry a supported rifle across the chest or back.
- Switch between front and back sling positions.
- Attach weapons directly to the character's skeleton.
- Weapons follow player movement and character animations.
- Independent front and back attachment configurations.
- Weapon props remain visible to nearby players.

**Controls:**
- `J` — Front Sling
- `K` — Back Sling
- `/sling` — Toggle Front Sling
- `/backsling` — Toggle Back Sling

### 🛠️ 2. Live 3D Weapon Attachment Editor

Customize rifle placement directly in-game without manually editing configuration files.

**Editor Features:**
- Real-time weapon positioning.
- Six-axis position and rotation adjustments.
- Move weapons left, right, up, down, forward, and backward.
- Rotate across X, Y, and Z axes.
- Fast and precise adjustment controls.
- Preview the weapon on the character before saving.
- Separate front and back sling calibration.
- Reset to default positioning.
- Save custom attachment offsets.

**Commands:**
- `/slingedit front`
- `/slingedit back`

**Editor Controls:**

| Key | Function |
|---|---|
| Left / Right Arrows | Move weapon left / right |
| Up / Down Arrows | Move weapon up / down |
| Page Up / Page Down | Move weapon forward / backward |
| Tap Left Shift | Switch rotation axis Z → Y → X |
| Q / E | Rotate selected axis |
| Hold Left Shift | Faster adjustments |
| Enter | Save calibration |
| Backspace | Cancel editing |
| Delete | Preview default position |

### 👕 3. Stock GTA V Clothing Compatibility

Designed to work with standard FiveM freemode clothing without requiring additional custom clothing downloads.

- Supports male and female freemode characters.
- Uses existing GTA V clothing and character components.
- No custom `.ydd` or `.ytd` clothing streams required.
- Compatible with different jackets, hoodies, shirts, and tactical outfits.
- Adjust rifle placement to minimize clipping with clothing.
- Front and back attachments can be customized independently.

**No additional weapon or clothing models are required for the initial Assault Rifle release.**

### 💾 4. Outfit-Based Weapon Position Presets

Different clothing combinations may require different weapon positions.

The attachment editor includes an outfit-based calibration system designed to save and load custom positions automatically.

- Store custom weapon offsets in MySQL.
- Save presets for different clothing combinations.
- Maintain separate front and back positions.
- Load saved presets when using the same outfit again.
- Restore saved positioning after returning a rifle to inventory and re-slinging it.
- Synchronize attachment configurations for nearby players.
- Fall back to default settings when an outfit has no saved preset.

### 📦 5. Physical Weapon Drop & Pickup

Weapons can exist as visible props in the game world instead of disappearing immediately.

- Drop supported weapons onto the ground.
- Pick up dropped weapons with the interaction key.
- Ground placement designed to prevent floating weapons.
- Persistent server-side weapon records.
- Preserve supported weapon metadata during transfers.

**Controls:**
- `/dropgun` — Drop the equipped rifle.
- `/dropgun front` — Drop the front-slung rifle.
- `/dropgun back` — Drop the back-slung rifle.
- `E` — Pick up a nearby dropped weapon.

### 🔐 6. Server-Side Weapon Management

Weapon transfers are processed through server-side checks to help maintain consistent ownership and reduce duplication risks.

- MySQL-backed weapon persistence.
- Inventory integration.
- Weapon serial and metadata handling.
- Validation during sling, inventory, drop, and pickup transfers.
- Server-side control over weapon location changes.

### 🌐 7. Multi-Framework Compatibility

Designed with adapters for popular FiveM frameworks.

| Framework | Inventory |
|---|---|
| Qbox | ox_inventory |
| QBCore | qb-inventory |
| QBCore | ox_inventory |
| ESX Legacy | Native weapon loadout |
| ESX Legacy | ox_inventory |

Framework-specific behavior depends on the installed framework and inventory versions.

### ⚙️ 8. Lightweight & Configurable

- Lua-based resource.
- Uses built-in GTA V weapon assets.
- Configurable keybindings.
- Front and back attachment offsets.
- Database-backed calibration profiles.
- No custom clothing streaming dependency.
- Separate, modular implementation suitable for stock framework servers.

---

## CURRENT WEAPON SUPPORT

**Initial Supported Weapon:**
- Assault Rifle — `WEAPON_ASSAULTRIFLE`

Additional weapon types and attachment profiles may be introduced in future releases.

## DEVELOPMENT STATUS

**Version:** 2.1.2 — Free Testing Edition

The resource has undergone Lua syntax checks and simulated framework, inventory, database, and editor tests.

Full compatibility, attachment appearance, synchronization, and persistence still require verification on live FiveM servers. Features may require additional adjustments during testing.

## REQUIREMENTS

- FiveM server with OneSync
- Qbox, QBCore, or ESX Legacy
- Compatible inventory system
- oxmysql
- Supported GTA V freemode character

Refer to the included installation guide for any additional dependencies.

---

**PRICE: FREE — $0.00**

**DEVELOPED BY DAN6CD**

Created for the FiveM development and roleplay community.

*Independent FiveM modification. Not affiliated with Rockstar Games, Cfx.re, or the framework developers.*
