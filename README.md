![Mendix Architect](brand/banner-1280x640.png)

# Mendix Architect

**Understand a Mendix application without opening hundreds of documents.**

A Studio Pro extension for developers, technical leads and solution architects. It scans the
model once and answers the questions that otherwise cost an afternoon of clicking: what
depends on this, what breaks if I change it, what can I safely remove, and how did this app
end up shaped like this.

Verified live on Studio Pro **10.24.10**, **11.12.0** and **11.14.0** from a single build, against a
52 MB app (2,887 documents / 14,318 references) and a 62-module app (9,258 documents / 58,388
references).

**Version 1.1.0.** What changed: [CHANGELOG.md](CHANGELOG.md).

---

## Install

Mendix Architect is installed from the Mendix Marketplace, like any other module.

1. Open your app in Studio Pro (10.24.10 or later, including 11.x) and sign in.
2. Open the Marketplace: **View → Marketplace**, or the Marketplace icon on the right of the top bar.
3. Search for **Mendix Architect** and open it.
4. Click **Download**.
5. In the **Import Module** dialog, choose **Add as a new module** and click **Import**.
6. Studio Pro asks whether to trust the module's extension: choose **Trust module and enable
   extension**, then **OK**. No restart is needed.
7. Open it from **Extensions → Mendix Architect → Open Architect**. The first scan starts on its own.

To update, download the new version the same way and choose **Replace existing module**.

The extension is read-only. It never writes to your model, and neither do its command-line tool
and its server for AI agents.

---

## Screenshots

All screenshots are of **NorthwindOps**, a demo application built for this purpose. Every
name in them is invented.

| | |
|---|---|
| ![Architecture overview](screenshots/01-architecture-overview.png) | ![Treemap](screenshots/02-treemap.png) |
| **Architecture overview** — composition, coupling, cycles | **Treemap** — the whole app, sized by weight, coloured by severity |
| ![Module network](screenshots/03-module-network.png) | ![Paths](screenshots/05-paths-and-chokepoints.png) |
| **Module network** — with the cost of extracting a module | **Paths** — every route between two elements, chokepoint named |
| ![Removal candidates](screenshots/07-removal-candidates.png) | ![SARIF export](screenshots/08-sarif-export.png) |
| **Removal candidates** — candidates, never "dead code" | **SARIF export** — findings in your pull request |

More: [Explorer](screenshots/04-explorer.png) ·
[Recommendations](screenshots/06-recommendations.png) ·
[Ask](screenshots/09-ask.png) ·
[Dutch](screenshots/10-dutch.png)

---

## What it does

### Find and follow

- **Explorer** — search every document, filter by type and module, with usage counts
- **Find Usages** — reverse dependencies grouped by kind, each showing the property the
  reference came through
- **Impact analysis** — direct and indirect, depth-limited, grouped by type
- **Paths** — every route between two elements, with the chokepoints every route passes
  through
- **Dependency graph** — layered subgraph with lazy expansion and clustering
- **Open in Studio Pro** — jump from any result to the real document

### See the shape of the app

- **Architecture overview** — composition, module coupling, cycles
- **Module network** — force-directed or layered, cycle collapse, dependency-structure matrix
- **Treemap** — the whole app in one picture, sized by weight and coloured by severity
- **Domain model** — entities, associations, and who reads or writes each
- **Coupling and instability metrics** — Martin's I, with tiers derived from your app
- **Workflows** *(1.1)* — each workflow as a process diagram, and what can stall it
- **C4 model** *(1.1)* — context, containers and modules, exported as Structurizr DSL,
  C4-PlantUML or Mermaid

### Judge it

- **Recommendations** — what to split, simplify, move or replace, on a refactor quadrant
- **Security analyser** — roles as first-class nodes, five rules, role inventory
- **Reachability** — six kinds of entry point, transitive dead-region detection
- **Unused** — removal candidates with a confidence rating and the reasoning behind it
- **Layering rules** — a checked-in rule file, baseline generation, violations that carry
  their evidence
- **Safe delete** — what breaks, and what is freed, if an element were removed
- **Tests** *(1.1)* — which microflows the unit tests reach, and the risky ones none reach
- **Duplicates** *(1.1)* — copied-and-renamed microflows and pages
- **Sensitive data** *(1.1)* — personal and secret attributes, and whether anonymous users or
  external systems can reach them
- **Policies** *(1.1)* — *must* and *must not* rules on individual elements, checked live

### Plan the next step *(new in 1.1)*

- **Upgrade** — what stands between the app and Mendix 12 (the React client), page by page,
  with rough hours, and Java library conflicts
- **Hotspots** — what changes most and what changes together, from the app's Git history
- **Debt** — every finding priced in minutes, summed into days, and ranked by how often its
  document changes

### Outside Studio Pro *(new in 1.1)*

- **Command line and pull-request gate** — the same analysis without Studio Pro, reading the model
  with Mendix's own `mx` tool; the gate fails only on findings that are new since the base branch
