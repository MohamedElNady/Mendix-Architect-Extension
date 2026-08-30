# Reports and CI

Getting the analysis out of the pane and to the people who need it.

## Explain this app

A written summary assembled from the model, for someone who does not yet know what to ask.
What the app is, how the outside world gets in, how it is put together, and what the scan
could not see.

Every figure is measured and nothing is inferred. The last section states the limits, and it
is there on purpose: a handover document that omits them hands over false confidence.

Exportable as Markdown.

## Guided review

The architecture review as an agenda, in an order that holds up: structure first, because a
cycle changes what every number below it means.

Each question already carries its answer, so you can see which are live on this app before
opening anything. Tick them off as you go, and jump straight to the tab holding the evidence
for any of them.

There is deliberately no overall score. A single number over these would be invented
weighting, and it would be quoted long after the detail behind it was forgotten.

Exportable as meeting minutes.

## Architecture dossier

Every tab's answer in one Markdown document: the narrative, the module table, a Mermaid
dependency diagram, the domain model, the interfaces, the Marketplace inventory and the
findings, with the blind spots stated at the end.

Markdown because it can be committed beside the code and diffed between releases. The diagram
is Mermaid, which renders on GitHub and in most wikis, for the same reason.

This is the artefact people mean when they ask for "the architecture documentation", and it is
generated rather than written, so it cannot go stale quietly.

## SARIF export

One SARIF 2.1.0 file containing every finding from Security, Recommendations, Reach, Domain
and Rules. GitHub Code Scanning, Azure DevOps, SonarQube and VS Code all read it with no
setup, so findings appear in the pull request next to the change.

Two deliberate choices:

**Nothing is ever emitted at severity `error`.** These are architectural opinions measured
against your app's own distribution. They must not fail a build.

**Marketplace modules are off by default.** A finding you cannot act on is noise on someone
else's pull request.

**No line numbers.** A Mendix document is a row in a binary `.mpr`, not a text file, so results
carry a *logical* location — the qualified name and document kind — and point at the `.mpr`
itself. Code Scanning lists every finding but cannot annotate a diff line, and the tab says so
rather than letting you discover it.

Findings also go to Studio Pro's own **Errors pane** automatically, so they are visible without
opening the extension at all.

## Compare

What a branch changed architecturally, against a saved scan.

The workflow is manual, and stated on screen rather than hidden behind a button that looks
automatic. `IVersionControlService` exposes the current branch's name, the head commit, and
whether the app is version controlled. Nothing more: no way to open another branch's model, and
no way to enumerate branches. So a comparison needs two scans that both actually happened.

Scan on the base branch and save it, switch branch in Studio Pro, rescan, compare.

It distinguishes a rename from an add plus a delete, a brand-new module coupling from one that
merely got heavier, and names cycles introduced and cycles resolved.

**Trend** places every saved scan by *when* it was taken rather than evenly, so a gap in the
record looks like a gap. A snapshot exists only where someone pressed save: this is a record of
when the tool was run, not of when the app changed, and the chart says so.

**Cross-app comparison** widens the list to snapshots from other apps on this machine, which is
how you see a shared module drifting apart between two applications. Off by default, and the
pane warns that document counts between two different apps are meaningless — read the module
coupling instead.
