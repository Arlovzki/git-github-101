# Git & GitHub 101
SIALANA
The hands-on repository for the Git & GitHub 101 workshop. Fork it, clone your fork,
break things and undo them, branch, and send a pull request. Every command you need
is on the workshop site.

Workshop site: https://www.arloubeloria.com/workshop/git-github-101 (slides, cheat sheet, resources)

## The activity

1. **Fork** this repository into your GitHub account.
2. **Clone your fork** to your laptop: `git clone git@github.com:<your-username>/git-github-101.git`
3. **Add the original as `upstream`**, then sync before you branch:
   ```
   git remote add upstream git@github.com:Arlovzki/git-github-101.git
   git switch main
   git fetch upstream
   git merge upstream/main
   git push
   ```
4. **Branch**: `git switch -c feature/add-your-name`, then add `attendees/<your-username>.md`.
5. **Commit** with an imperative subject under 50 characters: `git commit -m "Add Alex to attendees"`.
6. **Push** the branch to your fork: `git push -u origin feature/add-your-name`.
7. **Pull request** from your fork back to this repository. It gets merged live.

Then pull everyone's names:

```
git switch main
git pull upstream main
```

## origin and upstream

`origin` is your fork. `upstream` is this repository. You push to `origin` and pull from
`upstream`. Your fork does not update itself, so sync before you branch. Every time.

## Naming things

Branch names are a type, a slash, then a few hyphenated words. One topic per branch.

```
feature/add-alex-to-attendees   good: the type, then the what
fix/pages-404                   good: short and searchable
patch-1                         bad: GitHub's default, means nothing
my-stuff                        bad: whose, and what stuff?
```

Commit subjects are imperative, under 50 characters, no full stop. Finish the sentence
"if applied, this commit will ___".

```
Add Alex to attendees             good: says what changed
Fix the 404 on the Pages deploy   good
update                            bad: update what?
final FINAL fix pls work          bad, and you will read it again in a year
```

## The merge strategy: merge, squash, or rebase

The green button on a pull request has a dropdown with three options. They do different
things to history, and the repository lives with whichever you pick.

Say your branch has three commits, `A`, `B` and `C`, and `main` is at `M`.

### Create a merge commit

All three commits land on `main`, plus one extra merge commit tying them together.
Nothing is lost, including the commit you called `wip`. This is GitHub's default, and it
is what produces those `Merge pull request #2 from ...` lines in the log.

```
main:    M ─────────────── merge
              \           /
branch:        A ── B ── C
```

### Squash and merge

The three commits are flattened into one new commit on `main`. Your branch history
disappears and `main` gains a single tidy commit. This is the most common choice on
teams, because one pull request becomes one line in the log.

```
main:    M ── ABC
```

### Rebase and merge

The three commits are replayed one by one on top of `main`, with no merge commit. History
stays linear and every commit is kept, so it only reads well if every commit was worth
keeping. The commits get new IDs, which is why they are written `A'` here rather than `A`.

```
main:    M ── A' ── B' ── C'
```

**If you are unsure, squash.** `git log --oneline` then reads like a changelog instead of
a diary.

### The same two, as commands

Squash and rebase also exist as commands you run yourself, before you ever open a pull
request.

```
git merge --squash feature/thing   stage the branch's work as one change, then commit it
git rebase main                    replay your branch's commits on top of main
git rebase -i HEAD~3               tidy your last 3 commits: reword, squash, drop
git rebase --abort                 back out, any time mid-rebase
```

`git rebase` rewrites commits. That is fine on a branch only you have, and it is the
normal way to clean up before asking for review.

> **The golden rule of rebase:** never rebase a branch other people have already pulled.
> Rewriting shared history forces everyone else to repair their copy. On a shared branch
> use `git revert` instead, which undoes a commit by adding a new one.

## Undo

```
git restore file            throw away edits you have not committed
git reset --soft HEAD~1     uncommit, keep the work staged
git reset --hard HEAD~1     uncommit and discard the work
git revert HEAD             undo a pushed commit by adding a new one
git reflog                  everything you did, including what you thought you lost
```

`restore` for files, `reset` for commits only you have, `revert` for commits others may
have pulled. Never `reset --hard` on a shared branch.
