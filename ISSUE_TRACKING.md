# D3Clarity Issue Tracking & Labeling Standard

How we file, type, label, and track issues across **all** D3Clarity repositories.
GitHub Issues — not Jira — is our tracker for AWS infrastructure and product work.
The goal: any issue reads as a best-practice example — clear, scoped, actionable,
and consistent with our **proportionality** constraint (the smallest thing that
fully solves the stated problem).

This standard lives in the org `.github` repo, so the issue Forms here apply as
**defaults to every D3Clarity repo** that doesn't define its own.

## The model: native fields first, labels for cross-cutting tags

Use GitHub's native features for anything that has **exactly one value per issue**;
use **labels** only for genuinely **cross-cutting, many-per-issue** tags.

> One-and-only-one per issue → native field/type. Many per issue → label.
> Hierarchy/blocking → relationships. Release/time grouping → milestone/iteration.

| Concern | Mechanism | Notes |
|---|---|---|
| **Type** (what kind of work) | **Native Issue Type** | `Bug` / `Feature` / `Task` / `Docs` (org-level). Set automatically by the issue Forms. One per issue. The old `bug`/`enhancement`/`task`/`documentation` **labels are retired** — the native Type replaces them. |
| **Priority** | **Issue Field** (org) — `Urgent` / `High` / `Medium` / `Low` | Single-select, pinned to all types; shows on every issue and as a Project column, searchable org-wide. Default **Medium**. Replaces the retired `priority:` labels. |
| **Effort** | **Issue Field** (org) — single-select sizing | Pinned to Bug/Feature/Task. Set during sprint planning. Effort is stable even when calendar time isn't (client work preempts). |
| **Sprint** | **Project field** — Iteration (weekly) | Which weekly sprint we're attempting; unfinished work rolls to the next iteration (honest carryover, no stale dates). |
| **Pipeline status** | **Project** `Status` field | Backlog / Ready / In progress / Blocked / Done — on the org Project board, not labels. |
| **Blocked / depends-on** | **Issue dependencies** | Use "Mark as blocked by / blocking". (A `blocked` label is fine as an extra visual flag.) |
| **Epics / breakdown** | **Sub-issues** | Break a large issue into native sub-issues rather than checkbox lists. |
| **Release / version** | **Milestone** | Group by release (ties to SemVer tags + CHANGELOG). |
| **Area / component** | **Label** `area: *` | e.g. `area: widget-engine`, `area: deploy-config`, `area: assistant`, `area: lambda`, `area: theming`. Per-repo areas may vary. |
| **Cross-cutting tags** | **Labels** | `ai-agent`, `good first issue`, `help wanted`, `client`, `internal_only`, `security`. |
| **Resolution** | **Close reason** | Close as **completed** (via a merged PR `Closes #N`) or **not planned**; `duplicate` may also be a label/close note. |

> Dates (`Start date` / `Target date`) are deliberately **not** part of the standard:
> non-client work is regularly preempted by client work, so calendar targets go
> stale. The **Sprint** iteration + stable **Effort** carry the time/size signal instead.

### Labels — the canonical cross-cutting set

| Label | Use for |
|---|---|
| `area: *` | Which subsystem (one per issue). |
| `ai-agent` | AI-agent (e.g. "Dee") prompt, knowledge & guardrail work — **instance-specific**. ("agent" alone = a *human* Connect agent; this tag is the **AI** agent.) |
| `security` | Security-related but **non-sensitive** work. (Real vulnerabilities → private reporting, never a public issue — see SECURITY.md.) |
| `good first issue` / `help wanted` | Onboarding / community signals. |
| `client` | Work tied to enabling/validating a client deployment. |
| `internal_only` | D3Clarity-internal; not for client-facing repos/views. |
| `blocked` | Optional visual flag; the real blocker is the **dependency** relationship. |

> **Retired** (do not use): `bug`, `enhancement`, `task`, `documentation`, `question`
> (→ native **Type**), and `priority: p0–p3` (→ **Priority** issue field).

## Issue body standard

The Forms enforce this — every issue should carry:

1. **Summary** — one or two sentences: what and why.
2. **Context / Component** — the repo, file, script, flow, or AWS resource; severity for bugs.
3. **Acceptance criteria** — a verifiable checklist that defines "done".
4. **Proportionality note** — the smallest fix; what is explicitly out of scope.
5. **References** — links to code, docs, related issues/PRs.

Write only what is known. If a cause or fix is uncertain, list it as a triage
question rather than asserting it.

## Lifecycle

```
open  →  typed + prioritized + added to the Project (Backlog)  →  Ready  →  In progress  →  closed
                                   │
                                   └── Blocked (issue dependency; optional `blocked` label)
```

- **Triage**: confirm the native **Type**, set **Priority** (default Medium) and one
  `area:` label, and add the issue to the org Project. Issues filed via the Forms
  already carry their Type.
- **Close** via a merged PR that references the issue (`Closes #N`), or as
  *not planned* with a one-line reason (e.g. duplicate).
- **Block**: mark the dependency ("blocked by"); name it in a comment.

## Boards

Track work on a Project created from the recommended **"D3Clarity Delivery"**
template (standard Status/Sprint and the Board / Backlog / Current-sprint views).
Note: **auto-add workflows do not copy** from a template — enable "auto-add" on
each new board.

## Per-repo overrides

A repo may add its own `area:` labels or its own issue templates (which override
these org defaults). Keep the Type / Priority / Project model consistent.
