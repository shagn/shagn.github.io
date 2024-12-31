---
title: "Git"
date: "2024-12-30"
description: "Overview of often used commands with examples"
tags: ["Work in progress"]
---

<!-- [this works!](#history) -->

## Terms

`HEAD`: reference pointing to where you are in the commit history (`cat .git/HEAD`)

- Typically pointing to a \``head`\` (the named reference to the commit of the tip of a branch)
- If it not references a branch, it is called `detached HEAD`[^git-scm]

<!-- `--force-with-lease`: only allows a push to proceed if the remote branch hasn't been updated by someone else since your last fetch -->

## Configuration

...

## Create a repository

- Create a new local repository: `git init`
- Clone an existing repository
  - from remote: `git clone <link to repo e.g. https://github.com/dmlc/xgboost>` (creates automatically a remote connection called `origin`)
  - locally: `git clone <path to repo> <path to new directory>`

## Branches

...

## Undo / Reset

...

## History

- Show all commits: `git log` / `git log --oneline`
- Show commits which changed a file: `git log <path to file>` / `git log -p <path to file>`

## Miscellaneous

`git add` is synonymous to `git stage`

Git shortcuts / aliases of oh my zsh git plugin: [ohmyzsh/git.plugin.zsh](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh)

.gitignore templates: https://github.com/github/gitignore

Short cheatsheet:  https://www.git-tower.com/blog/git-cheat-sheet/

[^git-scm]: https://git-scm.com/docs/user-manual.html#glossary
