---
name: artifact-bundle-qa
description: "Use when QA-ing bundles."
version: 1.0.0
author: qa-jim
license: MIT
platforms: [windows, macos, linux]
metadata:
  hermes:
    tags: [qa, artifacts, zip, bundles, release-readiness, evidence]
    related_skills: [dogfood, systematic-debugging]
---

# Artifact and Portable Bundle QA

## Purpose

Independently review exported deliverables, portable agent bundles, ZIP packages, and generated documents without modifying or publishing them. Produce a grounded PASS or blocker decision based on the exact artifact currently on disk.

## When to Use

Use this skill when a user asks for read-only QA of a ZIP bundle, exported artifact set, generated document, or release package, especially when exact hashes, required files, runtime exclusions, or evidence provenance matter.

## Evidence discipline

1. Use the exact user-provided path. Hash the artifact before relying on prior reports; stale copies and regenerated documents are common.
2. Read back the artifact with an appropriate parser, not only a filename listing. For DOCX, validate the package and inspect text/structure/revisions/comments. For ZIP, test every member and inspect its manifest/readme.
3. Distinguish evidence levels explicitly:
   - independently read-back local artifact;
   - user-reported result;
   - Preview/Test Site result;
   - published/live result.
   Never convert a user-reported, Preview, or Test Site result into an independent production PASS.
4. Verify every acceptance criterion, including negative requirements and exclusions. A healthy package can still fail content, scope, or release criteria.
5. Report discrepancies rather than reconciling them by assumption: hash mismatch, claimed-vs-actual structure, count mismatch, stale copy, or unsupported claim.

## ZIP and portable-bundle workflow

1. Run `ZipFile.testzip()` and record the result. A `None` result means CRC/integrity testing passed; it does not prove content correctness.
2. Enumerate archive entries and derive exact top-level/profile roots. Confirm every required agent/profile is present.
3. Read the import README and manifest. Compare declared inclusions/exclusions with actual entries and report documentation drift.
4. Check forbidden content by exact basename, path component, and extension. For a credentials/runtime exclusion policy, inspect at minimum:
   - `.env`, `auth.json`, `auth.lock`;
   - session/conversation databases;
   - `sessions`, `logs`, `caches`, runtime-lock directories;
   - `.db`, `.sqlite`, `.sqlite3`, `.log` files;
   - `__pycache__` directories and `.pyc` files.
5. Avoid false positives from benign names such as `fetch_logs.py`, documentation examples, or a skill mentioning `database`. Match actual path components and inspect suspicious file contents for real credential material.
6. Scan text for concrete credential patterns (provider keys, private-key blocks, bearer tokens), while treating redacted/documentation placeholders as non-secret examples. Never print a discovered secret.
7. If any content violates an explicit exclusion, block until the bundle is rebuilt and retested. Do not modify the archive during QA.

## Generated document workflow

1. Validate package health with the document-specific validator.
2. Read full text and structure; verify headings, paragraph/table counts, and required content.
3. Check revisions and comments separately.
4. Independently count words when length is an acceptance criterion. If the claimed count differs, report the measured count and whether the acceptance limit still passes.
5. Note rendering limitations separately from structural PASS/FAIL; do not claim visual pagination was verified without a renderer.

## Web-commerce and deployment evidence

For storefront or fundraiser artifacts, retain the server-side product-assignment/campaign-scope boundary. Verify order and export persistence independently, and treat campaign attribution as a separate criterion from Student Name persistence. Policy changes that intentionally remove a cart blocker do not resolve unrelated live/Test Site failures.

## Reporting format

Return:
- Decision: PASS or BLOCKER.
- Exact artifact path and hash where applicable.
- Evidence for each required criterion.
- Discrepancies and release impact.
- Non-blocking limitations (such as unavailable rendering) separately.

Do not modify, publish, push, or delete the reviewed artifact unless the user explicitly requests that action.

## References

See `references/portable-bundle-exclusion-checklist.md` for the reusable exclusion and verification checklist.
