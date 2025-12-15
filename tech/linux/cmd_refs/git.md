# Git

## See also
- [git-bash](./git-bash.md)

###### Test git connection
```bash
ssh -T git@github.com
```

###### Delete commit history
```bash
git checkout --orphan latest_branch
git add -A
git commit -am "initial commit"
git branch -D main
git branch -m main
git push -f origin main
```

###### Diff a file with the previous version
```bash
git diff HEAD^ HEAD -- path/to/file
```

###### Diff a file with the previous version using graphical diff tool
```bash
git difftool HEAD^ HEAD -- path/to/file
```

###### Diff a file two commits back
```
git diff HEAD~2 HEAD -- path/to/file
```

###### Diff a file between two branches 
```bash
git diff main dev -- path/to/file
```

###### Test git connection
```bash
ssh -T git@github.com
```

###### Commit all modified files with a message
```bash
git commit -a -m "changed some files"
```

###### Push to remote repository
```bash
git push origin master
```

###### Set current local branch to track remote branch
```bash
git push -u {remote}
```

###### Set upstream branch tracking
```bash
git branch --set-upstream-to=origin/branch-name branch-name
```

###### Unstage files (undo `git add -A`) without losing changes
```bash
git reset --soft HEAD
```

###### Revert changes to all modified files
```bash
git reset --hard HEAD
```

###### Hard reset to remote
```bash
git fetch origin
git reset --hard origin/main
```

###### Reset to a specific commit
```bash
git reset --hard f2c02a0
```

###### Revert changes to a single modified file
```bash
git checkout HEAD /path/to/file
```

###### List branches
```bash
git branch -va
```

###### List branches (very verbosely?)
```bash
git branch -vv
```

###### Stash (shelve) changes
```bash
git stash
```

###### Unstash (unshelve) changes method 1: `git stash pop`
```bash
git stash pop
```

###### Unstash (unshelve) changes method 2: `git stash apply`
```bash
git stash apply
```

###### How git stash pop and apply differ

The key difference between git stash pop and apply involves the stash history. When a developer uses the `git stash apply` command, the most recently saved stash overwrites files in the current working tree but leaves the stash history alone. In contrast, the `git stash pop` command restores files but then deletes the applied stash. If a developer ever feels the need to use that restored stash again, it will be saved in the local file system.

###### Typical git stash workflow
```bash
git stash
git pull origin
git stash pop
```

###### Oops, I forgot to make a branch

If you have a low # of commits and you don't care if these are combined into one mega-commit, this works well and isn't as scary as doing git rebase:
unstage the files (replace 1 with # of commits)
```bash
git reset --soft HEAD~1
```
Create a new branch
```bash
git checkout -b NewBranchName
```
Add the changes
```bash
git add -A
```
Make a commit
```bash
git commit -m "Whatever"
```

###### Disable SSL validation globally
```bash
git config --global http.sslVerify "false"
```

###### Disable SSL validation for a single command (in this example `git pull`)
```bash
git -c http.sslVerify=false pull
```

###### List modified files
```bash
git status
```

###### Show differences in modified files
```bash
git diff
```

```bash
git diff --staged
```

```bash
git diff --cached
```

###### List untracked files
```bash
git status -u
```

###### List ignored files
```bash
git status --ignored
```

###### `git pull {remote}` is equivalent to _____
```bash
git fetch {remote}
git merge {remote}/{branch}
```

###### Remove all untracked files and directories
```bash
git clean -f
```

###### Remove all untracked files and directories
```bash
git clean -fd
```

###### Remove all untracked files and directories, including ignored
```bash
git clean -fdx
```

###### Remove only ignored files
```bash
git clean -fX
```

###### How to abort a git merge?
```bash
git merge --abort
```

###### Delete a branch both locally and remotely
```bash
git branch -d {branch}
git push origin --delete {branch}
```

###### Create a new local branch and push it to a remote
```bash
git checkout -b {branch}
git push origin {branch}
```

###### Remove local branches that no longer exist on the server
```bash
git fetch --all --prune
```

###### List remote branches (3 ways)
```bash
git branch -a
git branch -r
git remote show {remote}
```

###### List tags with 1 line tag message
```bash
git tag -l -n1
```
`-l` list

###### Push tags to remote
```bash
git push origin --tags
```

###### Pull using rebase instead of merge
```bash
git pull -r
```

###### Show git config
```bash
git config --list --global
```

###### Show git log
```bash
git log
```

###### Configure git user.name and user.email
```bash
git config --global user.name "Firstname Lastname"
git config --global user.email "firstname.lastname@host.com"
```

###### Remove remote repo history:

Step 1 - Remove all history
```
$ cd myrepo
$ rm -rf .git
```

Step 2 - Init a new repo
```
$ git init
$ git add .
$ git commit -m "Removed history, due to sensitive data"
```

Step 3 - Push to remote
```
$ git remote add origin github.com:yourhandle/yourrepo.git
$ git push -u --force origin master
```

###### Git difftool
```bash
git difftool
```

###### Git difftool configuration
```bash
git config --global difftool.prompt false
git config --global diff.tool bc3
git config --global difftool.bc3.trustExitCode true
```

###### Using meld with git diff

Create a bash script somewhere under your path called `git-meld` with this in it:
```
#!/bin/bash
meld $2 $5
```
Don't forget to make it executable.
Add the following to your `~/.gitconfig` file
```
[diff]
external = git-meld
```
Source: http://blog.deadlypenguin.com/blog/2011/05/03/using-meld-with-git-diff/

###### Get help
```bash
git help {verb}
git {verb} --help
```

###### Create a Git bundle
```bash
cd reponame
git bundle create file.bundle main
git tag -f latestBundle main
```

###### Load (clone) a repo from Git bundle
```
git clone -b main file.bundle reponame
```
