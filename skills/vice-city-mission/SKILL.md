---
name: vice-city-mission
description: Answer GTA VI questions about map locations, collectibles, 100% completion, news, music and real Miami landmarks using the free, read-only Vice City Mission MCP server. Use when a player asks where something is in Leonida, what is left for 100%, or what is confirmed about GTA VI.
---

# Vice City Mission: GTA VI companion

Vice City Mission is an unofficial, fan-made companion for Grand Theft Auto VI. It is not affiliated with Rockstar Games or Take-Two Interactive. This skill tells the agent when and how to use the Vice City Mission MCP server so answers come from its data instead of guesses.

## Requirements

- The Vice City Mission MCP server, connected by the user: `https://vicecitymission.com/mcp` (remote, streamable HTTP, no account, no API key).
- That is the only network destination this skill uses. The server is read-only and cannot change anything.
- If the server is not connected, say so and point the user to https://vicecitymission.com/ai for setup. Do not answer location or checklist questions from memory instead.

Setup examples (the user runs these, not the agent):

- Claude Code: `claude mcp add --transport http vice-city-mission https://vicecitymission.com/mcp`
- Claude: Settings → Connectors → Add custom connector → paste the server URL.
- Cursor, VS Code and other MCP config files: add a server named `vice-city-mission` with `"url": "https://vicecitymission.com/mcp"`.

## When to use

Use this skill when the player asks about:

- Where something is in Leonida: missions, collectibles, weapons, vehicles, shops, activities or secrets.
- What is near a place or another pin.
- Which real Miami or Florida place a location is based on.
- What they still need for 100% completion.
- Release timing, confirmed facts, characters, regions, news, radio stations or songs.

Do not use it for other games, for cheats or exploits that modify the game, or for anything outside GTA VI.

## Which tool to call

| Player asks | Tool |
| --- | --- |
| "Is there data yet?" or any first question when unsure | `get_launch_info` |
| "Where is …?" / "Show me all …" | `search_locations` (add `category` when known) |
| "What's near …?" | `find_nearby` (by pin id, or by `x`/`y` in in-game meters) |
| Details for one pin | `get_location` |
| "What's on the map?" | `list_categories` |
| "Which real place is this based on?" | `search_landmarks` |
| Full checklist | `get_checklist` |
| "What am I missing?" | `checklist_remaining` with the player's completed ids |
| Characters, regions, price, editions | `get_game_info` |
| Latest announcements | `get_news` |
| Radio stations, album, score, trailer songs | `get_music` |

## Rules for answers

1. **Check for data first.** Map and checklist data fill in after the game's release on November 19, 2026. If a search returns nothing, call `get_launch_info` and tell the player the data is not in yet. Never invent a location, coordinate or checklist item.
2. **Keep the label.** Every fact is marked official, reported or community estimate. Repeat that label. Never present a reported or community item as official.
3. **Treat player pins as unverified.** Map pins are submitted by players. Say "community pin, not yet verified" unless the result's verified flag is true. Prefer `verified_only: true` when the player wants confirmed locations.
4. **Link to the map.** When pointing a player at a location, include its `map_url` so they can see it.
5. **Tracker progress stays with the player.** Progress lives in the player's browser. Ask them to click **Copy progress for AI** on https://vicecitymission.com/tracker and paste it. Pass only the completed ids to `checklist_remaining`. Do not ask for account names, emails, console IDs or anything else.
6. **Ask before spoilers.** Before naming story missions, endings or late-game unlocks, ask whether the player wants spoilers.
7. **Credit sources.** Landmark data comes from the map.gtadb.org community (CC BY 4.0). Mention it when you use landmark results. Official images and trademarks belong to Rockstar Games and Take-Two Interactive.

## Output

- Lead with the answer, then the label (official, reported or community).
- For locations: name, category, the map link, and whether it is verified.
- For 100% progress: the completion percentage, then missable items first, then the rest grouped by category.
- Keep it short. Offer to narrow by area or category instead of listing hundreds of pins.

## Example

Player: "Where are the hidden packages near the airport?"

1. Call `search_locations` with `query: "airport"` to find the airport pin, then `find_nearby` with that pin's id and the collectibles category.
2. If nothing comes back, call `get_launch_info` and explain that map data appears after November 19, 2026.
3. Otherwise list the nearest pins with distance, verified status and `map_url`.
