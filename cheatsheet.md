# Git cheat sheet

## Once

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global pull.rebase false
ssh-keygen -t ed25519 -C "you@example.com"
ssh -T git@github.com
```

## Every day

```
git status
git add .
git commit -m "message"
git push
git pull
```

## Per project

```
git init
git remote add origin git@github.com:user/repo.git
git push -u origin main
git clone git@github.com:user/repo.git
```

## When needed

```
git switch -c name
git switch main
git merge name
git restore file
git reset --soft HEAD~1
git reset --hard HEAD~1   # discards work
git revert HEAD
git reflog
```
