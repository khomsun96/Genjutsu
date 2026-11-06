---
description: Stub out a dependency (service, client, module) so code can be tested in isolation
argument-hint: <dependency to stub> [for <file or test under test>]
---

Create a test stub for: $ARGUMENTS

1. Read the real dependency and list the parts the code under test actually calls. Stub only those.
2. Use the project's existing test doubles approach (jest.mock, vitest vi.mock, unittest.mock, pytest fixtures, gomock, interfaces + fakes). Do not add a new mocking library if one is already in use.
3. Keep the stub's signatures identical to the real thing so type checks still pass.
4. Make behaviour configurable per test: success, failure/exception, and slow/timeout where it matters.
5. Place it with the other test helpers, not in production code, and mark it `genjutsu:mock`.
6. Write or update one example test that uses the stub, then run that test and report the result.
