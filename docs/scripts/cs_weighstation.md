# ⚖️ cs_weighstation Documentation

`cs_weighstation` is a configurable vehicle weight station system for FiveM.
Players or job restricted staff can weigh vehicles to check cargo load — with a clean UI showing items, weights, and load limits.

---

# 📦 Installation

1. Place `cs_weighstation` inside your `resources` folder
2. Add to your `server.cfg`:

   ```cfg
   ensure cs_weighstation
   ```

3. Configure `config.lua` to match your server setup

---

# ⚙️ Configuration Guide

---

## 🔍 Version Check

```lua
Config.VersionCheck = true
```

| Option  | Description                                   |
| ------- | --------------------------------------------- |
| `true`  | Console will notify if the script is outdated |
| `false` | Disable version checking                      |

---

## 🌐 General

```lua
Config.Locale = 'en'
Config.Debug = false
Config.ShowItems = true
Config.Framework = 'auto'
Config.InventorySystem = 'auto'
Config.Target = 'auto'
```

| Option            | Description                                                        |
| ----------------- | ------------------------------------------------------------------ |
| `Locale`          | Language: `en`, `nl`, `de`                                         |
| `Debug`           | Show zone debug boxes in-game                                      |
| `ShowItems`       | Show individual items in the UI (false = only show total weight)   |
| `Framework`       | `auto`, `esx`, `qbcore`, or `qbox`                                 |
| `InventorySystem` | `auto`, `ox_inventory`, or `qb-inventory`                          |
| `Target`          | `auto`, `ox_target`, or `qb-target`                                |

---

## 📍 Default Blip

```lua
Config.DefaultBlip = {
    sprite = 50,
    color = 5,
    scale = 0.8,
}
```

Applies to all weight stations on the map. Adjust sprite/color using the [FiveM blip reference](https://docs.fivem.net/docs/game-references/blips/).

---

## ⚖️ Load Limits

```lua
Config.UseLoadPercentage = true
Config.LoadPercentage = 0.30
```

| Option               | Description                                                        |
| -------------------- | ------------------------------------------------------------------ |
| `UseLoadPercentage`  | `true` = limit based on % of vehicle weight, `false` = use class limits |
| `LoadPercentage`     | Fraction of vehicle weight allowed as cargo (`0.30` = 30%)         |

When `UseLoadPercentage = false`, limits are set per vehicle class in `Config.VehicleLoadLimits`.

### Vehicle Class Limits (kg)

Only used when `UseLoadPercentage = false`:

| Class | Type         | Limit  |
| ----- | ------------ | ------ |
| 0     | Compacts     | 500    |
| 1     | Sedans       | 600    |
| 2     | SUVs         | 800    |
| 8     | Motorcycles  | 200    |
| 10    | Industrial   | 2000   |
| 12    | Vans         | 2500   |
| 16    | Planes       | 20000  |
| 20    | Commercial   | 2500   |
| ...   | (see config) | ...    |

```lua
Config.DefaultLoadLimit = 500 -- Fallback if vehicle class is not listed
```

---

## 🚦 Zone Cones

```lua
Config.ShowZoneCones = true
```

Spawns orange traffic cones at the corners of each weighing zone so drivers know exactly where to stop.

---

## 🏗️ Weight Stations

Defined in `Config.WeightStations`. Each station has weighing zones and interaction zones.

```lua
{
    name = "Weight Station 1",
    weighingZones = {
        {
            coords = vector4(x, y, z, rotation),
            size = vector3(width, length, height)
        },
    },
    interactionZones = {
        {
            coords = vector4(x, y, z, rotation),
            size = vector3(width, length, height)
        },
    },
    allowedJobs = {"police", "mechanic"} -- Leave empty for all jobs
}
```

| Field              | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `name`             | Station label shown in-game                              |
| `weighingZones`    | Box zones where a vehicle must be parked to be weighed   |
| `interactionZones` | Clickable target zones (e.g. kiosk location)             |
| `allowedJobs`      | Job whitelist — leave empty `{}` to allow everyone       |

You can add **multiple weighing zones** and **multiple interaction zones** per station.

---

# 🖥️ Usage

1. Drive a vehicle onto a **weighing zone**
2. Walk to an **interaction zone**
3. Interact using the target system
4. The UI shows vehicle weight, cargo items, and load status
5. Press `ESC` to close

---

# 🌍 Localization

Translation files are in the `locales/` folder:

| File      | Language |
| --------- | -------- |
| `en.json` | English  |
| `nl.json` | Dutch    |
| `de.json` | German   |

Edit these files to customize all labels, notifications, and UI text.

---

# 📖 Feature Overview

✔ Vehicle Weight Checking
✔ Per-Station Job Restrictions
✔ Percentage or Class-Based Load Limits
✔ Item List in UI (toggleable)
✔ Traffic Cone Zone Markers
✔ Multi-Framework Support (ESX, QBCore, QBox)
✔ Auto-Detection for Framework, Inventory & Target
✔ Multiple Weighing & Interaction Zones per Station

---

# 🛠️ Support

If you encounter issues:
1. Set `Config.Debug = true` to visualize zones
2. Check F8 console for errors
3. Make sure your framework starts before `cs_weighstation`
4. Join our Discord: https://discord.gg/qrAdgGDnvB
