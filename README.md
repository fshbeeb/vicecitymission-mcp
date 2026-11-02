# Vice City Mission MCP server

[![Scanned by Foo Guard: Vice City Mission: GTA VI companion v1.0.0](https://fooguard.com/api/public-library/community-b75596ca-9888-4d7f-92c6-6787f41b5126/1.0.0/badge.svg)](https://fooguard.com/library/community-b75596ca-9888-4d7f-92c6-6787f41b5126/1.0.0/verify)

A free, read-only [MCP](https://modelcontextprotocol.io) server for **Grand Theft Auto VI**, run by the fan site [vicecitymission.com](https://vicecitymission.com). Connect it to Claude, Cursor or any MCP client, then ask things like "what songs has Rockstar confirmed for Cocoteo FM?" or "which real Miami places match the landmarks near Ocean Beach?".

> **Unofficial.** Vice City Mission is a fan project. It is not affiliated with, endorsed by, or sponsored by Rockstar Games or Take-Two Interactive.

This repository documents the hosted server. The server itself runs on vicecitymission.com; there is nothing to install or run.

## Connect

| | |
|---|---|
| URL | `https://vicecitymission.com/mcp` |
| Transport | Streamable HTTP |
| Sign-in | None |
| Access | Read-only |
| Limits | Calls that read data are limited to 600 an hour per network. `ping`, `initialize` and listing the tools are not limited. |
| Registry name | `com.vicecitymission/gta6` (on the [official MCP Registry](https://registry.modelcontextprotocol.io)) |

**Claude Code**

```bash
claude mcp add --transport http vice-city-mission https://vicecitymission.com/mcp
```

**Cursor** (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "vice-city-mission": { "url": "https://vicecitymission.com/mcp" }
  }
}
```

**Other clients:** any client that supports remote Streamable HTTP servers can use the URL above. More setup help is at [vicecitymission.com/ai](https://vicecitymission.com/ai).

## Tools

All 11 tools are read-only.

| Tool | What it does |
|---|---|
| `get_launch_info` | Release date of GTA VI, days remaining, and how much community data the Vice City Mission map and tracker have so far. |
| `get_game_info` | Confirmed facts about GTA VI: quick facts (price, platforms, editions), the playable and supporting characters, and the regions of Leonida with their real-world inspirations. |
| `get_music` | Confirmed GTA VI music: radio stations (genre, on-air hosts, reported voice actors, previewed songs), Grand Theft Auto VI: The Album singles, Justice's original score, and songs from each trailer. |
| `get_news` | Major GTA VI announcements, newest first, each with a date, status (official/reported/community) and source links. |
| `search_landmarks` | Search ~1,900 GTA VI locations matched to the real Miami/Florida places they're based on (community data from map.gtadb.org, CC BY 4.0). |
| `list_categories` | The kinds of locations on the map (missions, collectibles, weapons, vehicles, shops, activities, secrets) with how many pins each has. |
| `search_locations` | Search community-submitted GTA VI map pins by text and/or category. |
| `get_location` | Full details for one map pin by its id. |
| `find_nearby` | Find pins close to another pin or to a map position, nearest first. |
| `get_checklist` | The completion checklist from the Vice City Mission tracker: story missions, side missions, activities, collectibles and trophies. |
| `checklist_remaining` | Given the ids a player has completed (from the tracker's 'Copy progress for AI' button), return what is still left, with missable items first, and the completion percentage. |

## Agent skill

[`skills/vice-city-mission/SKILL.md`](skills/vice-city-mission/SKILL.md) tells an agent when and how to use this server: which tool fits which question, to check whether data exists before answering, to keep the official/reported/community label, to treat player pins as unverified, and to ask before spoilers. It needs no API key and uses only `https://vicecitymission.com/mcp`.

Install it the way your agent loads `SKILL.md` skills, for example by copying the `vice-city-mission` folder into `~/.claude/skills/` for Claude Code.

Version 1.0.0 is published in the [Foo Guard public Library](https://fooguard.com/library/community-b75596ca-9888-4d7f-92c6-6787f41b5126/1.0.0/verify), which ran a deterministic static scan over these exact bytes (Grade A, 0 findings). A static scan is not proof of runtime safety. To check that your copy matches the scanned file:

```bash
shasum -a 256 skills/vice-city-mission/SKILL.md
# expected: de4a2ad4baff793b532cd68c17807858bcf7e7b3d3dc76e5b881b85d2c373c68
```

If you edit the skill, the hash changes and the badge no longer describes your copy.

## Example questions

- "How many days until GTA VI comes out, and what's confirmed so far?"
- "What songs has Rockstar confirmed for Cocoteo FM, and where can I stream them?"
- "Find landmarks near Ocean Beach and tell me which real places they match."
- "Show me the latest GTA VI news, and say which items are official."
- "What's left for 100%?" (the checklist fills in after the game releases on November 19, 2026)

## About the data

- **Facts are labelled** as *official* (confirmed by Rockstar), *reported* (from news outlets or insiders) or *community estimate*, so an assistant can say how sure it is.
- **Landmarks** come from the [gtadb.org](https://map.gtadb.org) community, under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Placements are fan estimates until the game is out.
- **Map pins** are submitted by players and verified by other players' votes, so treat them as community data.
- Rockstar's images and trademarks belong to their owners.

## Links

- Website: <https://vicecitymission.com>
- GTA 6 map: <https://vicecitymission.com/map>
- AI setup page: <https://vicecitymission.com/ai>
- Credits: <https://vicecitymission.com/credits>

## License

[MIT](LICENSE) for the contents of this repository (the documentation). It doesn't cover the vicecitymission.com service, its data, or Rockstar's and Take-Two's trademarks.
