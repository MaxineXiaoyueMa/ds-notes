# Cheatsheet - Git
**Commonly used git commands**

## Repository
- initialize a git repo:
    1. cd to the directory where we want git to track Changes
    1. initialize the repo: `git init`
- check the contents of a repository: `git status`
- remove git from current directory: `rm -rf .git`

## Tracking
- add file/folder to staging area: `git add file_name`
- remove a file that is not ready for a commit, a.k.a., undo add: `git reset file_name`
- commit change: `git commit -m "commit message"`
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
    * 6afe247 delete files now in .gitignore
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

## Remote

- Adding a remote repository: `git remote add origin repository_url`
- update remote repo:`git push origin master`
- Checking remote repository status:`git remote`
- update local repo:`git pull origin master`
- Remove a remote repository:
`git remote -v`
`git remote rm origin`
`git remote -v`
- Comprare the difference between remote and local:
`git fetch` + `git diff ...origin/master`

- Comparing the difference between two versions::
`git diff first_id second_id`
- Comparing the difference between working directory and staging area:
`git diff`
- Comparing the difference between staging aread and most recent commit:
`git diff --staged`
- Comparing the difference between a commit and its parent:
`git show commit_id`

- Cloning a Repository:
`git clone repository_URL`

- Getting Colored Output:
`git config --global color.ui auto`

- Restoring to a commit temporarily:
`git checkout commit_id`

HEAD_current commit
Octopus_

## branches
- Create a branch
`git branch branch_name`
- Checking which branch is being worked on
`git branch`

- Delete a branch
`git branch -d branch_name`

- Merge a branch
`git merge name`
If confict, make changes, then:
`git add file_name(where conflicts occur)`
`git commit`

- Pushing a branch to the remote
`git push (to) remote_name branch_name`

---

setting up workspace recanolrence:
https://classroom.udacity.com/courses/ud775/lessons/2980038599/concepts/33331589510923#

[git config --global core.editor "'/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl' -n -w"
git config --global push.default upstream
git config --global merge.conflictstyle diff3]

## Utilities

- Checking the git version: `git --version`
- source ~/git-completion.bash

- colors!
green="\[\033[0;32m\]"
blue="\[\033[0;34m\]"
purple="\[\033[0;35m\]"
reset="\[\033[0m\]"

- Change command prompt
source ~/git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
- '\u' adds the name of the current user to the prompt
- '\$(__git_ps1)' adds git-related stuff
- '\W' adds the name of the current directory
export PS1="$purple\u$green\$(__git_ps1)$blue \W $ $reset"

## .gitignore
- create .gitignore file:
  ```text
  # OSX
  .DS_Store

  # Environment
  .venv

  # Mkdocs
  /site/
  ```
- untrack everything that is now in .gitignore:
  1. commit all changes
  2.  remove everything from the repo: `git rm -r --cached .` (recursively remove all files from the index)
  3. re add everything: `git add .`
  4. commit: `git commit -m '.gitignore fix'`
