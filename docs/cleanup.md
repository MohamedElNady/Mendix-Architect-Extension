# Cleanup

*New in 1.3.* **Review → Unused** lists what no entry point reaches. It can also remove it: tick
documents (or a whole wave), check what the selection would break, confirm, and Studio Pro deletes
them in one step.

## What can be deleted

Only pages, microflows, rules, enumerations and constants: the types Studio Pro's extension API can
remove. Never offered for deleting:

| Never deleted | Why |
|---|---|
| Entities, attributes, associations | Removing them drops data on the next deploy |
| Nanoflows, snippets, JavaScript actions, building blocks, mappings | The extension API cannot delete them; delete them in Studio Pro |
| Java actions | Java code can call them, and the `.java` file would stay behind |
| Scheduled events, workflows, services, layouts, images, roles | Started from outside the model, or structure |
| Anything in a Marketplace module | An update brings it back |
| Anything exported from its module | Other apps may use it |
| Anything named in the app's Java or JavaScript | Code can call it by name |
| Microflows named `TEST_…` or `UT_…` | The UnitTesting module runs them by name |
| Anything on the team's keep list | Someone decided to keep it, and said why |
| Anything a document that stays still uses | Deleting it would leave that reference dangling |

## Waves

Deleting a document can leave the documents it called with no caller. The plan shows that in
**waves**: wave 1 is what nothing references, wave 2 is referenced only from wave 1, and so on.
*Select wave N* selects one wave. **Why the rest stays** counts the other candidates by reason.

## The selection check

Before anything is deleted, the view lists every reference from a document you did not select into
one you did, and offers *Add the documents that use them*. *Delete…* stays disabled until nothing
would be left dangling.

## What happens when you confirm

1. The dialog lists every document, with the count per type. Cancel has the focus.
2. The list is saved to `%LOCALAPPDATA%\MendixArchitect\cleanup\` first.
3. Studio Pro removes everything in one step; if anything fails, nothing is removed.
4. The scan refreshes.

Nothing is committed. The change appears in Studio Pro's **Changes** pane: commit it when you are
happy, or use **Version Control → Revert changes** to undo it. Ctrl+Z cannot undo a delete made by an
extension.

## Excluding instead of deleting

*Exclude…* sets **Exclude from app** on the documents, which one checkbox undoes. So it reaches
further than deleting: Java actions, documents named in code (the dialog shows the file and line that
names them) and unit-test microflows (the UnitTesting module will not find them) can be excluded, with
a warning. Rows that can only be excluded carry an **exclude only** chip.

**Excluded from the app** at the bottom of the view lists every document excluded today, whoever
excluded it. Tick some and *Include again…* puts them back, in one step.

The dialog's top edge says how hard the step is to undo: red for delete, amber for exclude, blue for
include again.

## The keep list

*Keep* on a row adds the document to the rule file (`mendix-architect.rules.json`, beside the `.mpr`),
with a reason:

```json
{
  "keep": [
    { "name": "Reporting.ACT_MonthEnd", "reason": "Started by the finance team's Excel import" },
    { "name": "Legacy.*", "reason": "Archive module, kept for audits" }
  ]
}
```

A name ending in `.*` keeps a whole module. An entry without a reason is refused: the point of the list
is that the next person knows why.

## Agents

`cleanup_plan` lists the waves, what can only be excluded and what is excluded today.
`delete_unused_documents` and `include_excluded_documents` take two calls: the first changes nothing
and returns the list with a confirmation code; the second asks Studio Pro, which shows its own question
dialog. Nothing changes unless you click *Delete* (or *Exclude*, *Include*) there.

## Fewer false "unused"

Published OData services, business event services and unit tests run by the UnitTesting module are
treated as ways into the app. Scheduled events switched off in the model still count, because in the
cloud each event is switched on or off in the Mendix Portal. Task queues are low confidence, because
Java can use a queue by name. Java and JavaScript are read for quoted `Module.Name` strings and calls to
generated microflow proxies: a candidate named there becomes low confidence, with the file and line.
