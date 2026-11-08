# Mendix Architect — documentation

Thirty-five views in six groups, arranged by what you are trying to do rather than by what the data
is. Version 1.1 added the Evolve group, eight views and two ways to use it outside Studio Pro; 1.2 added
the Production group, Naming and a Mendix 11 target; 1.3 added Page flow, Documentation, cleanup and
the first changes to the app, each confirmed by you.

| Guide | Covers |
|---|---|
| [Getting started](getting-started.md) | Install, first scan, what the numbers mean |
| [Explore](explore.md) | Explorer, Graph, Network, Domain, Paths, Impact, Cycles, Inventory, Workflows, Page flow, C4 model |
| [Review](review.md) | Recommendations, Rules (with Policies), Naming, Unused, Reach, Tests, Duplicates |
| [Cleanup](cleanup.md) | Delete, exclude and include unused documents, waves, the keep list |
| [Production](production.md) | Go-live, Security (with Sensitive data), Performance, Integrations, Translations |
| [Reports and CI](reports-and-ci.md) | Explain this app, guided review, dossier, SARIF, Compare |
| [Evolve](evolve.md) | Upgrade (Mendix 12, Java libraries, Mendix 11), Hotspots, Debt, module health |
| [Documentation](documentation.md) | Coverage, drafts, documentation set, deprecation register |
| [Studio Pro integration](studio-pro.md) | Right-click questions, editor tabs, Find Results, pickers, badge, tidy layout |
| [Agents and the command line](agents-and-cli.md) | MCP server for AI agents, CLI, pull-request gate |
| [Ask](ask.md) | Questions in plain language, local or cloud |
| [What it cannot see](limits.md) | The honest limits, and why each one exists |
| [Troubleshooting](troubleshooting.md) | When something looks wrong |

## The one idea worth reading first

Every number in this tool comes from the model, and the tool is careful about the difference
between *what it measured* and *what that means*.

Impact says "potentially affected", never "broken". Unused says "candidates", never "dead
code". Thresholds come from your app's own distribution, not from a rulebook, and every
finding shows what was measured and which threshold it crossed.

That is not hedging for its own sake. A tool that overstates once is a tool nobody checks
again, and the whole point of this one is that you can argue with it.

[What it cannot see](limits.md) is the shortest guide here and the most useful.
