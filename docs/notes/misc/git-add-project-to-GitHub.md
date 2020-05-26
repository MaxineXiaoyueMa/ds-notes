# How to add a project to Gibhub

## Preparation:
- **Check git is installed on your machine:** `git --version`
- **Download the latest git:** `git clone https://github.com/git/git`

## Create a new repository(repo) in GitHub
1. Click `+ New Repository` on the right hand corner on the menu bar
2. Name the new repo
3. Don't initialize with `README.md` or `.gitignore` yet to avoid conflicts at this time
4. Copy the new repo's URL on clipboard

## Create repo in local directory
0. Open terminal
1. `cd` into the project directory
2. Initialize local repo: `git init`
3. Stage all changes in current directory,
i.e., all files in the curent directory to the repo: `git add --all`
4. Commit all stages files

## Linking the local repo with the remote repo
1. Add the remote repo to the local repo, and alias it as 'origin':
 `git remote add origin copy-new-repo-URL`
2. Verify the remote repo: `git remote -v`
3. Push commits to github repo: `git push origin master(or branch name)`

## Troubleshoot error message: 'git@github.com: Permission denied (publickey)'.
1. Check for existing ssh key: https://help.github.com/en/github/authenticating-to-github/error-permission-denied-publickey
2. Generate a new ssh key: https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
3. Add the ssh key to Github account: https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-accountå



Reference:

- Adding an existing project to GitHub using the command line:
https://help.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line
