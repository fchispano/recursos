# GIT CheatSheet

- [Configuration](#configuration-)
- [Working with the local repo](#working-with-the-local-repo-)
  - [Tracking and staging changes](#tracking-and-staging-changes-)
  - [Commiting changes](#commiting-changes-)
  - [Branching](#branching-)
  - [Merging](#merging-)
  - [Handling tags](#handling-tags-)
- [Working with the remote repo](#working-with-the-remote-repo-)
  - [Bringing changes](#bringing-changes-)
  - [Remote branching](#remote-branching-)
  - [Sending changes](#sending-changes-)
- [Retrieving information](#retrieving-information-)
  - [Differences](#differences-)
  - [Logs](#logs-)
  - [Remotes](#remotes-)
  - [Responsibility](#responsibility-)
  - [Other info](#other-info-)
- [Undo and modify commits](#undo-and-modify-commits-)
  - [Undo a commit and redo](#undo-a-commit-and-redo-)
- [Searching for a bug](#searching-for-a-bug-)
- [Contributing](#contributing-)
  - [Process to contribute and solve merge conflicts](#process-to-contribute-and-solve-merge-conflicts-)
  - [Keep your forked repository up-to-date with the original](#keep-your-forked-repository-up-to-date-with-the-original-)
- [Other tips](#other-tips-)
  - [A nice formated git log --graph](#a-nice-formated-git-log--graph-)

## Configuration [↑](#git-cheatsheet)

* `git config --global user.name "John Doe"`  →  config the user name for local repositories
* `git config --global user.email johndoe@example.com`  →  config the user email for local repositories
* `git config --global core.editor <editor path>`  →  config main text editor for edit git related stuff
* `git config --global core.editor “’editor_path’ -n -w"`
* `git remote add <remote name> <url>`  →  create the remote repository

## Working with the local repo [↑](#git-cheatsheet)

* `git init`  →  start a git repo in the working folder

### Tracking and staging changes [↑](#git-cheatsheet)

* `git add (file)`  →  begin tracking changes in `file` and prepare it to be committed, that's known as "stage" a file, because we add it to the staging area
* `git add .`  →  stage all files: new, modified or deleted
* `git add -A` or `git add --all`  →  does the same that the previous command, but looks more straightforward

### Commiting changes [↑](#git-cheatsheet)

* `git commit -m “message"`  →  commit all staged files and add a short message explaining the changes
* `git commit -am “message"`  →  stages all tracked files and does a commit with the specified message

### Branching [↑](#git-cheatsheet)

* `git branch`  →  list all the branches in the repository
* `git branch <new-branch-name>`  →  create a new branch `<new-branch-name>
* `git checkout -b <new-branch-name>`  →  create and move the a new branch `<new-branch-name>`
* `git branch -d <branch-name-to-delete>`  →  delete the branch `<branch-name-to-delete>` (the branch changes must be fully merged in upsteam, usually master, or the deletion will fail)
* `git branch -m <old-branch-name> <new-branch-name>`  →  rename a local branch

### Merging [↑](#git-cheatsheet)

* `git merge <branch-name>`  →  merge `<branch-name>` with the actual branch
* `git merge --no-ff <branch-name>`  →  avoid fast-forward merge, creating a commit for the merge

### Handling tags [↑](#git-cheatsheet)

* `git tag`  → view branch tags
* `git tag -a v1.4 -m "my version 1.4"`  →  add an annotated tag
* `git tag -d <tag>` → deletes <tag>


## Working with the remote repo [↑](#git-cheatsheet)

### Bringing changes [↑](#git-cheatsheet)

* `git pull <remote-repo> <local-branch>`  →  pull the changes in `<remote-repo>` not in `<local-branch>`
* `git fetch`  →  new label on the local repository with the commits up-to-date of remote

### Remote branching [↑](#git-cheatsheet)

* `git push <remote-repo> :<remote-branch>`  →  delete a remote branch, be careful!
* `git push <remote-repo> :<remote-old-branch-name> <remote-new-branch-name>`  →  delete the remote old branch name and push the just renamed branch

### Sending changes [↑](#git-cheatsheet)

* `git push <remote-repo> <local-branch>`  →  push the changes in `<local-branch>` to `<remote-repo>`

* `git push --all <remote-repo>`  →  push all branches to `<remote-repo>`, useful when you want to push changes in several branches (caveat: keep your local branches tidy and clean)


## Retrieving information [↑](#git-cheatsheet)

### Differences [↑](#git-cheatsheet)

* `git diff`  →  show differences between what is already in the index and files that have changed and could be added
* `git diff <hash1> <hash2>`  →  show differences between commit with `<hash1>` and commit with `<hash2>`
* `git diff <branch1>..<branch2>`  →  show what is in `<branch2>` that isn't in `<branch1>`
* `git diff <branch1>...<branch2>`  →  show what is in `<branch1>` or in `<branch2>`, but not in both (XOR operation)

### Logs [↑](#git-cheatsheet)

* `git log`  →  shows the commit log
* `git log -1` → shows the last commit. Change the number to see more commits
* `git log --graph --oneline`  →  shows a resumed version of `git log`, and draws with ASCII a commit history graph

### Remotes [↑](#git-cheatsheet)

* `git remote`  →  list remote repositories
* `git remote -v`  →  as `git remote` but with extra info

### Responsibility [↑](#git-cheatsheet)

* `git blame -L <startingLine>,<endingLine> <file> → Shows the author of every line in the given range for the specified line. [more info](https://git-scm.com/docs/git-blame#_specifying_ranges)

### Other info [↑](#git-cheatsheet)

* `git ls-files`  →  See files being tracked
* `git show --stat --oneline <commit>` -> Show the commit message and the files modified in that commit [source](http://stackoverflow.com/a/11442967)

## Undo and modify commits [↑](#git-cheatsheet)

* `git reset`  →  remove all from staging area
* `git commit --amend -m <“message”>`  [Edit an incorrect commit message in Git](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git)
* `git rm --cached file.txt`  →  delete a file from the repo but not from the filesystem
* `git reset --hard <commit>`  →  revert last changes to the commit, for the last changes we can use HEAD as commit

### Undo a commit and redo [↑](#git-cheatsheet)

```
$ git commit -m "Something terribly misguided"              (1)
$ git reset --soft HEAD~                                    (2)
$< edit files as necessary >>                               (3)
$ git add .                                                 (4)
$ git commit -c ORIG_HEAD                                   (5)
```
[Source](http://stackoverflow.com/questions/927358/how-do-you-undo-the-last-commit)


## Searching for a bug [↑](#git-cheatsheet)

1. `git bisect start`
2. `git bisect bad`
3. `git bisect good <commit>` → A commit you know for sure doesn't have the bug

After this, the process of searching will begin. In each step git selects a new
commit, you test it and decide what to do until you narrow down the issue to
a single commit.

* If the commit has the bug: `git bisect bad`
* If the commit doesn't have the bug: `git bisect good`

When you have the commit with the issue, type `git bisect restart` to go back
to the HEAD of your current branch.

For more info read the git documentation about [git bisect](https://git-scm.com/book/es/v2/Git-Tools-Debugging-with-Git#Binary-Search).

## Contributing [↑](#git-cheatsheet)

### Process to contribute and solve merge conflicts: [↑](#git-cheatsheet)

1. Fork the repository
2. Make changes on a local branch
3. pull Master to be up-to-date
4. merge master into you branch
5. push your branch
6. pull request to merge.

### Keep your forked repository up-to-date with the original [↑](#git-cheatsheet)

Configure the remote upstream. **You have to do this just once**

1. `git remote add upstream https://github.com/fchispano/recursos.git`

Get the latest changes in the repo:

2. `git fetch upstream`
3. `git checkout master`
4. `git merge upstream/master`

## Other tips [↑](#git-cheatsheet)

### A nice formated git log --graph [↑](#git-cheatsheet)

Give the following command an alias (e.g: gitl) and enjoy ;)

`git log --graph --abbrev-commit --decorate --format=format:"%C(bold yellow)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n""   %C(white)%s%C(reset) %C(dim white)- %an%C(reset)" --all`

Sources:

* [Configuring a remote for a fork](https://help.github.com/articles/configuring-a-remote-for-a-fork/)
* [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)
* [A successful git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
