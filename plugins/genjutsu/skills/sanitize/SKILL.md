---
name: sanitize
description: How to scrub real captured data (HAR files, logs, database dumps, API responses) into safe mock data while keeping its shape. Use when turning real traffic or records into fixtures or mocks, for example in /genjutsu:record.
---

# Sanitizing real data into mocks

Real captures make the best mocks, and the riskiest. Keep the shape, replace the content.

## Always remove
- Auth: `Authorization`, `Cookie`, `Set-Cookie`, `X-Api-Key`, bearer tokens, JWTs, session IDs, CSRF tokens, OAuth codes and refresh tokens
- Secrets anywhere in a body or URL: keys, passwords, signed URLs (`X-Amz-Signature`, `sig=`), webhook secrets
- Internal hosts and IPs: replace with `api.example.com` and `192.0.2.x` (a reserved documentation range)

## Always replace (keep the format)
- Names, emails, phones, addresses, birth dates: use the `mock-data` rules (reserved domains, fictional phone ranges)
- Government IDs, bank and card numbers: replace with obviously fake values of the same length, or published test numbers
- User-generated text (messages, comments, notes): replace with neutral text of a similar length
- IDs: replace consistently. The same real ID must map to the same fake ID everywhere in the set, so relations still hold.

## Keep
- Field names, nesting, types, nulls, array lengths
- Enum values, status codes, error message formats
- Relative timing (keep `created_at <= updated_at`; shifting all dates by the same offset is fine)
- Pagination fields and cursors (replace the cursor value, keep its format)

## Check before writing
- Search the output for anything that still looks like a token (long random strings, `eyJ` JWT prefixes), a real email domain, or a real hostname.
- If you are unsure whether a field is sensitive, scrub it and list it in your report.
- Never write the unsanitized original into the repository, not even temporarily.
