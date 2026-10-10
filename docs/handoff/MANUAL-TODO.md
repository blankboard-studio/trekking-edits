# Manual Designer steps

Everything the Webflow MCP can't do, for a person to do in the Designer.
Claude adds a row the moment it hits a limit, with *why* the API can't;
the person marks it done; Claude then reads the result back (or checks it on
the canvas when the API can't read it) and says so.

Common reasons, so they don't need re-explaining (see the skill's
`lessons/mcp.md`):
- a value mixing a variable with `calc()`, a gradient or a shadow;
- conditional visibility on a CMS field; a list sourced from a
  multi-reference or multi-image field; "exclude current item";
- a link to the current CMS item, in a list or a component prop;
- tag styles that have never been set; reserved class names;
- placeholders, slot names, variant props exposed from nested instances.

How to enter a value with variables: select the class, switch to the
breakpoint, type `calc(` in the field and insert variables with the
variable picker. Gradients: Backgrounds → gradient, pick each stop from the
variables.

Letters run A, B, C… then AA, AB… and are never reused, so a letter
mentioned in GOTCHAS or a commit stays unambiguous.

| ID | Where (page › element or class) | Breakpoint | Set | Why the API can't | Done |
| --- | --- | --- | --- | --- | --- |
| A | CMS panel › all 10 collections (People, Articles, Evidence, Facts, Changes, Price Observations, Nepal - Villages / Permits / Costs / Logistics) | — | Delete each collection (removes its items and template page). Reference fields were already removed, so any order works | The Data API has no delete-collection call | ☑ |
| B | Pages panel › Nepal, Permits and rules, Costs, Logistics, Villages and teahouse prices, Tools, Permit and fee calculator, Trek cost calculator, Evidence, Changelog, Method, Corrections, Disclosure, Submit a receipt, About, Dispatches; folders `nepal`, `tools` | — | Delete the 16 pages, then the two empty folders. Keep Home and `design/style-guide` | The Data API has no delete-page or delete-folder call | ☑ |
| C | Pages panel › Utility pages (404, Password) | — | Check both are Webflow defaults with no leftover content | The MCP can't reach utility pages | ☑ |
| D | GitHub › blankboard-studio/trekking-edits › Settings | — | Pages → Source: GitHub Actions. Collaborators and teams → add the developers team (Write) | Repo settings, not Webflow; needs an org admin | ☑ |
| E | Repo › first push | — | After Claude's commit ask: push, wait for the staging workflow, check `https://blankboard-studio.github.io/trekking-edits/styles.css` loads | Needs the commit OK and step D | ☑ |
| F | Site settings › Custom code (head, footer) and Embeds 2a/2b | — | Head and footer code written through the MCP on 2026-10-10 (loader.html pieces 1 and 3). Still open: Embeds 2a/2b in G \| Components, built with the base system (no starter site to duplicate) | The canvas Embeds need the shell components | ☐ |
| G | Site settings › webflow.io staging | — | Turn off webflow.io subdomain indexing (Site settings › SEO) until launch. No staging password: decided 2026-10-10 | No API for site password or indexing settings | ☐ |
| H | Site settings › Custom code › Footer | — | Re-install `loader.html` piece 3 (changed in template v0.2.0: stylesheet swap without an unstyled gap). Do it when the build starts, with Embeds 2a/2b in F. Claude can write it through the MCP on your go-ahead | Needs the Webflow go-ahead; the design must be signed off first | ☐ |
