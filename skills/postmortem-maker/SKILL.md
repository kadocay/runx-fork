---
name: postmortem-maker
version: 1.0.0
description: "Turn incident fragments into traceable postmortems — reads from real incident sources, separates known facts from unknowns, produces action items, and publishes when ready."
scope:
  - postmortem
  - incident
  - report
  - runx
allowed_tools:
  - web_fetch
  - web_search
  - terminal
  - read_file
  - write_file
digest: sha256:c00eeea135b7f8c6e28bb6898e17a3aef9e5ab42183ea0c0f33318c2b8215893
wraps: skill-registry:open-incident-skill@1.0.0
---

# Postmortem Maker

Reads an incident record from a real source (web-fetch of a real incident thread or ticket read_projection), separates known facts from hypotheses, produces a structured postmortem with action items, and when publishable, seals a comms send_plan.

## Inputs

| Name | Type | Description |
|------|------|-------------|
| `source` | string | Incident read_projection handle or thread URL |
| `postmortem_policy` | string | Policy for postmortem generation (optional) |

## Outputs

| Name | Type | Description |
|------|------|-------------|
| `postmortem` | object | Structured postmortem with summary, timeline, impact, root_cause, status |
| `unknowns` | array | Facts that remain unresolved |
| `action_items` | array | Action items from the analysis |
| `publish_result` | object | Sealed publish_result when postmortem is publishable |

## Behavior

1. Reads the incident record from the specified source
2. Separates known facts from hypotheses/unknowns
3. Produces timeline, impact analysis, root cause
4. Generates action items
5. If publishable, executes send_plan via send-as skill
