# Mendix Architect — documentation

Twenty tabs, grouped by what you are trying to do rather than by what the data is.

| Guide | Covers |
|---|---|
| [Getting started](getting-started.md) | Install, first scan, what the numbers mean |
| [Explore](explore.md) | Explorer, Graph, Network, Domain, Paths, Impact, Cycles, Inventory |
| [Review](review.md) | Recommendations, Security, Rules, Unused, Reach |
| [Reports and CI](reports-and-ci.md) | Explain this app, guided review, dossier, SARIF, Compare |
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
