# Portable Bundle Exclusion Checklist

Use this checklist after ZIP CRC testing and before PASS:

1. Confirm required roots/profile names from the acceptance criteria.
2. Read `README_IMPORT.md` and `manifest.json`; compare declared inclusions/exclusions with actual ZIP entries.
3. Match exact forbidden basenames: `.env`, `auth.json`, `auth.lock`.
4. Match forbidden path components: `sessions`, `logs`, `caches`, `cache`, runtime-lock directories, and `__pycache__`.
5. Match state extensions: `.db`, `.sqlite`, `.sqlite3`, `.log`, and compiled `.pyc` files.
6. Treat source files or documentation that merely mention logs, databases, API keys, or bearer tokens as non-secret unless they contain concrete values.
7. Scan for concrete provider-key/private-key/bearer-token patterns without printing matches.
8. If a forbidden artifact exists, report BLOCKER; do not delete it from the reviewed bundle. Require a rebuild and repeat the full check.
9. Report documentation drift separately, such as README claims about cron definitions when no cron paths are present.
