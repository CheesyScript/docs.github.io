# 📅 cs_daily Documentation

`cs_daily` is a fully configurable daily & weekly quest system for FiveM.
Players complete quests, earn rewards, and maintain login streaks — with VIP support, leaderboards, and an in-game admin menu.

---

# 📦 Installation

1. Place `cs_daily` inside your `resources` folder
2. Import `installation/query.sql` into your database
3. Add to your `server.cfg`:

   ```cfg
   ensure ox_lib
   ensure oxmysql
   ensure cs_daily
   ```

   > Make sure `ox_lib` and `oxmysql` start **before** `cs_daily`.

4. Configure `shared/config.lua` to match your server setup

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
Config.General = {
    ServerName = "My Server",
    Locale = "en",
    ResetTime = 0,
    MinimumHoursBetweenClaims = 20,
    StreakGracePeriodHours = 4,
    DailyQuestCount = 3,
    EnableWeeklyQuests = true,
    WeeklyQuestCount = 2,
    InteractionType = "auto",
    EnableWeekendBonus = true,
    WeekendMultiplier = 1.5,
    UpdateInterval = 5000,
}
```

| Option                      | Description                                                   |
| --------------------------- | ------------------------------------------------------------- |
| `ServerName`                | Displayed in the UI header                                    |
| `Locale`                    | Language: `en`, `nl`, `de`                                    |
| `ResetTime`                 | Hour of day quests reset (0–23, `0` = midnight)               |
| `MinimumHoursBetweenClaims` | Prevents players from gaming the reset                        |
| `StreakGracePeriodHours`    | Hours after reset where streak is still maintained            |
| `DailyQuestCount`           | How many daily quests each player gets (1–5 recommended)      |
| `EnableWeeklyQuests`        | Toggle the weekly quest system                                |
| `WeeklyQuestCount`          | Number of weekly quests per player (1–3 recommended)          |
| `InteractionType`           | `auto`, `ox_target`, `qb-target`, or `zones`                  |
| `EnableWeekendBonus`        | Apply a reward multiplier on Saturday & Sunday                |
| `WeekendMultiplier`         | Multiplier applied on weekends (`1.5` = 50% bonus)            |
| `UpdateInterval`            | How often quest progress updates in ms (default: `5000`)      |

---

## 🎨 Branding

```lua
Config.Branding = {
    Colors = {
        primary = "#FFC107",
        ...
    },
    Logo = "open/logo.svg",
    FontFamily = "Chakra Petch",
}
```

| Option       | Description                                                       |
| ------------ | ----------------------------------------------------------------- |
| `Colors`     | UI color palette (primary, text, accent, danger, success, etc.)   |
| `Logo`       | Path to your logo — supports `.svg`, `.png`, `.jpg`               |
| `FontFamily` | `Chakra Petch`, `JetBrains Mono`, or `Syne`                       |

---

## 🔥 Streak System

```lua
Config.Streak = {
    Protection = {
        Enabled = true,
        AutoUseFreeze = true,
        FreeFreezesPerMonth = 2,
        MaxFreezes = 5,
        PurchasableFreeze = true,
        FreezeCost = {money = 25000, moneyType = "bank"},
    },
}
```

| Option                | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| `Enabled`             | Enable streak freeze protection                                |
| `AutoUseFreeze`       | Auto-use a freeze when a player misses a day                   |
| `FreeFreezesPerMonth` | Number of free freezes given per month                         |
| `MaxFreezes`          | Maximum freezes a player can hold                              |
| `PurchasableFreeze`   | Allow players to buy freezes                                   |
| `FreezeCost`          | Cost to buy a freeze (`bank`, `cash`, or `money`)              |

### Streak Multipliers

Defined in `open/quests.lua`:

| Streak | Multiplier | Badge |
| ------ | ---------- | ----- |
| 3 days | ×1.1       | 🔥    |
| 7 days | ×1.25      | 🔥🔥  |
| 14 days| ×1.5       | 🔥🔥🔥|
| 30 days| ×2.0       | ⭐    |
| 60 days| ×2.5       | ⭐⭐  |
| 100 days| ×3.0      | 💎    |
| 365 days| ×5.0      | 👑    |

### Streak Milestones

One-time rewards at milestone streaks (7, 30, 60, 100, 365 days). Defined in `open/quests.lua`.

---

## 💎 VIP System

```lua
Config.VIP = {
    Enabled = false,
    DetectionMethod = "custom",
    Tiers = {
        standard = {multiplier = 1.0},
        vip      = {multiplier = 1.5},
        vipplus  = {multiplier = 2.0},
    },
}
```

| Option            | Description                                              |
| ----------------- | -------------------------------------------------------- |
| `Enabled`         | Toggle the VIP reward multiplier system                  |
| `DetectionMethod` | `ace` (ACE permissions) or `custom` (via `open/custom.lua`) |
| `Tiers`           | Define multipliers per VIP tier                          |

Custom VIP detection is handled in `open/custom.lua` → `Custom.GetVIPTier`.

---

## 🏆 Leaderboard

```lua
Config.Leaderboard = {
    Enabled = true,
    ShowTop = 25,
    RefreshInterval = 300000,
    Categories = {
        {id = "current", label = "Current Streak"},
        {id = "longest", label = "Longest Streak"},
        {id = "claims",  label = "Total Claims"},
    },
}
```

| Option            | Description                                 |
| ----------------- | ------------------------------------------- |
| `Enabled`         | Show the leaderboard tab in the UI          |
| `ShowTop`         | Number of players shown                     |
| `RefreshInterval` | How often the leaderboard refreshes (ms)    |
| `Categories`      | Leaderboard tabs/categories                 |

---

## 🛠️ Admin

```lua
Config.Admin = {
    EnableAdminCommands = true,
    DevMode = false,
}
```

Grant admin access in `server.cfg`:

```cfg
add_ace group.admin cs_daily.admin allow
add_principal identifier.fivem:YOUR_ID group.admin
```

In-game command: `/dailyadmin`

**Admin menu options:**
- View Player Stats
- Set Player Streak
- Give Streak Freezes
- Reset Today's Quests
- Wipe All Player Data

---

# 📋 Quest Configuration

All quests are defined in `open/quests.lua`.

## Quest Types

| Type       | Description                                        |
| ---------- | -------------------------------------------------- |
| `instant`  | Claim immediately — no action required             |
| `time`     | Stay online for X seconds                          |
| `location` | Travel to a specific location                      |
| `activity` | Drive or walk a set distance                       |
| `task`     | Perform an animation at a location                 |
| `collect`  | Collect props from spawn locations on the map      |

## Difficulty Pools

Quests are split into `easy`, `medium`, and `hard` pools, each with a `weight` that controls how often they appear.

```lua
Config.DailyQuestPools = {
    easy   = {weight = 50, quests = { ... }},
    medium = {weight = 30, quests = { ... }},
    hard   = {weight = 20, quests = { ... }},
}
```

Weekly quests use the same format under `Config.WeeklyQuestPools`.

## Adding a Quest

```lua
{
    id = "my_quest",
    type = "task",
    title = "My Custom Quest",
    description = "Do something cool",
    icon = "⭐",
    difficulty = "medium",
    preset = "dance",
    location = vector3(0.0, 0.0, 0.0),
    radius = 5.0,
    duration = 30,
    rewards = {
        money = 3000,
        items = {
            {name = "lockpick", amount = 2},
        }
    },
}
```

## Task Presets

Predefined animations for `task` quests. Defined in `open/quests.lua`.

| Preset     | Description           |
| ---------- | --------------------- |
| `dance`    | Dance animation       |
| `clean`    | Broom cleaning        |
| `mow`      | Lawn mower animation  |
| `exercise` | Push-ups              |
| `repair`   | Wrench repair         |
| `garden`   | Garden spade          |

---

# 🔧 Customization Hooks

Defined in `open/custom.lua`. These are called automatically by the script.

| Hook                    | When it fires                            |
| ----------------------- | ---------------------------------------- |
| `Custom.GetVIPTier`     | On player connect — return VIP tier      |
| `Custom.OnQuestComplete`| When a player completes a quest          |
| `Custom.OnDailyClaim`   | When a player claims their daily reward  |
| `Custom.OnMilestoneReached` | When a streak milestone is hit       |
| `Custom.OnStreakLost`   | When a player loses their streak         |
| `Custom.ModifyRewards`  | Modify rewards before they are given     |
| `Custom.GiveExtraRewards`| Give extra rewards after default ones   |

### Discord Logging

```lua
Custom.Discord = {
    Enabled = true,
    WebhookURL = "https://discord.com/api/webhooks/...",
    BotName = "CheesyScripts",
}
```

---

# 💬 Commands

| Command       | Description                                 |
| ------------- | ------------------------------------------- |
| `/daily`      | Open the daily quests & rewards menu        |
| `/dailyadmin` | Open the admin menu (requires permission)   |

---

# 📖 Feature Overview

✔ Daily & Weekly Quest System
✔ Login Streak with Multipliers & Milestones
✔ Streak Freeze Protection
✔ VIP Reward Multipliers
✔ Weekend Bonus Rewards
✔ Leaderboard
✔ Discord Logging
✔ In-Game Admin Menu
✔ Multi-Framework Support (ESX, QBCore, QBox)
✔ Fully Customizable Quests & Hooks

---

# 🛠️ Support

If you encounter issues:
1. Check F8 console for errors
2. Verify `ox_lib` and `oxmysql` start before `cs_daily`
3. Confirm `installation/query.sql` was imported
4. Check item names in `open/quests.lua` match your inventory system
5. Join our Discord: https://discord.gg/qrAdgGDnvB
