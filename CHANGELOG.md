# Changelog

## 1.3.0 — 2026-11-26

**Clean up, document, decide.** The biggest release so far, and the first that can change your app:
delete, exclude or include documents, rename, write documentation and tidy a domain model. Every
change is listed first, needs your confirmation, happens in one Studio Pro step and is never
committed for you. Two new views (Page flow, Documentation), new sections in six more, and 37 MCP
tools. Verified live on Studio Pro 10.24.10 and 11.14.0 from one build.

**Clean up, safely** (Review → Unused) — tick documents or a whole wave and delete them. Wave 1 is
what nothing references; wave 2 what only wave 1 references. Before anything goes, the view lists
every reference the selection would leave dangling and offers to add the documents that use them. The
app's Java and JavaScript are read too: a document named in code is never offered for deleting.
*Exclude* is the reversible alternative and reaches further (Java actions, documents named in code,
unit tests, each with a warning); **Excluded from the app** lists what is excluded today, with
*Include again*. A team **keep list** in the rule file, with a reason per entry. Deleting can be
undone with Version Control → Revert changes until you commit.

**Fewer false "unused"** — published OData services, business event services and unit tests run by
the UnitTesting module are ways into the app; scheduled events switched off locally still count
(the cloud decides); task queues are low confidence.

**Security** (Production → Security → Access) — who may create, read, write and delete each
entity, per user or module role, with a CSV for auditors; stored entities apart from in-memory ones.
**Pages and flows**: which roles may open each page and run each microflow or nanoflow. New rules
**SEC006** (a microflow keeps allowed roles although nothing in the browser calls it, so a user can
run it directly) and **SEC007** (allowed only for roles no user has). **Corrected:** SEC002 and
SEC003 described Mendix security backwards; a page or flow without allowed roles is open to no one,
not to everyone. Both are now low and say what happens: an access error.

**Explore** — *Page flow* (new): from the menu to every page, in clicks, through buttons, snippets
and the microflows that open pages, and what each page triggers. *Domain*: the **entity lifecycle**
(where each entity is created, changed, committed, deleted and retrieved, and tables that only grow),
a **deprecation register** (`@deprecated` in an element's Documentation; every remaining use becomes
finding DEP001), and **Tidy layout** for a module's domain model, previewed, with undo. *Network*:
modules that act as one, as merge suggestions.

**Change and review** (System → Compare) — **compare with any commit**: the commit's model is read
from Git history without touching your working copy. **Review of the change**: a summary for a pull
request, the new findings first (security on top), the documents with the widest reach, exported as
Markdown. The CLI does the same with `--base-commit` and `check --review`.

**Naming** — the **rename plan** lists every suggested rename, riskiest first; **Apply renames**
renames the low- and medium-risk ones in Studio Pro, which updates every reference, XPath included.
Undo renames the batch back.

**Evolve** — *Documentation* (new): coverage per kind and module and what to document first;
**drafts** written from what the model shows, never a guess, edited and then written into empty
Documentation fields; a **documentation set**, a page per module as HTML or Markdown. *Debt*:
**module health**, a grade from A to F with every deduction listed, and **work items** as a CSV for
Azure DevOps or Jira.

**More of Studio Pro** — right-click a document or entity: *How is this reached?*, *What breaks if
I delete this?*, *Page flow from here*, *Who can create, read, write and delete it?*, *Who can open
this page?*. Any view opens as an editor tab. Usages in Studio Pro's own Find Results, documents
from Studio Pro's own pickers, a badge for new findings, a notification when a long scan finishes,
and an Explorer that can follow the editor you have open.

**Also** — results from mxlint, mxcli lint and CLEVR Lint beside these findings (System → CI);
team labels and personal favourites in the Explorer; two microflow checks, MF008 (a boolean compared
with true or false) and MF009 (more than six parameters); the document types Studio Pro 11.x adds
(up to 11.15) are recognised. A calmer, Apple-like look, checked on every view down to 300 px.

**Agents** — 37 MCP tools. Four of them change the app (delete or exclude, include again, apply
renames, write documentation), each in two calls with a confirmation code, and Studio Pro shows its
own question dialog before anything happens.

**Changed** — the first time an app is opened after updating, it is scanned again. SARIF gains the
`deprecation` rule group and new rules (SEC006, SEC007, MF008, MF009, DEP001), so the first pipeline
run on 1.3 reports those as new: accept them with a baseline, or run the gate with
`--fail-on new-warnings`. The rule file accepts `keep` and `labels`.

## 1.2.0 — 2026-10-19

**Ready for production.** Five new views, a new **Production** group and the whole interface in Dutch.
Every check comes from Mendix's own guidance: the Best Practice Recommender, the naming, security and
error-handling best practices, the language settings and the 10 → 11 upgrade guide. Verified live on
Studio Pro 10.24.10 and 11.14.0 from one build.

**Production** (new group) — *Go-live*: the production review as a checklist of passed, warning and
blocker, answered from the model: security level, demo users, the administrator's default name,
password rules, strict mode, published services without authentication and constants sent to the
browser. Names and passwords are never read, and the checklist exports to Markdown. *Performance*:
commits, retrieves, deletes and service calls inside loops, also when they hide in a sub-microflow
the loop calls; pages that nest data containers three deep or fetch once per row; inheritance more
than two levels deep and calculated attributes on pages. *Integrations*: what every outbound call
does when the other side fails (default error handling, errors caught and then lost, no timeout,
hard-coded hosts), grouped by external system. *Translations*: per language, the texts users will not
read in their language and those they see as `[no translation]`. *Security* moves here from Review.

**Review** — *Naming*: prefixes checked against what each microflow actually does, such as a
scheduled-event prefix on a microflow no scheduled event runs; your own convention in the rule file.

**Evolve → Upgrade** — a *Mendix 11 target*: what the move from 10 to 11 breaks or deprecates
(document templates, the Deep Link module, `mx.logger`, comparisons with `''` whose meaning changes,
the Java version, a removed setting).

**Everywhere** — the whole interface is Dutch when you choose Dutch; element names and findings stay
as they are. Tab rows that do not fit show icons instead of hiding tabs, and **Go to** (Ctrl+K) has a
button in the title bar. The MCP server has 21 tools (six new: performance, integrations, naming,
translations, go-live and the Mendix 11 target).

**Changed** — the first time an app is opened after updating, it is scanned again. SARIF gains six
rule groups (`performance`, `integration`, `naming`, `translation`, `golive`, `mendix11`), so the
first pipeline run on 1.2 reports those as new: accept them with a baseline, or run the gate with
`--fail-on new-warnings`. The rule file accepts a `naming` section.

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
