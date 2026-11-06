---
description: Cast a mock API server from an OpenAPI spec, route code, or a plain description
argument-hint: <spec file | route folder | description of the API>
---

Build a runnable mock server for this API: $ARGUMENTS

1. Work out the API's shape. In order of preference: an OpenAPI/Swagger file, existing route or controller code, existing client code that calls the API, or the description above. If none of these is clear, ask one question before writing anything.
2. Match the project's stack. Reuse a mocking tool it already has (MSW, json-server, WireMock, Prism, nock, responses, etc.). If it has none, pick the lightest option for its language and say which you chose.
3. Put the mock under a clearly named folder such as `mocks/` or `__mocks__/`, never inside production source.
4. For each endpoint, return realistic data with the real field names and types, plus at least one error case (4xx) and an empty-list case where it applies.
5. Add one script or command to start the mock, and show it to the user.
6. Tag every generated file with a top comment `genjutsu:mock` so `/genjutsu:dispel` can find it later.

Finish with a short table: endpoint, method, and the scenarios it covers.
