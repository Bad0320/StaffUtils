# Staff Utils Wiki

**Staff Utils** is a moderation and staff-management plugin by **Bad_0320**.

This README is the official wiki for the plugin.

---

## 1. Overview

Staff Utils provides a complete set of everyday moderation tools:

- Staff Mode
- Advanced Vanish
- InvSee
- EnderSee
- Random Teleport
- GodMode
- Fly
- Gamemode shortcuts
- CPS checks
- Reports
- Staff Chat
- SocialSpy
- Staff action logs

The modern `26.x` edition also supports MariaDB, Redis synchronization, SQLite fallback, Paper and Folia.

---

# 2. Staff Mode

## Command

```text
/staffmode
/staffmode on
/staffmode off
/staffmode toggle
```

Aliases:

```text
/staff
/modmode
```

Permission:

```text
staffutils.staffmode
```

## Behaviour

When Staff Mode is enabled, Staff Utils:

1. saves the player's normal inventory;
2. saves armor, offhand and relevant inventory state;
3. clears the normal inventory;
4. gives the Staff Mode hotbar;
5. enables configured flight;
6. applies saturation;
7. optionally enables Vanish.

When Staff Mode is disabled, the original player inventory/state is restored.

Staff tools are protected so they cannot be freely moved, dropped or used as normal vanilla items.

---

# 3. Staff Mode Hotbar

Default layout:

```text
Slot 0  InvSee
Slot 1  EnderSee
Slot 2  Random TP
Slot 3  Empty
Slot 4  Vanish
Slot 5  Empty
Slot 6  GodMode
Slot 7  Staff Chat
Slot 8  Reports
```

Pattern:

```text
[item] [item] [item] [empty] [item] [empty] [item] [item] [item]
```

Every item has one purpose.

## InvSee

Right-click a player to inspect their inventory.

The visual item resembles a Spyglass, but the actual base material is non-interactive so the vanilla zoom animation does not start.

## EnderSee

Right-click a player to inspect their Ender Chest.

## Random TP

Right-click to teleport to a random eligible online player.

Players with:

```text
staffutils.randomtp.exempt
```

are ignored by the random selector.

## Vanish

Default visual state:

```text
GRAY_DYE = OFF
LIME_DYE = ON
```

## GodMode

Right-click to toggle GodMode.

## Staff Chat

Right-click to toggle Staff Chat.

## Reports

Right-click to access report functionality.

---

# 4. Vanish

## Command

```text
/vanish
/vanish on
/vanish off
/vanish toggle
/vanish <state> <player>
```

Alias:

```text
/v
```

Permissions:

```text
staffutils.vanish
staffutils.vanish.others
staffutils.vanish.see
```

## Features

When enabled, Vanish can:

- hide the staff member from normal players;
- allow authorized staff to see vanished players;
- prevent item pickup;
- prevent physical player collision;
- prevent the vanished staff member from attacking players;
- silence join/leave behaviour while vanished.

Relevant configuration:

```yaml
vanish:
  prevent-pickup: true
  prevent-player-collision: true
  prevent-attacking-players: true
  silent-join-leave-while-vanished: true
```

---

# 5. InvSee

## Command

```text
/invsee <player>
```

Permission:

```text
staffutils.invsee
```

InvSee opens a controlled view of another player's inventory.

Outside Staff Mode, inspection is read-only.

Inside Staff Mode, supported builds allow staff workflows involving temporary inspected items. These actions are tracked by the plugin.

Temporary moderation items:

- can be moved where allowed;
- cannot be used normally;
- disappear when discarded;
- are cleaned up on Staff Mode disable/quit when required;
- are protected against common duplication paths.

---

# 6. EnderSee

## Command

```text
/ecsee <player>
```

Aliases:

```text
/endersee
/echestsee
```

Permission:

```text
staffutils.enderchest
```

Opens a controlled view of a player's Ender Chest.

The same Staff Mode safety rules used by inventory inspection apply where supported.

---

# 7. Random Teleport

The Staff Mode Random TP tool teleports staff to a random eligible online player.

Permission:

```text
staffutils.randomtp
```

Exemption permission:

