# Mendix Architect

**Understand a Mendix application without opening hundreds of documents.**

Mendix Architect is a Studio Pro extension for developers, technical leads and solution architects. It scans the model once and answers the questions that otherwise cost an afternoon of clicking: what depends on this, what breaks if I change it, what can I safely remove, what blocks Mendix 12, and how did this app end up shaped like this.

Version **1.1.0**. Works with Studio Pro **10.24.10 and later, including 11.x**, from a single build. Verified live on 10.24.10, 11.12.0 and 11.14.0.

Screenshots, a video and the full guides are on GitHub: https://github.com/MohamedElNady/Mendix-Architect-Extension

## Typical usage scenarios

- **Taking over an app.** Get a written handover summary, the module structure, the cycles and the riskiest areas before opening a single microflow.
- **Before changing something.** See everything that depends on an entity, attribute, microflow or page, and what would break if you removed it.
- **Cleaning up.** Find removal candidates, copied-and-renamed microflows and pages, and code no test reaches.
- **Planning the next release.** Size the Mendix 12 (React client) upgrade, find the hotspots in your Git history, and see your technical debt in days.
- **Reviewing a pull request.** Run the same analysis in your pipeline and fail only on findings that are new.
- **Working with AI agents.** Let Maia, Claude Code, Cursor or VS Code ask the same questions the pane answers.

## Features

The pane has 28 views in five groups.

**Explore**
- Explorer: search every document, filter by type and module, with usage counts
- Find usages, grouped by kind, each showing the property the reference came through
- Impact analysis, direct and indirect, depth-limited
- Paths: every route between two elements, and the chokepoints all routes pass through
- Dependency graph, module network with cycle collapse, and a dependency-structure matrix
- Treemap of the whole app, sized by weight and coloured by severity
- Domain model: entities, associations, and who reads or writes each
- Inventory of background load, configuration and integration surface
- Workflows (new in 1.1): each workflow as a process diagram, and what can stall it
- C4 model (new in 1.1): context, containers and modules, exported as Structurizr DSL, C4-PlantUML or Mermaid

**Review**
- Recommendations: what to split, simplify, move or replace
- Security: roles as first-class nodes, with a role inventory
- Sensitive data (new in 1.1): personal and secret attributes, and whether anonymous users or external systems can reach them
- Layering rules in a checked-in rule file, with baseline generation
- Policies (new in 1.1): must and must-not rules on individual elements, checked live
- Unused: removal candidates with a confidence rating and the reasoning behind it
- Reachability across six kinds of entry point
- Tests (new in 1.1): which microflows the unit tests reach, and the risky ones none reach
- Duplicates (new in 1.1): copied-and-renamed microflows and pages
- Safe delete: what breaks, and what is freed, if an element were removed

**Evolve** (new in 1.1)
- Upgrade: what stands between the app and Mendix 12's React client, page by page with rough hours, and Java library conflicts
- Hotspots: what changes most and what changes together, from the app's Git history
- Debt: every finding priced in minutes, summed into days, ranked by how often its document changes

**Report**
- Explain this app: a written handover summary
- Guided review: the architecture review as an agenda, each question with its answer
- Architecture dossier: every view's answer in one Markdown document
- SARIF export for GitHub Code Scanning, Azure DevOps, SonarQube and VS Code
- Findings in Studio Pro's own Errors pane
- Compare: what a branch changed architecturally

**System**
- Ask: questions in plain language, answered from the measured facts, using a local model (Ollama) or any OpenAI-compatible endpoint
- Agents (new in 1.1): an MCP server for AI agents
- CI (new in 1.1): a preview of the pull-request gate, and pipeline snippets
- Diagnostics: scan coverage and what the scanner saw
- English and Dutch

## Installation

1. Open your app in Studio Pro (10.24.10 or later) and sign in.
2. Open the Marketplace: **View → Marketplace**, or the Marketplace icon on the right of the top bar.
3. Search for **Mendix Architect** and open it.
4. Click **Download**.
5. In the **Import Module** dialog, choose **Add as a new module** and click **Import**.
6. Studio Pro asks whether to trust the module's extension. Choose **Trust module and enable extension**, then **OK**. No restart is needed.
7. Open it from **Extensions → Mendix Architect → Open Architect**.

**Updating from 1.0:** download 1.1.0 the same way and choose **Replace existing module**. The first time the app opens after the update, it is scanned again.

