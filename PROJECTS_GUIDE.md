# D3Clarity Projects & Issue Management Guide

**Audience:** Project Managers and Developers  
**Purpose:** How to create, track, and manage work using GitHub Issues and Projects

This guide covers the practical workflows for using the D3Clarity issue tracking standard documented in [ISSUE_TRACKING.md](ISSUE_TRACKING.md).

---

## Table of Contents

- [Quick Start](#quick-start)
- [Creating Issues](#creating-issues)
- [Working with Projects](#working-with-projects)
- [Sprint Planning](#sprint-planning)
- [Developer Workflow](#developer-workflow)
- [Project Manager Workflow](#project-manager-workflow)
- [Common Scenarios](#common-scenarios)
- [Tips & Best Practices](#tips--best-practices)

---

## Quick Start

### For Developers

1. **Find your work**: Check the Project board's "Current Sprint" view
2. **Pick a task**: Move an issue from `Ready` → `In progress`
3. **Work & commit**: Reference the issue in commits (`#123`)
4. **Close via PR**: Use `Closes #123` in the PR description
5. **Move on**: The issue auto-moves to `Done` when the PR merges

### For Project Managers

1. **Triage new issues**: Set Priority, add to Project (goes to `Backlog`)
2. **Plan sprint**: Move issues from `Backlog` → `Ready`, assign Sprint iteration
3. **Monitor progress**: Use Board view for status, Current Sprint view for focus
4. **Unblock**: Track dependencies, reassign as needed

---

## Creating Issues

### Using Issue Forms

All D3Clarity repos inherit org-level issue forms. When creating an issue:

1. **Choose the right template**:
   - **Bug Report** → Something is broken (Type: Bug)
   - **Feature Request** → New capability (Type: Feature)
   - **Task** → Work item without deliverable code (Type: Task)
   - **Documentation** → Docs update (Type: Docs)

2. **Fill required fields**:
   - **Summary**: One sentence — what and why
   - **Component**: Which part of the system
   - **Acceptance criteria**: Checklist that defines "done"
   - **Proportionality**: The smallest fix; what's out of scope

3. **The form auto-sets the Issue Type** — you don't need to label it

### After Creation

**Triage immediately** (or flag with `needs: triage` for PM review):

1. Set **Priority** field (Urgent / High / **Medium** / Low)
2. Add one **`area:`** label (e.g., `area: widget-engine`)
3. Add to the **Project board** (goes to `Backlog` status)
4. Add cross-cutting labels if needed (`client`, `security`, `ai-agent`, etc.)

**Example triage for a bug:**
- Type: `Bug` (auto-set by form)
- Priority: `High` (user-facing failure)
- Labels: `area: widget-engine`
- Project: Add to `d3c-custom-widget-delivery` → lands in `Backlog`

---

## Working with Projects

### Project Structure

Standard D3Clarity projects (created from the "D3Clarity Delivery" template) have:

**Status Field** — pipeline position:
- `Backlog` — Triaged, not yet scheduled
- `Ready` — Prioritized for current/next sprint
- `In progress` — Actively being worked
- `Blocked` — Waiting on dependency
- `Done` — Completed / closed

**Sprint Field** — weekly Iteration (e.g., "Sprint 12 - Jun 16")

**Priority Field** — Urgent / High / Medium / Low

**Effort Field** — sizing (XS / S / M / L / XL) — set during planning

**Three Views**:
1. **Board** — Kanban by Status (default view)
2. **Backlog** — Table view for triage and planning
3. **Current Sprint** — Board filtered to this iteration

### Adding Issues to a Project

**Method 1: From the issue**
1. Open the issue
2. Right sidebar → "Projects"
3. Select the project → issue lands in `Backlog`

**Method 2: From the project**
1. Open the Project → Backlog view
2. Click "+ Add item"
3. Search/select issues → they land in `Backlog`

**Method 3: Auto-add (recommended for active projects)**
- Enable auto-add workflow in Project settings
- New issues in linked repos auto-add to `Backlog`

---

## Sprint Planning

### Weekly Sprint Workflow

**Before the sprint** (PM-led):

1. **Review Backlog**: Open the Backlog view
2. **Size work**: Set Effort field on unestimated items
3. **Prioritize**: Order by Priority + business value
4. **Move to Ready**: Drag High/Urgent items to `Ready` status
5. **Assign Sprint**: Set the Sprint iteration field (e.g., "Sprint 15 - Jun 30")
6. **Capacity check**: Don't overcommit — client work preempts

**During the sprint**:

- Developers pick from `Ready` → move to `In progress` when starting
- PM monitors the "Current Sprint" view
- Blocked items → mark dependency, move to `Blocked` status
- Completed items → auto-move to `Done` when PR merges (`Closes #N`)

**After the sprint**:

- Unfinished work rolls to next sprint (update Sprint field)
- Retrospective: review Done count, Effort accuracy, blockers

### Sprint Naming Convention

Use GitHub's weekly Iteration field with descriptive names:

```
Sprint 12 - Jun 16
Sprint 13 - Jun 23
Sprint 14 - Jun 30
```

The date is the **Monday** of the sprint week.

---

## Developer Workflow

### Picking Up Work

1. **Check "Current Sprint" view** on the Project board
2. **Filter by your assignment** (if used) or pick from `Ready`
3. **Move to `In progress`** — this signals you own it
4. **Check for blockers**: Dependencies marked? All info present?

### Working on an Issue

1. **Create a feature branch**: `git checkout -b fix/issue-123-session-bug`
2. **Reference the issue** in commits: 
   ```
   git commit -m "Add session timeout handling (#123)"
   ```
3. **Update the issue**: Comment with progress, blockers, or questions
4. **Keep it moving**: If blocked, mark the dependency and move to `Blocked` status

### Closing an Issue

**Always close via a merged PR** (not manually):

1. **Create PR** with issue reference in description:
   ```markdown
   Closes #123
   
   - Added session timeout handling
   - Verified with manual test
   ```
2. **PR merges** → issue auto-closes and moves to `Done`
3. **Verify**: Check the Project board — issue should be in `Done` column

**Exception: Not Planned**
- Close as "Not planned" with a one-line reason (dup, won't fix, superseded)
- Optionally add `duplicate` or `wontfix` label

### Working with Sub-Issues

For complex work, break into sub-issues:

1. **Create sub-issues**: Use "Convert to issue" on task lists
2. **Link dependency**: Mark parent as "blocked by" the sub-issue
3. **Close sub-issues first** → parent unblocks
4. **One PR per sub-issue** when practical

---

## Project Manager Workflow

### Daily/Weekly Monitoring

**Check the Board view**:
- `Backlog` size — too large? Need refinement?
- `Ready` queue — enough for next sprint?
- `In progress` — anything stalled? (old dates, no commits)
- `Blocked` — dependencies clear? Escalation needed?

**Check the Current Sprint view**:
- On track? How many Done vs In progress?
- Effort estimate vs actual — learning for next sprint

### Triage Workflow

**New issues come in** → triage within 1 business day:

1. **Validate**: Is the issue well-formed? Acceptance criteria clear?
   - If not → comment with questions, add `needs: triage` label
2. **Set Priority**: Default is Medium; adjust based on impact/urgency
3. **Assign area**: Add one `area:` label
4. **Add to Project**: Issue goes to `Backlog`
5. **Estimate if obvious**: Set Effort field (defer complex ones to planning)

**Triage checklist**:
- [ ] Priority set
- [ ] One `area:` label
- [ ] On Project board (Backlog status)
- [ ] Acceptance criteria clear
- [ ] Cross-cutting labels added (client, security, ai-agent, etc.)

### Handling Blocked Issues

1. **Identify the blocker**: What's the dependency? External? Internal?
2. **Mark the dependency**: Use "blocked by" relationship
3. **Escalate if needed**: External vendor, infrastructure, architecture decision
4. **Optional `blocked` label**: Visual flag on the issue (but dependency is the source of truth)
5. **Update Sprint**: If it won't complete this sprint, move to next

### Capacity Planning

**D3Clarity constraint**: Client work preempts internal work.

- Don't rely on **Start/Target dates** — they go stale
- Use **Sprint** (weekly iteration) + **Effort** (stable size)
- Plan conservatively: assume ~70% capacity for sprint commitments
- Unfinished work rolls to next sprint (honest carryover, no pressure)

---

## Common Scenarios

### Scenario 1: Creating a Bug Report

**Developer discovers a bug in production**:

1. **File issue**: Use "Bug Report" form
   - Summary: "Chat widget fails to load when GTM tracking enabled"
   - Component: `static/js/chatwidget-3.5.js`
   - Steps to reproduce: List steps
   - Severity: `High` (user-facing)
   - Acceptance: "Widget loads on pages with GTM enabled"
2. **Triage**: PM sets Priority `High`, adds `area: widget-engine`, adds to Project
3. **Sprint**: PM moves to `Ready` for current sprint
4. **Fix**: Dev picks up, moves to `In progress`, creates PR with `Closes #23`
5. **PR merges** → issue auto-closes and moves to `Done`

### Scenario 2: Planning a Feature

**PM identifies a new capability needed**:

1. **File issue**: Use "Feature Request" form
   - Summary: "Add 'Restart Chat' button when session ends"
   - Component: Widget UI
   - Acceptance: "Button appears when session ends, starts new session on click"
   - Proportionality: "Manual restart only; auto-reconnect is out of scope"
2. **Triage**: PM sets Priority `Medium`, adds `area: widget-engine`, adds to Project (`Backlog`)
3. **Sprint planning**: Team estimates Effort `M`, moves to `Ready` for next sprint
4. **Implementation**: Dev creates design in issue comments, gets approval, implements
5. **PR with `Closes #21`** → merges → Done

### Scenario 3: Handling a Blocked Issue

**Dev discovers a blocker mid-sprint**:

1. **Dev comments on issue**: "Blocked: needs Lambda endpoint (issue #42) before we can test"
2. **Mark dependency**: Use "Mark as blocked by #42"
3. **Update Status**: Move to `Blocked` on the board
4. **PM escalates**: Checks #42 status, reprioritizes if needed
5. **Unblocks**: When #42 closes, dev moves back to `In progress`

### Scenario 4: Multi-Repo Work

**Issue spans multiple repos** (widget + CDK):

**Option A: Single issue, multiple PRs**
- One issue: "Update widget + CDK to support new param"
- Acceptance criteria list both repos
- Two PRs, both reference the issue: `Closes #50 (widget part)`
- Last PR closes the issue

**Option B: Parent + sub-issues**
- Parent issue #50: "Add feature X"
- Sub-issue #51: "Widget changes for X"
- Sub-issue #52: "CDK changes for X"
- Mark #50 as "blocked by #51, #52"
- Close sub-issues first → parent unblocks

### Scenario 5: Using Milestones

**Tracking a release**:

1. **Create milestone**: `v3.6 - Chat Resilience` (due: Jul 15)
2. **Add issues**: Assign all issues for the release to the milestone
3. **Monitor progress**: Milestone view shows completion %
4. **Close milestone**: When all issues complete, close milestone
5. **Tag release**: `git tag v3.6.0`, update CHANGELOG

---

## Tips & Best Practices

### For Developers

- **Reference issues in every commit**: Makes history searchable
- **Update issue comments**: Progress, blockers, questions — keep PM informed
- **Don't close manually**: Always via merged PR (`Closes #N`)
- **Ask early**: If blocked or unclear, comment immediately — don't sit on it
- **One PR per issue** when practical — easier to review, easier to revert

### For Project Managers

- **Triage fast**: New issues triaged within 1 business day
- **Keep Backlog refined**: If >30 items, run a grooming session
- **Don't overcommit sprints**: Client work preempts — plan conservatively
- **Use effort, not dates**: Effort is stable; dates go stale when priorities shift
- **Close stale issues**: If an issue sits untouched >60 days and isn't a future need, close as "not planned"

### For Everyone

- **Write clear acceptance criteria**: If you can't check it off, rewrite it
- **Respect proportionality**: Smallest thing that solves the problem; note what's out of scope
- **Link related work**: Use issue relationships (blocks, blocked by, related)
- **Keep issue bodies updated**: Edit the description if requirements change
- **Use sub-issues for complexity**: Checkbox lists are for steps, sub-issues are for separate work

---

## Reference

### Status Definitions

| Status | Meaning | Who Moves It |
|--------|---------|--------------|
| `Backlog` | Triaged, not yet scheduled | PM (auto-lands here when added) |
| `Ready` | Prioritized, ready to pick up | PM (during sprint planning) |
| `In progress` | Actively being worked | Developer (when starting work) |
| `Blocked` | Waiting on dependency | Developer or PM (when blocker identified) |
| `Done` | Completed / closed | Auto (when issue closes) |

### Priority Guidelines

| Priority | Use For | SLA |
|----------|---------|-----|
| `Urgent` | Production down, data loss, security incident | Hours |
| `High` | User-facing bug, client blocker | Current sprint |
| `Medium` | Standard feature/bug work (default) | Next 1-2 sprints |
| `Low` | Nice-to-have, tech debt, future optimization | Backlog |

### Effort Sizing

| Effort | Rough Estimate | Example |
|--------|----------------|---------|
| `XS` | <2 hours | Fix typo, update config |
| `S` | Half day | Add validation, simple bugfix |
| `M` | 1-2 days | New API endpoint, UI component |
| `L` | 3-5 days | Integration, multi-file refactor |
| `XL` | 1-2 weeks | New subsystem, architecture change |

> **Note:** Anything larger than XL should be broken into sub-issues.

---

## Getting Help

- **Standard reference**: [ISSUE_TRACKING.md](ISSUE_TRACKING.md)
- **Issue templates**: `.github/ISSUE_TEMPLATE/` (org-level)
- **Security reports**: [SECURITY.md](SECURITY.md)
- **Project template**: Create from "D3Clarity Delivery (Template)" (#5)

Questions? Ask in the team channel or tag your PM.
