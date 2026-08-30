# What it cannot see

Read this one. Everything else in the tool is easier to trust once you know where it stops.

None of these are hidden in the UI. Each tab states its own limits where the numbers appear.

## Four things no Mendix extension can see

**Java and JavaScript action bodies are not in the model.** Only the signature is. A Java
action that calls another module's logic is not a visible dependency, and no tool built on
the Mendix APIs can make it one.

**XPath constraints are plain strings.** No Mendix API parses XPath. This extension reads
them *lexically*: it extracts names and resolves each against the model, so a string that
merely looks like a qualified name produces nothing. The failure mode is a missed reference,
never an invented one. What it recovers and what it could not are both counted and reported.

**There are no model-change events.** The C# API exposes only `ActiveDocumentChanged`. An
incremental refresh is impossible, which is why rescanning is a button.

**Studio Pro does not report its own version.** The host process file version is read
instead, and labelled as such.

## What the analysis will not claim

**Impact says "potentially affected".** A reference means something *could* be affected by a
change. The model cannot prove it will break, and a tool that said "broken" would be wrong
often enough to be ignored.

**Nothing is called dead code.** The Unused tab reports *candidates*. Six things are ruled
out first, each counted so the number is explainable:

| Ruled out | Why |
|---|---|
| `markAsUsed` is set | Mendix's own flag for documents invoked in ways the model cannot express. Authoritative, never second-guessed |
| A `url` is set | Reachable by direct link with no model reference at all |
| `excluded` is set | Not part of the running app |
| Platform entry points | Scheduled events, navigation, published services. Nothing references these because they are what the platform calls into |
| Structural containers | Modules, folders, domain models. A folder with no inbound reference is not a finding |
| Marketplace modules | Not code you maintain. Includable via a toggle |

Even after all six, the answer is "no entry point reaches this", which is a stronger test
than "nothing references it" and still not proof. Run **What breaks if I delete this?** before
acting.

**Thresholds are yours, not ours.** "Long" means longer than the 90th percentile of *your*
microflows. Below eight samples a percentile means nothing, so the engine falls back to a
fixed floor and says which it used. Every finding shows what was measured and which threshold
it crossed.

**Nothing is emitted at severity `error`.** These are architectural opinions measured against
your app's distribution. An opinion that fails a build stops being useful within a week.

**Delete and commit leave no trace at entity level.** A Delete activity takes a *variable*,
not an entity type, so an entity that is only ever deleted looks unwritten in the domain
model. Passing an object to a sub-microflow counts as neither a read nor a write.

## Coverage, measured

On the larger verification app — 62 modules, 9,258 documents, 58,388 references:

| | Count | Share |
|---|---|---|
| Resolved to a scanned node | 311,822 | **96.2%** |
| Self-referencing, correctly not drawn | 7,073 | 2.2% |
| Unresolved | 5,178 | **1.6%** |

Of that 1.6%, all but **0.015%** is two structural categories: page-local widget bindings
(`grid1`, `Risk`), which are page-internal and not document references; and Mendix's built-in
`System` module, which is not enumerated as a project module and is therefore outside the
model by construction.

That leaves 49 genuinely unresolved references out of 324,073.

The **System → Diagnostics** tab reports these numbers for *your* app, grouped by the property
each unresolved reference came through.

## A number that used to be wrong

This was reported as 3.8% unresolved until the names behind it were sampled. Sixty per cent of
that figure turned out to be self-references: an entity access rule granting permission on
`Module.Login.Username` folds the attribute up to `Module.Login`, which is the element holding
the rule. The scan resolved it perfectly and then correctly declined to draw a node depending
on itself.

That is not a coverage gap, and counting it as one overstated the number this page exists to
report honestly. They are counted separately now.
