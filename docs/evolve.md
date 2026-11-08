# Evolve

*New in 1.1.* Three views about where the app is going rather than what it is today.

## Upgrade

What stands between the app and **Mendix 12**, where the React client becomes the only client.

- Widgets and JavaScript the React client does not support: Dojo-based widgets, `dojo` and `dijit`
  API calls, and a custom `index.html`.
- Every page is put in one of three groups: ready, converts in Studio Pro, or needs manual work,
  with a rough estimate in hours.
- **Java libraries**: two versions of the same jar, a jar in `userlib` that shadows one in
  `vendorlib`, and jars no module declares.

Estimates are rough by design: use them to size the work, not to plan the sprint.

### Mendix 11 target

*New in 1.2.* For apps still on Mendix 10, choose **Mendix 11 (from 10)** in the Upgrade tab: what the move
breaks or deprecates, from the official upgrade guide. Document templates, the Deep Link module,
`mx.logger` in JavaScript actions, client-side comparisons with `''` (whose meaning changes in 11), a Java
version below 21, and the removed *System context tasks* setting. Each item lists the documents it
touches, with a rough effort. On an app already on 11, these are the deprecations still to clear.

## Hotspots

What changes most, and what changes together, read from the app's **Git** history. Apps in the MPR v2
format store each document as its own file, so the history is per document.

- **Churn**: the documents changed most often, and by how many people. Authors are shown as
  opaque hashes, never names or e-mail addresses.
- **Change coupling**: documents that keep changing in the same commits although the model does
  not connect them. That is a dependency the model cannot show, and a good question for a review.

Large commits that touch many documents at once (merges, mass renames) are set aside, so they do
not drown out the real pairs. For an app without Git history the view says so: *No version history
for this app*.

## Debt

Every finding priced in minutes: the time to make the change in Studio Pro, not to test or release
it. The prices are summed into days per area and per module, and the documents are ranked by how
often they change, because debt in a document that changes every week is paid again and again.

The default prices are rough averages. Set your own per rule in the rule file, and the pane,
the SARIF export, the dossier and the pull-request gate all use them. One refactor that resolves
several findings is priced once.

### Module health *(1.3)*

A grade per module, **A to F**, from debt per document against the app's median, open security
findings, coupling, module cycles and complex flows no test reaches, with every deduction listed. A
bar of modules per grade, and a quadrant of size against debt per document: the modules both big and
expensive are the ones to plan for.

## Documentation *(1.3)*

How much of the app is documented, and what to document first. See [Documentation](documentation.md).
