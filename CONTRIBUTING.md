# Contributing to FoodZyn

Thanks for helping build FoodZyn. These rules apply to every repository in the
organization unless a repository says otherwise.

## Issues first

- Every change starts from an issue. Use the issue forms (bug, feature, user story).
- Label new issues with a `type:` label; triage adds `area:` and `priority:`.

## Branches

- `main` is always deployable. Never push to it directly — open a pull request.
- Branch names: `<type>/<issue-number>-<short-description>`, for example
  `feat/42-company-pages` or `fix/57-feed-pagination`.

## Commits

We use [Conventional Commits](https://www.conventionalcommits.org/):

```text
feat(feed): show sourcing stories from connected producers
fix(jobs): keep salary range when editing a posting
docs(adr): propose tech stack options
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `perf`.

## Pull requests

- Keep pull requests small and focused on one issue; link it with `Closes #123`.
- Fill in the pull request template, including how you tested the change.
- At least one approving review before merging. CI must be green.
- Squash-merge; the pull request title becomes the commit message, so write it as a
  Conventional Commit.

## Architecture decisions

Significant technical decisions are recorded as ADRs in `docs/adr/` of the
`platform` repository. Propose a new ADR in a pull request before building on a
decision that is hard to reverse.

## Secrets and personal data

Never commit secrets, API keys, `.env` files or real user data. Use example values
in `.env.example` and test fixtures.
