---
name: mock-data
description: How to make fake data that looks real - realistic names, emails, money, dates, IDs and relations - while staying obviously safe (no real people, no real card numbers). Use whenever generating mock API responses, fixtures, seed data or test stubs.
---

# Mock data that holds up

Fake data should be indistinguishable from real data in shape, and impossible to mistake for real data in content.

## Shape: match reality
- Use the real field names, types and nesting from the code. Never invent fields.
- IDs follow the project's format (UUID, ULID, auto-increment, prefixed like `usr_...`).
- Dates are ISO 8601 with a timezone unless the code uses something else. Keep `created_at <= updated_at`.
- Money uses the project's representation (integer cents vs decimal) and a real currency code.
- Lists vary in length (0, 1, many) across records. Not every record should be perfect.
- Relations are consistent: a foreign key points at a record that exists in the same set.

## Content: obviously safe
- Emails use reserved domains only: `example.com`, `example.org`, `example.net`.
- Phone numbers use reserved fictional ranges (for example US `555-0100` to `555-0199`).
- Card numbers: only the payment provider's published test numbers (for example `4242 4242 4242 4242`).
- Names: varied and international (include accents and non-Latin scripts), never real public figures.
- Addresses: plausible but fictional; no real private addresses.
- Never copy production data, real customer records, or real secrets into mocks.

## Edge cases worth including
- empty optional fields and `null` where allowed
- the longest allowed string
- Unicode and right-to-left text
- boundary dates (month end, leap day, timezone change)
- zero and negative amounts, where the type allows

## Marking
Tag generated files with a `genjutsu:mock` comment (or a `_genjutsu` key in formats without comments) so `/genjutsu:dispel` can tell intended mocks from leaks.
