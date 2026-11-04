# Contributing to FoodZyn

Thanks for helping build FoodZyn. These rules apply to every repository in the
organization unless a repository says otherwise.

## Issues first

- Every change starts from an issue. Use the issue forms (bug, feature, user story).
- Label new issues with a `type:` label; triage adds `area:` and `priority:`.

## Branches

- `main` is always deployable. Never push to it directly — open a pull request.
- Branch names: `<type>/<issue-number>-<short-description>`, for example
  `feat/42-order-lists` or `fix/57-import-unit-mapping`. A coding agent whose
  session gives it a fixed branch (`claude/…`, `codex/…`) keeps that name.
- Once a branch's pull request is merged, the branch is done. Start the next
  change from an up-to-date `main`; never add commits on top of merged history.

## Commits

We use [Conventional Commits](https://www.conventionalcommits.org/):

```text
feat(catalogue): filter a supplier's articles by price status
fix(imports): keep the original cell value when a row is corrected
docs(adr): propose tech stack options
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `perf`.

- One commit per logical step, each with its own message: pull requests are
  merged with a merge commit, so every commit lands on `main` as written.
- A commit written by a coding agent names it in a `Co-Authored-By:` trailer.

## Pull requests

We work the same way whether a person, Claude Code or Codex writes the change:

1. **Check before you push.** Run the repository's own checks (its `AGENTS.md`
   lists them) on what you changed.
2. **Open a draft.** Push the branch and open a draft pull request against
   `main`. Fill in the template; link the issue with `Closes #123`. Keep it
   small and focused on one issue.
3. **Review the draft.** Before anything else, run a code review of the whole
   pull request: `/code-review <PR number>` in Claude Code, `/review` against
   `main` in Codex (or `@codex review` on the pull request). Check every
   finding against the code, fix the confirmed ones in follow-up commits and
   push them together. Note in the pull request what the review found.
4. **Mark it ready.** That starts CI; drafts are skipped. Every push to a ready
   pull request runs CI again, and private repositories share 2,000 Actions
   minutes a month, so collect fixes into one push.
5. **Get one approving review** from the other side: `CODEOWNERS` requests it,
   and GitHub never asks the author. CI must be green. Our plan does not let
   GitHub enforce either for private repositories, so whoever merges checks both.
6. **Merge with a merge commit**, never squash or rebase, titled
   `Merge pull request #<number>: <pull request title>`. Write the pull request
   title as a Conventional Commit. Then delete the branch.

Coding agents never push to `main`, never force-push a branch someone else
works on, never skip, disable or loosen a test to make CI green, and merge only
when a person tells them to.

Dependabot's grouped updates are the exception: one commit each, squash-merged
by the auto-merge workflow once CI is green.

## Architecture decisions

Significant technical decisions are recorded as ADRs in `docs/adr/` of the
`platform` repository. Propose a new ADR in a pull request before building on a
decision that is hard to reverse.

## Secrets and personal data

Never commit secrets, API keys, `.env` files or real user data. Use example values
in `.env.example` and test fixtures.
