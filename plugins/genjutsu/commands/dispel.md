---
description: Kai! Find mocks, fakes and hardcoded placeholders that leaked into production code
argument-hint: [path to scan, defaults to the whole repo]
allowed-tools: Read, Grep, Glob
---

Scan this path for illusions (if it is empty, scan the whole repository): $ARGUMENTS

Look for illusions that should not ship. This is a read-only pass: report, do not edit.

Delegate the scan to the `illusionist` agent if it is available; otherwise do it yourself.

Look for, outside test, mock and fixture folders:
- files or blocks marked `genjutsu:mock`
- imports of mock/fake/stub modules or mocking libraries
- hardcoded fake data: `lorem ipsum`, `foo@example.com`, `John Doe`, `123-456-7890`, `test123`, `TODO: replace`
- mocked network layers left switched on (MSW `worker.start()`, `USE_MOCKS=true`, `nock` outside tests)
- feature flags or env checks that always return the fake path

Report a table grouped by severity:
- **Blocker**: mock code reachable in a production build
- **Warning**: placeholder data or a suspicious flag
- **Info**: properly isolated mocks (count only)

For each finding give `file:line`, what it is, and the one-line fix. End by asking whether to apply the fixes.
