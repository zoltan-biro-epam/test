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

```bash
$ git branch -va
* lolz                edcf391 Resolved.
 master                edcf391 Resolved.
```

To publish a branch, you need to push it to a remote:

```bash
$ git push origin lolz
$ git push origin lolz:lolz # Local_Branch:Remote_Branch
```

You can public

## Remote branches

You can add arbitrary remote repos to connect to. Use *git clone* to not to have to worry about remotes and have the original repository properly set up as the tracked remote.

```bash
$ git remote -v
origin  p:/git/1 (fetch)
origin  p:/git/1 (push)
```

*git fetch* will copy all HEAD references, and all corresponding commit, tree and blob objects (and their parents):

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
```

Please note that remote and local branch names are not required to match and you should not expect it either. (Although it is a good default practice.

```
$ git branch -va
* lolz                  edcf391 Resolved.
  master                edcf391 Resolved.
  remotes/origin/lolz   edcf391 Resolved.
  remotes/origin/master edcf391 Resolved.
```

You can remove a branch:

```bash
$ git branch -d lolz # Locally
$ git push origin :lolz # Remote
```

Without a branch referencing to them, commits (and corresponding commit, tree, blob objects) are garbage collected by local git repos over time.

## Tags

You can create tags just like branches to point to a particular commit. In contrast to branches you can't change the HEAD of a tag, ever. So created tags are permanent references to a particular state. You can delete tags (and re-use the name), but this is not advised! You can protect yourself against such a change in tags by not pulling them.

```bash
$ git v1.1 # Leightweight tag, no message
$ git -a v2.0 -m "July major release."
```

You push, fetch and checkout tags just like branches.

# Branching Strategy

The branching strategy is the quintessence of the workflow using a CVS/SCM. Many teams fail here and use the tool at hand incorrectly. It is essential to have an understanding of the underlying mechanisms, and [to have a plan for each flow: from daily dev work through hotfixes til release](http://nvie.com/posts/a-successful-git-branching-model/).

##### What branch should developers commit to?

Development happens on private feature branches. That is, for each story/task development happens on a dedicated branch, so starting a new dev task/story as the first thing would be to create a new branch. This means you can commit your daily work without affecting the dev build, without the need to have to resolve any conflicts. You can push this branch to share your current work, other can use it in part or in full to in their work.

##### How are completed features 

Depending on the nature of your work, you can ask testers to try out your branch. If the feature branch meets the done criteria, it is ready to go back to the shared dev branch. You can either merge your work into that branch yourself, or ask the owners of that branch to do so. The latter is called a *pull request*

##### Who resolves conflicts?

Conflicts need to be resolved when merging in changes. So if you are merging you have to resolve the conflicts. If you create a pull request, the one pulling must resolve. In the latter case it might be policy that before creating the pull request, in order to minimize potential conflicts, you have to rebase your feature branch on top of the latest dev branch, encountering some conflicts too.

##### How are releases selected?

You can branch and merge dev to release (candidate) branch(es). Likewise you can branch these to follow up on requested hotfixes.

### Merge

Tips:

* Set up a proper three-way merge tool (e.g. KDiff3, GVim, Perforce Mergetool). Do not even attempt to use a two-way one (like the default with TortoiseGit.)
* Always check what branch you are one. You will merge into that branch!
* Use *git fetch* to update you index instead of *git pull*. The latter would also merge whatever changes into the branch you are on right now.
* Understand fast forward.
* Understand --no-commit and --squash.
* Know alternate merge strategies.

### Rebase

Use rebase with caution and only when really needed. Understand what it does and do not mix merge and rebase. Reabse should be used rarely. Don't worry about the looks of your history. When you rebase, "yours" and "theirs" is the other way around, e.g. "theirs" strategy would accepts all of your changes and "yours" strategy would accept all remote changes!

http://stackoverflow.com/questions/804115/git-rebase-vs-git-merge
http://kentnguyen.com/development/visualized-git-practices-for-team/