---
name: notion-task
description: Use when asked to create a task or ticket - generates markdown formatted for Notion with Story, Background, and ACs
---

# Create Notion Task

## Overview

Generate tasks in markdown format ready to paste into Notion. Output a title (for the title field) and body (Story, Background, Acceptance Criteria).

**Trigger:** User explicitly asks to create a task/ticket.

## The Process

1. **Gather context** - From the conversation or user's description of the work
2. **Infer engineer role** - Based on the type of work
3. **Clarify if needed** - Ask one question if critical info is missing
4. **Output** - Title + formatted markdown body

## Output Format

```
**Title:** [Concise title for the task]

---

## Story
As a [Role] Engineer, I want to [action] so that [benefit].

## Background
[1-3 sentences explaining context/motivation - why this matters]

## Acceptance Criteria
- [ ] [Concrete, verifiable item]
- [ ] [Concrete, verifiable item]
- [ ] [Concrete, verifiable item]
```

## Role Inference

Infer the engineer role from the work being described:

| Role | Keywords/Topics |
|------|-----------------|
| Security Engineer | vulnerabilities, compliance, audits, access control, secrets, scanning, CVEs, permissions |
| DevOps Engineer | CI/CD, deployments, pipelines, monitoring, automation, builds, releases |
| Infra Engineer | servers, networking, cloud resources, scaling, databases, Kubernetes, Terraform |

## Guidelines

**Story:**
- Format: "As a [Role] Engineer, I want to [action] so that [benefit]"
- The benefit should explain why this matters to the team/org

**Background:**
- 1-3 sentences of context
- What problem exists without this work
- Why it matters now

**Acceptance Criteria:**
- 3-6 concrete, verifiable items
- Checkbox format (`- [ ]`)
- Focus on outcomes, not implementation details
- Each item should be independently testable

## Example

User: "We need to rotate the database credentials and update the secrets in Vault"

Output:

```
**Title:** Rotate database credentials and update Vault secrets

---

## Story
As a Security Engineer, I want to rotate the database credentials and update them in Vault so that we maintain our security posture and comply with credential rotation policies.

## Background
Database credentials should be rotated regularly to limit exposure from potential leaks. The current credentials have been in use beyond our rotation policy window.

## Acceptance Criteria
- [ ] New database credentials generated
- [ ] Credentials updated in Vault
- [ ] Applications verified to authenticate with new credentials
- [ ] Old credentials revoked
- [ ] Rotation documented in runbook
```
