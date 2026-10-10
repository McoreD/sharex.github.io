---
name: Update ShareX changelog
description: >-
  When asked to bring the ShareX website changelog.md up to date with new
  commits on the ShareX develop branch.
---
# Update ShareX changelog

Inputs: the source repo (ShareX/ShareX, branch `develop`, read-only) and the website fork that holds `changelog.md` (write target, primary branch).

## Rules
- The upstream source repo is read-only: only pull and read it, and never commit there.
- Write and commit only in the website fork, directly on its primary branch (`master`). Don't create a feature branch.
- Push with a normal push only, never a force push, and only when the user asks you to.

## Steps
1. In the fork, run `git checkout master` and `git pull origin master`.
2. In the source repo, run `git checkout develop` and `git pull`.
3. Read `changelog.md` and learn its exact format: the version header pattern `## [ShareX X.Y.Z](https://github.com/ShareX/ShareX/releases/tag/vX.Y.Z) - <date or Unreleased> {#vX.Y.Z}`, the `*` bullets with 4-space nested sub-bullets, grouped "... improvements:" parents, past tense ("Added", "Fixed"), quoted tool names, `<kbd>` keys and inline links.
4. Find the newest version the changelog covers, and match it to its git tag (for example `v21.0.0`). The range to cover is `<tag>..develop`.
5. Go through the commits in that range. Read the actual diffs (`git show`, file stats, new UI strings), not only the commit messages, which are often vague or wrong. Go by what the diff does.
6. Write user-facing entries in the existing style. Leave out internal churn: build and signing changes, package bumps, refactors, translation scripts, README edits and trivial fixes.
7. For the version number, check `Directory.build.props`, but ask the user if the next version isn't clear. Use "Unreleased" until there's a release date.
8. Insert the new section above the previous newest one. Change only `changelog.md`, and don't touch existing lines (watch out for encoding problems).
9. Commit on `master` with the message "Update changelog.md".
10. Report the commit hash, the commit range covered, the new entries, any mismatches between commit messages and diffs, uncertain items, and what you left out on purpose.
