# Branch Structure

Git has a lightweight and useful branching concept. Git has internally (.git/refs/heads) a table of branch names with the corresponding HEAD pointing to the latest commit of the branch. (A branch also consist of each preceding commit object of its HEAD and each and every corresponding tree and blob object.)

# Creating Branches

You can create a new branch any time:

```bash
$ git branch lolz
```

This will copy the current HEAD with a new name, but not switch to the newly created branch.

# Switching Branches

You can switch to any of the local branches at any time:

```bash
$ git checkout lolz
```

You can create and switch the a new branch in one command:

```bash
$ git checkout -b lolz
```

You can list current branches:

```git bash
$ git branch -va
* master                edcf391 Resolved.
```

## Remote branches

You can add arbitrary remote repos to connect to. Use *git clone* to not to have to worry about remotes and have the original repository properly set up as the tracked remote.

```git bash
$ git remote -v
origin  p:/git/1 (fetch)
origin  p:/git/1 (push)
```

*git fetch* will copy all HEAD references, all corresponding commit, tree and blob objects (and their parents):

```bash
$ git fetch origin
remote: Counting objects: 20, done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 15 (delta 5), reused 0 (delta 0)
Unpacking objects: 100% (15/15), done.
From git@github.com:schacon/simplegit
 * [new branch]      lolz -> origin/lolz

$ git branch -va
* master                edcf391 Resolved.
  remotes/origin/lolz   edcf391 Resolved.
  remotes/origin/master edcf391 Resolved.
```


HEAD references are put into .git/remotes/[REMOTE]/[BRANCH_NAME]. If you like to switch to such a (remote) branch, you need a branch first in your local repo:

```bash
$ git checkout -b lolz origin/lolz
Branch lolz set up to track remote branch refs/remotes/origin/lolz .
Switched to a new branch "lolz "

$ git branch -va
* lolz                  edcf391 Resolved.
  master                edcf391 Resolved.
  remotes/origin/lolz   edcf391 Resolved.
  remotes/origin/master edcf391 Resolved.
```

To publish a branch, you need to push it to a remote:

```bash
$ git push origin lolz
$ git push origin lolz:lolz # Local_Branch:Remote_Branch
```

You can remove a branch:

```bash
$ git branch -d lolz # Locally
$ git push origin :lolz # Remote
```

Without a branch referencing to them, commits (and corresponding commit, tree, blob objects) are garbage collected by local git repos over time.

# Branching Strategy

### Merge

### Rebase