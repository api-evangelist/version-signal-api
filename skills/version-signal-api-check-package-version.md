---
name: check-package-version
description: >-
  Look up the current stable version and publication date of an npm or PyPI package using the
  Version Signal API. Free, no authentication required.
api: Version Signal API
operations:
  - "GET /api/version"
generated: '2026-09-20'
method: generated
source: openapi/version-signal-api-openapi.json
---

# Check a package's current stable version

Use the Version Signal API to resolve the canonical latest stable version of a package.

## When to use

- You need the current published version of an `npm` or `pypi` package.
- You want the publication date of that release, sourced from the canonical registry.

## Steps

1. Choose the ecosystem: `npm` or `pypi`.
2. Call the endpoint (no auth, no signup):

   ```
   GET https://version-signal.inboxtzdjqv.workers.dev/api/version?ecosystem=npm&package=express
   ```

3. Read the JSON response:

   ```json
   { "ecosystem": "npm", "package": "express", "version": "5.2.1",
     "publishedAt": "2025-12-01T20:49:43.268Z", "source": "https://registry.npmjs.org/express" }
   ```

   - `version` — current stable version string.
   - `publishedAt` — ISO 8601 publish timestamp of that version.
   - `source` — the canonical registry URL the fact was read from.

## Errors

- `400 {"error":"ecosystem and package required"}` — supply both `ecosystem` and `package` query params.
- `404 {"error":"not_found"}` — the package does not exist in that registry.

## Notes

- Both `ecosystem` and `package` are required query parameters. `ecosystem` must be `npm` or `pypi`.
- No API key is needed; the API is public and free.
