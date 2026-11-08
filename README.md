![Mendix Architect](brand/banner-1280x640.png)

# Mendix Architect

**Understand a Mendix application without opening hundreds of documents.**

A Studio Pro extension for developers, technical leads and solution architects. It scans the
model once and answers the questions that otherwise cost an afternoon of clicking: what
depends on this, what breaks if I change it, what can I safely remove, and how did this app
end up shaped like this.

Verified live on Studio Pro **10.24.10**, **11.12.0** and **11.14.0** from a single build (1.2 and 1.3: on 10.24.10 and 11.14.0), against a
52 MB app (2,887 documents / 14,318 references) and a 62-module app (9,258 documents / 58,388
references).

**Version 1.3.0.** What changed: [CHANGELOG.md](CHANGELOG.md).

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

The extension reads your app. It changes something only when you ask for it: deleting, excluding or
including documents, renaming, writing documentation or tidying a domain model. Each change is listed
first, needs your confirmation, happens in one Studio Pro step and is never committed for you. The
command-line tool never changes anything.

---

## What's new in 1.3.0

[![Mendix Architect 1.3 — what's new (video, 3:38)](video/mendix-architect-1.3-cover.png)](https://youtu.be/qnJHF9jg8OM)

▶ **[Watch the 1.3 video on YouTube](https://youtu.be/qnJHF9jg8OM)** (3 min 38 s, with voice-over; [download](video/mendix-architect-1.3-whats-new.mp4)):
what Mendix Architect already does, the 1.3 features, and what comes next.

**Clean up, document, decide.** The first release that can change your app, and only when you confirm: every
change is listed first, happens in one Studio Pro step and is never committed for you. Full notes:
[CHANGELOG.md](CHANGELOG.md).

| Area | New in 1.3.0 |
|---|---|
| **Clean up** | Delete or exclude unused documents in waves, with a check for references left dangling · *Include again* · a team keep list · Java and JavaScript read, so code that names a document protects it |
| **Security** | **Access matrix**: who may create, read, write and delete each entity · which roles may open each page and run each flow · new rules SEC006 and SEC007 |
| **Explore** | **Page flow**: from the menu to every page, in clicks · **entity lifecycle** · **deprecation register** · **tidy layout** for a domain model · modules that act as one |
| **Change and review** | **Compare with any commit**, read from Git · **review of the change** for pull requests · module health grades A to F |
| **Naming** | Rename plan, and **Apply renames**: Studio Pro updates every reference, XPath included, with undo |
| **Documentation** | Coverage, **drafts** written from the model, a **documentation set** per module as HTML or Markdown |
| **Studio Pro** | Right-click questions, any view as an editor tab, Find Results, pickers, a badge for new findings |
| **Also** | Work items for Azure DevOps or Jira · results from mxlint, mxcli lint and CLEVR Lint · labels and favourites · 37 MCP tools · an Apple-like look |

The screenshots use **Contoso Logistics**, an invented demo app. Every name in them is made up.

| | |
|---|---|
| ![Cleanup](screenshots/29-cleanup.png) | ![Delete confirmation](screenshots/30-delete-confirmation.png) |
| **Cleanup** — waves, and why the rest stays | **Confirmation** — the full list, before anything changes |
| ![Access matrix](screenshots/31-access-matrix.png) | ![Pages and flows](screenshots/32-pages-and-flows-access.png) |
| **Access matrix** — who may change each entity | **Pages and flows** — which roles may open and run what |
| ![Page flow](screenshots/33-page-flow.png) | ![Review of the change](screenshots/34-review-of-the-change.png) |
| **Page flow** — from the menu to every page | **Review of the change** — for a pull request |
| ![Apply renames](screenshots/36-apply-renames.png) | ![Entity lifecycle](screenshots/37-entity-lifecycle.png) |
| **Apply renames** — safe ones ticked, Studio Pro updates references | **Entity lifecycle** — created, changed, deleted, and what deserves a look |
| ![Documentation set](screenshots/40-documentation-set.png) | ![Tidy layout](screenshots/38-domain-tidy.png) |
| **Documentation set** — a page per module | **Tidy layout** — a domain model, before and after |

More: [Module health](screenshots/35-module-health.png) ·
[Documentation coverage](screenshots/39-documentation.png) ·
[Documentation drafts](screenshots/41-documentation-drafts.png)

---

## What's new in 1.2.0

[![Mendix Architect 1.2 — what's new (video, 2:47)](video/mendix-architect-1.2-cover.png)](https://youtu.be/CBsv5-0Jl5Y)

▶ **[Watch the 1.2 video on YouTube](https://youtu.be/CBsv5-0Jl5Y)** (2 min 47 s, with voice-over; [download](video/mendix-architect-1.2-whats-new.mp4)):
a short tour of what Mendix Architect already does, the 1.2 features, and what comes in 1.3.

**Ready for production.** A new **Production** group, built from Mendix's own best practices, and the whole
interface in Dutch. Full notes: [CHANGELOG.md](CHANGELOG.md).

| Area | New in 1.2.0 |
|---|---|
| **Production** *(new group)* | **Go-live** — the production review as a checklist, answered from the model; names and passwords are never read · **Performance** — work inside loops (also hidden in a sub-microflow), deep page nesting, per-row fetches · **Integrations** — what every outbound call does when the other side fails · **Translations** — what users will not read in their own language · **Security** moves here |
| **Review** | **Naming** — do the prefixes tell the truth about what each microflow does? |
| **Evolve** | **Mendix 11 target** — what the move from 10 to 11 breaks or deprecates |
| **Everywhere** | The whole interface in **Dutch** · tab rows that switch to icons instead of hiding tabs · **Go to** (Ctrl+K) in the title bar · **21 MCP tools** |
| **Changed** | The app is scanned again once after updating. The first pipeline run on 1.2 reports the six new rule groups as new: accept them with a baseline, or use `--fail-on new-warnings` |

The screenshots use **Contoso Logistics**, an invented demo app. Every name in them is made up.

| | |
|---|---|
| ![Go-live](screenshots/22-go-live.png) | ![Performance](screenshots/23-performance.png) |
| **Go-live** — readiness, by area, every check with its evidence | **Performance** — what runs inside loops, and pages by nesting depth |
| ![Integrations](screenshots/24-integrations.png) | ![Translations](screenshots/25-translations.png) |
| **Integrations** — how failures are handled, by external system | **Translations** — coverage per language and kind of document |
| ![Naming](screenshots/26-naming.png) | ![Mendix 11 target](screenshots/27-mendix-11-target.png) |
| **Naming** — prefixes against what each microflow does | **Mendix 11 target** — what the upgrade from 10 touches |

More: [Go-live in Dutch](screenshots/28-dutch.png)

---

## What's new in 1.1.0

[![Mendix Architect 1.1 — what's new (video, 2:47)](video/mendix-architect-1.1-cover.png)](video/mendix-architect-1.1-whats-new.mp4)

▶ **[Watch the 1.1 video](video/mendix-architect-1.1-whats-new.mp4)** (2 min 47 s, with voice-over).

Eight new views, a new **Evolve** group, and two ways to use the analysis outside Studio Pro.
Full notes: [CHANGELOG.md](CHANGELOG.md).

| Area | New in 1.1.0 |
|---|---|
| **Explore** | **Workflows** — each workflow as a process diagram, and what can stall it · **C4 model** — context, containers and modules, exported as Structurizr DSL, C4-PlantUML or Mermaid |
| **Review** | **Tests** — what the unit tests reach, and the risky microflows none reach · **Duplicates** — copied-and-renamed microflows and pages · **Sensitive data** — personal and secret attributes, and who can reach them · **Policies** — must and must-not rules on individual elements |
| **Evolve** *(new group)* | **Upgrade** — what stands between the app and Mendix 12's React client, with rough hours, and Java library conflicts · **Hotspots** — what changes most and together, from Git history · **Debt** — every finding priced, summed into days |
| **Outside Studio Pro** | **Command line and pull-request gate** — fails only on new findings · **MCP server** — Maia, Claude Code, Cursor and VS Code can ask the analysis |
| **Changed** | The app is scanned again once after upgrading. The first pipeline run on 1.1 reports the new rule groups as new: accept them with a baseline, or use `--fail-on new-warnings` |

The 1.1 screenshots use **Contoso Logistics**, an invented demo app. Every name in them is made up.

| | |
|---|---|
| ![Workflows](screenshots/11-workflows.png) | ![C4 model](screenshots/12-c4-model.png) |
| **Workflows** — process diagram, who each task targets, what can stall | **C4 model** — containers drawn from the model, ready to export |
| ![Sensitive data](screenshots/15-sensitive-data.png) | ![Policies](screenshots/16-policies.png) |
| **Sensitive data** — where personal data travels, and who reaches it | **Policies** — rules on elements, with the violations and their evidence |
| ![Upgrade](screenshots/17-upgrade-mendix-12.png) | ![Hotspots](screenshots/18-hotspots.png) |
| **Upgrade** — Mendix 12 readiness, page by page | **Hotspots** — changes against size, from Git history |
| ![Technical debt](screenshots/19-technical-debt.png) | ![Agents](screenshots/20-agents-mcp.png) |
| **Debt** — every finding priced, by area and module | **Agents** — the MCP server and how to connect Maia |

More: [Tests](screenshots/13-tests.png) ·
[Duplicates](screenshots/14-duplicates.png) ·
[Pull-request gate](screenshots/21-ci-gate.png)

---

## Screenshots

These screenshots, from 1.0, are of **NorthwindOps**, a demo application built for this purpose.
Every name in them is invented.

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
- **Right-click questions** *(1.3)* — in Studio Pro: how is this reached, what breaks if I delete it,
  who may use it; any view as an editor tab; usages in Studio Pro's own Find Results
- **Follow the editor** *(1.3)* — the Explorer selects whatever you open in Studio Pro

### See the shape of the app

- **Architecture overview** — composition, module coupling, cycles
- **Module network** — force-directed or layered, cycle collapse, dependency-structure matrix
- **Treemap** — the whole app in one picture, sized by weight and coloured by severity
- **Domain model** — entities, associations, and who reads or writes each
- **Entity lifecycle** *(1.3)* — where each entity is created, changed, committed and deleted
- **Page flow** *(1.3)* — from the menu to every page, in clicks, and what each page triggers
- **Deprecation register** *(1.3)* — `@deprecated` in the Documentation, and every use left
- **Tidy layout** *(1.3)* — rearranges a module's domain model, previewed, with undo
- **Coupling and instability metrics** — Martin's I, with tiers derived from your app
- **Workflows** *(1.1)* — each workflow as a process diagram, and what can stall it
- **C4 model** *(1.1)* — context, containers and modules, exported as Structurizr DSL,
  C4-PlantUML or Mermaid

### Judge it

- **Recommendations** — what to split, simplify, move or replace, on a refactor quadrant
- **Naming** *(1.2)* — prefixes and suffixes checked against what each element actually does; from 1.3 a
  rename plan, and **Apply renames** with undo
- **Reachability** — six kinds of entry point, transitive dead-region detection
- **Unused** — removal candidates with a confidence rating and the reasoning behind it; from 1.3
  **cleanup**: delete or exclude in waves, include again, a team keep list
- **Layering rules** — a checked-in rule file, baseline generation, violations that carry
  their evidence
- **Safe delete** — what breaks, and what is freed, if an element were removed
- **Tests** *(1.1)* — which microflows the unit tests reach, and the risky ones none reach
- **Duplicates** *(1.1)* — copied-and-renamed microflows and pages
- **Sensitive data** *(1.1)* — personal and secret attributes, and whether anonymous users or
  external systems can reach them
- **Policies** *(1.1)* — *must* and *must not* rules on individual elements, checked live

### Get it ready for production *(new in 1.2)*

- **Go-live checklist** — the production review as passed, warning or blocker: security level, demo
  users, the administrator's default name, password rules, strict mode, services without
  authentication, constants sent to the browser; names and passwords are never read
- **Security analyser** — roles as first-class nodes, role inventory, sensitive data *(1.1)*; from 1.3 the
  **access matrix** (entities, pages and flows per role)
- **Performance** — commits, retrieves, deletes and service calls inside loops, also hidden in a
  sub-microflow; deep page nesting and per-row fetches; inheritance depth and calculated attributes
- **Integrations** — what every outbound call does when the other side fails, by external system
- **Translations** — per language, what users will not read in their own language

### Plan the next step *(new in 1.1)*

- **Upgrade** — what stands between the app and Mendix 12 (the React client), page by page,
  with rough hours, and Java library conflicts; from 1.2 also the Mendix 11 target, for apps on 10
- **Hotspots** — what changes most and what changes together, from the app's Git history
- **Debt** — every finding priced in minutes, summed into days, and ranked by how often its
  document changes; from 1.3 **module health** grades and work items for Azure DevOps or Jira
- **Documentation** *(1.3)* — coverage, drafts written from the model, and a documentation set

### Outside Studio Pro *(new in 1.1)*

- **Command line and pull-request gate** — the same analysis without Studio Pro, reading the model
  with Mendix's own `mx` tool; the gate fails only on findings that are new since the base branch
- **MCP server for AI agents** — Maia, Claude Code, Cursor, VS Code and other agents can ask the
  questions the pane answers; off until you start it, local only, token-protected; 37 tools from 1.3,
  four of which change the app only after a confirmation code and Studio Pro's own dialog

### Work with it

- **Explain this app** — a written handover summary assembled from the model
- **Guided review** — the architecture review as an agenda, each question carrying its answer
- **Architecture dossier** — every tab's answer in one Markdown document
- **SARIF export** — findings in GitHub Code Scanning, Azure DevOps, SonarQube or VS Code
- **Compare** — what a branch changed architecturally, against a saved scan or *(1.3)* any commit,
  with a review of the change for pull requests
- **Ask** — questions in plain language, answered from the measured facts, against a local
  model (Ollama) or any OpenAI-compatible endpoint
- **Dutch** — the whole interface *(1.2)*; element names and findings stay as they are

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

**Changes to your app** happen only when you confirm them, in one Studio Pro step, and are never
committed: review them in Studio Pro's Changes pane. Before a delete, the list is saved to
`%LOCALAPPDATA%\MendixArchitect` so you know what went.

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
| [Review](docs/review.md) | Recommendations, Rules, Naming, Unused, Reach, Tests, Duplicates |
| [Cleanup](docs/cleanup.md) | Delete, exclude and include documents, waves, the keep list *(1.3)* |
| [Production](docs/production.md) | Go-live, Security, Performance, Integrations, Translations *(1.2)* |
| [Reports and CI](docs/reports-and-ci.md) | Explain this app, dossier, SARIF, Compare |
| [Evolve](docs/evolve.md) | Upgrade to Mendix 12 and 11, Hotspots, Debt, module health |
| [Documentation](docs/documentation.md) | Coverage, drafts, documentation set, deprecation register *(1.3)* |
| [Studio Pro integration](docs/studio-pro.md) | Right-click questions, editor tabs, Find Results, badge *(1.3)* |
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
