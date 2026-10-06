# Changelog

## 1.1.0 — 2026-10-06

**Eight new views, a new Evolve group, and two ways to use it outside Studio Pro.** Verified live on
Studio Pro 10.24.10, 11.12.0 and 11.14.0 from one build.

**Explore** — *Workflows*: each workflow as a process diagram, and what can stall it (a task that
targets nobody, a task page no role may open, a workflow nothing starts). *C4 model*: context,
containers and modules, exported as Structurizr DSL, C4-PlantUML or Mermaid.

**Review** — *Tests*: what the unit tests reach, and the risky microflows none reach.
*Duplicates*: copied-and-renamed microflows and pages. *Sensitive data*: personal and secret
attributes, and whether anonymous users or external systems reach them. *Policies*: must and
must-not rules on individual elements, checked live.

**Evolve** (new) — *Upgrade*: what stands between the app and Mendix 12's React client, page by
page with rough hours, and Java library conflicts. *Hotspots*: what changes most and what changes
together, from Git history. *Debt*: every finding priced, summed into days, ranked by change
frequency.

**Outside Studio Pro** (new) — a command-line tool and pull-request gate that reads the model with
Mendix's `mx` tool and fails only on new findings; an MCP server so Maia, Claude Code, Cursor and
VS Code can ask the questions the pane answers. Both ship inside the module, run on Studio Pro's
own Node, and are read-only. The server is off until started, local only and token-protected.

**Charts** — every new view has charts (donuts, bar lists, scatters, heatmaps, flow and C4
diagrams) with a palette checked for colour-vision deficiency, in light and dark, down to a 380 px
docked pane and in Dutch.

**Changed** — the first time an app is opened after upgrading, it is scanned again (the cache
format changed). SARIF exports gain new rule groups (`upgrade`, `javalibs`, `history`, `tests`,
`policy`, `workflow`) and a fix time on every result, so the first pipeline run on 1.1 reports
those as new: accept them with a baseline, or run the gate with `--fail-on new-warnings`. The rule
file accepts three new optional sections: `sensitive`, `policies` and `debt`. Unnamed documents
are labelled by module, for example *Orders · Domain model*.

**Fixed** — a page or snippet parameter named like a module no longer resolves to that module;
project-level findings are no longer sent to Studio Pro's Errors pane, which shows only
document-level warnings; charts in narrow panes keep readable labels.

## 1.0.0 — 2026-08-30

First public release.

**Explore** — Explorer with search and filters, Find Usages, impact analysis, path finding
with chokepoints, dependency graph with lazy expansion, module network with cycle collapse
and a dependency-structure matrix, treemap, domain model, inventory of background load,
configuration and integration surface.

**Review** — recommendations on a refactor quadrant, security analyser with roles as nodes,
reachability across six kinds of entry point, removal candidates with confidence ratings,
layering rules with baseline generation, safe-delete simulation.

**Report** — "Explain this app" handover summary, guided architecture review, architecture
dossier, SARIF export for GitHub Code Scanning, Azure DevOps, SonarQube and VS Code, findings
in Studio Pro's own Errors pane, branch comparison against saved scans.

**Ask** — questions in plain language against a local model (Ollama) or any OpenAI-compatible
endpoint, answered from measured facts. A digest is sent, never the model.

**Dutch** — system menus, buttons and context menus. Element names stay as they are in your
model, and analysis prose stays in English where its wording is carefully hedged.

Verified on Studio Pro 10.24.10 and 11.12.2 from a single build.
