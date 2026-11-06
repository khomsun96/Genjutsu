---
description: Add named, switchable scenarios (happy, empty, error, slow, ...) to existing mocks
argument-hint: <scenario name or description> [mock file or folder]
---

Add this mock scenario: $ARGUMENTS

1. Find the existing mocks: files tagged `genjutsu:mock`, or the folder given above. If there are none, say so and suggest `/genjutsu:mock-api` first. Do not create a mock server here.
2. Find out how scenarios are switched today, if at all (env var, query param, header, MSW handler sets, WireMock scenarios). Reuse that mechanism. If there is none, add one switch, defaulting to an env var `GENJUTSU_SCENARIO`, with `default` meaning the current behaviour.
3. Interpret the requested scenario. Common ones:
   - `empty`: lists return `[]`, optional objects are missing
   - `error`: 500 for writes, 503 with `Retry-After` for reads
   - `unauthorized`: 401 everywhere except login
   - `slow`: add 3 to 8 seconds of latency
   - `flaky`: about 1 in 3 requests fails with 502
   - anything else: ask one question if the meaning is unclear
4. Apply it only to the endpoints where it makes sense, and keep `default` unchanged.
5. Keep all scenario code inside the mock folder and tag it `genjutsu:mock`.

Show how to switch to the new scenario (the exact command or setting) and list the endpoints it changes.
