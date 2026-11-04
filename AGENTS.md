# FoodZyn `.github`: rules for people and agents

This repository holds the organisation's public profile and the defaults every
FoodZyn repository inherits. It is public: never put internal information,
names of customers, prices or credentials here.

- Commits, branches and pull requests follow [CONTRIBUTING.md](CONTRIBUTING.md),
  the same for people, Claude Code and Codex: draft pull request, code review
  of the draft with every finding categorised (blocker, small, later, drop),
  a design review with the impeccable skill when the user interface changes,
  ready for review, one approving review, merge commit.
- The profile describes FoodZyn as being built: intentions ("is meant to"),
  never figures, customers or results.
- A file here is the default for every repository that has none of its own;
  check what a change does to `platform` and `website` before making it.

## Checks before a push

```bash
npx --yes markdownlint-cli2@0.18.1 "**/*.md"
```
