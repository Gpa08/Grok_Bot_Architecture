# GROK BOT $ARCHITECTURE

### THANK YOU TO EVERYONE SUPPORTING $ARCHITECTURE — THIS EXPERIENCE WAS BUILT FOR YOU, SO THE COMMUNITY CAN BECOME A VISIBLE PART OF THE PROJECT.
###  → https://archirecture-holders.com


**Autonomous multi-agent operations interface for research, production, evidence control, review, and human-approved delivery.**

![Grok Bot $ARCHITECTURE operations floor](preview.png)

Grok Bot $ARCHITECTURE turns a team of specialist AI agents into a visible operating system. Instead of hiding agent work behind a chat window, it presents the entire workflow as a live operations floor: bots move between workstations, exchange artifacts, report progress, emit telemetry, and stop at an approval boundary before consequential actions.

The included mission, **NS-INT-042**, demonstrates a complete competitor-intelligence workflow. At normal speed it runs for approximately five minutes and processes 24 sources, creates a structured evidence pack, performs an independent audit, and prepares a controlled release.

> Grok Bot $ARCHITECTURE is an independent interface concept and is not an official xAI product.

## What the interface provides

- A continuous pixel-art operations room with six visible specialist bots.
- Live agent movement through collision-aware office routes.
- Live Agent Comms with routed message cards, animated channels, and moving work packets between specialists.
- Real-time task labels such as `reading pricing pages`, `sourced 6 links`, and `cross-checking 24 citations`.
- Animated wall telemetry, workstation displays, city lights, and a real-time analog clock.
- A mission timeline with progress, ETA, cost, artifacts, and operational stages.
- A realistic event feed containing source discovery, handoffs, warnings, audit results, and system events.
- A cryptographic Mission Ledger with SHA-256 hashes, artifact versions, and parent lineage.
- A persistent visual release rail: `SOURCES → PACK → BRIEF → AUDIT → RELEASE`.
- Large in-room system notices for sealed artifacts, stale audits, and policy decisions.
- Audit invalidation when an already-reviewed artifact is revised.
- Human approval controls for external or high-impact actions.
- Responsive full-screen layout for desktop, laptop, tablet, and mobile widths.
- A GitHub-backed **LIVE** desk feed (`desk/comms.json`) so Chief of Staff can append real messages without a backend server.
- No framework, package installation, build process, or API key required.

## Agent team

The six floor bots are the live Grok Bot desk. Internal ids stay `helm` / `scout` / `forge` / `archive` / `sentinel` / `relay` so the NS-INT-042 demo still runs; the names and roles on the floor are the desk.

| Floor id | Name | Role | Typical output |
| --- | --- | --- | --- |
| **Helm** | Helm | Chief of Staff | Mission scope, delegation, desk decisions |
| **Scout** | Mimir | Crypto research | Funding, tape, verified crypto notes |
| **Forge** | Njord | US stocks | Session tape, breadth, equity signals |
| **Archive** | Heimdall | Market regime | Regime tags, volatility, hold/flip calls |
| **Sentinel** | Syn | Safety | Policy checks, airlock holds |
| **Relay** | Huginn | X monitor | Mention clusters, staged (never auto-posted) releases |

## Mission lifecycle

```text
Scope → Research → Synthesis → Evidence → Review → Release
```

1. **Helm** receives the objective and creates the work graph.
2. **Scout** collects and verifies 24 first-party sources.
3. Scout meets **Forge** at the handoff table and transfers the research pack.
4. Forge resolves conflicting claims and builds a 12-page intelligence brief.
5. **Archive** stores 18 traceable artifacts with citation backlinks.
6. **Sentinel** performs 12 structural, evidence, and safety checks.
7. **Relay** stages the audited release package.
8. The workflow pauses at the **Approval Airlock** until a human selects `Approve` or `Reject`.

## Quick start

Clone the repository:

```bash
git clone https://github.com/monokernn/Grok_Bot_Architecture.git
cd Grok_Bot_Architecture
```

The application is completely static. You can open `index.html` directly, or serve the directory locally:

```bash
npx serve .
```

Then open the URL printed in the terminal, normally `http://localhost:3000`.

You can also use Python:

```bash
python -m http.server 8080
```

Then visit `http://localhost:8080`.

## Operating guide

### Watch the live desk

