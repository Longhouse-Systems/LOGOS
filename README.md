# LOGOS — Community Operating System

> **Moderation with memory. Accountable authority. Informed decisions.**
> *Understand the whole before judging a part.*

**Developed by [Sovereign Systems](https://github.com/Longhouse-Systems)**

---

LOGOS is not a moderation bot.

It is a community operating system — a governance, security, verification, and memory platform built to help people run complex online communities without losing the context behind their decisions.

A traditional moderation bot asks: *what command should run?*

LOGOS asks:

```
WHAT HAPPENED?
      ↓
WHAT DO WE ACTUALLY KNOW?
      ↓
WHAT DO WE THINK IS HAPPENING?
      ↓
WHAT ARGUES AGAINST THAT?
      ↓
WHAT POLICY APPLIES?
      ↓
WHAT AUTHORITY EXISTS?
      ↓
WHAT ACTION IS PROPORTIONAL?
      ↓
WHAT HAPPENED AFTERWARD?
      ↓
WHAT SHOULD THE SYSTEM REMEMBER?
```

That chain — observation, distinction, interpretation, authority, proportional action, outcome, memory — is the foundation of everything LOGOS does.

---

## Repository Structure

```
LOGOS/
├── latest/                  ← Current v40-series release
│   ├── logos_mod_v48.py     ← Main Redbot cog (134 commands, 61 tables)
│   ├── logos_api.py         ← FastAPI dashboard backend
│   ├── logos_server.py      ← Multi-port web server (3 services)
│   ├── logos_dashboard.html ← Public multi-server staff dashboard
│   ├── logos_homepage.html  ← Public marketing homepage
│   └── logos_install.py     ← Self-contained Arch Linux installer
├── LICENSE
└── README.md
```

> **Platform:** Python 3.11+ · Red-DiscordBot (Redbot) · PostgreSQL · discord.py

---

## Version History

LOGOS has evolved continuously from a simple moderation cog into a full community operating platform. Each major series introduced a new architectural layer.

---

### v10 Series — Foundation
*Basic moderation cog for Redbot*

The beginning. A straightforward set of Discord moderation commands built as a Redbot cog.

**What existed:**
- `>warn`, `>mute`, `>kick`, `>ban`, `>unban`
- Basic action logging to a flat table
- Simple role-based permission checks using Discord native roles
- In-memory fallback when no database was configured

**What was missing:**
Everything else. No memory across restarts, no conflict detection, no verification, no appeals. Actions happened and were immediately forgotten.

---

### v20 Series — Memory & Structure
*Persistent database, action history, staff tiers*

The v20 series introduced PostgreSQL as the persistence layer and the concept of a *moderation record* — not just a log entry, but a structured record with context.

**What changed:**
- PostgreSQL schema with `actions`, `warns`, `notes` tables
- Staff tier system: `mod` → `senior_mod` → `admin` — each with different authority limits
- Hard ban limit for mods: 5 bans per 24h with an automatic owner DM above that
- Moderation notes separate from punitive actions
- `>history @member` — full action history per member
- In-memory fallback fully functional for testing without a database
- `>modstats` — moderator action breakdown

**Architecture shift:** LOGOS started thinking about *who* was doing the action, not just *what* was done.

---

### v30 Series — Verification, Voice & Community
*Verification flow, VC controls, clubs, tickets, XP*

The v30 series expanded LOGOS from a moderation tool into a community platform. Three major systems arrived simultaneously.

**Verification system:**
- Three modes: `off`, `camera`, `id`
- Camera mode: private VC created per session, staff must physically join before approving
- Unverified member tracking with configurable kick timer
- Age verification (`>ageverify`) separate from base verification
- `>forceverify` admin override with full audit trail

**Voice system:**
- User-owned voice channels — members create VCs by joining a trigger channel
- VC control panel sent as DM to channel owner
- Lock, unlock, rename, user limit, kick, allow/block per-user
- Voice room preference memory — default name and limit saved per member
- Staff voice action reason system — mods have a configurable window to file a reason after a voice action, otherwise it auto-reverts

**Community features:**
- Clubs — member-created groups with emblem, description, member list, premium tier
- Sponsors panel — community partner applications
- Role panel — self-assign roles via buttons
- XP system — message XP, voice XP, reaction XP, level roles, achievements, multipliers
- Ticket system — private channel per ticket with claim/close/escalate controls
- Softban — restricts text while preserving voice access, with appeal flow

**Background tasks introduced:**
`check_verify_sessions`, `check_unverified`, `check_timed_mutes`, `check_pending_voice_actions`, `refresh_vc_panels`, `check_xp_voice`, `cleanup_archived_tickets`

---

### v40 Series — Intelligence, Detection & Governance
*Alt detection, Spiral engine, case system, dashboard, installer*

The v40 series is where LOGOS became something meaningfully different from a moderation bot. The intelligence layer arrived.

---

#### v40–v43 — Alt Detection Engine

The alt detection system fires on every member join and scores them across 8 independent signals:

| Signal | Max Points | Description |
|--------|-----------|-------------|
| Account age | +40 | New accounts score higher |
| Join timing | +50 | Linear decay from last ban event |
| Invite chain risk | +35 | Inviter's historical ban-to-invite ratio |
| Username similarity | +30 | Bigram comparison against recent joins |
| Avatar hash match | +70 | Exact match against banned fingerprints |
| Public invite clustering | +40 | Catches Disboard-style bypass |
| Offender registry | +80 | Manual staff-added entries |
| Confirmed alt network | +90 | Previously confirmed alt pair |

**Thresholds (all configurable):**
- `30` — log silently
- `60` — alert staff
- `75` — hold for review
- `90` — auto-kick

**Commands:** `>altconfig`, `>altcheck`, `>altdeny`, `>altconfirm`, `>altstatus`, `>althistory`, `>altnetwork`, `>offenders`, `>inviterank`

**Tables added:** `banned_fingerprints`, `alt_detection_config`, `alt_detections`, `join_clusters`, `offender_registry`, `confirmed_alts`

Ban fingerprints are captured automatically on every ban — the comparison pool grows passively.

---

#### v44–v45 — Dashboard & Web Infrastructure

LOGOS became a three-service web application:

```
Port 8080  →  FastAPI backend (internal only)
Port 8081  →  Public homepage (internet-facing)
Port 8082  →  Staff dashboard (localhost / SSH tunnel only)
```

**Public dashboard features:**
- Discord OAuth2 login — works across every server LOGOS is in
- Server picker — shows only guilds where you have Manage Server
- Community Health page — coherence score, stats, live activity timeline
- Invite Graph — animated network graph of all recorded joins with alt flag overlay
- Moderation Queue — pending voice reasons with live countdown, open appeals, ticket queue
- Audit Log — searchable, filterable, CSV export
- Members — searchable list, profile drill-down, mod history
- Alt Detection — pending detections, offender registry management, confirm/false-positive
- XP Leaderboard
- Clubs directory
- Panel status with one-click re-post
- Settings — verify mode, reason window, warn expiry, invite mode, appeal mode
- Theme editor — accent colour, presets, branding, live Discord embed preview

**`logos_install.py` — self-contained Arch Linux installer:**
- Bundles all five files (no internet required after download)
- Installs PostgreSQL, runs initdb, hardens `pg_hba.conf`, applies `postgresql.conf` tweaks
- Creates dedicated `logos` system user (nologin, no home)
- Creates `logos_db` database user with least-privilege grants
- Runs full 61-table schema
- Detects or creates Redbot instance, installs cog
- Collects Discord credentials, sets up `.env` (mode 600)
- Configures firewall (ufw or iptables script)
- Installs hardened systemd user service with full sandboxing directives
- Generates security audit report

---

#### v46–v47 — Settings Category & USERDB

**Settings category** — nine persistent panels posted to a SETTINGS Discord category visible to all verified members:

| Channel | Panel | Purpose |
|---------|-------|---------|
| `#mod-status` | ModStatusView | Mods toggle on/off duty, set status message |
| `#call-mod` | CallModView | Members ring on-duty mods with reason |
| `#clubs-panel` | ClubsManageView | Personal club creation, editing, leaderboard |
| `#voice-room` | VoiceRoomView | VC preference memory, live channel controls |
| `#data-request` | DataRequestView | GDPR export/deletion requests |
| `#mailbox` | MailboxView | Message mod team at any tier (mod/senior/admin) |
| `#contact-us` | ContactUsView | Tickets, reports, mailbox shortcuts |
| `#help` | TicketOpenView | Support ticket opener |
| `#server-info` | Static embed | Server description, rules, stats, socials |

**Mailbox system:**
- Members choose which tier to contact: Mod / Senior Mod / Admin+Owner
- Optional anonymous sending
- Staff reply via `>mailreply <id> <message>` — relayed back to member by bot
- Full audit trail with timestamps and reply status

**Tables added:** `mailbox_messages`, `voice_room_prefs`, `mod_status`, `call_mod_log`, `data_requests`, `server_info_config`, `settings_panels`, `userdb_whitelist`

**New commands:** `>reasonwindow`, `>warnexpiry`, `>serverhealth`, `>forceverify`, `>clubstop`

---

#### v48 — Panel Redesign, Spiral Engine & Branding

**v48 is the current release.**

**Panel design system:**

All panels redesigned with a consistent visual language:

```
🟢 Green  — approved / clear / complete
🟡 Gold   — pending / needs attention
🟠 Orange — elevated / warning
🔴 Red    — urgent / blocked / critical
🔵 Blue   — informational / in progress
⚫ Dark   — inactive / staff context
```

Mobile-first: maximum 5 buttons per row, short labels, all mod interactions ephemeral, member VC controls persistent in DM.

**ModDash split into 3 embeds:**
1. Server Snapshot — member counts, verification status, alert summary, voice activity
2. Needs Attention — pending voice reasons with live countdown, active mutes, open tickets
3. Recent Actions — last 6 actions with type icons and relative timestamps

**All panels redesigned:** VerifyView, _VCControlView, ClubsPanelView, SoftbanAppealView, _SoftbanAppealDecisionView, SponsorsPanelView, RolePanelView, _VerifySessionStaffView, VoiceActionReasonView, _AltDecisionView

**Verify + Alt integration:**
- Alt score shown to staff at session start with colour coding
- Offender registry and confirmed alt status shown
- Alt risk warning displayed at the moment of approval if score ≥ hold threshold
- Staff must be physically in the verification VC to approve

**Spiral Decision Engine (Phase 1–4):**

The Spiral runs before every punitive action. It collects observations silently from existing LOGOS data and evaluates them against a flag framework before any Discord action executes.

```
>ban @member reason
      ↓
Spiral collects observations:
  account age, server age, prior history, alt score,
  verification status, COI check, open tickets,
  actor budget, active appeals, offender registry
      ↓
Flags raised if warranted
      ↓
CLEAN    → executes silently
ADVISORY → brief note, executes
MEDIUM   → mod must acknowledge
HIGH     → written reason required, senior DM sent
BLOCK    → hard stop, senior approval required
      ↓
Decision record saved permanently
```

**Flag types:**
- `COI_DETECTED` — conflict of interest between actor and target
- `BUDGET_WARNING` / `BUDGET_EXHAUSTED` — approaching or exceeding 24h action budget
- `NO_ESCALATION_PATH` — first offense, low alt score, no prior history
- `ACTIVE_APPEAL` — target has a pending appeal
- `OPEN_TICKET_FILER` — target has an open support ticket

**Action budgets apply to all authority, not just bans:**
Ban, Kick, Mute, Timeout, Softban, Warn, Channel modifications, Role changes, Verification overrides — all tracked. As a mod approaches their budget, the Spiral starts requiring acknowledgement earlier.

**Spiral commands:**
- `>spiraldecision <id>` — look up any decision record by ID
- `>spiraloverrides` — senior staff only, full override history
- `>challenge <id>` — senior staff only, LOGOS searches for counterevidence and may revise recommendation

**`SpiralAcknowledgeView` and `SpiralOverrideModal`:**
- MEDIUM flag → "Acknowledge & Proceed" button (one tap)
- HIGH flag → modal opens, minimum 20 character written justification, permanently logged, senior DM sent
- BLOCK → buttons disabled, senior DM already sent, cannot self-approve

**Schema additions in v48:** `spiral_observations`, `spiral_evidence`, `spiral_decisions`, `spiral_action_budgets`, `spiral_overrides`, `logos_roles`, `logos_member_roles`, `logos_defcon`, `logos_defcon_history`, `logos_duty_log`, `logos_capability_overrides`

**LOGOS Internal Roles (v48):**

LOGOS maintains its own role system independent of Discord roles. No Discord role needed to grant authority — LOGOS assigns capability sets directly to members.

| Role | Hierarchy | Key Capabilities |
|------|-----------|-----------------|
| `owner` | 100 | Wildcard — all capabilities |
| `administrator` | 80 | Full moderation, authority management, DEFCON control |
| `senior_mod` | 60 | All moderation, cases, appeals review, verification |
| `moderator` | 40 | Warn, timeout, kick, softban, basic verification |
| `junior_mod` | 20 | Warn, timeout only |
| `appeals_agent` | 30 | Appeals review and resolution, case viewing |
| `verify_agent` | 15 | Verification approval |
| `observer` | 5 | Read-only staff view |

**DEFCON system (v48):**

```
DEFCON 5  🟢  NORMAL      — Full authority active
DEFCON 4  🔵  WATCH       — Enhanced logging
DEFCON 3  🟡  ELEVATED    — Sensitive changes need re-verification
DEFCON 2  🟠  RESTRICTED  — Bans need approval, mass actions frozen
DEFCON 1  🔴  LOCKDOWN    — Most authority suspended
DEFCON 0  ⚫  SAFE MODE   — Emergency recovery kernel only
```

**Sovereign Systems rebranding:**
All tooling, documentation, and installer references updated from Longhouse Systems to Sovereign Systems.

---

## Feature Summary (v48)

### Moderation
- Warn, timeout, mute, softban, kick, ban, unban with full receipt system
- Per-guild warn expiry (`>warnexpiry <days>`)
- Per-guild voice reason window (`>reasonwindow <seconds>`, 30–600s)
- COI detection — bidirectional, 14-day decay window
- Velocity limiting — per tier, per action type
- Conflict-of-interest gate — blocks mods with recorded interaction against target
- Moderation notes separate from punitive record
- `>serverhealth` — coherence score with reason compliance, appeal outcomes, conflict health
- **Spiral engine** runs before every ban (other punitive actions in progress)

### Verification
- Three modes: off / camera / id
- Private VC creation per session
- Staff must join VC before approving — physically gated
- Alt score shown at session start and approval point
- Age verification with separate role grant
- `>forceverify` admin override
- Unverified member tracking with configurable kick timer

### Alt Detection
- 8-signal scoring engine, max 250 points
- Configurable thresholds (log/alert/hold/kick)
- Per-signal toggles
- Score decay on timing signal
- Offender registry — manual entries with +80pt signal weight
- Confirmed alt network — +90pt signal weight
- Fingerprint capture on every ban (avatar hash, username)
- Daily cleanup task — configurable retention
- Full command suite: `>altconfig`, `>altcheck`, `>altdeny`, `>altconfirm`, `>altstatus`, `>althistory`, `>altnetwork`, `>offenders`, `>inviterank`

### Voice
- User-owned voice channels (create-on-join)
- VC control panel in owner DM — persistent, no timeout
- Lock/unlock, rename (modal), user limit (modal), kick, allow/block
- Voice room preference memory (default name, limit, lock state)
- Staff voice action reason system with per-guild configurable timeout
- Auto-revert on expired reason window

### Community
- Clubs — create, join, edit, premium, emblem, member management
- Clubs leaderboard (`>clubstop`, aliases: `>clubleaderboard`)
- Sponsors — application panel, staff review, approval flow
- Self-assign role panel — dynamic buttons from DB config, toggle add/remove
- XP system — message XP, voice XP (5-min task), reaction XP listener
- Level roles, multipliers, achievements with DM notification
- Ticket system — private channels, claim/close/escalate/archive

### Staff Operations
- ModDash — 3-embed panel, 14-button interface, 2-minute auto-refresh
- Mailbox — tiered messaging (mod/senior/admin), anonymous option, reply relay
- Call-mod panel — rings on-duty mods with reason
- Mod status panel — on/off duty toggle, status message
- Data request panel — GDPR export/deletion with 30-day SLA tracking
- Verification queue management from dashboard
- `>spiraldecision`, `>spiraloverrides`, `>challenge` for Spiral governance

### Web
- Multi-server OAuth dashboard (Discord login, any server with Manage Server)
- Live coherence score with breakdown
- Animated invite network graph with alt flag overlay
- Queue management — pending reasons, appeals, tickets
- Audit log with search, filter, CSV export
- Member profiles with history drill-down
- Alt detection management — confirm/false-positive, whitelist
- XP leaderboard
- Panel status with one-click re-post
- Settings editor (all guild config)
- Theme editor — 6 presets, custom colours, live Discord embed preview

### Security & Infrastructure
- **Spiral Decision Engine** — observation, flag, proportionality, acknowledgement
- **LOGOS Internal Roles** — capability-based authority independent of Discord roles
- **DEFCON system** — 6 levels, reduces effective authority without rewriting roles
- **Action budgets** — per-mod per-action-type 24h limits across all authority types
- **Pool lifecycle management** — `_closing` flag, race condition protection on reload
- **14 background tasks** — all guarded with pool-alive check
- Hardened systemd service — NoNewPrivileges, PrivateTmp, ProtectSystem=strict, MemoryDenyWriteExecute, CapabilityBoundingSet=∅
- Dedicated `logos` system user (nologin)
- PostgreSQL hardening — localhost-only, scram-sha-256, least-privilege grants
- `.env` mode 600, secret key from `/dev/urandom`
- Firewall — only port 8081 exposed publicly, 8082 localhost-only

---

## Database (61 Tables)

| Category | Tables |
|----------|--------|
| Core moderation | `actions`, `warns`, `notes`, `appeals`, `mod_cooldowns`, `per_target_cooldowns`, `abuse_flags`, `pending_voice_actions`, `pending_deletes`, `action_spam_tracker`, `action_velocity` |
| Members | `unverified_members`, `softban_list`, `softban_appeals`, `age_verifications`, `superuser_ids` |
| Verification | `verify_sessions` |
| Tickets | `tickets` |
| Voice | `user_voice_channels` |
| Invites | `invite_tracking`, `invite_snapshots` |
| Clubs | `clubs`, `club_members` |
| Sponsors | `sponsors` |
| XP | `xp_config`, `member_xp`, `xp_events`, `level_roles`, `xp_multipliers`, `achievements`, `member_achievements` |
| Theme | `guild_theme`, `guild_panel_overrides` |
| Dashboard | `dashboard_jobs` |
| Alt Detection | `banned_fingerprints`, `alt_detection_config`, `alt_detections`, `join_clusters`, `offender_registry`, `confirmed_alts` |
| Settings | `mailbox_messages`, `voice_room_prefs`, `mod_status`, `call_mod_log`, `data_requests`, `server_info_config`, `settings_panels`, `userdb_whitelist` |
| LOGOS Roles | `logos_roles`, `logos_member_roles`, `logos_defcon`, `logos_defcon_history`, `logos_duty_log`, `logos_capability_overrides` |
| Spiral | `spiral_observations`, `spiral_evidence`, `spiral_decisions`, `spiral_action_budgets`, `spiral_overrides` |
| Guild | `guild_settings` |

---

## Background Tasks (14)

| Task | Interval | Purpose |
|------|----------|---------|
| `check_verify_sessions` | 60s | Expire stale verification sessions |
| `check_invites` | 15s | Enforce invite mode, track join sources |
| `check_dashboard_jobs` | 5s | Process queued dashboard actions |
| `check_xp_voice` | 5m | Award XP for voice time |
| `check_pending_deletes` | 1m | Execute scheduled message deletions |
| `check_pending_voice_actions` | 10s | Per-guild timeout, auto-revert voice actions |
| `check_unverified` | 1m | Kick unverified members past deadline |
| `update_activity_panel` | 30m | Refresh activity statistics |
| `refresh_moddash_panels` | 2m | Push updated 3-embed ModDash |
| `check_timed_mutes` | 30s | Lift expired mutes |
| `check_warn_expiry` | 10m | Mark expired warns inactive |
| `refresh_vc_panels` | 90s | Update VC panel embeds |
| `cleanup_archived_tickets` | 6h | Delete archived ticket channels past retention |
| `cleanup_alt_data` | 24h | Purge fingerprints and clusters past retention |

---

## Installation (Arch Linux)

```bash
# Download the self-contained installer
curl -O https://raw.githubusercontent.com/Longhouse-Systems/LOGOS/main/latest/logos_install.py

# Run it — sudo is requested only when needed
python3 logos_install.py
```

The installer handles everything: PostgreSQL, schema, Redbot detection, cog install, Discord credentials, firewall, systemd service, security audit.

**Requirements:**
- Arch Linux (pacman)
- Python 3.11+
- Red-DiscordBot installed or installable via pip
- A Discord application with bot token and OAuth2 secret

**Manual install (any Linux):**
1. Copy `logos_mod_v48.py` to your Redbot cog directory as `logos.py`
2. Set `DATABASE_URL` in your environment
3. Load with `[p]load logos` then run `>setup`

---

## Quick Start

```
[p]load logos       — load the cog
>setup              — interactive setup wizard
>moddash            — post the staff dashboard
>verifypanel        — post the verification panel
>altconfig          — configure alt detection
>defcon             — view current DEFCON level
>role list          — view LOGOS internal roles
```

---

## What's Coming

The following systems are designed and in active development:

**Zone System** — flat channel access zones (Gateway/Member/Age-Verified/Trusted/Softban/Contained/Staff). Every channel belongs to a zone. Every member belongs to a zone. LOGOS manages all Discord permission overwrites automatically on zone transitions. Every behavior per zone is configurable (text, voice, features, visibility).

**LOGOS Permissions** — per-member capability grants and Discord channel/category overrides managed by LOGOS independently of Discord roles. `>permit @member #channel`, `>deny @member capability`, `>perms @member`, `>whycan @member action`.

**Case & Investigation System** — any member can open `>case @user <description>`. Emergency page to bot owner. Per-case HUD in private server with overview, timeline, evidence, actions, and comms channels. Controlled server owner notifications with tone options. Harassment watchlist for confirmed cases.

**Cross-Server Safety Network** — network-wide fingerprint sharing, global ban enforcement across all LOGOS servers, personal watchlist gated on active harassment case.

**Spiral Phase 5+ — Challenge LOGOS** — senior staff can challenge any Spiral decision. LOGOS searches for counterevidence and may revise recommendation. Full `>challenge <id>` flow.

**Settings Category Completion** — zone-based enforcement for the full settings category. All 9 panels wired to zone transitions.

**Sovereign Systems Homepage** — updated public site reflecting new branding.

---

## The Spiral

Every punitive action in LOGOS passes through the Spiral before executing.

```
                    SPIRAL
                       │
                POLICY ENGINE
                       │
           ┌───────────┴───────────┐
           │                       │
       IDENTITY                CONTEXT
           │                       │
           └───────────┬───────────┘
                       │
                LOGOS AUTHORITY
                       │
             ROLES + CAPABILITIES
                       │
                    SCOPES
                       │
          MEMBER + CHANNEL POLICIES
                       │
                  CONDITIONS
                       │
                    DEFCON
                       │
                   SENTINEL
                       │
             SECURITY / CONFLICT
                       │
          EFFECTIVE AUTHORITY
                       │
       EFFECTIVE CHANNEL ACCESS
                       │
             DISCORD ENFORCEMENT
                       │
              ACTION / CONTAIN
                       │
              CASE + AUDIT LOG
                       │
             REVIEW / CHALLENGE
                       │
             ROLLBACK / RECOVER
                       │
                    SPIRAL
```

The Spiral does not replace human judgment. It gives humans enough context to exercise it well.

**Core principles:**

> Evidence ≠ Inference
> Risk ≠ Guilt
> Confidence ≠ Authority
> Authority ≠ Immunity From Review
> Containment ≠ Punishment
> Automation ≠ Sovereignty

---

## Philosophy

Communities are not collections of isolated commands. They are systems — with history, relationships, policies, authority structures, and accumulated context.

LOGOS is built around one conviction: *the context surrounding a decision matters as much as the decision itself.*

A warning doesn't exist in isolation. It exists because of something that happened, issued by someone with particular authority, against a member with a particular history, under a particular policy, at a particular security state. That full picture is what makes the warning meaningful — or questionable.

LOGOS preserves that picture.

---

## About Sovereign Systems

Sovereign Systems is an independent technology group focused on building operating systems for communities and digital worlds.

LOGOS is one part of a broader direction: tools that help people govern responsibly, protect members and infrastructure, understand incidents, and preserve institutional memory.

**License:** Apache 2.0

**Status:** Active Development — Public Project

---

*LOGOS — Built by Sovereign Systems*
