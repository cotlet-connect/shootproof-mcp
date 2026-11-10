# How to connect ShootProof to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your ShootProof account.** ShootProof offers a developer API for custom integrations, but it is not a ready-made ChatGPT app or Claude connector. Cotlet.dev connects your own signed-in ShootProof account to any AI agent, so you can ask in plain words and the AI handles galleries, orders and contracts for you.

## What you can ask

> Send Emma and Jake Miller their wedding gallery from Saturday and set it to expire in 60 days.

> Which orders from the last 7 days are still open? List the client, total and print items.

> Send my wedding contract to Olivia Chen for her June 14 date and ask her to sign by Friday.

> Who hasn't signed their contract after 5 days? Draft a friendly reminder for each of them.

> Which galleries had visitors but no orders in the last 14 days? Draft a print sale email for those 12 clients.

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

This repo is a real MCP server. It speaks MCP over stdio, lists its ShootProof tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"shootproof":{"command":"uvx","args":["shootproof-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t shootproof-mcp .
docker run -i --rm -e COTLET_API_KEY shootproof-mcp
```

Tools: `shootproof_guide`, `shootproof_status`, `shootproof_open`, `shootproof_read`, `shootproof_click`, `shootproof_type`, `shootproof_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install shootproof-mcp        # or run it once: uvx shootproof-mcp connect
shootproof-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 shootproof_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 shootproof_agent.py status    # is ShootProof ready in your Cotlet.dev account
python3 shootproof_agent.py guide     # ShootProof screens and sign-in link
python3 shootproof_agent.py read      # open ShootProof, read the page, close the browser
python3 shootproof_agent.py tools     # list Cotlet.dev tools
python3 shootproof_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from ShootProof users

**Does ShootProof have an API?**

ShootProof has an OAuth API that is free with an account, but you get a client ID only by emailing ShootProof support, then build an app. Cotlet.dev works in your own signed-in ShootProof account instead, so your AI agent can deliver galleries, send contracts and check orders.

**How do I connect ShootProof to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to ShootProof once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no ShootProof API key.

**Is there a way to use Claude with ShootProof?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own ShootProof account.

**Is there a ShootProof MCP server?**

ShootProof has no official MCP server and no official app in ChatGPT or Claude (checked November 2026). Cotlet.dev is a hosted ShootProof MCP server that works in your own account, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [ShootProof on Cotlet.dev](https://cotlet.dev/integrations/shootproof-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=shootproof&utm_content=find)
- [PyPI package shootproof-mcp](https://pypi.org/project/shootproof-mcp/)
- [Odel](https://odel.app/modules/cotlet/shootproof)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-shootproof-to-ai-agents-guide)

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
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/shootproof-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=shootproof

Start free: https://cotlet.dev/signup?app=shootproof&utm_source=github&utm_medium=readme&utm_campaign=shootproof
