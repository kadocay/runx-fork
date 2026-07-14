---
name: overlay-open-skill-1
description: Governed overlay for find-skills from the open skill ecosystem.
runx:
  category: authoring
  allowed_tools:
    - filesystem.read
    - filesystem.write
    - web.fetch
    - terminal.exec
    - skills.list
  scopes:
    - search_skills
    - install_skills
    - list_skills
  overlay:
    wraps:
      ref: "https://raw.githubusercontent.com/vercel-labs/skills/main/skills/find-skills/SKILL.md"
      digest:
        algorithm: sha256
        value: "c00eeea0e13e74fe4a9d84ba0a8542205a1b736d65f13134fe1a6647eb14976f"
    digest_stale_behavior: refuse
---

# overlay-open-skill-1

This is a **governed overlay** that wraps `find-skills` from the open agent skills ecosystem. It pins the upstream SKILL.md by SHA-256 digest, bounds the skill's operational scope, and restricts it to an explicit tool allowlist. The upstream file is never copied or edited — the overlay references it by registry ref and pinned digest.

## Upstream

- **Name:** find-skills
- **Repository:** [vercel-labs/skills](https://github.com/vercel-labs/skills)
- **License:** MIT (permissive, actively maintained)
- **Path:** `skills/find-skills/SKILL.md`
- **Pinned Commit:** main branch HEAD as of 2026-07-14
- **Pinned Digest (SHA-256):** `c00eeea0e13e74fe4a9d84ba0a8542205a1b736d65f13134fe1a6647eb14976f`

## Scope

This overlay may:

- Search the open skill ecosystem for installable skills
- Recommend and install skills via `npx skills` CLI
- Read skill metadata from skills.sh

This overlay may NOT:

- Publish or modify skills in the registry
- Write files outside the agent's skills directory
- Modify repository contents
- Execute arbitrary shell commands beyond skill installation

## Allowed Tools

- `terminal` — for running `npx skills find`, `npx skills add`, and `npx skills update`
- `web_search` — for verifying skill quality and checking skills.sh
- `read_file` — for reading installed skill SKILL.md files

## Digest Stale Behavior

If the upstream SKILL.md content no longer matches the pinned SHA-256 digest, the overlay **refuses to run** and reports `runx.overlay.digest.stale`. The operator must explicitly update the pinned digest before the overlay will execute again. This protects against silent upstream edits changing behavior after adoption.

## Usage

```bash
# Install
runx add <owner>/overlay-open-skill-1@1.0.0

# Run (with dogfood input)
runx skill <owner>/overlay-open-skill-1@1.0.0 --input-json '{"query": "test automation"}' --json

# Verify the receipt
runx verify --receipt <receipt.json> --json
```

## Verification

The upstream REFERENCE resolves from `https://raw.githubusercontent.com/vercel-labs/skills/main/skills/find-skills/SKILL.md`. A reviewer can recompute the digest with:

```bash
curl -sL https://raw.githubusercontent.com/vercel-labs/skills/main/skills/find-skills/SKILL.md | sha256sum
```
