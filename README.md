<div align="center">

# LOG-OS

### Moderation with memory.

**A Discord community-operations system for moderation, verification, staff oversight, security intelligence, appeals, voice operations, activity, and community tooling.**

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Red-DiscordBot](https://img.shields.io/badge/Red--DiscordBot-Cog-c0392b)](https://docs.discord.red/)
[![Discord](https://img.shields.io/badge/Platform-Discord-5865F2?logo=discord&logoColor=white)](https://discord.com/)
![Archive](https://img.shields.io/badge/Archive-Original%20%E2%86%92%20v48-202833)
![Latest family](https://img.shields.io/badge/Latest-v40%20family-5865F2)

**[Latest — v48](./Latest/logos_mod_v48.py)** · **[Latest family](#latest-family)** · **[Version archive](#version-archive)** · **[Feature map](#what-log-os-covers)** · **[Installation](#installation)**

</div>

---

## What is LOG-OS?

LOG-OS is a large [Red-DiscordBot](https://docs.discord.red/) cog that grew from a conventional moderation system into a broader **community operations platform**.

Most moderation systems can be described like this:

```text
Member event
    ↓
Command
    ↓
Punishment
    ↓
Log entry
```

LOG-OS is built around a larger operational loop:

```text
Context
   ↓
Staff action
   ↓
Moderation / verification / security workflow
   ↓
Persistent record
   ↓
Review / appeal / follow-up
   ↓
Future context
```

The result is a bot that does more than execute commands. It keeps the surrounding **history, staff workflow, verification state, security signals, community systems, and operational records** connected.

> **Every action has context. Every decision leaves a record.**

---

## Latest snapshot

### [LOG-OS v48](./Latest/logos_mod_v48.py)

The supplied v48 source is the largest snapshot in this archive:

- **19,060 lines** of Python
- **66 classes**
- **134 command decorators**
- **32 `discord.ui.View` classes**
- **85 button decorators**
- **6 select-menu decorators**
- **14 background task loops**
- Red-DiscordBot / discord.py architecture
- PostgreSQL persistence through `asyncpg`, with memory fallback where supported

v48 includes the mature feature families accumulated across the archive, including moderation, appeals, verification, tickets, voice systems, staff dashboards, setup tooling, clubs, invite intelligence, age verification, XP/profiles, alt intelligence, themes, health/status tooling, warning-expiry controls, and more.

If you are browsing the project for the first time, start with **[v48](./Latest/logos_mod_v48.py)** and use the archive below to see how the system evolved.

---

# Repository layout

```text
LOG-OS/
├── README.md
├── Latest/
│   ├── logos_mod_v40.py
│   ├── logos_mod_v42.py
│   ├── logos_mod_v43.py
│   ├── logos_mod_v44.py
│   ├── logos_mod_v45.py
│   ├── logos_mod_v46.py
│   ├── logos_mod_v47.py
│   └── logos_mod_v48.py
└── versions/
    ├── logos_mod.py
    ├── logos_mod_v2.py
    ├── logos_mod_v3.py
    ├── ...
    └── logos_mod_v48.py
```

- **`Latest/`** contains the modern **v40 family** for quick browsing and deployment comparison.
- **`versions/`** preserves the complete source history supplied with this repository.
- The archive does not include source snapshots named **v5, v6, v7, or v41**.

# Latest family

The `Latest/` folder is the fastest way to inspect the modern LOG-OS line. These versions represent the v40-era expansion into invite intelligence, security correlation, progression, identity intelligence, and health tooling.

| Version | Focus | Source |
|---|---|---|
| **v40** | Invite intelligence foundation | **[Open v40](./Latest/logos_mod_v40.py)** |
| **v42** | Invite bans/blocklists, join velocity, staff-role expansion | **[Open v42](./Latest/logos_mod_v42.py)** |
| **v43** | Continued v40-family refinement | **[Open v43](./Latest/logos_mod_v43.py)** |
| **v44** | Expanded help and softban-appeal workflows | **[Open v44](./Latest/logos_mod_v44.py)** |
| **v45** | XP, levels, profiles, achievements, progression | **[Open v45](./Latest/logos_mod_v45.py)** |
| **v46** | Alt-intelligence command family and themes | **[Open v46](./Latest/logos_mod_v46.py)** |
| **v47** | Confirmed-alt networks, offender registry, invite ranking | **[Open v47](./Latest/logos_mod_v47.py)** |
| **v48** | Health/status, warning-expiry, verification and club controls | **[Open v48](./Latest/logos_mod_v48.py)** |

> **Recommended starting point:** browse **[v48](./Latest/logos_mod_v48.py)** for the newest snapshot, then use the table above or the complete archive to trace individual systems backward.

---

# What LOG-OS covers

LOG-OS is intentionally broader than a punishment-command cog.

| Domain | Included in the archive |
|---|---|
| **Moderation** | Warnings, mute/timeout, kicks, bans, unbans, notes, purge, moderation history, staff statistics, conflict checks |
| **Appeals & review** | Appeals, resolution workflows, softban appeals, appeal routing/modes, resend/recovery tools |
| **Verification** | Verification panels, manual verification, age verification, verification sessions, staff verification workflow, force verification |
| **Security intelligence** | Abuse flags, conflict checks, invite intelligence, join velocity, alt checks, alt history, confirmed-alt networks, offender tracking |
| **Tickets** | Ticket panels, ticket listing, reopening, roles, archive workflow |
| **Voice operations** | Join-to-create voice, member/staff controls, staff VCs, VC panels, VC moderation oversight |
| **Staff operations** | ModDash, moderator management, staff-role configuration, superuser/staff controls |
| **Community** | Clubs, club panels, sponsor panels, color roles, ping roles, welcome/community utilities |
| **Activity & progression** | Activity panel, XP, levels, rank, leaderboards, profiles, achievements, configurable multipliers/roles |
| **Server administration** | Setup wizard, backups/restores, role panels, server stats, health checks, themes, configuration commands |
| **Persistence** | PostgreSQL via `asyncpg` with in-memory fallback where supported |

The defining idea is integration: **moderation remembers, verification has context, security can correlate relationships, and staff actions remain part of an operational history.**

---

# Core principles

### Moderation with memory

A moderation action should not become an isolated line in a log channel. LOG-OS preserves context around members, staff actions, cases, appeals, verification, and security events.

### Risk is not guilt

LOG-OS contains security and identity-correlation systems, but suspicious signals are meant to provide **context for review**, not automatically establish wrongdoing.

### Staff actions matter too

The system includes conflict checks, abuse flagging, action oversight, reason requirements, cooldowns, and review workflows because moderation authority itself should remain observable.

### Community operations, not only punishment

Clubs, activity, progression, role panels, tickets, voice tooling, sponsors, profiles, and other community systems sit beside moderation and security rather than in an unrelated second bot.

---

# Version archive

This repository preserves historical LOG-OS source snapshots so the project can be inspected **as it evolved** rather than exposing only the newest build.

> **Note:** The supplied archive does not contain snapshots named **v5, v6, v7, or v41**. The table below links only files that were actually present in the uploaded archive.

## Quick navigator

| Era | Versions |
|---|---|
| **Foundation** | [Original](./versions/logos_mod.py) · [v2](./versions/logos_mod_v2.py) · [v3](./versions/logos_mod_v3.py) · [v4](./versions/logos_mod_v4.py) |
| **Persistence / verification / voice** | [v8](./versions/logos_mod_v8.py) · [v9](./versions/logos_mod_v9.py) · [v10](./versions/logos_mod_v10.py) · [v11](./versions/logos_mod_v11.py) · [v12](./versions/logos_mod_v12.py) |
| **Community expansion** | [v13](./versions/logos_mod_v13.py) · [v14](./versions/logos_mod_v14.py) · [v15](./versions/logos_mod_v15.py) · [v16](./versions/logos_mod_v16.py) · [v17](./versions/logos_mod_v17.py) · [v18](./versions/logos_mod_v18.py) · [v19](./versions/logos_mod_v19.py) |
| **Operations / staff tooling** | [v20](./versions/logos_mod_v20.py) · [v21](./versions/logos_mod_v21.py) · [v22](./versions/logos_mod_v22.py) · [v23](./versions/logos_mod_v23.py) · [v24](./versions/logos_mod_v24.py) · [v25](./versions/logos_mod_v25.py) · [v26](./versions/logos_mod_v26.py) · [v27](./versions/logos_mod_v27.py) · [v28](./versions/logos_mod_v28.py) |
| **Verification / command-system expansion** | [v29](./versions/logos_mod_v29.py) · [v30](./versions/logos_mod_v30.py) · [v31](./versions/logos_mod_v31.py) · [v32](./versions/logos_mod_v32.py) · [v33](./versions/logos_mod_v33.py) · [v34](./versions/logos_mod_v34.py) · [v35](./versions/logos_mod_v35.py) · [v36](./versions/logos_mod_v36.py) · [v37](./versions/logos_mod_v37.py) · [v38](./versions/logos_mod_v38.py) |
| **Security / intelligence expansion** | [v39](./versions/logos_mod_v39.py) · [v40](./versions/logos_mod_v40.py) · [v42](./versions/logos_mod_v42.py) · [v43](./versions/logos_mod_v43.py) · [v44](./versions/logos_mod_v44.py) · [v45](./versions/logos_mod_v45.py) · [v46](./versions/logos_mod_v46.py) · [v47](./versions/logos_mod_v47.py) · **[v48](./versions/logos_mod_v48.py)** |

---

## Evolution at a glance

The descriptions below are based on observable command/class additions between the supplied snapshots. They are intended as an archive guide, not a complete changelog.

| Snapshot | Approx. size | Major visible evolution |
|---|---:|---|
| **[Original](./versions/logos_mod.py)** | 487 lines | Core moderation foundation: warn, mute, kick, ban, unban, notes, purge, audit/server stats |
| **[v2](./versions/logos_mod_v2.py)** | 584 | Appeals, abuse flagging, appeal resolution |
| **[v3](./versions/logos_mod_v3.py)** | 847 | Action records and member-facing history |
| **[v4](./versions/logos_mod_v4.py)** | 1,229 | Ticket workflow, message-deletion oversight, interactive ticket UI |
| **[v8](./versions/logos_mod_v8.py)** | 2,893 | Database layer, verification, moderation utilities, voice systems, audit listeners |
| **[v9](./versions/logos_mod_v9.py)** | 3,588 | Expanded moderator/council voice-control system and staff VC tooling |
| **[v11](./versions/logos_mod_v11.py)** | 4,293 | Role configuration and interactive role panels |
| **[v13](./versions/logos_mod_v13.py)** | 4,465 | Color-role tooling |
| **[v14](./versions/logos_mod_v14.py)** | 4,608 | Ping-role tooling |
| **[v15](./versions/logos_mod_v15.py)** | 5,198 | Activity panel and first major clubs/community expansion |
| **[v16](./versions/logos_mod_v16.py)** | 5,655 | Interactive clubs panel, descriptions and emblems |
| **[v17](./versions/logos_mod_v17.py)** | 6,014 | Sponsor/community-server panel workflow |
| **[v18](./versions/logos_mod_v18.py)** | 6,320 | Welcome/nickname-management expansion |
| **[v19](./versions/logos_mod_v19.py)** | 6,226 | Verification-prefix/reapply workflow |
| **[v20](./versions/logos_mod_v20.py)** | 6,662 | Server backup and restore commands |
| **[v21](./versions/logos_mod_v21.py)** | 7,166 | Superuser tooling, ticket roles/archive, expanded staff operations |
| **[v22](./versions/logos_mod_v22.py)** | 7,788 | **ModDash** introduced |
| **[v23](./versions/logos_mod_v23.py)** | 8,255 | Richer moderation UI: reason/timeout/warn/kick/ban interaction views |
| **[v25](./versions/logos_mod_v25.py)** | 8,899 | Softban-management surface and superuser VC panel |
| **[v26](./versions/logos_mod_v26.py)** | 10,168 | Large interactive **setup wizard** |
| **[v28](./versions/logos_mod_v28.py)** | 10,268 | Conflict-check command and expanded setup-navigation UI |
| **[v29](./versions/logos_mod_v29.py)** | 10,724 | Age-verification workflow |
| **[v31](./versions/logos_mod_v31.py)** | 11,119 | Moderator-target cooldown inspection/control |
| **[v32](./versions/logos_mod_v32.py)** | 11,442 | Age-verification logs and richer review UI |
| **[v33](./versions/logos_mod_v33.py)** | 12,237 | Large slash-command grouping experiment / command-surface expansion |
| **[v34](./versions/logos_mod_v34.py)** | 11,541 | Command surface consolidated after v33 while retaining later feature families |
| **[v35](./versions/logos_mod_v35.py)** | 11,801 | Club display tooling |
| **[v36](./versions/logos_mod_v36.py)** | 12,147 | Club premium/promotion workflow |
| **[v38](./versions/logos_mod_v38.py)** | 12,252 | Role-panel removal/management tooling |
| **[v39](./versions/logos_mod_v39.py)** | 13,150 | Major verification-session expansion: staff channel, modes, approvals, ID checks |
| **[v40](./versions/logos_mod_v40.py)** | 13,873 | Invite intelligence: allow/revoke/purge/log/mode/list + invite listeners |
| **[v42](./versions/logos_mod_v42.py)** | 15,253 | Invite bans/blocklists/checking, staff-role tooling and join-velocity reporting |
| **[v44](./versions/logos_mod_v44.py)** | 15,988 | Expanded help system and structured softban-appeal workflow |
| **[v45](./versions/logos_mod_v45.py)** | 17,141 | XP, levels, profiles, achievements, leaderboard and progression system |
| **[v46](./versions/logos_mod_v46.py)** | 18,005 | Alt-intelligence command family and theme support |
| **[v47](./versions/logos_mod_v47.py)** | 18,691 | Confirmed-alt networks, alt status, offender registry and invite ranking |
| **[v48](./versions/logos_mod_v48.py)** | 19,060 | Server-health, warning-expiry, reason-window, force-verification and club-stop controls |

Snapshots not called out individually above are still linked in the [Quick navigator](#quick-navigator) and may contain internal refinements, fixes, or implementation changes even when no large new command family is obvious from the public surface.

---

# Feature families in v48

## Moderation

```text
warn       mute       kick       ban        unban
notes      purge      lock       unlock     slowmode
warns      clearwarn  modstats   auditlog   conflictcheck
```

LOG-OS also tracks moderation action metadata, IDs, reasons, receipts, history, cooldowns, and oversight workflows.

## Appeals

```text
appeal
resolveappeal
appealchannel
appealmode
softbanappeals
resendappeal
resendappealdecision
```

Appeal workflows are connected back to moderation state instead of being treated as an unrelated generic support conversation.

## Verification

```text
verifypanel
manualverify
verify
verifymode
verifysessions
verifystaffchannel
approveverify
cancelsession
forceverify
idcheck
checkage
revokeage
agelog
```

Verification evolved from a panel into a larger admission/review system with staff workflow and age-verification support.

## Invite intelligence

```text
invitelist
invitelog
invitemode
inviteallow
inviterevoke
invitepurge
invitecheck
inviteban
inviteunban
inviteblocklist
inviterank
velocityreport
```

Invite creation/deletion and member-join context are also observed by listeners in later snapshots.

## Alt / identity intelligence

```text
altcheck
altconfig
altdeny
althistory
altconfirm
altnetwork
altstatus
offenders
```

The later archive includes multi-signal account relationship analysis and confirmed-alt network tooling rather than relying on one binary indicator.

## Voice operations

```text
vcsetup
vcpanel
vclist
vcdelete
vcstafflist
staffvcdelete
suvcpanel
```

LOG-OS contains member, moderator and higher-trust voice-control workflows alongside audit attribution and action-reason oversight.

## Tickets

```text
ticketpanel
tickets
reopen
ticketarchive
ticketrole
```

## Staff operations

```text
moddash
mods
addmod
removemod
staffroles
```

## Clubs / community

```text
clubs
club
create/management commands
clubspanel
clubdisplay
clubpremium
clubpremiumpromote
clubstop
sponsorspanel
```

## Progression

```text
xp
rank
profile
leaderboard
achievements
achievement
givexp
removexp
resetxp
levelconfig
levelrole
memberrole
xpmultiplier
grantachievement
```

## Administration

```text
setup
backup
restore
serverstats
serverhealth
helplogos
theme
roleconfig
rolelist
rolepanel
rolepanelremove
```

---

# Architecture

The historical source is primarily a **large Red-DiscordBot cog** built on the discord.py ecosystem.

```text
Discord
   │
   ▼
Red-DiscordBot
   │
   ▼
LOG-OS Cog
   ├── Moderation
   ├── Appeals
   ├── Verification
   ├── Security / identity
   ├── Tickets
   ├── Voice
   ├── Community systems
   ├── Progression
   ├── Staff panels
   └── Administration
           │
           ▼
      PostgreSQL
      (when configured)
```

Primary technologies visible in the current archive:

- Python
- Red-DiscordBot
- `discord.py`
- `discord.app_commands`
- `discord.ext.tasks`
- `asyncio`
- `asyncpg`
- PostgreSQL
- Discord persistent views, buttons, selects, and modals

---

# Installation

These files are **historical source snapshots**. Choose the version you want to run and package/place it according to your Red-DiscordBot cog setup.

For a new deployment, start with **[v48](./Latest/logos_mod_v48.py)** unless you intentionally need an earlier snapshot.

### 1. Have a working Red-DiscordBot instance

Follow the official Red documentation:

https://docs.discord.red/

### 2. Install PostgreSQL support if you want persistent DB storage

```bash
pip install asyncpg
```

Then configure:

```bash
export DATABASE_URL='postgresql://USER:PASSWORD@HOST:5432/DATABASE'
```

If `asyncpg` or `DATABASE_URL` is unavailable, later snapshots contain an in-memory fallback for supported paths. Do **not** treat memory-only operation as durable audit storage.

### 3. Put the selected LOG-OS source into your Red cog path

From Discord, the Red owner can inspect configured cog paths with:

```text
[p]paths
```

`[p]` means your configured Red prefix.

### 4. Load the cog

The source snapshots expose Red's standard async setup entry point:

```python
async def setup(bot: commands.Bot):
    ...
```

Once packaged in your Red cog layout, load it using your normal Red cog workflow.

### 5. Run setup

Recent snapshots contain an interactive setup command:

```text
[p]setup
```

Useful later-version commands also include:

```text
[p]moddash
[p]helplogos
[p]serverhealth
[p]backup
```

---

# Configuration

Later versions read a number of settings from environment variables. v48 includes values such as:

```text
DATABASE_URL
LOGOS_WARN_DECAY
LOGOS_WARN_THRESHOLD
LOGOS_ABUSE_COOLDOWN
LOGOS_CONFLICT_WINDOW
LOGOS_DELETE_TIMEOUT
LOGOS_VERIFY_NUDGE
LOGOS_MEMBER_ROLE
LOGOS_ADULT_ROLE
LOGOS_MOD_LOG_CHANNEL
LOGOS_WELCOME_CHANNEL
LOGOS_APPEAL_CHANNEL
LOGOS_TICKETS_CHANNEL
LOGOS_TICKET_CATEGORY
LOGOS_VOICE_TIMEOUT
LOGOS_SPAM_WINDOW
LOGOS_TICKET_DAY_LIMIT
LOGOS_TICKET_MON_LIMIT
LOGOS_APPEAL_COOLDOWN_DAYS
LOGOS_VERIFY_CAM_TIMEOUT
LOGOS_VERIFY_APP_TIMEOUT
```

Check the top of the exact source snapshot you intend to run because configuration behavior changes across versions.

---

# Discord permissions

Required Discord permissions depend on which LOG-OS systems you enable. The v48 source documents operational needs including permissions around:

- Manage Roles
- Manage Channels
- Kick Members
- Ban Members
- Moderate Members
- View Audit Log
- Manage Messages
- Move Members

Additional workflows may require additional Discord permissions.

Use the minimum permissions necessary for the features you actually deploy.

---

# Browsing the history

This repository is intentionally useful as more than a download page.

A few interesting development paths to follow:

### Moderation → accountability

[Original](./versions/logos_mod.py) → [v2 appeals](./versions/logos_mod_v2.py) → [v3 action history](./versions/logos_mod_v3.py) → [v28 conflict checking](./versions/logos_mod_v28.py) → [v44 expanded appeals](./versions/logos_mod_v44.py)

### Verification → admission intelligence

[v8 verification](./versions/logos_mod_v8.py) → [v29 age verification](./versions/logos_mod_v29.py) → [v39 verification sessions](./versions/logos_mod_v39.py) → [v40 invite intelligence](./versions/logos_mod_v40.py) → [v42 velocity/blocklist controls](./versions/logos_mod_v42.py) → [v48 force-verification controls](./versions/logos_mod_v48.py)

### Identity/security evolution

[v40 invite intelligence](./versions/logos_mod_v40.py) → [v42 join velocity](./versions/logos_mod_v42.py) → [v46 alt intelligence](./versions/logos_mod_v46.py) → [v47 alt networks/offenders](./versions/logos_mod_v47.py)

### Community-system evolution

[v11 role panels](./versions/logos_mod_v11.py) → [v15 clubs/activity](./versions/logos_mod_v15.py) → [v17 sponsors](./versions/logos_mod_v17.py) → [v36 club premium](./versions/logos_mod_v36.py) → [v45 XP/profiles/achievements](./versions/logos_mod_v45.py)

### Operator experience

[v4 interactive tickets](./versions/logos_mod_v4.py) → [v9 voice panels](./versions/logos_mod_v9.py) → [v22 ModDash](./versions/logos_mod_v22.py) → [v26 setup wizard](./versions/logos_mod_v26.py) → [v44 integrated help](./versions/logos_mod_v44.py)

---

# Archive notes

- Each `.py` file is a **snapshot**, not a patch file.
- `Latest/` is a convenience collection for the v40 family; `versions/` is the historical archive.
- Later version numbers do not imply that every previous behavior is unchanged; inspect the version you intend to deploy.
- The uploaded archive includes **44 Python snapshots**: the original `logos_mod.py` plus numbered versions through v48.
- **v5, v6, v7 and v41 were not present in the supplied archive.**
- Several snapshots add substantial internal changes even when their visible command list changes very little.
- v33 has a notably expanded grouped/slash-command surface that is consolidated again in v34.

---

# Security & privacy

LOG-OS handles moderation and potentially sensitive community-operational data. If you deploy it:

- Never commit Discord bot tokens.
- Never commit PostgreSQL credentials.
- Keep moderation/verification exports private unless intentionally disclosed.
- Review the permissions granted to the bot.
- Back up persistent data before upgrading between historical snapshots.
- Test moderation, verification, voice, and restore workflows in a controlled server before production use.

When filing public bug reports, remove member-private information and all credentials from logs.

---

# Contributing / issue reports

When reporting a problem, useful information includes:

```text
LOG-OS source version
Red-DiscordBot version
Python version
Database mode (PostgreSQL / memory)
Relevant traceback
Steps to reproduce
Expected behavior
Observed behavior
```

Historical versions are preserved for reference, comparison, regression testing, and understanding the evolution of the project.

---

<div align="center">

## LOG-OS

**Moderation with memory.**
