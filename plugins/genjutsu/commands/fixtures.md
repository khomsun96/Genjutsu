---
description: Generate realistic test fixtures or seed data from your models or schema
argument-hint: <model, table, type or schema file> [count]
---

Generate realistic fixture data for: $ARGUMENTS

Use the `mock-data` skill for how the data should look.

1. Find the source of truth for the shape: ORM models, database migrations, TypeScript types, Pydantic/dataclass models, JSON Schema, or GraphQL types. Read it before writing data.
2. Default to 10 records if no count is given.
3. Respect every constraint you can see: required fields, enums, unique keys, foreign keys, string lengths, date ranges. Related records must point at IDs that exist in the same fixture set.
4. Include edge cases on purpose, and name them: an empty optional field, a max-length string, a Unicode name, a boundary date.
5. Write the output where the project already keeps fixtures or seeds. If there is no such place, use `fixtures/` and the format the project's tests already read (JSON, YAML, SQL, factory code).
6. Add a `genjutsu:mock` marker comment, or a `_genjutsu` key where the format allows no comments.

Report the file path, the record count, and the edge cases included.
