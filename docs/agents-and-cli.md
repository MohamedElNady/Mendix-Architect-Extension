# Agents and the command line

*New in 1.1.* The same analysis outside the pane: for AI agents, and for pipelines.

Both are part of the module you installed. Nothing else needs downloading: they run on the Node
runtime that Studio Pro installs.

## MCP server for AI agents

**System → Agents → Start server.** An AI agent can then ask the questions the pane answers: what
to fix first, how much debt a module carries, what breaks if an entity is deleted, what blocks
Mendix 12.

- It speaks the Model Context Protocol, which Maia (Studio Pro 11.8 and later), Claude Code,
  Cursor, VS Code and most other agents support.
- It is **off until you start it**, listens on `127.0.0.1` only (port 7791 by default), refuses
  requests from web pages, and requires a token. It stops when Studio Pro closes.
- All 15 tools are **read-only**. They answer from the last scan; rescan in the pane to update what
  agents see.

The Agents tab shows a ready-made snippet for each client. The token is filled in only after you
tick *Show token*.

**Connecting Maia** (Studio Pro 11.8 and later):

1. **View → MCP Settings**, or the *Configure MCP Connections* icon under *Maia Chat*.
2. **Add MCP Server**: name *Mendix Architect*, URL `http://127.0.0.1:7791/mcp`, connection type
   **HTTP (Streamable)**.
3. **Authentication**: **Bearer Token**, and paste the token from the Agents tab.
4. Expand the card and enable the tools: tools from a new server start disabled.

## Command line and pull-request gate

The command-line tool is `extensions/MendixArchitect/cli/mendix-architect.mjs` in your app folder.
It reads the model with Mendix's own `mx` tool, so Studio Pro does not need to be running.

```bash
node mendix-architect.mjs scan   --mpr App.mpr --out scan.json
node mendix-architect.mjs check  --mpr App.mpr --base-mpr base/App.mpr --sarif out.sarif --summary gate.md
node mendix-architect.mjs diff   --base a.json --head b.json --out diff.md
node mendix-architect.mjs report --mpr App.mpr --out dossier.md
node mendix-architect.mjs c4     --mpr App.mpr --format structurizr --out workspace.dsl
```

`check` compares the pull request with its base branch and **fails only on findings that are new**,
so an existing app can adopt it without fixing everything first. Findings you accept can be
suppressed in the rule file with a reason; they are shown but never fail the gate.
`--fail-on new-warnings` ignores new notes, `any` fails on any finding, `never` only reports.
The summary also says how much debt the change adds and how much it pays off.

**System → CI** in the pane previews the gate against a saved scan and has pipeline snippets.
