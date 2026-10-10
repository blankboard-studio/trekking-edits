# Gotchas

A running log of things that cost time on this project. Agents read it at
the start of every session and add to it when they hit something new (see
the Session protocol in `AGENTS.md`). Never delete an entry — update its
`Status` instead.

Lessons from earlier builds are in the skill, not here:
`.claude/skills/webflow-build/lessons/` (one file per area). Read the file
for the area you work in. Entries tagged `Scope: template-candidate` are
collected from client repos into those files.

## Entry format

```md
### YYYY-MM-DD · Short title
- Area: designer | css | loader | release | mcp | ci | js | perf
- Scope: project | template-candidate
- Symptom: what was observed
- Cause: why it happened
- Fix: what was done, or the workaround
- Status: open | fixed <sha> | upstreamed wf-template <sha>
- Found by: claude | codex | human
```

## This project

### 2026-10-10 · Template history rewritten after the repo was created
- Area: ci
- Scope: template-candidate
- Symptom: `.wf-template.json` pinned skills to `master@63bfb79`; a day later `brandvm/wf-template` had one commit, `7c48bf0`, and GitHub's compare said "No common ancestor", so the pin could not be diffed.
- Cause: the template's master was squashed and force-pushed when v0.2.0 was tagged. 0.1.0 was never tagged.
- Fix: diffed against the `v0.2.0` tarball instead, ran `pnpm update-skills` (it follows the latest tag), and ported the non-skill changes by hand (`loader.html` pieces 2b and 3, `AGENTS.md`, README, `tests/css-swap.spec.mjs`). Template-only files (CHANGELOG, CONTRIBUTING, issue templates, `harvest.mjs`) stay out, as `new-project` removes them.
- Status: open (template: tag every release and never rewrite master; `update-skills` could also port the non-skill files)
- Found by: claude

<!-- Add new entries here, newest first. -->
