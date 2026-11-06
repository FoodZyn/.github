# Contributing to FoodZyn

Thanks for helping build FoodZyn. These rules apply to every repository in the
organization unless a repository says otherwise.

## Issues first

- Every change starts from an issue. Use the issue forms (bug, feature, user story).
- Label new issues with a `type:` label; triage adds `area:` and `priority:`.

## Branches

- `main` is always deployable. Never push to it directly — open a pull request.
- Branch names: `<type>/<issue-number>-<short-description>`, with `type` from
  the commit types below and a few lower-case words joined by hyphens, for
  example `feat/42-order-lists` or `fix/57-import-unit-mapping`; without an
  issue, `<type>/<short-description>`, such as `docs/pr-workflow`.
- Coding agents name their branches the same way. A session handed a generated
  branch (`claude/…`, `codex/…`) creates a properly named one from `main` and
  works and pushes there. Only where its environment can push nowhere else
  does it keep the generated name and say so in the pull request. Dependabot's
  branches keep their own names.
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
   small and focused on one issue. Whenever work stops before it is done,
   push it and write its state in the template's *Handover* section, so the
   next person or agent session can continue from the pull request alone.
3. **Review the draft.** Before anything else, run a code review of the whole
   pull request: `/code-review <PR number>` in Claude Code, `/review` against
   `main` in Codex (or `@codex review` on the pull request). Check every
   finding against the code and give each confirmed one a category:
   - *blocker*: the change itself is wrong (a bug, a security hole, a broken
     business rule, a test that proves nothing); fixed before the merge.
   - *small*: a wrong comment, commit or pull request text, or a missing test
     for what the pull request claims; fixed in the same round.
   - *later*: true, but older than the pull request or outside its scope; it
     becomes an issue (or a line in the repository's plan), linked from the
     pull request.
   - *drop*: taste, or already settled in an ADR or a decision log; not fixed.

   Push the fixes together. Only fixed blockers earn another review, which
   checks the fixes and looks for new blockers; its smaller findings go to
   *later*. The loop ends when no blocker is left. List the findings with their
   category in the pull request's "Review" section; the review itself posts
   nothing to the pull request unless its author asks.

   **A change people see gets a design review too.** When a pull request
   changes what people see in an app or site (pages, components, layout, UI
   texts), check every page it reaches with the impeccable skill,
   `/impeccable critique <page>` and `/impeccable audit <page>`, at desktop
   and phone width and in each role whose view differs; a repository's
   `AGENTS.md` names its widths and how the review runs there. Use a local
   app with synthetic data: never real customer data, and never save,
   upload or submit anything on a live site or backend. Until the skill is
   installed for an agent (Codex), the pull request says the design review
   did not run, and the other person runs it before approving. Its findings
   get the same categories; a WCAG 2.2 AA failure the change brings in is a
   blocker, an older one *later*. A fixed blocker earns another round of the
   review it came from, and of the design review too when the fix changes
   what people see. List the findings next to the code review's and attach
   the screenshots it took.
4. **Mark it ready.** That starts CI; drafts are skipped. Every push to a ready
   pull request runs CI again, and private repositories share 2,000 Actions
   minutes a month, so collect fixes into one push.

   **Skip CI where it has nothing to check.** When a push changes nothing CI
   tests beyond what you already checked locally (documentation after
   `markdownlint-cli2`, comments, templates), its head commit message carries
   `[skip ci]` and the pull request says which checks ran locally. Code,
   tests, dependencies, migrations, the Dockerfile and the workflows always
   run CI.
5. **Get one approving review** from the other side: `CODEOWNERS` requests it,
   and GitHub never asks the author. CI must be green, or skipped as above.
   Our plan does not let GitHub enforce either for private repositories, so
   whoever merges checks both.
6. **Merge with a merge commit**, never squash or rebase, titled
   `Merge pull request #<number>: <pull request title>`. Write the pull request
   title as a Conventional Commit. Then delete the branch.

Coding agents never push to `main`, never force-push a branch someone else
works on, never skip, disable or loosen a test to make CI green, and merge only
when a person tells them to.

Dependabot's minor and patch groups are the exception: one commit each,
squash-merged by the auto-merge workflow once CI is green. Major and security
updates wait for a person and are merged like any other pull request.

## Architecture decisions

Significant technical decisions are recorded as ADRs in `docs/adr/` of the
`platform` repository. Propose a new ADR in a pull request before building on a
decision that is hard to reverse.

## Secrets and personal data

Never commit secrets, API keys, `.env` files or real user data. Use example values
in `.env.example` and test fixtures.
