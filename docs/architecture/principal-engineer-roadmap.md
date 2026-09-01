# Principal engineer feedback: roadmap fit

Status: Draft roadmap, not a product commitment
Date: 2026-09-01

## What is already implemented

The current product already has the skeleton of a team review queue and a policy-based auto-approval flow:

- Review queue with a personal lens: `Needs my review`, `All open`, `Blocked`, and `Stale`
- Queue filters for repository and author
- Auto-approve setting with a maximum acceptable risk threshold
- GitHub review activity surfaced in the queue and detail flow, including review counts and review-request context

This means the product is already solving the basic triage problem: identify which pull requests are relevant, what is blocked, and when an AI review may be safely auto-approved under a risk policy.

## What the principal-engineer feedback adds

The new feedback is not a new product category; it is a refinement of the queue from team-level triage into personal, policy-aware, review-scope control:

1. Easy reviews should be surfaced as "easy wins" for AI self-approval under company rules
2. The queue should show which engineers approved a pull request
3. Review steps should be configurable per engineer rather than a single team-wide policy
4. Filters need to be granular enough to remove a reviewer from work that does not actually need their interaction

## How this fits in the roadmap

### Phase 1 — AI self-approval for easy wins

Goal: automatically find PRs that are low-risk and policy-compliant enough to skip human review, while still preserving a clear audit trail.

Planned scope:

- Add a policy model for "easy review" and "self-approved" eligibility
- Evaluate repository, file, diff-size, and severity targets before the PR is surfaced as eligible
- Require a clearly defined company rule set, not ad hoc thresholds
- Keep an explicit approval record so the queue shows why a PR was auto-approved and by which rule

This is the lowest-risk expansion of the current auto-approve feature and fits naturally beside the existing Maximum risk to auto-approve setting in the review configuration screen.

### Phase 2 — queue enrichment for review ownership

Goal: make the queue answer the question, "who has already approved this, and who is still relevant to the decision?"

Planned scope:

- Add an `approved by` list to each queue row and detail panel
- Show reviewer status in the queue without opening the PR
- Distinguish between "review requested", "self-approved by policy", and "human approval by named reviewer"
- Surface a compact approval context alongside the queue's risk and wait timing

This is the direct next step after the AI self-approval policy: the queue can already tell you where a PR sits, but it still needs a clearer story about human sign-off coverage.

### Phase 3 — engineer-specific review steps and policy profiles

Goal: move from a shared review posture to a per-person review operating model.

Planned scope:

- Introduce an engineer profile that owns review steps, review risk tolerance, and self-approval policy
- Allow teams to define different reviewer workflows by repo, author group, or engineer role
- Support a "default" policy plus overrides for specific engineers or teams
- Guarantee that whatever is configured in the settings screen matches the queue logic and personal filters

This is the right place for the request that each engineer has their own set of steps. It maps cleanly to the existing settings architecture, but the current product still treats review policy as mostly homogeneous.

### Phase 4 — reviewer-specific filters that remove noise

Goal: let a reviewer reliably remove themselves from PRs that truly do not need their involvement.

Planned scope:

- Add a granular personal filter model: `not needed`, `already approved`, `already covered`, `not my area`, `no interaction required`
- Let the queue distinguish between "needs my review" and "needs my interaction"
- Add a filter stack that combines personal rules, repo ownership, approval coverage, and AI self-approval status
- Make the default lens broader than explicit GitHub review requests, but allow a stricter mode when the reviewer wants only active work

This is where the principal-engineer feedback around taking oneself out of reviews that do not require interaction becomes a real queue experience upgrade rather than a manual checklist.

## Recommended sequencing

The most natural order is:

1. Phase 1: easy-review AI self-approval
2. Phase 2: approval visibility in the queue
3. Phase 3: engineer-specific policy profiles
4. Phase 4: personal exclusion and no-interaction filters

That keeps the timeline aligned with the existing architecture: there is already an auto-approve control and a queue model, so the first change is to make that path more specific and more policy-aware before broadening it into per-engineer behavior.

## Suggested product framing

A good summary for the working roadmap is:

> Shift Komodo from team-wide review triage to policy-aware personal review routing: easy wins can self-approve under company rules, the queue shows who has already signed off, each engineer can have their own workflow, and the reviewer can filter away work that does not require their interaction.

This keeps the current implementation intact while making a clear path from the present queue to the next generation of reviewer-specific review automation.
