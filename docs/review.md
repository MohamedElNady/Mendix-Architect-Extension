# Review

Judging the app, rather than exploring it.

## Recommendations

What to enhance, restructure, remove or replace.

It leads with the **refactor quadrant** rather than a list, because the first question is
"where do I start" and a list cannot answer that. Complexity across, how many things depend on
it up. The top-right corner is both hard to change and widely relied upon, which is where
effort pays.

Every finding shows what was measured and which threshold it crossed:

> **29 activities** · p90 of this app = 27

Thresholds come from your app's own distribution, never fixed numbers. That is what makes a
finding arguable instead of a rule handed down. Performance anti-patterns are deliberately left
to Mendix's own Best Practice Recommender rather than duplicated here.

## Security

Roles are promoted to first-class nodes, which is what turns "which role can do what" from
unanswerable into an ordinary graph question.

Five rules, covering entities with no access rules, client-callable microflows with no role
restriction, and pages with a direct URL and no restriction.

**XPath constraints on access rules are not evaluated.** A constraint can only narrow access,
never widen it — so anything reported as unrestricted really is, while anything reported as
restricted may be restricted further than shown. The error only runs one way, and that is
stated on the tab.

**Live only** is on by default: dead code is not a risk, and findings on unreachable elements
are noise.

**Roles** switches to the inventory: what each module role actually grants. A role granting
nothing is either dead, or something that should be restricted to it is not.

## Rules

Layering rules, checked in beside your `.mpr` as `mendix-architect.rules.json`, so they are
reviewed in pull requests alongside the code they constrain.

**Start from the app you have.** A rule file written from scratch produces hundreds of
violations on day one and gets deleted. *Generate baseline, minus cycles* encodes today's
structure and allows everything except the circular pairs, which are already known to be
wrong. It starts green and you tighten it deliberately.

**The ratchet.** Freezing a baseline records the violations that exist today so only *new*
ones fail. The debt stays counted either way. Stale baseline entries — ones that no longer
match anything — are reported, because leaving them in would silently re-accept a regression.

Freezing also offers a **decision record**: a draft ADR with what was accepted, when, and on
which branch. Why and Consequences are left blank. The tool knows what was accepted and cannot
know why, and a plausible-sounding invented rationale would be worse than an honest gap.

**Team ownership** is declared in the same file, not guessed. Ownership is not in the Mendix
model — it is a fact about your organisation. Guessing team boundaries from module names would
be inventing your org chart, so nothing is assumed. Once declared, "which teams does this
change touch" becomes answerable.

## Unused

Removal candidates, with a confidence rating and the reasoning behind each.

The banner says **candidates, not dead code**, and means it. See
[what it cannot see](limits.md) for the six things ruled out before anything qualifies.

**Only dead refs** means something does point at it, but that something is unreachable too —
which the older "no inbound reference" test could never find.

Before deleting anything, open it and run **What breaks if I delete this?**. It re-runs
reachability on the app without that element and shows what would dangle and what becomes
removable along with it.

## Reach

Entry points, and what they can get to.

Every other view answers a local question: what references this. That is not the same
question. A microflow called only by a page nothing can open has an inbound reference and is
still unreachable.

Six kinds of entry point are counted and listed explicitly, so you can see exactly which doors
were considered: navigation and menus, deep links, scheduled events, published services,
startup hooks, and Mendix's own "marked as used" flag.

**Invisible control flow** is the second mode, and the one most people have not thought about:
entity event handlers run on commit or delete from wherever that happens, with *nothing calling
them*. Reading the model gives no hint they exist. A Before handler that can veto is business
logic hidden behind a save button, and anyone debugging a save that silently fails will not
find it by reading the page.

## Tests

*New in 1.1.* What the unit tests (`TEST_` and `UT_` microflows) actually reach, followed through
every call. The microflows worth testing first are the complex, widely used ones that no test
reaches; they are listed with their size and how many documents depend on them.

## Duplicates

*New in 1.1.* Microflows and pages that are at least 90% alike in shape: copied, renamed and
changed a little. Names and captions are ignored; the structure is compared. Each pair is a
candidate for one shared microflow or snippet.

## Sensitive data

*New in 1.1, the third view under Security.* Personal and secret attributes, and whether anonymous
users or external systems can reach them. Declare them in the rule file; until you do, attributes
are suggested by name: credentials, identity numbers, financial, health, contact and personal
details (for example *Password*, *NationalId*, *IBAN*, *Email*, *DateOfBirth*).

## Policies

*New in 1.1, a section under Rules.* Rules on individual elements rather than layers: select
elements by type, module or name, then require or forbid a call, a reference or reach to others,
with the reason. A violation comes with its evidence, like every other finding.

