# GIT CheatSheet
## Configuration
* `git config --global user.name "John Doe"`
* `git config --global user.email johndoe@example.com`
* `git config --global core.editor <editor path>`
* `git config --global core.editor “’editor_path’ -n -w"`
* `git remote add <remote name> <url>` (create the remote repository)

## Working with the repo
* `git init`
* `git add (file)`
* `git add .`
* `git commit -m <“message">`
* `git push <remote repo> <local branch>`
* `git pull <remote repo> <local branch>`
* `git fetch` (new label on the local repository with the commits up-to-date of remote)
* `git branch`
* `git branch <new_branch_name>`
* `git checkout -b branchName`
* `git branch -d <branch_name_to_delete>` (delete the branch label, not the commits!)
* `git branch -m old_branch_name new_branch_name` (rename a local
  branch)
* `git push <remote_repo> :<remote_branch>` (delete a remote branch, be careful!)
* `git push <remote repo> :<remote_old_branch_name>
  <remote_new_branch_name>` (delete the remote old branch name and push
  the just renamed branch)
* `git merge branchName`
* `git merge --no-ff branchName` (avoid fast-forward merges creating always a commit for the merge)

## Retrieving information
* `git diff`
* `git diff <hash1> <has2>`
* `git diff <branch1>..<branch2>` (show what is in branch2 that isn't in
  branch1)
* `git diff <branch1>...<branch2>` (show what is in branch1 or in
  branch2, but not in both [XOR operation])
* `git log`
* `git log --graph --oneline`
* `git remote` (show remote repository)
* `git remote -v` (as git remote but with extra info)

## Undo and modify commits
* `git reset` (remove all from staging area)
* `git commit —amend -m <“message”>` [Edit an incorrect commit message in Git](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git)
* `git rm --cached file.txt` (delete a file from the  repo but not from the system)
* `git reset --hard <commit>` (revert last changes to the commit, for the last changes we can use HEAD as commit)

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
