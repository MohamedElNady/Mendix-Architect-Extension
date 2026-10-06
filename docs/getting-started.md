# Getting started

## Install

Mendix Architect is installed from the Mendix Marketplace, like any other module.

1. Open your app in Studio Pro (10.24.10 or later, including 11.x) and sign in.
2. Open the Marketplace: **View → Marketplace**, or the Marketplace icon on the right of the top bar.
3. Search for **Mendix Architect** and open it.
4. Click **Download**.
5. In the **Import Module** dialog, choose **Add as a new module** and click **Import**.
6. Studio Pro asks whether to trust the module's extension: choose **Trust module and enable
   extension**, then **OK**. No restart is needed.
7. Open it from **Extensions → Mendix Architect → Open Architect**. The first scan starts on its own.

To update, download the new version the same way and choose **Replace existing module**.

The pane docks like any other. It is read-only and never writes to your model.

## The first scan

It starts automatically. A 52 MB app takes 15–20 seconds; a 62-module app takes closer to a
minute. Progress is reported by phase, so the wait is legible rather than a spinner.

93% of that time is reading properties out of the model. That is the cost of seeing every
reference rather than guessing from names, and it is paid once: the result is cached, and the
cache survives restarting Studio Pro. Everything after the first scan is instant.

**Rescan** when you have changed the model and want the analysis to catch up. Nothing watches
the model for you — the Mendix API exposes no model-change event, so an automatic refresh is
not something any extension can offer.

## Reading the Overview

The first screen is four numbers and two lists.

**Elements, References, Modules, Cycles.** Cycles is the one to look at first. A circular
group means none of the modules in it can be extracted, tested or deployed independently of
the rest, and it changes what every other number below means.

**Composition** is what the app is made of, by document type. It answers "is this a
microflow-heavy app or a page-heavy one" in one glance.

**Module coupling** is how often one module references another. High counts between modules
that should be independent are the coupling worth questioning. Modules that reference nothing
and are referenced by everything are usually infrastructure, and that is fine.

## Two buttons worth pressing early

**Explain this app** writes a handover summary from the model: what it is, how the outside
world gets in, how it is put together, and what the scan could not see. Assembled for someone
who does not yet know what to ask.

**Guided review** turns the architecture review into an agenda where each question already
carries its answer, so you can see which ones are live on this app before opening anything.
There is deliberately no overall score. A single number over these would be invented
weighting, and it would be quoted long after the detail behind it was forgotten.

## Marketplace modules

Hidden from browsing by default, because they are code you do not maintain. They stay fully
present in dependencies, impact and the graph — a dependency reaching into one is exactly
what you need to see. Every view that can include them has a toggle.

Which modules are from the Marketplace is read from Mendix's own flag, not guessed from
names, so a renamed or forked module is still recognised.

## Language

English and Dutch. The switch is in the title bar.

Dutch covers the chrome: tabs, buttons, menus, filters. Element names stay as they are,
because they are identifiers from your model and a translated name would not match what
Studio Pro shows beside it. Analysis prose stays in English where its wording is carefully
hedged, and the pane says so rather than leaving you to discover it.
