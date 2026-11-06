---
description: Turn real API responses (HAR file, saved JSON, curl output) into sanitized fixtures and mock handlers
argument-hint: <HAR file | folder of saved responses | pasted response> [endpoint filter]
---

Record these real responses as safe mocks: $ARGUMENTS

Use the `sanitize` skill for how to scrub the data, and the `mock-data` skill for how the replacements should look.

1. Read the input. Accept a `.har` export, saved response files, or pasted output. Do not call live APIs yourself unless the user explicitly asks; if they do, ask before each non-GET request.
2. If an endpoint filter was given, keep only matching requests. Drop static assets (images, fonts, JS, CSS) and analytics calls.
3. Sanitize every response and request before writing anything: secrets, tokens, cookies, personal data and internal hostnames. Keep shape, types, lengths and ID formats.
4. Group by endpoint and method. Keep one representative response per status code (for example 200, 404, 422) instead of every duplicate.
5. Write the results where the project keeps mocks or fixtures. If the project already has a mock server (for example one made by `/genjutsu:mock-api`), add handlers to it; otherwise write plain fixture files.
6. Tag every file with `genjutsu:mock` and add `recorded-from: <source file>` next to it.

Report a table: endpoint, method, status codes kept, and what was scrubbed (counts per category). List anything you were unsure was sensitive so the user can check it.
