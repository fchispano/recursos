# GIT CheatSheet
## Configuration
* `git config --global user.name "John Doe"`  →  config the user name for local repositories
* `git config --global user.email johndoe@example.com`  →  config the user email for local repositories
* `git config --global core.editor <editor path>`  →  config main text editor for edit git related stuff
* `git config --global core.editor “’editor_path’ -n -w"`
* `git remote add <remote name> <url>`  →  create the remote repository

## Working with the repo
* `git init`  →  start a git repo in the working folder
* `git add (file)`  →  begin tracking changes in `file` and prepare it to be committed, that's known as "stage" a file, because we add it to the staging area
* `git add .`  →  stage all files: new, modified or deleted
* `git add -A` or `git add --all`  →  does the same that the previous command, but looks more straightforward
* `git commit -m “message"`  →  commit all staged files and add a short message explaining the changes
* `git commit -am “message"`  →  stages all tracked files and does a commit with the specified message
* `git push <remote-repo> <local-branch>`  →  push the changes in `<local-branch>` to `<remote-repo>`
* `git pull <remote-repo> <local-branch>`  →  pull the changes in `<remote-repo>` not in `<local-branch>`
* `git fetch`  →  new label on the local repository with the commits up-to-date of remote
* `git push --all <remote-repo>`  →  push all branches to `<remote-repo>`, useful when you want to push changes in several branches (caveat: keep your local branches tidy and clean)
* `git branch`  →  list all the branches in the repository
* `git branch <new-branch-name>`  →  create a new branch `<new-branch-name>
* `git checkout -b <new-branch-name>`  →  create and move the a new branch `<new-branch-name>`
* `git branch -d <branch-name-to-delete>`  →  delete the branch `<branch-name-to-delete>` (the branch changes must be fully merged in upsteam, usually master, or the deletion will fail)
* `git branch -m <old-branch-name> <new-branch-name>`  →  rename a local branch
* `git push <remote-repo> :<remote-branch>`  →  delete a remote branch, be careful!
* `git push <remote-repo> :<remote-old-branch-name> <remote-new-branch-name>`  →  delete the remote old branch name and push the just renamed branch
* `git merge <branch-name>`  →  merge `<branch-name>` with the actual branch
* `git merge --no-ff <branch-name>`  →  avoid fast-forward merge, creating a commit for the merge

## Retrieving information
* `git diff`  →  show differences between what is already in the index and files that have changed and could be added
* `git diff <hash1> <hash2>`  →  show differences between commit with `<hash1>` and commit with `<hash2>`
* `git diff <branch1>..<branch2>`  →  show what is in `<branch2>` that isn't in `<branch1>`
* `git diff <branch1>...<branch2>`  →  show what is in `<branch1>` or in `<branch2>`, but not in both (XOR operation)
* `git log`  →  shows the commit log
* `git log --graph --oneline`  →  shows a resumed version of `git log`, and draws with ASCII a commit history graph
* `git remote`  →  list remote repositories
* `git remote -v`  →  as `git remote` but with extra info
* `git ls-files`  →  See files being tracked

## Undo and modify commits
* `git reset`  →  remove all from staging area
* `git commit --amend -m <“message”>`  [Edit an incorrect commit message in Git](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git)
* `git rm --cached file.txt`  →  delete a file from the repo but not from the filesystem
* `git reset --hard <commit>`  →  revert last changes to the commit, for the last changes we can use HEAD as commit

### Undo a commit and redo
```
$ git commit -m "Something terribly misguided"              (1)
$ git reset --soft HEAD~                                    (2)
$< edit files as necessary >>                               (3)
$ git add .                                                 (4)
$ git commit -c ORIG_HEAD                                   (5)
```
[Source](http://stackoverflow.com/questions/927358/how-do-you-undo-the-last-commit)

## Contributing

### Process to contribute and solve merge conflicts:
1. Fork the repository
2. Make changes on a local branch
3. pull Master to be up-to-date
4. merge master into you branch
5. push your branch
6. pull request to merge.

### Keep your forked repository up-to-date with the original
Configure the remote upstream. **You have to do this just once**

1. `git remote add upstream https://github.com/fchispano/recursos.git`

Get the latest changes in the repo:

2. `git fetch upstream`
3. `git checkout master`
4. `git merge upstream/master`

Sources:
* [Configuring a remote for a fork](https://help.github.com/articles/configuring-a-remote-for-a-fork/)
* [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)
* [A successful git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