```text
staffutils.randomtp.exempt
```

On modern Paper/Folia builds, teleport work is scheduled using the appropriate safe scheduler/async teleport path.

---

# 8. GodMode

## Commands

```text
/godmode
/godmode on
/godmode off
/godmode toggle
/godmode <state> <player>
```

Alias:

```text
/god
```

Permissions:

```text
staffutils.god
staffutils.god.others
```

GodMode prevents configured damage while active.

The Staff Mode hotbar also provides a dedicated GodMode toggle.

---

# 9. Flight

## Commands

```text
/fly
/fly on
/fly off
/fly toggle
/fly <state> <player>
```

Permissions:

```text
staffutils.fly
staffutils.fly.others
```

Staff Utils keeps `/fly` state consistent across supported gamemode changes.

---

# 10. Gamemode Shortcuts

```text
/gmc [player]
/gms [player]
/gmsp [player]
/gma [player]
```

Permissions:

```text
staffutils.gamemode.creative
staffutils.gamemode.survival
staffutils.gamemode.spectator
staffutils.gamemode.adventure
staffutils.gamemode.others
```

Mappings:

```text
/gmc  -> CREATIVE
/gms  -> SURVIVAL
/gmsp -> SPECTATOR
/gma  -> ADVENTURE
```

---

# 11. CPS Check

## Command

```text
/cpscheck <player> [seconds]
```

Alias:

```text
/cps
```

Permission:

```text
staffutils.cps
```

Default configuration:

```yaml
cps:
  sample-seconds: 10
  alert-threshold: 18
```

The result reports CPS data including peak activity. Staff Utils can display an alert when the configured threshold is exceeded.

---

# 12. Reports

## Player command

```text
/report <player> <reason>
```

Permission:

```text
staffutils.report
```

## Staff commands

```text
/reports list
/reports view <id>
/reports close <id>
```

Permissions:

```text
staffutils.report.notify
staffutils.report.manage
```

Configuration:

```yaml
reports:
  max-reason-length: 140
  cooldown-seconds: 30
```

Staff with the notification permission receive new-report notifications.

---

# 13. Staff Chat

## Command

```text
/staffchat
```

Alias:

```text
/sc
```

Permission:

```text
staffutils.staffchat
```

Staff Chat can be toggled on/off.

The Staff Mode hotbar includes a dedicated Staff Chat item.

On the modern multi-server edition, messages can be synchronized with Redis.

---

# 14. SocialSpy

## Commands

Enable global Spy:

```text
/spy
```

Monitor only one player:

```text
/spy <player>
```

Disable Spy:

```text
/spy
```

Alias:

```text
/socialspy
```

Permission:

```text
staffutils.spy
```

## Default private-message aliases

```text
/msg
/tell
/w
/whisper
/pm
/message
/dm
```

These aliases are configurable:

```yaml
spy:
  private-command-aliases:
    - "msg"
    - "tell"
    - "w"
    - "whisper"
    - "pm"
    - "message"
    - "dm"
```

Namespaced variants such as `/minecraft:msg` are handled by the modern implementation.

---

# 15. Staff Logs

## Command

```text
/stafflogs
```

Alias:

```text
/slogs
```

Permission:

```text
staffutils.logs
```

Default configuration:

```yaml
logs:
  latest-default-amount: 10
  latest-max-amount: 50
```

The log system records supported moderation actions and allows staff activity to be reviewed.

---

# 16. Administration

## Commands

```text
/staffutils reload
/staffutils status
```

Alias:

```text
/su
```

Permission:

```text
staffutils.admin
```

`reload` reloads Staff Utils configuration.

`status` shows current storage/synchronization status on the modern edition.

---

# 17. Permissions Reference

```text
staffutils.admin
staffutils.staffmode
staffutils.vanish
staffutils.vanish.others
staffutils.vanish.see
staffutils.invsee
staffutils.enderchest
staffutils.randomtp
staffutils.randomtp.exempt
staffutils.god
staffutils.god.others
staffutils.fly
staffutils.fly.others
staffutils.gamemode.creative
staffutils.gamemode.survival
staffutils.gamemode.spectator
staffutils.gamemode.adventure
staffutils.gamemode.others
staffutils.cps
staffutils.report
staffutils.report.notify
staffutils.report.manage
staffutils.staffchat
staffutils.spy
staffutils.logs
```

