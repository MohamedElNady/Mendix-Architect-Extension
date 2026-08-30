# Troubleshooting

## The pane is empty, or says "No app open"

Open an app in Studio Pro first. The extension reads the model of the app you have open and
has nothing to show without one.

## Changes in Studio Pro are not reflected

Press **Rescan**. Nothing watches the model for you: the C# Extensibility API exposes no
model-change event, so no extension can refresh automatically. This is a documented limit, not
a bug.

## The scan is slow

15–20 seconds on a 52 MB app is expected, and about 93% of it is reading properties out of the
model. That is the cost of seeing every reference rather than inferring from names.

It runs off Studio Pro's UI thread, so the IDE stays usable, and the result is cached — you pay
it once per change, not once per question.

## A number looks wrong

Open **System → Diagnostics**. It reports, for your app:

- References resolved, unresolved, and self-referencing, counted separately
- Unresolved references grouped by the property they came through, with examples
- Which metamodel types were seen, and how many of each
- XPath constraints found, references recovered from them, and the ones that named nothing

That page usually explains the discrepancy without anyone needing to see your model. If you
report a problem, it is the most useful thing to include.

## Something says a document is unused and it is not

That is why it says *candidates*. See [what it cannot see](limits.md): a document can be
reached from Java, from a deep link, or from an XPath constraint, and the first two are
invisible to any Mendix API.

If Mendix's own **Mark as used** flag is set, the tool honours it and will never list the
document. That flag is the supported way to tell any tool that something is invoked in a way
the model cannot express.

## A tab throws an error

Each tab is wrapped so one failure costs that tab and not the session. The message is shown
rather than hidden, because there is nothing sensitive in it that the pane is not already
displaying, and it is the only trace that survives — Studio Pro's WebView has no reachable
console.

Switch tabs and back, or rescan. If it persists, the message plus which tab you were on is
enough to reproduce it.

## Ask cannot connect

**HTTP 404** usually means the endpoint is missing its `/v1` suffix. Ollama's OpenAI-compatible
API lives at `http://localhost:11434/v1`, not `http://localhost:11434`. The tool appends it
when the path is empty, but a wrong path is left alone.

**HTTP 401** means the key. **Test connection** distinguishes the two and returns the model
list when it succeeds.

## Findings do not appear in Studio Pro's Errors pane

They are pushed when a scan completes. If the pane has never been opened in this session, open
it once. Failure is silent by design — it degrades to "no warnings in the Errors pane", which
is the state before the feature existed.

## Reporting a problem

Open an issue on this repository. Include:

- Studio Pro version
- What you did, and what you expected
- The **Diagnostics** tab contents

Please do not attach a `.mpr` or a scan export. Both contain every qualified name in your
application, and Diagnostics is almost always enough.
