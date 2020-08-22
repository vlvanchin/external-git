# Delete branch locally and remotely:

```
// to delete a local branch
$ git branch --delete <<local_branch>>
or
$ git branch -d <<local_branch>>

// To delete a local un-merged branch
$ git branch -D <<local_branch>>

// to delete a local remote - tracking branch
$ git branch --dr <<remote>>/<<branch-name>>

// to delete a remote branch
$ git push --delete <<remote>> <<branch-name>>
```

# Cherry-pick commits:

```
* find the common parent as the inital state
* $ git checkout -b <<cherry-pick-branch-name>> <<initial-commit-id>> // create a new branch for cherry-pick
* $ git cherry-pick <<commit-id-wanted>> // select the commit that you want
* Fix any conflicts that arrise
** $ git cherry-pick --continue // to proceed on cherry-pick
* git push <<remote>> <<cherry-pick-branch-name>>
```

# Other useful commands:

### how to view logs for a specific branch
```
$ git log --oneline --decorate <branch>
```

### to show all the names of the files committed in this commit
```
$ git show  --name-only <commit-id>
```

### to list the last 5 logs of a specific file
```
$ git log -5 --follow <file-path>
```

### to checkout a specific commit of a specific file
```
$ git checkout <commit-id> -- <file-path>
```

### reset a file from staged to work area
```
$ git reset HEAD <file-path>
```

### to show differences of a staged file
```
$ git diff --cached <file-path>
```

### to show differences of a file within an old and new commits
```
$ git diff <old-commit-id> <new-commit-id> <file-path>
```

### to stash modified files except the staged
```
$ git stash save --keep-index
```

### to add a file based on individual changes in that file, interactive mode
```
$ git add --patch <file-path>
```

## How to reset last commit in local and remote:

```
* reset head softly locally first
$ git reset HEAD~1

* push forcefully to remote repo
$ git push <<remote>> <<branch>> -f
```

## How to list all different commits between two Branches in a Repo

```
# To list right-only branch commits that are not in the develop (left branch)
$ git log --cherry-pick --right-only --no-merges develop...master 

# To list left-only branch commits that are not in the master (right branch)
$ git log --cherry-pick --left-only --no-merges develop...master
```

## How to merge a Tag in a branch to another branch

```
# change dir to the destination branch
$ git checkout <<destination_branch>>

# fetch the tags from the remote
$ git fetch --tags origin

# do merge tag
$ git merge <<tag_name>>
```

## How to get log based on filters

```
// fetch commits based on commit messages
git log --all --oneline --decorate --grep "message"

// fetch commits based on author and commit message
git log --oneline --author="authorName" --grep "messageStr"

// to display all the files for a specific commit id
git show --name-only f2c06ff6

// to display the commit contents of a file on a specific commit
git show -p <commit-id> -- <filename>

// to display all commit ids along with author name
git log --format='%H %an'
```

[Back to Homepage](../tips-repo)