## Configuration

None is required. The first scan starts on its own: a 52 MB app takes 15 to 20 seconds, and the result is cached, so everything after it is instant, also after restarting Studio Pro. Click **Rescan** after you change the model.

Optional:
- **Rule file.** Layering rules, policies, sensitive attributes and your own debt prices live in `mendix-architect.rules.json` in the app folder, so they are reviewed and committed with the app. Create and edit it from **Review → Rules**.
- **Ask.** Point it at a local Ollama model, or at any OpenAI-compatible endpoint, under **System → Ask**.
- **AI agents.** Under **System → Agents**, click **Start server**. To connect Maia (Studio Pro 11.8 and later): **View → MCP Settings → Add MCP Server**, URL `http://127.0.0.1:7791/mcp`, connection type **HTTP (Streamable)**, authentication **Bearer Token** with the token from the Agents tab, then enable the tools.
- **Pipelines.** The command-line tool ships inside the module, at `extensions/MendixArchitect/cli/mendix-architect.mjs`. It runs on Node and reads the model with Mendix's own `mx` tool, so no Studio Pro is needed. **System → CI** has ready-made snippets for GitHub Actions and Azure DevOps.

## Privacy and security

- Your model never leaves your machine. The extension reads the open app and keeps the result in memory and in a local cache under your user profile. There is no telemetry.
- The extension, its command-line tool and its MCP server are **read-only**. They never change your model.
- The MCP server is off until you start it. It listens on `127.0.0.1` only, refuses requests from web pages, and requires a token.
- Ask is the only feature that contacts another machine, and only after you configure it. It sends a digest of measured facts (counts, coupling, findings), never document contents. With Ollama, nothing leaves the machine.
- Git authors are shown as opaque hashes, never names or e-mail addresses. Outbound calls are recorded by location only; headers and credentials are never read.

## Limitations

- **Impact means "potentially affected", not "broken".** A reference means something could be affected; the model cannot prove it will break.
- **Unused means "candidate", never "dead code".** A document can still be used by reflection or runtime configuration. Platform entry points, Mendix's "mark as used", URLs, excluded documents and Marketplace modules are ruled out first.
- **Java and JavaScript action bodies are not in the model**, only their signatures. Calls made from inside them are not visible.
- **XPath is read, not evaluated.** Names inside constraints are resolved against the model; anything that does not resolve is reported, not guessed.
- **There are no model-change events** in the Studio Pro extension API, so the scan does not refresh by itself: click Rescan.
- **Thresholds come from your app**, not from a rulebook, and every finding shows what was measured. Debt prices are averages: use them for order of magnitude and trend.
- **Hotspots needs Git history.** Without it, that view says so.
- Nothing is reported at severity `error`: these are architectural opinions and must not fail a build on their own.

## Troubleshooting

- **The extension does not appear under Extensions.** Make sure you chose *Trust module and enable extension* when importing. If you declined, re-open the app, or trust the module from the extension prompt.
- **A number looks wrong.** Open **System → Diagnostics**. It reports scan coverage, unresolved references by property, and the metamodel types the scanner saw. That page usually explains what happened without sharing your model.
- **The pipeline cannot find `mx`.** Pass `--mx`, set `MX_EXE`, or put `mx` on the PATH. Otherwise the tool looks for an installed Studio Pro that matches the app's version.

## Release notes: 1.1.0

- Eight new views and a new Evolve group: Workflows, C4 model, Tests, Duplicates, Sensitive data, Policies, Upgrade (Mendix 12), Hotspots and Debt.
- A command-line tool and pull-request gate that fails only on new findings.
- An MCP server for AI agents (Maia, Claude Code, Cursor, VS Code): local, token-protected, read-only.
- Charts in every new view, checked for colour-vision deficiency, in light and dark, and in Dutch.
- Changed: apps are scanned again once after updating. SARIF gains new rule groups and a fix time per result, so the first pipeline run on 1.1 reports those as new: accept them with a baseline, or run the gate with `--fail-on new-warnings`.
- Fixed: a page or snippet parameter named like a module no longer resolves to that module; project-level findings are no longer sent to the Errors pane.

## Support

Report problems or ideas on GitHub: https://github.com/MohamedElNady/Mendix-Architect-Extension/issues

When reporting a problem, include what **System → Diagnostics** shows.
