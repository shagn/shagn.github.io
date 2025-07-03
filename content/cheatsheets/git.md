---
title: "Git"
description: "Overview of often used commands with examples"
date: "2025-07-03"
tags: ["wip"]
draft: false
---

## Glossary

`HEAD`: reference pointing to where you are in the commit history (check with `cat .git/HEAD`)

- Typically pointing to a `head` (the named reference to the commit of the tip of a branch)
- If it not references a branch, it is called `detached HEAD`[^git-scm]

<!-- `--force-with-lease`: only allows a push to proceed if the remote branch hasn't been updated by someone else since your last fetch -->

## Configuration

Each git config variable can be stored in 3 different levels:

1. `--system`: System level - applied to every user user on the system and all their repositories
1. `--global`: Global level - values specific personally to you, the user
1. `--local`: Repository level - specific to a single repository

- View configuration:

  - all levels: `git config --list`
    - `--show-origin`: with origin
  - for a specific level: `git config --list --system/global/local`

- Set configuration: `git config --system/global/local <setting> <value>`

  - e.g. system: `git config --system color.ui true`
  - e.g. setting user name: `git config --global user.name "John Doe"`
  - e.g. setting empty user email for a repo: `git config --local user.email '<>'`
  - e.g. setting _nano_ as editor: `git config --global core.editor "nano"`

- Delete configuration:

  - one value: `git config --global --unset user.name`
  - one section: `git config --global --remove-section user`

- Edit configuration file directly: `git config --global --edit`

Selected configuration parameters

- _user.name_
- _user.email_
- _push.autoSetupRemote_

> \[!TIP\]
> git config --global rererre.enabled true  # remembers conflict resolution
> git config --global column.ui auto
> git maintenance start [^git-video]

## Create a repository

- Create a new local repository: `git init`
- Clone an existing repository
  - from remote: `git clone <link to repo e.g. https://github.com/dmlc/xgboost>` (creates automatically a remote connection called `origin`)
  - locally: `git clone <path to repo> <path to new directory>`

## Branches

- List existing branches: `git branch`

  - `-a`: list both remote-tracking branches and local branches
  - `-v`: list remote-tracking branches

- Create a branch: `git branch <branchname>`

- Switch to a branch: `git switch <branchname>`

- Delete a branch:

  - local: `git branch --delete <branch name>`
  - remote: `git push origin --delete <branch name>`

- Rename a branch:

  - local branch: `git branch -m <branchname> <new branchname>`
  - remote branch: `git remote rename <branchname> <new branchname>`

- Set tracking information to a local branch: `git branch --set-upstream-to=origin/<remote branch> <local branch name>`

## Make a commit

- Show the current status: `git status`

  - `-s`: show only affected files and their short status

- Show changes in a file: `git diff <path to file>`

- Stage / Unstage files:

  - stage everything: `git add .`
  - stage specific file `git add <path to file>`
  - unstage specific file `git restore --staged <path to file>`
    (`git add` is synonymous to `git stage`)

- Create a commit

  - with a message: `git commit -m '<commit message>'`
  - without triggering pre-commit and commit-msg hooks: `git commit -m '<commit message>' --no-verify`

- Change the last commit:

  - change the commit message: `git commit --amend -m "an updated commit message"`
  - change files: `git commit --amend --no-edit`

- Squashing commits:

  - Squashing the last _n_ commits:
    - `git reset --soft HEAD~<n>`
    - `git commit -m "<new commit message>"`
    - (`git push --force-with-lease"`)

## Undo / Reset

### Local

- Undo the last commit, unstage changes: `git reset HEAD~1`
- Undo the last commit, keep the changes staged: `git reset --soft HEAD~1`
- Undo changes to a tracked file: `git checkout -- <path_to_file>`
- Remove local untracked files: `git clean -f -d`
- Reset to a remote branch: `git reset --hard <remote name e.g. origin>/<branch name>`

### Puplic

`git revert` e.g. revert last commit `git revert HEAD`

## Remote

The `git remote` command lets you manage connections to other repositories.

- List configured remotes: `git remote -v`
- Add remote: `git remote add <remote name e.g. origin> <remote_url>`
- Remove remote: `git remote remove/rm <remote name e.g. origin>`

## Update / Publish

- `git fetch`: downloads all changes from remote, but does not update the local repo's working state
  - `--prune/-p`: remove any remote-tracking references that no longer exist on the remote [^git-scm-fetch]
- `git pull`: downloads all changes from remote and directly merges it into `HEAD`
- merge changes from one branch into another: (on the branch which should be merged into) `git merge <branchname which should be merged>`
- rebase a branch on another: `git rebase <branchname which should be rebased on>`
- cherry-picking: `git cherry-pick <commit_id>`

## Stash

- Show stashes: `git stash list`
- Create a stash:
  - `git stash save "<name>"`
  - `--staged`: only stash staged files
- Show changes of stash: `git stash show`
- Apply the last stash:
  - with deleting: `git stash pop`
  - without deleting: `git stash apply`
- Apply specific file/stash:
  - `git stash apply 1`
  - only retrieve one file from stash: `git checkout stash@{0} -- <file_name>`
- Delete a stash:
  - the last one: `git stash drop`
  - all stashes: `git stash clear`
- Recover (recently) deleted stash:
  1. If terminal is still open:
  - get hash from the `git stash pop` command
  - otherwise use `git fsck --no-reflog | awk '/dangling commit/ {print $3}'`
  2. `git stash apply <hash>`

## History

- Show all commits: `git log` / `git log --oneline`
- Show commits which changed a file: `git log <path to file>` / `git log -p <path to file>`

## Miscellaneous

Git shortcuts / aliases of oh my zsh git plugin: [ohmyzsh/git.plugin.zsh](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh)

.gitignore templates: https://github.com/github/gitignore

Short cheatsheet:  https://www.git-tower.com/blog/git-cheat-sheet/

## References

[^git-scm]: https://git-scm.com/docs/user-manual.html#glossary
[^git-scm-fetch]: https://git-scm.com/docs/git-fetch
[^git-video]: https://www.youtube.com/watch?v=aolI_Rz0ZqY
