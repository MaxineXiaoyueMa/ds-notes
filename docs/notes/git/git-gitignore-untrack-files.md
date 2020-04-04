gitignore and untrack ignored files

1. create .gitignore file: e.g. `echo .DS_Store >> .gitignore`
  ```shell
  # OSX
  .DS_Store

  # Environment
  .venv

  # Mkdocs
  /site/
  ```

2. untrack everything that is now in .gitignore:
  1. commit all changes
  2. remove everything from the repo: `git rm -r --cached .` (recursively remove all files from the index)
     or, remove a specific file: `git rm --cached some.txt`
  3. re add everything: `git add .`
  4. commit: `git commit -m '.gitignore fix'`