The permission reference is also kept at the top of `config.yml`.

---

# 18. Sounds

Staff Utils supports separate configurable sounds for:

- successful actions;
- command execution;
- command errors.

Example modern configuration:

```yaml
sounds:
  success:
    sound: "minecraft:entity.experience_orb.pickup"
    volume: 0.75
    pitch: 1.35

  execution:
    sound: "minecraft:block.note_block.pling"
    volume: 0.65
    pitch: 1.25

  error:
    sound: "minecraft:block.note_block.bass"
    volume: 0.85
    pitch: 0.65
```

---

# 19. Storage — 26.x

The modern edition supports three storage/synchronization layers.

## MariaDB

Used as the persistent multi-server source of truth when enabled.

```yaml
storage:
  mariadb:
    enabled: false
    host: "127.0.0.1"
    port: 3306
    database: "staff_utils"
    username: "root"
    password: "password"
```

## Redis

Used for instant cross-server synchronization.

```yaml
redis:
  enabled: false
  host: "127.0.0.1"
  port: 6379
  database: 0
  channel: "staffutils:sync"
```

## SQLite fallback

If multi-server storage is disabled/unavailable and fallback is enabled, Staff Utils uses SQLite locally instead of crashing.

```yaml
storage:
  fallback-to-sqlite-when-sync-unavailable: true

  sqlite:
    file: "staffutils.db"
```

---

# 20. Multi-Server Configuration

Give each server a unique ID:

```yaml
server:
  id: "survival-1"
```

Example network:

```text
survival-1
survival-2
practice-1
```

Use the same MariaDB and Redis backend across servers when multi-server synchronization is required.

---

# 21. Paper & Folia

The `26.x` edition is designed for Paper and Folia.

The modern implementation uses:

- entity schedulers for player-specific work;
- safe global scheduling where appropriate;
- asynchronous persistence/network I/O;
- async teleport paths where appropriate;
- no NMS for normal plugin functionality.

Legacy branches use the APIs appropriate for their Minecraft generation.

---

# 22. Supported Version Branches

Separate projects are maintained for:

```text
1.8.x
1.9.x
1.10.x
1.11.x
1.12.x
1.13.x
1.14.x
1.15.x
1.16.x
1.17.x
1.18.x
1.19.x
1.20.x
1.21.x
26.x
```

Separate builds are intentional. Minecraft/Bukkit/Paper APIs changed substantially between these generations.

Do not assume a jar compiled for one branch should be used on every other branch.

---

# 23. Building

Each version folder contains a Maven project.

Build one version:

```bat
build.bat
```

Or from Maven:

```text
mvn -U -DskipTests clean package
```

The project is configured to produce a lightweight plugin jar without ProGuard or code obfuscation.

Heavy runtime dependencies are not intended to be blindly shaded into the plugin.

---

# 24. Installation

1. Choose the Staff Utils build matching your server version.
2. Stop the Minecraft server.
3. Put the Staff Utils `.jar` inside `plugins/`.
4. Start the server.
5. Configure permissions.
6. Edit `plugins/StaffUtils/config.yml`.
7. Restart or reload the plugin if necessary.

---

# 25. Recommended First Test

Before production use, test:

```text
Staff Mode enable/disable
Inventory save/restore
InvSee
EnderSee
Random TP
Vanish visibility
Vanish collision
Vanish attack blocking
GodMode
Fly
GMS -> GMC -> GMS flight behaviour
Staff Chat
Reports
CPS Check
SocialSpy global
SocialSpy per-player
Staff Logs
Quit/rejoin while using Staff Mode
```

For multi-server installations also test:

```text
MariaDB connection
Redis synchronization
SQLite fallback
Cross-server Staff Chat
Cross-server persisted reports/logs
```

---

# 26. License

Staff Utils is proprietary software by **Bad_0320** and is distributed under an **All Rights Reserved** license.

See the `LICENSE` file for the full terms.
