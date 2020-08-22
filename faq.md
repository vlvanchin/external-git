# How to fix the miss commits between the two branches in two separate repositories?

Steps to be done to fix the miss commits between the two branches say the development branch in origin and upstream remotes.

> Find out the common commit for the two branches in the past and checkout a new branch within the origin remote eg: commonCommitBranch
 ```
$ git checkout -b commonCommitBranch 2449134b726f723fa
```

> update both the remotes
```
$ git fetch upstream
$ git fetch origin
```

> now rebase from the upstream branch to the working branch
```
$ git rebase upstream/development
```

Now the upstream/development branch is merged with origin/commonCommitBranch but the origin/development contains many commits that are not in the remote/development and origin/commonCommitBranch. 

In order to find all the non-synced commits we do the following step

> list all different commits between two Branches (origin/commonCommitBranch and origin/development)
```
$ git log --cherry-pick --left-only --no-merges development...commonCommitBranch
```
This will give all the left over commits that are not present in the origin/commonCommitBranch branch

We do the following for every single commit from bottom-up till the latest commit.
```
$ git cherry-pick <<commit-id>>
```
If there are any conflicts, need to be fixed manually and follow the hints given by Git.

Once all cherry-picks are done, then push the origin/commonCommitBranch and then create a pull request to merge to remote/development branch from Github dashboard.

```
$ git push origin commonCommitBranch
```

[Back to Homepage](../tips-repo)
