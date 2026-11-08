# Documentation

*New in 1.3.* **Evolve → Documentation**: how much of the app is documented, what to document first,
and two ways to produce documentation from the model.

## Coverage

How much is documented per kind (entities, attributes, microflows, nanoflows, pages), the least
documented modules, and **Document these first**: the undocumented elements used the most.

## Drafts

**Draft documentation…** drafts the Documentation of undocumented entities, attributes and
associations from what the model shows: where an entity is created, changed and deleted, who may
change it, its associations; where an attribute is set and read; an association's delete behaviour.
Never a guess at the business meaning: that is yours to add.

Edit each draft, tick the ones to keep, and **Write**: Studio Pro fills them in one step, only into
fields that are still empty (anything documented meanwhile is skipped and counted). Nothing is
committed; undo it in the dialog or with Version Control → Revert changes. Microflows and pages are not
offered, because the extension API cannot write their Documentation.

## Documentation set

**Documentation set…** writes a page per module and previews it: the module's description (its domain
model's Documentation), its entities with their Documentation, attributes and associations, where they
are created and deleted and who may change them, then its flows, pages and other documents with what
starts them and which user roles may use them. Save it as one HTML file or as Markdown, for one module
or the whole app. Undocumented elements say so; nothing is invented, and nothing is written to the app.

The command line writes the same set: `docs --out-dir <folder> [--format md|html]`.

## Deprecation register

A line starting with `@deprecated` in an element's Documentation marks it deprecated; the rest of the
line is the reason. **Explore → Domain → Deprecated** lists every deprecated element with the uses left,
and each use is a finding (DEP001), so a new use shows in the pull-request gate and in the review of
the change. An entity's panel can mark the entity, an attribute or an association, or remove the mark,
keeping the rest of the Documentation, with undo.
