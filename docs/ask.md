# Ask

Questions about the app in plain language, answered from what the scan measured.

## What gets sent

A **digest of measured facts**: module coupling, entry points, the circular groups, entity
read and write counts, findings, composition. Counts and names, no document contents.

Your model is not uploaded. The `.mpr` never leaves the machine.

## Local, or cloud

**Local model (Ollama).** Point it at `http://localhost:11434/v1` and nothing leaves the
laptop at all. This is the right answer for customer work.

**Cloud.** Any OpenAI-compatible endpoint: OpenAI, NVIDIA NIM, Groq, Together and others all
speak the same protocol, so there is one code path rather than several that drift.

The extension makes the call, not the pane. A browser cannot reach `localhost:11434` from a
page served by Studio Pro's web server — both are cross-origin, and Ollama refuses browser
origins unless reconfigured. Proxying through the extension sidesteps that, and it means the
API key never reaches the WebView at all.

## Where the key lives

Under your local application data, outside the app folder. An API key has no business anywhere
near a repository.

It is written once and never sent back to the pane, which is why the field shows only whether
a key exists rather than the key itself. **Remove** deletes the stored connection rather than
blanking it.

**Test connection** proves the endpoint, the key and the network in one call, and returns the
provider's model list — which is what makes the model box fillable rather than guessable.

## What it is good at

Questions that would otherwise mean cross-referencing several tabs:

- Which module is most depended on?
- How many entities are on an external contract?
- What is in the biggest circular group?
- How much of this app can no entry point reach?
- What would it cost to extract the Orders module?

It answers from the same numbers the tabs show, and tells you which tab to check.

## What it is not

The pane says this before you type anything, and it is worth repeating:

> Answers come from what the scan measured, and the model can still be wrong — check anything
> that matters against the tab it came from.

Grounding a model in measured facts is a great deal better than letting it improvise about
code it has never seen. It is not a substitute for the tab that owns the number.
