# overlay-open-skill-1 — Delivery Report
runx-cli-version: 0.7.1

## Summary

- **Bounty:** #100 — runx skill overlay bookkeeper ($8)
- **Skill:** overlay-open-skill-1 — governed overlay for find-skills
- **Upstream:** vercel-labs/skills, MIT license, pinned by SHA-256
- **Registry:** Published at kadocay/overlay-open-skill-1@1.0.0 via registry publish
- **PR:** #327 to runxhq/runx (open, awaiting review)

## What to Inspect

- **SKILL.md** — Frontmatter carries runx extension with overlay wraps, pinned digest, scopes, allowed_tools, and digest_stale_behavior: refuse
- **X.yaml** — Agent-type runner with 2 harness cases (ecosystem-query-pass, digest-stale-refusal)
- **Registry** — Published at `kadocay/overlay-open-skill-1@1.0.0` (first-party trust tier)
- **PR #327** — Submitted to runxhq/runx for inclusion in curated skill ecosystem

## Commands to Verify

```bash
# 1. Check published skill in registry
runx registry read kadocay/overlay-open-skill-1@1.0.0 --registry https://api.runx.ai

# 2. Verify upstream digest hasn't drifted
curl -sL https://raw.githubusercontent.com/vercel-labs/skills/main/skills/find-skills/SKILL.md | sha256sum

# 3. Install and attempt run (requires agent context)
runx add kadocay/overlay-open-skill-1@1.0.0
runx skill kadocay/overlay-open-skill-1 --input-json '{"query":"test automation"}' --json
```

## Known Gap

- Harness reports `needs_agent` — expected for agent-type runner
- Receipt not yet issued — requires actual agent execution
- PR pending maintainer review at runxhq/runx

## Artifacts Delivered

| # | Name | URL |
|---|------|-----|
| 1 | public_url | https://runx.ai/x/kadocay/overlay-open-skill-1@1.0.0 |
| 2 | source_url | GitHub tree pinned to commit |
| 3 | pr_url | https://github.com/runxhq/runx/pull/327 |
| 4 | skill_md | Raw SKILL.md from source |
| 5 | x_yaml | Raw X.yaml from source |
| 6 | verification_json | Verifier packet attached |
| 7 | evidence_json | Dogfood + runx_version evidence |
| 8 | receipt_ref | Registry publish receipt |
| 9 | report | This document |
