# How to connect BookingKoala to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your BookingKoala account.** BookingKoala has no official ChatGPT or Claude app, and its integration docs point to Zapier and Make instead. Cotlet.dev connects your own signed-in BookingKoala account to any AI agent, so you can ask in plain words and the AI assigns providers, reschedules jobs and follows up on unpaid invoices for you.

## What you can ask

> Book a deep clean for Maria Lopez at 42 Oak Street next Tuesday at 9 am and assign it to Carla.

> Who is free on Saturday afternoon? Assign the 3 unassigned jobs to them.

> Move all of Thursday's bookings to Friday at the same times and let each customer know.

> List customers with invoices unpaid for more than 14 days and send each one a friendly reminder.

> Which customers haven't booked in 60 days? Show their last service and total spent.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its BookingKoala tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"bookingkoala":{"command":"uvx","args":["bookingkoala-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t bookingkoala-mcp .
docker run -i --rm -e COTLET_API_KEY bookingkoala-mcp
```

Tools: `bookingkoala_guide`, `bookingkoala_status`, `bookingkoala_open`, `bookingkoala_read`, `bookingkoala_click`, `bookingkoala_type`, `bookingkoala_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install bookingkoala-mcp        # or run it once: uvx bookingkoala-mcp connect
bookingkoala-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 bookingkoala_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 bookingkoala_agent.py status    # is BookingKoala ready in your Cotlet.dev account
python3 bookingkoala_agent.py guide     # BookingKoala screens and sign-in link
python3 bookingkoala_agent.py read      # open BookingKoala, read the page, close the browser
python3 bookingkoala_agent.py tools     # list Cotlet.dev tools
python3 bookingkoala_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from BookingKoala users

**Does BookingKoala have an API?**

BookingKoala's integration docs point to Zapier and Make for connecting other apps. Cotlet.dev works in your BookingKoala account directly, so your AI agent can read and change your bookings and customers.

**How do I connect BookingKoala to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to BookingKoala once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no BookingKoala API key.

**Is there a way to use Claude with BookingKoala?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own BookingKoala account.

**Is there a BookingKoala MCP server?**

BookingKoala has no official MCP server. Cotlet.dev is a hosted MCP server that works in BookingKoala for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [BookingKoala on Cotlet.dev](https://cotlet.dev/integrations/bookingkoala-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=bookingkoala&utm_content=find)
- [PyPI package bookingkoala-mcp](https://pypi.org/project/bookingkoala-mcp/)
- [Odel](https://odel.app/modules/cotlet/bookingkoala)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-bookingkoala-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/bookingkoala-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=bookingkoala

Start free: https://cotlet.dev/signup?app=bookingkoala&utm_source=github&utm_medium=readme&utm_campaign=bookingkoala
