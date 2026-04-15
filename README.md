# Discord Bot via Claude Channels

A Discord bot powered by Claude Code skills. Messages sent to the bot on Discord are routed to Claude Code running locally, which uses custom skills to handle the request and replies back through Discord.

## Platform

**Discord** — connected via Claude Channels.

## Skills

### 1. `weather`
Looks up current conditions and a 3-day forecast for any city via Open-Meteo (no API key needed).

**Example**
> User: what's the weather in Ulaanbaatar?
> Bot: **Weather — Ulaanbaatar, Mongolia** / Now: -4°C, Clear, humidity 38%, wind 12 km/h / Next 3 days: ...

### 2. `lyrics`
Looks up song lyrics by title and artist.

**Example**
> User: lyrics to Bohemian Rhapsody
> Bot: **Bohemian Rhapsody** — Queen / Is this the real life? ...

### 3. `exchange-rate`
Live currency conversion. Defaults target to MNT.

**Example**
> User: how much is 250 USD in MNT?
> Bot: **250 USD = 872,500 MNT** / Rate: 1 USD = 3,490 MNT / As of: 2026-04-15

## Setup

### Prereqs
- Claude Code installed and running on the host machine
- A Discord account with permission to create a bot

### Steps
1. Clone this repo: `git clone https://github.com/chtsogt-jpg/discord-bot.git`
2. `cd discord-bot` — the `.claude/skills/` folder auto-loads when Claude Code runs here.
3. Create a Discord application at https://discord.com/developers/applications and add a bot user. Copy the bot token.
4. Invite the bot to your test server with `applications.commands` and `bot` scopes.
5. Run Claude Channels to connect Discord → Claude Code:
   ```
   claude channels connect discord
   ```
   Paste the bot token when prompted.
6. Leave Claude Code running. Message the bot on Discord — it will respond via the skills above.

## Development Workflow

- **Issues**: https://github.com/chtsogt-jpg/discord-bot/issues — one per skill
- **Branches**: one feature branch per skill (`feature/<skill>-skill`)
- **Worktrees**: `lyrics` and `exchange-rate` were built in parallel via `git worktree`
  ```bash
  git worktree add ../discord-bot-lyrics   -b feature/lyrics-skill
  git worktree add ../discord-bot-exchange -b feature/exchange-rate-skill
  ```

## Project Structure
```
discord-bot/
├── .claude/
│   └── skills/
│       ├── weather/SKILL.md
│       ├── lyrics/SKILL.md
│       └── exchange-rate/SKILL.md
└── README.md
```