- **MCP server for AI agents** — Maia, Claude Code, Cursor, VS Code and other agents can ask the
  questions the pane answers; off until you start it, local only, token-protected

### Work with it

- **Explain this app** — a written handover summary assembled from the model
- **Guided review** — the architecture review as an agenda, each question carrying its answer
- **Architecture dossier** — every tab's answer in one Markdown document
- **SARIF export** — findings in GitHub Code Scanning, Azure DevOps, SonarQube or VS Code
- **Compare** — what a branch changed architecturally, against a saved scan
- **Ask** — questions in plain language, answered from the measured facts, against a local
  model (Ollama) or any OpenAI-compatible endpoint
- **Dutch** — system menus, buttons and context menus

---

## What it does not claim

This is the part worth reading before you rely on any number in it.

**Impact analysis says "potentially affected", not "broken".** A reference means something
*could* be affected by a change. The model cannot prove that it will break.

**Nothing is ever called dead code.** The Unused tab reports *candidates*, because absence of
a reference in the model is not absence in the running app. Before anything becomes a
candidate, six things are ruled out and counted: Mendix's own `markAsUsed` flag, a non-empty
`url`, exclusion from the app, platform entry points, structural containers, and Marketplace
modules.

**XPath is read lexically, not parsed.** Constraints are plain strings in the model and no
Mendix API parses them. Names inside a constraint are extracted and resolved against the
model, so a false match produces nothing rather than an invented reference. What that cannot
recover is reported rather than hidden.

**Java and JavaScript action bodies are not in the model.** Only the signature is. A Java
action calling another module's logic is not a visible dependency, and no tool built on the
Mendix APIs can see it.

**Thresholds come from your app, not from a rulebook.** "Long" means longer than the 90th
percentile of your own microflows. Every finding shows what was measured and which threshold
it crossed, so it can be argued with.

**Nothing is emitted at severity `error`.** These are architectural opinions measured against
your app's own distribution. They must not fail a build.

Coverage on the larger verification app: **96.2%** of references resolved to a scanned node,
2.2% self-referencing and correctly not drawn, **1.6%** unresolved. Of that 1.6%, all but
0.015% is two structural categories — page-local widget bindings, and Mendix's built-in
`System` module, which is not enumerated as a project module.

---

## Performance

A 52 MB, 2,282-document app scans in **15–20 seconds**. 93% of that is reading properties
from the model, not traversal.

The scan runs off Studio Pro's UI thread, so the IDE stays responsive, and reports live
progress rather than an indeterminate spinner. The result is cached, so everything after the
first scan is instant, and the cache survives restarting Studio Pro.

---

## Privacy

Your model never leaves your machine.

The extension reads the open app and holds the result in memory and in a local cache under
your user profile. Nothing is uploaded, and there is no telemetry.

The optional **Ask** feature is the only thing that makes a network call to another machine, and
only once you configure it. It sends a digest of measured facts — counts, module coupling, findings — and
never document contents. Point it at Ollama and nothing leaves the machine at all. If you use
a cloud endpoint, the API key is stored under your local application data, outside the app
folder, and is never sent back to the pane once saved.

The **MCP server** for AI agents is off until you start it. It listens on `127.0.0.1` only, refuses
requests from web pages and needs a token. Version history is read locally, and authors are shown
as opaque hashes, never names or e-mail addresses. Outbound calls are recorded by location only;
headers and credentials are never read.

---

## Requirements

| | |
|---|---|
| Studio Pro | 10.24.10 or later, including 11.x |
| .NET | 8.0 runtime, shipped with Studio Pro |
| Node | only for the optional command line and MCP server; the one Studio Pro installs is used |
| Platform | Windows and macOS |

---

## Documentation

Full guides live in [docs/](docs/README.md).

| Guide | Covers |
|---|---|
| [Getting started](docs/getting-started.md) | Install, first scan, reading the overview |
| [Explore](docs/explore.md) | Explorer, Graph, Network, Domain, Paths, Impact, Cycles, Inventory |
| [Review](docs/review.md) | Recommendations, Security, Rules, Unused, Reach |
| [Reports and CI](docs/reports-and-ci.md) | Explain this app, dossier, SARIF, Compare |
| [Evolve](docs/evolve.md) | Upgrade to Mendix 12, Hotspots, Debt *(1.1)* |
| [Agents and the command line](docs/agents-and-cli.md) | MCP server for AI agents, CLI and pull-request gate *(1.1)* |
| [Ask](docs/ask.md) | Questions in plain language, local or cloud |
| [What it cannot see](docs/limits.md) | The honest limits, and why each exists |
| [Troubleshooting](docs/troubleshooting.md) | When something looks wrong |

---

## Support

Open an issue on this repository.

When reporting a problem, the **System → Diagnostics** tab reports scan coverage, unresolved
references grouped by property, and the metamodel types it saw. That page is usually enough
to explain what happened without sharing your model.

---

## Licence

Commercial. See [LICENSE](LICENSE). The source is not distributed.

© 2026 Mohamed El Nady. All rights reserved.
