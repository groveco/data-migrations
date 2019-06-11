# Data Migrations for [Grove][groveco/grove]

This repository represents standalone data migrations for our [main
application][groveco/grove] that are either in proposal or have been applied to
the production database. Alongside this `README` file are a number of
directories indicating the order of the data migrations as they have been
applied. For example:

```
-+ README.md -- this document
 |-+ migrations_0001 -- the first data migration
 | |- README.md -- What does it do? How do I do it?
 | |- Pipfile -- Python requirements, if any
 | |- supporting.py -- referenced in `README.md`
 | +- some-gnarly.sql -- that I might need to run per `./README.md`
 +-+ migrations_XXXX -- the XXXX-th migration
   +- . . . -- you get the picture, I hope.
```

## The Process

### 1. Create a new branch containing `migrations_XXXX/README.md` that describes the work to be done.

- Include the reasons _why_ the migration is applied, referencing JIRA issues
  or PRs from [the main repo][grovceco/grove]
- Include step-by-step instructions for how to apply the migration, referencing
  support files as necessary.
- Please _always_ include instructions and support files to reverse-apply the migration.

### 2. Open a Pull Request and solicit code reviews

- Please review the proposed migration up and down and attempt applying it in a safe environment.

### 3. Merge to `master` when approved!

- This signals that the proposed migration slot is "taken" and outstanding PRs
  should catch up, possibly renumbering their own migrations. [See "Pro
  Tips"](#pro-tips).
- Migrations in `master` are "ready to be applied" in a DevOps task. [See
  "Applying Migrations"](#applying-migrations)

## Applying Migrations

- Create a branch named `applying-migrations---XXXX-YYYY` where `XXXX` is the
  first migration to be applied and `YYYY` is the last. It's okay to omit
  `YYYY` if there's only one.
- Patch each migrations' `README` file with the date and time of when the
  migration was applied at the _top_ of the file, e.g.
  ```markdown
  ---
  appliedAt: 2019-05-01
  ---
  ```
- Include any notes or deviations that were necessary from the instructions,
  first as comments in the PR, then as adjustments to the `README.md`
- Get approval via a Code Review and merge to `master`; the merge commit will
  refer to the PR that applied the migrations for traceability.

## Pro Tips

It's recommended that you name the branch according to the _intent_ of the
migration rather than the number, as another Engineer might need to "jump the
line" and publish a simpler or higher-value migration ahead of yours.

For example, a branch named `migrate-orders-to-historical-models` might contain
`migrations_1234/README.md` because `1234` is the next number in the sequence.
While in review, _another Engineer_ proposes `migrate-expired-offers-2019-Q3`
that _also_ contains `migration_1234/README.md`, since that is stil _the next
migration to run_, and gets it merged ahead of the earlier-opened PR.

The first Engineer now has conflicts for `migrations_1234/README.md` and needs
to renumber the migration in the branch before it can be merged.

If there's ever a time that _many_ branches and PRs are outstanding, Engineers
should coordinate their work by figuring out a reasonable order to merge and
renumber. Communication trumps process!

[groveco/grove]: https://github.com/groveco/grove
