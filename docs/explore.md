# Explore

Finding things, and following what connects them.

## Explorer

Search every document in the app. Filter by type, by module, or both. Each row shows its
usage count, so the heavily-referenced things are visible without opening anything.

Selecting a document opens its detail: what it depends on, what depends on it, and every
reference grouped by the property it came through — `Microflows$MicroflowCall.microflow`,
`DomainModels$AttributeRef.attribute`, and so on. That property is the evidence. It is shown
rather than summarised so a surprising edge can be checked rather than believed.

**If this changes** states plainly whether an entry point reaches the element, and says when
that is not proof of anything.

Right-click anything, anywhere in the tool, for: open in Studio Pro, show in Explorer, view
dependency graph, analyse impact, find paths from here, copy qualified name.

## Graph

The neighbourhood of one document, laid out in layers. Left-to-right or top-down.

- **Depth** controls how far it walks
- **Direction** picks what it uses, what uses it, or both
- **Focus mode** isolates a node's two-hop neighbourhood when you click it
- Groups over eight siblings collapse into one node, so a hub does not draw a wall

Double-click a node to expand through it. **Make focus** re-centres the whole graph on it.

## Network

The same idea one level up: modules rather than documents.

**Force-directed** shows clusters. **Layered** shows direction of dependency, which is where
a layering violation becomes visible as an arrow pointing the wrong way.

**Collapse cycles** folds each circular group into a single node, which is usually the only
way to see the rest of the picture on a tangled app.

**Matrix** is a dependency-structure matrix ordered by dependency rank. Layering shows as a
clean triangle; cycles show as blocks straddling the diagonal. On a large app this is easier
to read than any node-link diagram.

Selecting a module gives you the part most people come here for:

**Extraction** — what it would cost to lift this module out. How many references to how many
modules would have to be cut or re-pointed, and whether it sits inside a cycle that has to be
broken first.

**Where it would come apart** — if the module were split, the groups it would fall into, and
the exact document coupling each group to the rest. The panel says out loud that this is what
the graph sees and not a refactoring plan: two groups can be one business concept.

**Circular with** — for each mutual pair, which of the two directions is the cheap cut, and
what cutting it would actually achieve. Cycles before and after, and which modules come free.
Sometimes the answer is none, and it says so.

## Domain

Entities, associations, and who reads or writes each.

Read and write come from the metamodel property behind each reference: a retrieve reads, a
create or member-change writes. **Delete and commit take a variable, not an entity type**, so
they leave no trace here — an entity only ever deleted will look unwritten.

- **Delete cascade** — which associations delete the other side, and how far that reaches
- **Storage** — entities read often or unusually wide with no index, naming the attributes
  the XPath constraints filter on
- **Persistability** — entities used in a way their persistability contradicts

The read/write split is the shape of the thing: many readers and one writer is configuration;
many writers and few readers is a log.

## Paths

Every route between two elements, with the hops and the property each reference came through.

The useful part is the line above the list: **every route passes through X**. That is a
chokepoint, and it is usually where the work belongs. It cannot be seen from inside any single
document.

## Impact

What references this, directly or transitively, depth-limited and grouped by type.

It says *potentially affected*. A reference means something could be affected by a change; the
model cannot prove it will break.

## Cycles

Circular dependency groups, via Tarjan. The chain shown is a real closed walk that exists in
the model, not the group's members joined with arrows — for a group of three or more those are
not the same thing, and drawing the second would assert references that may not be there.

## Inventory

Four questions that have no other home.

**Background load** — what runs on a timer. Nothing references a scheduled event, so it has no
inbound dependencies and looks like dead code to anything counting them. Disabled ones are
listed rather than hidden: "this exists but is switched off" is usually the answer to why
something stopped happening.

**Configuration** — the constants, and which are read by nothing in the model. That is *not* a
deletion list: a constant can be read from Java, and a wrong removal here breaks an
environment rather than a build.

**Integration** — what the app publishes and consumes, and which entities sit on a contract
with a system nobody in this repository controls. Renaming an attribute on one of those is not
a local refactor.

**Marketplace** — vendor modules, versions, and how much of your own code references each,
which is what it would cost to replace one.

## Workflows

*New in 1.1.* Each workflow drawn as a process: its user tasks, decisions and outcomes. Next to it,
what can make it stall:

- a user task that targets nobody;
- a task page that no role is allowed to open;
- a targeting XPath that names a role the app does not have;
- a workflow that nothing starts.

Workflows from Studio Pro 10.x and 11.x are both read.

## C4 model

*New in 1.1.* The app as a C4 model. User roles become people; outbound calls and published APIs
become external systems; modules become components. It is drawn in the pane at context,
container and component level, and exported as **Structurizr DSL**, **C4-PlantUML** or
**Mermaid**, ready for an architecture repository.

Systems whose address is computed at run time cannot be named from the model. They are grouped
under the module that calls them.

