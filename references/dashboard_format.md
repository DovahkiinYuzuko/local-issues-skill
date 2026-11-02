# local-issues DASHBOARD Format Specification

This document defines the output contract for `docs/local-issues/DASHBOARD.md`.

```markdown
<!-- GENERATED FILE - DO NOT EDIT MANUALLY. Run 'issue_hub.py sync' to regenerate. -->
# {Project Name} Task Dashboard

- **Last Updated**: yyyy-MM-dd
- **Total Issues**: {N}
- **Completion Rate**: {X.X}% ({Done}/{Total})

## Progress Summary

| Status | Total Issues |
| :---: | :---: |
| 🟩 Done | {N} |
| 🟨 In Progress | {N} |
| 🟦 Ready to Start | {N} |
| 🟥 Blocked | {N} |

### Recommended Next Steps (Prioritized by unblock impact)

- [ ] [issue-{num}: {Title}](./not-started/{category}/issue-{num}-{slug}.md) (Unblocks {count} task(s))

---

## Category: {CATEGORY}

<details open>
<summary>Click to expand ({N} items)</summary>

| Status | Issue | Description | Prerequisites |
| :---: | :--- | :--- | :--- |
| 🟩 | [issue-1](./done/feat/issue-1-db.md) | **{Title}**<br>{Description} | None |
| 🟦 | [issue-2](./not-started/feat/issue-2-api.md) | **{Title}**<br>{Description} | issue-1 (🟩Done) |
| 🟥 | [issue-3](./not-started/feat/issue-3-ui.md) | **{Title}**<br>{Description} | issue-2 (🟦Ready) |

</details>

---
```

## Frontmatter Contract for `issue-*.md`
Each task markdown file in `docs/local-issues/{not-started,wip,done}/` should contain:

```markdown
---
type: feat             # feat | fix | refactor | chore | docs
description: "Brief summary of the issue"
depends_on:            # Optional list of prerequisite issue IDs
  - issue-1
---

# issue-{num}: {Title}

## Overview
...
```
