# Cheatsheet - Git
> **Commonly used git commands**

## Repository
- initialize a git repo:
    1. cd to the directory where we want git to track Changes
    1. initialize the repo: `git init`
- check the contents of a repository: `git status`
- remove git from current directory: `rm -rf .git`
- clone a repository:
`git clone repository_URL`

## Tracking
- add file/folder to staging area:
`git add file_name`

- remove a file that is not ready for a commit, a.k.a., undo add:
`git reset file_name`

- commit change:
`git commit -m "commit message"`

- list all the files being tracked: `git ls-tree -r master --name-only`

- rename a file in git:
`git mv old_file_name new_file_name`
`git commit -m 'rename file'`
`git push origin master`

- check git history, visualize branches :
    - Viewing git log: `git log`
    - Exiting git log: press q (for quit)
    - Viewing git log in graph form
    `git log --graph --abbrev-commit --pretty=oneline`
    `git log --oneline --graph`

    where:
      `--graph` give visualization of branches,
      `--oneline` allows tighter and tidier presentation

```sh
    * | 7d7ee90 update readme.md
    |/
    * 2d26671 update readme.md
```
    vs. without `--oneline`

```sh
    * | commit 7d7ee90df266f08201275427623d78d316e5b959
    |/  Author: Xiaoyue<xxxxxxXiaoyueMa@users.noreply.github.com>
    |   Date:   Fri Mar 20 18:52:23 2020 -0700
    |
    |       update readme.md
    |
    * commit 2d26671d93cfad488e18804f071d409b9dfa17ff
    | Author: Xiaoyue <xxxxxxXiaoyueMa@users.noreply.github.com>
    | Date:   Fri Mar 20 18:35:16 2020 -0700
```
- compare the difference between two versions::
`git diff first_id second_id`

- compare the difference between working directory and staging area:
`git diff`

- compare the difference between staging aread and most recent commit:
`git diff --staged`

- compare the difference between a commit and its parent:
`git show commit_id`

- restore to a commit temporarily:
`git checkout commit_id`

## Remote
- add a remote repository:
`git remote add origin repository_url`

- update/sync remote repository with local repo:
`git push origin master`

- check remote repository status:
`git remote`

- get more information on remote:
`git remote show origin`

- update/sync local repo with remote repo:
`git pull origin master`

- rename a remote repository:
    - rename remote repo on github,
    - update local repo's remote url:
  `git remote set-url origin new-rul`
- check remote repo url:
`git config --get remote.origin.url`

- remove a remote repository:
`git remote -v`
`git remote rm origin`
`git remote -v`

- comprare the difference between remote and local:
`git fetch` + `git diff ...origin/master`



## Branch
- create a branch:
`git branch branch_name`

- check which branch is being worked on:
`git branch`

- delete a branch:
`git branch -d branch_name`

- merge a branch:
`git merge name`
If confict, make changes, then:
`git add file_name(where conflicts occur)`
`git commit`

- push a branch to the remote:
`git push (to) remote_name branch_name`

## Utilities
- check the git version: `git --version`

- get colored Output:
  `git config --global color.ui auto`

- colors:
    - green="\[\033[0;32m\]"
    - blue="\[\033[0;34m\]"
    - purple="\[\033[0;35m\]"
    - reset="\[\033[0m\]"

- Change command prompt
`source ~/git-prompt.sh`
`export GIT_PS1_SHOWDIRTYSTATE=1`
`export PS1="$purple\u$green\$(__git_ps1)$blue \W $ $reset"`
    - `\u` adds the name of the current user to the prompt
    - `\$(__git_ps1)` adds git-related stuff
    - `\W` adds the name of the current directory