This is the path Mike uses to monitor the real desk from the same pixel-art floor.

1. Serve the repository (do not open `index.html` as a `file://` URL — the browser cannot poll the desk file that way):

```bash
python -m http.server 8080
```

2. Open `http://localhost:8080` (or `http://localhost:8080/index.html?autoplay=live`).
3. Confirm the header badge reads **GROK LINK · LIVE** once `desk/comms.json` contains events. The footer says `LIVE` instead of `SIM`.
4. Watch **Live Agent Comms** for routed desk cards (`MIMIR → HELM`, `NJORD → HELM`, `HUGINN → HELM`, …). Agents move and update their task labels from the file.
5. To publish a new floor message, append an event to `desk/comms.json` and save. The floor polls every 3 seconds. If the file is updated via GitHub, pull or let Pages rebuild, then the next poll paints the card.

Chief of Staff can commit events from the desk without a backend. Copy the shape in `desk/comms.example.json`.

Preview the example (including an airlock hold) with:

```text
index.html?feed=desk/comms.example.json
```

### Run the NS-INT-042 demo

Start mission / NS-INT-042 is unchanged demo mode. It does not replace the live feed; it plays the canned competitor-intelligence timeline on the same floor.

1. Open the interface and confirm that all six agents show as online.
2. Select **Start mission** to begin NS-INT-042.
3. Watch the progress bar, remaining time, spend, agent statuses, and Live Feed.
4. Click any bot to inspect its current task and location.
5. Use the speed selector to run the workflow at `1x`, `2x`, `4x`, or `10x`.
6. When Huginn (Relay) reaches the Approval Airlock, select:
   - **Inspect** to review target, payload, rollback, and evidence.
   - **Reject** to block publication and return the mission for revision.
   - **Approve** to release the report and complete the mission.

Consequential desk actions (`trade`, `order`, `publish`, `execute`, or `approval: true`) always stop at the Approval Airlock. The floor never auto-executes a trade.

### Controls

| Control | Action |
| --- | --- |
| `Start mission` | Starts the mission timeline |
| Pause button | Pauses or resumes execution |
| Reset button | Returns agents and mission state to the beginning |
| `1x–10x` | Changes system speed |
| `Space` | Starts, pauses, or resumes |
| `R` | Resets the mission |
| Agent card or bot | Opens the current task and location |

## Interface map

- **Operations Floor** — spatial view of agents, desks, shared equipment, and handoffs.
- **Crew Manifest** — current state and assignment of every bot.
- **Live Feed** — timestamped operational telemetry.
- **Active Mission** — objective, stage, progress, ETA, and risk state.
- **Approval Airlock** — human decision boundary for consequential actions.

## Architecture

The current repository contains a self-contained browser implementation:

```text
Mission timeline
      ↓
Agent state machine
      ↓
Route and handoff engine
      ↓
Canvas room renderer
      ↓
Live Feed + mission telemetry + approval state
```

The visual layer is intentionally separated from the mission events. A real agent backend can replace the built-in timeline by sending the same state transitions over WebSocket, Server-Sent Events, or an MCP bridge.

### Mock Grok Bot transport

The browser currently loads `grokbot-adapter.js` before the interface engine. It provides a production-shaped local transport without making external requests:

- persistent session IDs stored in `localStorage`;
- realistic connection and command acknowledgement latency;
- heartbeat, uptime, queue-depth, and round-trip telemetry;
- mission start, pause, resume, and reset commands;
- approval request and resolution commands;
- a 40-event local telemetry buffer.

The header displays `SIM` next to `GROK LINK` while only the mock transport is active. When `desk/comms.json` has events, the adapter flips to live mode and the same badge reads `LIVE`. Replace `window.grokBot` with an adapter exposing the same methods to connect a real service without changing the canvas renderer or mission controls.

### GitHub-backed live desk feed

`grokbot-adapter.js` still owns the mock command/heartbeat transport, and now also polls `desk/comms.json` (override with `?feed=`). New events are emitted as `desk` packets. `app.js` feeds them through the existing `agent()`, `event()`, and `sendComm()` path — no second renderer.

Event shape:

