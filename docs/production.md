# Production

*New in 1.2.* The questions a production review asks, answered from the model. Every check comes from
Mendix's own guidance: the Best Practice Recommender, the security, naming and error-handling best
practices, and the language settings.

## Go-live

The production review as a checklist: **passed**, **warning** or **blocker**, with a readiness score and
the result by area. Each check links to the tab with the detail.

- **Security settings:** security level, demo users, whether the administrator still has the default
  name, password length and complexity, password hashing, strict mode.
- **Access:** published services without authentication, constants sent to the browser, and the
  findings of the Security tab.
- **Integrations** and **what users will see**: the Integrations and Translations results.

**Names and passwords are never read.** The administrator is recorded only as "still the default name
or not", demo users as a count, constants without their values. **Export checklist** saves it as
Markdown for the review meeting.

## Security

Roles as first-class nodes, the role inventory, and **Sensitive data**: personal and secret
attributes, and whether anonymous users or external systems can reach them. Moved here from Review in
1.2; see [Review](review.md) for how the rules are defined.

**Access** *(1.3)* answers an auditor's first question in one table: which role may **create, read,
write and delete** each entity. By user role (what its module roles add up to) or by module role, per
module; darker the more it allows, lower case when only some members, `*` when an XPath constraint
narrows the rows. A chart shows what each role may change, a warning appears when the anonymous role
may change stored data, and *Access CSV* exports it. Entities that are never stored are listed apart,
so a form helper is not mistaken for data.

**Pages and flows** shows which user roles may open each page and run each microflow and nanoflow,
with a chart per role and *Only with findings*. Flows only server code calls are marked *server only*.
Right-click a page or microflow in Studio Pro and choose *Who can open this page?* or *Who can run
this microflow?* to open it on that one row.

## Performance

Work that costs a round trip every time it runs, found in the model before anyone measures it.

- **Inside loops:** commits, database retrieves, deletes and external calls, loops in loops, and the
  same work **hidden in a sub-microflow** the loop calls, followed six levels deep with the chain
  shown. That last case is the one Studio Pro's built-in recommender does not follow.
- **Pages:** data containers nested three or more levels deep, and widgets that fetch once per row.
- **Entities:** inheritance more than two levels deep, calculated attributes shown on pages or read by
  nothing, and temporary objects cached on System entities.

A heatmap shows where the problems are, by module.

## Integrations

What every outbound call does when the other side fails, grouped by external system:

- default error handling, or an error that is caught and then lost;
- no timeout, and hard-coded hosts;
- calls inside loops, and calls a user waits on.

The error path is followed along the microflow **and through the microflows it calls**, so a team that
logs through a shared error-handling microflow gets the credit.

## Translations

For each language: how much is translated, by kind of document and by module, with examples of what is
missing. Texts that have no default-language text are shown to users as `[no translation]`; they are
listed apart. Translations kept for languages the app does not have are counted too.
