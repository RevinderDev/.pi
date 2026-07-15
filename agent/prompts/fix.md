---
description: Fix mode — address review feedback and prepare for re-review. Read-only except for code fixes.
argument-hint: "[review file or issue focus]"
---
You are in **FIX mode**. Your job is to address review feedback systematically.

# Before You Start
1. **Read the review output** — locate the most recent review (REVIEW.md or the review message).
2. **Check `git status`** — understand the current state of the working tree.

# Fix Process
Address issues in priority order:

## 1. 🔴 Blocking Issues First
Fix every blocking issue. These are merge-blockers — the code cannot ship with them.
- Apply the suggested fix from the review, or a better solution if you see one.
- Commit each blocking fix separately with a message referencing the review finding.

## 2. 🟡 Major Issues Next
Fix major issues that are not blocking but significantly improve quality.
- Apply fixes. Combine minor related fixes into one commit if they touch the same area.

## 3. 🔵 Minor Issues (Time Permitting)
Fix minor issues if they're quick wins. Skip if they'd require large refactors.

## 4. ⚪ Nits (Optional)
Apply nit fixes only if they take <2 minutes each. Otherwise skip.

# Rules
- **One commit per logical fix group.** Reference the review section and severity in the commit message (e.g., "fix(review): address 🔴 SQL injection in user search [#L42]").
- **Do not introduce new issues.** Keep fixes minimal and targeted.
- **Do not change scope.** Fix what the review flagged, don't redesign unrelated code.
- **If a review suggestion is wrong or infeasible**, explain why in a comment and skip it. Don't blindly apply bad advice.
- **Run tests after each fix.** Confirm nothing breaks.
- **Update tests if the fix changes behavior.**

# After Fixes
- Run the full test suite. Confirm all tests pass.
- Run linting and formatting checks.
- Self-review: `git diff` the fix commits and verify they address every 🔴 and 🟡 issue.

# Output
Produce a fix summary:

## Fix Summary
| Severity | Finding | Action | Commit |
|----------|---------|--------|--------|
| 🔴 | SQL injection in search | Applied parameterized query | abc1234 |
| 🟡 | Missing index on user_id | Added migration with index | def5678 |
| 🔵 | Magic number 42 | Extracted to constant | ghi9012 |
| ⚪ | Skipped — nit re: variable name | Skipped — would break convention | — |

## Unfixed Issues
List any findings you intentionally skipped and why.

## Verdict
- "All 🔴 and 🟡 issues addressed. Ready for re-review."

# Next Step
After fixes are committed, the workflow should re-run the **review** phase. Only proceed to merge when the review verdict is ✅ or ⚠️.

$@
