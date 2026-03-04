# 🚗 cs_carlock Documentation

`cs_carlock` is a fully configurable vehicle key and locking system for FiveM.
It provides vehicle locking, key sharing, lockpicking, tracking, and admin tools with support for multiple frameworks.

---

# 📦 Installation

1. Place `cs_carlock` inside your `resources` folder
2. Add to your `server.cfg`:

   ```cfg
   ensure cs_carlock
   ```
3. Configure the `Config` file to match your server setup

---

# ⚙️ Configuration Guide

Below is a full explanation of the provided configuration file.

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

## 🚘 Plate Whitelist

```lua
Config.plateWhiteList = {
    "lily",
    "police",
    "admin"
}
```

Vehicles with these plates:

* Do **NOT** require keys
* Can always be accessed

---

## 🔑 Engine Behavior

```lua
Config.canLeaveEngineRunning = true
Config.canDriveIfEngineRunning = true
```

### `canLeaveEngineRunning`

* `true` → Short press exit = engine off
* Long press exit = engine stays on

### `canDriveIfEngineRunning`

* `true` → Anyone can drive away if engine is running
* `false` → Keys are always required

---

# 🔐 Key Sharing System

```lua
Config.enableKeySharing = true
Config.onlyVehicleOwnerCanShare = true
```

| Option                     | Description                                       |
| -------------------------- | ------------------------------------------------- |
| `enableKeySharing`         | Enables the key sharing system                    |
| `onlyVehicleOwnerCanShare` | Only first key receiver (vehicle owner) can share |

---

# 💬 Commands Configuration

```lua
Config.Commands = { ... }
```

---

## 🚗 Lock / Unlock Command

```lua
unlockVehicle = {
    command = "lockvehicle",
    keyMapping = "u",
    keyMappingDesc = "Use vehicle keys",
    chatSuggestion = "Use vehicle keys"
}
```

| Setting          | Description                 |
| ---------------- | --------------------------- |
| `command`        | Chat command                |
| `keyMapping`     | Default keybind             |
| `keyMappingDesc` | Description in keybind menu |
| `chatSuggestion` | Chat suggestion text        |

Set to `nil` to disable keymapping or chat suggestion.

---

## 🗝️ View Keys Command

```lua
viewKeys = {
    command = "keys",
    keyMapping = nil,
    chatSuggestion = nil
}
```

Command to open the keys menu.

---

## 🛠️ Admin Key Command

```lua
adminGetKey = {
    command = "getkey",
    perms = { ... }
}
```

Allows admins to obtain vehicle keys.

Usage:

```
/getkey
/getkey ABC123
```

---

### 🔐 Permission Framework

```lua
permsFramework = "aceperms"
```

Supported frameworks:

* `esx`
* `qbcore`
* `vrp`
* `aceperms`
* `identifiers`

Each framework has its own permission list:

```lua
['esx'] = {'superadmin', 'admin', 'mod'}
```

---

# 🔓 Lockpicking System

```lua
Config.lockpicking = { ... }
```

---

## Enable / Disable

```lua
isEnabled = true
```

Enables lockpicking for vehicles requiring keys.

---

## Ignore Vehicle Classes

```lua
ignoreVehicleClass = {
    18, -- Emergency
    19, -- Military
    21  -- Trains
}
```

Vehicle classes reference:
[https://wiki.rage.mp/wiki/Vehicle_Classes](https://wiki.rage.mp/wiki/Vehicle_Classes)

These classes cannot be lockpicked.

---

## Required Item

```lua
item = "lockpick"
itemLostOnFail = true
```

* `item` → Required inventory item
* `itemLostOnFail` → Removes item on failed attempt

---

## Minigame Options

```lua
minigame = "default"
```

Available types:

| Type          | Description                            |
| ------------- | -------------------------------------- |
| `default`     | Built-in Fallout/Skyrim style minigame |
| `skill-check` | ox_lib skillcheck                      |
| `none`        | 7 second progressbar                   |

---

## Car Alarm

```lua
carAlarmOnFail = true
carAlarmDuration = 30
```

If lockpicking fails:

* Alarm triggers
* Audio bank configurable
* Duration must be a number (seconds)

---

## 📡 Vehicle Tracker System

```lua
tracker = {
    enabled = true,
    options = {
        trackerItem = "gpstracker",
        ownedVehicleTable = "owned_vehicles",
        trackerDuration = 300,
    }
}
```

### Features

* Install GPS tracker on vehicles
* Requires `trackerItem`
* Only works on owned vehicles
* Tracking lasts `trackerDuration` seconds

---

# 🌍 Localization

You can fully modify notification and UI text:

```lua
Config.Locales = {
    plate = "plate",
    vehicleLocked = "Vehicle Locked",
    vehicleUnlocked = "Vehicle unlocked",
    ...
}
```

All displayed text can be customized here.

---

# 📖 Feature Overview

✔ Vehicle Lock / Unlock
✔ Key Ownership System
✔ Key Sharing
✔ Admin Key Command
✔ Lockpicking with Minigame
✔ Car Alarm System
✔ Vehicle GPS Tracker
✔ Multi-Framework Permission Support

---

# 🧩 Example Use Cases

* Police vehicles protected from lockpicking
* Admins able to recover keys
* Criminal RP with tracker & alarm system
* Shared company vehicles
* Public vehicles without keys

---

# 🛠️ Support

If you encounter issues:
1. Enable `Config.VersionCheck`
2. Check console logs
3. Verify permission framework
4. Ensure required items exist in your inventory system
---