```json
{
  "id": "desk-002",
  "missionId": "DESK-LIVE",
  "agent": "scout",
  "state": "working",
  "activity": "scanning BTC funding",
  "zone": "skill",
  "progress": 18,
  "timestamp": "2026-08-24T22:41:12Z",
  "from": "mimir",
  "to": "helm",
  "channel": "crypto",
  "title": "Funding flip",
  "text": "BTC funding flipped negative. Watching for a cascade, not trading it.",
  "tone": "amber"
}
```

`from` / `to` / `text` draw a Live Agent Comms card. `agent` / `state` / `activity` / `zone` move the bot. `approval: true` or `action: "trade"` opens the airlock and never places an order.

### Mission Ledger and artifact lineage

`mission-ledger.js` is a real event-sourced subsystem running in the browser:

- every ledger event includes the SHA-256 hash of the preceding event;
- artifact payloads are hashed using the Web Crypto API;
- every revision creates a new immutable artifact version;
- parent artifact IDs form a traceable lineage graph;
- an audit is bound to the exact hash it reviewed;
- changing an audited brief automatically marks that audit as stale;
- the release policy verifies lineage and the current audit hash before requesting human approval;
- the ledger, artifacts, and latest policy decision persist in `localStorage`.

Click **MISSION LEDGER** in the upper-left corner of the Operations Floor to inspect artifact passports and full hashes. The release rail stays visible along the bottom of the room and updates as the mission creates, audits, and approves work.

For the instant visual showcase, open:

```text
index.html?autoplay=ledger
```

This preloads a complete artifact lineage, opens the inspector, draws handoff packets across the room, and stops on the visible `APPROVAL REQUIRED` policy state.

### Live Agent Comms

Key mission handoffs now publish a visible inter-agent message. The demo still uses the same floor ids; the cards show desk names:

- Helm routes the research scope to Mimir;
- Mimir transfers the verified research pack to Njord;
- Njord sends the evidence bundle to Heimdall;
- Heimdall opens a lineage channel to Syn;
- Syn forwards the signed audit receipt to Huginn.

Live desk traffic uses the same panel. Open the floor over HTTP and the committed `desk/comms.json` events appear as soon as the adapter polls them. Open `index.html?autoplay=comms` for the canned three-channel showcase, or `index.html?autoplay=live` to watch the GitHub-backed file.

The Operations Floor draws the active channel directly between both bots, moves encrypted packets along the route, and keeps the three latest messages in the `LIVE AGENT COMMS` panel.

Suggested production event format (also used by `desk/comms.json`):

```json
{
  "missionId": "DESK-LIVE",
  "agent": "scout",
  "state": "working",
  "activity": "sourced 6 links",
  "zone": "library",
  "progress": 16,
  "timestamp": "2026-08-24T12:00:00Z",
  "from": "mimir",
  "to": "helm",
  "text": "Short comms card for the floor."
}
```

Consequential operations should always be represented as approval requests and must never be executed directly from a visual status event.

## Project structure

```text
.
├── index.html          Application shell and control panels
├── app.js              Mission engine, routing, agents, canvas renderer
├── grokbot-adapter.js  Mock transport, desk/comms.json poll, heartbeat
├── mission-ledger.js   Hash chain, artifact versions, lineage, policies
├── desk/comms.json     Live desk events (GitHub-backed, no server)
├── desk/comms.example.json  Copy-paste event shape + airlock example
├── styles.css          Base layout and component styles
├── theme-muted.css     Grok Bot $ARCHITECTURE theme and responsive rules
├── preview.png         Current interface preview
└── README.md           Product and operating documentation
```

## Customization

- Change agent names, roles, colors, and default positions in the `initial` array inside `app.js`.
- Append live desk messages to `desk/comms.json` (see `desk/comms.example.json`).
- Add or edit mission events in the `timeline` array.
- Adjust the five-minute runtime using `state.duration`.
- Add room destinations in the `points` object.
- Add artifact types and lineage relationships through `sealArtifact()` calls in the timeline.
- Change desktop and compact layouts in the `VIEWPORT-LOCKED RESPONSIVE SHELL` section of `theme-muted.css`.
- Replace events with backend messages while keeping the existing `agent()`, `event()`, and `stage()` update model.

## Current status

The interface, movement system, mission state machine, telemetry feed, mock transport, GitHub-backed desk feed, and approval flow run entirely in the browser. Open the floor, keep `desk/comms.json` updated, and watch Live Agent Comms. External broker/order execution is intentionally out of scope — the airlock is the stop.
