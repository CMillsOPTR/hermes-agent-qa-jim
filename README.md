# Hermes Agent Repository: qa-jim

This repository packages the portable `qa-jim` Hermes agent definition and its agent-owned project/workspace files.

## Contents

- `agent/` — profile configuration, role identity, memories, skills, assets, and portable cron definitions.
- `projects/` — files found in this agent's Hermes workspace.

## Import into Hermes

Copy the contents of `agent/` into the destination Hermes profile directory. For `default`, copy into the Hermes home; for named profiles, copy into `profiles/qa-jim/`. Keep destination credentials and runtime state separate.

## Exclusions

Secrets, OAuth files, sessions, logs, caches, databases, runtime locks, and compiled Python caches are intentionally excluded.

Project files copied from the source workspace: 0.
