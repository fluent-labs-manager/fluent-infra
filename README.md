# Fluent Infrastructure

This repository stores organization-wide infrastructure configuration for Fluent Labs Manager.

## Main branch ruleset

The [`main-branch-ruleset.json`](rulesets/main-branch-ruleset.json) file defines the active repository ruleset for the default branch (`main`). Its purpose is to keep the branch stable, reviewed, and continuously checked before changes are merged.

### Protected operations

- Deleting the default branch is blocked.
- Non-fast-forward updates are blocked, so force-pushing to `main` is not allowed.

### Pull request requirements

Changes to `main` must be merged through a pull request that has:

- At least one approving review.
- Stale approvals dismissed when new commits are pushed.
- All review threads resolved before merge.
- An additional approval when a change is not attributed to a GitHub user.

Merge commits, squash merges, and rebase merges are all permitted. Code-owner review and approval of the last push are not currently required.

### Automated checks and reviews

- Required status checks are enabled, but no individual check is currently configured as mandatory and the ruleset does not require branches to be up to date before merging.
- Code scanning is enforced with CodeQL: security alerts must be `high` severity or higher, and alert results must have the `error` level.
- Copilot code review runs for every push, including draft pull requests.
