# Postmortem Maker — Delivery Report

## Summary
Published `kadocay/postmortem-maker@1.0.0` — an overlay skill that wraps the open `incident-skill` with a pinned digest, scope bounds, and explicit allowed tool set. The skill reads real incident sources, separates known facts from unknowns, produces action items, and publishes when the postmortem is actionable.

## Package Details
- **Package**: `kadocay/postmortem-maker@1.0.0`
- **Registry**: https://runx.ai/x/kadocay/postmortem-maker@1.0.0
- **Source**: https://github.com/kadocay/runx-fork/tree/main/skills/postmortem-maker
- **PR**: https://github.com/runxhq/runx/pull/345
- **CLI Version**: runx-cli 0.6.14

## Harness Results
- **consistent-incident-seal** — SEALED ✅ (valid incident produces postmortem + publish)
- **digest-stale-refusal** — SEALED ✅ (conflicting evidence yields unknowns, no publish)

## Installation
```bash
runx add kadocay/postmortem-maker@1.0.0
runx skill kadocay/postmortem-maker@1.0.0 --json
```

## How to Use
1. `runx add kadocay/postmortem-maker@1.0.0`
2. `runx skill kadocay/postmortem-maker@1.0.0 --json source=https://status.vercel.com/incidents/<id>`
3. Review postmortem output and publish

## Upstream
- **Wrapped skill**: `open-incident-skill@1.0.0` (open ecosystem SKILL.md)
- **Repo**: https://github.com/vercel-labs/skills
- **License**: MIT
- **Pinned digest**: `sha256:c00eeea135b7f8c6e28bb6898e17a3aef9e5ab42183ea0c0f33318c2b8215893`
