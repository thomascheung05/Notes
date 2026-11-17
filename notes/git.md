# Git

## Setup

```bash
gh auth login        # log in to GitHub (GitHub CLI)
gh repo create       # create a new repo
git clone <repo url> # clone a repo
```

## Everyday commands

| Command | What it does |
|---|---|
| `git pull` | Pull latest updates to the repo |
| `git status` | Check local repo status |
| `git add myfile.py` | Add a single file to the commit |
| `git add .` | Add all changes to the commit |
| `git commit -m 'my commit message'` | Commit |
| `git push` | Push |

## Saving your work to GitHub

1. `git status` — see what needs to be committed
2. `git add <files>` — add the files you've edited
3. `git commit -m "what you changed"` — describe the edits
4. `git push` — finalize

## Return to a previous commit

1. `git log --oneline` — list commits (press `q` to exit)
2. `git reset --hard <commit SHA>` — **deletes all newer work** and returns to that commit
3. `git push --force` — make GitHub match (only if the newer commits were already pushed)

> Don't `git pull` after a reset — it pulls the newer commits straight back down.

## Branches

```bash
git branch                    # see active branch
git branch -a                 # see all branches (incl. remote)
git fetch origin              # update local git with online branches
git checkout <branch name>    # switch branches
git checkout -b my-new-branch # make a new local branch and switch to it
git branch -d <branch name>   # delete a local branch
git push origin --delete <branch name>  # delete a branch on GitHub
```

## Merge two branches

Merging `dev` changes into `master`:

1. Commit and push your `dev` changes
2. `git checkout master`
3. `git pull` — make sure master is up to date
4. `git merge dev`
5. `git push`
