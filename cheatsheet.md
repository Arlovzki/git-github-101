# Git cheat sheet

## Once

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase false
ssh-keygen -t ed25519 -C "you@example.com"
ssh -T git@github.com
gh auth login             # or let the GitHub CLI do all of it
```

## Every day

```
git status
git diff
git add .
git commit -m "message"
git push
git pull
git log --oneline
```

## Per project

```
git init
git remote add origin git@github.com:user/repo.git
git push -u origin main
git clone git@github.com:user/repo.git
git remote -v
git remote add upstream git@github.com:owner/repo.git
```

## Someone else's repo, every pull request

```
git switch main                                  1. start from a clean main
git fetch upstream && git merge upstream/main    2. sync before you branch
git push                                         3. update your fork too
git switch -c feature/the-thing                  4. type/what, one topic
git commit -m "Add the thing"                    5. imperative, under 50 chars
git push -u origin feature/the-thing             6. then open the pull request
                                                 7. title, what and why, Closes #12
git switch main && git pull                      8. after it merges
git branch -d feature/the-thing                  9. tidy up
```

## The merge strategy

Three commits `A B C` on your branch, `main` at `M`. The dropdown beside the green
Merge button picks which of these you get.

```
Create a merge commit    main: M ─────── merge     keeps every commit, adds one more
                                \       /
                                 A B C

Squash and merge         main: M ── ABC            one pull request, one commit

Rebase and merge         main: M ── A' B' C'       linear, every commit kept, new IDs
```

Unsure? **Squash.** The log then reads like a changelog instead of a diary.

The same two as commands, for cleaning up before review:

```
git merge --squash feature/thing   stage the branch's work as one change
git rebase main                    replay your commits on top of main
git rebase -i HEAD~3               reword, squash or drop your last 3 commits
git rebase --abort                 back out mid-rebase
```

**Golden rule:** never rebase a branch other people have pulled. Rewriting shared history
forces everyone else to repair their copy. Use `git revert` on a shared branch.

## Merge conflicts

```
git status                which files are conflicted
                          edit the file: keep what you want, delete the
                          <<<<<<<  =======  >>>>>>>  lines
git add the-file          staging it means resolved
git commit                no -m; Git wrote the message already
git merge --abort         bail out, nothing lost
```

## When needed

```
git switch -c name
git switch main
git merge name
git branch -d name
git restore file
git reset --soft HEAD~1
git reset --hard HEAD~1   # discards work
git revert HEAD
git reflog
git blame file
```
