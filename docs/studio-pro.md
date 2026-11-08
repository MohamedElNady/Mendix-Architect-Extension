# Studio Pro integration

*New in 1.3.* The pane answers questions from where you already are in Studio Pro.

## Right-click

In the App Explorer and the domain model editor, the **Mendix Architect** menu offers the questions
that fit what you clicked:

- **How is this reached?** — the route from an entry point, step by step
- **What breaks if I delete this?** — the delete simulation
- **Page flow from here** — on pages
- **Who can create, read, write and delete it?** — on entities, the access matrix for that entity
- **Who can open this page? / Who can run this microflow?**
- **Where is it created, changed and deleted?** — on entities, the lifecycle
- **Show dependency graph in an editor tab**

## Editor tabs

Any view opens as a Studio Pro editor tab, with the element you selected: from the button in the
pane's title bar, from **Extensions → Mendix Architect → Open Architect in an editor tab**, or from a
right-click. A graph finally gets the width it needs.

## Find Results and pickers

*Usages in Studio Pro* in the details panel shows the usages in Studio Pro's own **Find Results** pane,
down to the activity and the widget. Impact and Paths offer *Pick in Studio Pro* for documents and
entities.

## Follow the editor

The target button next to the Explorer's filters makes the pane follow Studio Pro: open a microflow or
page, and the pane selects it, with what it calls and what calls it.

## A badge for new findings

The pane's tab shows how many findings are new since the analysis before, per document and rule. A
notice lists them, and *Mark as seen* clears it. A reworded message is not "new".

## Scan finished

A scan that takes longer than ten seconds ends with a Studio Pro notification, so you can work
elsewhere meanwhile.

## Tidy layout

**Explore → Domain**, choose a module, **Tidy layout…**: Studio Pro moves the module's entities into a
readable layout in one step, previewed first, with undo. Box sizes are estimated, because the model
does not store them.
