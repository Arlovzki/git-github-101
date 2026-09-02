# Git & GitHub 101

The hands-on repository for the Git & GitHub 101 workshop. Fork it, clone your fork,
break things and undo them, branch, and send a pull request. Every command you need
is on the workshop site.

Workshop site: https://www.arloubeloria.com/workshop/git-github-101 (slides, cheat sheet, resources)

## The activity

1. **Fork** this repository into your GitHub account.
2. **Clone your fork** to your laptop: `git clone git@github.com:<your-username>/git-github-101.git`
3. **Branch**: `git switch -c add-your-name`, then add `attendees/<your-username>.md`.
4. **Pull request** from your fork back to this repository. It gets merged live.

Then pull everyone's names:

```
git remote add upstream git@github.com:Arlovzki/git-github-101.git
git pull upstream main
```
