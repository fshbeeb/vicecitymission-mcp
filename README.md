# Vice City Mission MCP server

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
