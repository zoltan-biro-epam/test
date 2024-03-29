# Versioning

In this chapter we examine operations to add and remove to and from the repository and how to stage, commit these changes.

### Staging Area

Git tracks each file in the working tree for changes. Before you commit, you must stage a set of changes to the staging area. Only changes in the staging area can be committed.
(This staging area is sometimes called the index or the cache.)

![Staging area](http://git-scm.com/figures/18333fig0201-tn.png)

Once an already staged file changes, you need to re-stage it.

``` bash
$ git init .
Initialized empty Git repository in /home/czigolag/git/.git/

czigolag@yldnw0400173clu ~/git
$ touch .gitignore

czigolag@yldnw0400173clu ~/git
$ git status
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       .gitignore
nothing added to commit but untracked files present (use "git add" to track)

czigolag@yldnw0400173clu ~/git
$ git add --all

czigolag@yldnw0400173clu ~/git
$ echo "*~" >> .gitignore

czigolag@yldnw0400173clu ~/git
$ git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#       new file:   .gitignore
#
# Changed but not updated:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   .gitignore
#
```

You can (re-)add and remove files from the staging area at any time. The staging area captures each file in the state it was staged.

If git encounters a *.gitignore*, it will apply its contents to ignore files/directories matching the provided patterns. These rules apply from the directory they are defined in. Example:

```
# a comment - this is ignored
# no .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the root TODO file, not subdir/TODO
/TODO
# ignore all files in the build/ directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .txt files in the doc/ directory
doc/**/*.txt
```

Git limitation: git can't track empty directories. Convention is to add an empty file named *empty* or *.gitignore*. In fact, Git does not track directories at all, it only tracks files, creating the directory structures based on their paths.

You can use *gir rm* and *git mv* to remove and move files. Git tracks moves implicitely.

### Commit

You can commit what you have staged. To see what you’ve changed but not yet staged, type *git diff*. To compare the staging area the last commit, you can use *git diff --staged*.

You can commit staged files any time. **Check to be on the correct branch before committing.**

```bash
$ git commit -m "Initialize repository."
[master 536f407] Initialize repository.
 1 files changed, 0 insertions(+), 1 deletions(-)
 delete mode 100644 .gitignore
```

If not yet pushed, you can amend (modify) previous commits with --amend.

If you wish to commit all your changes as-is, you can use the -a flag with commit to stage all current changes beforehand.

As a result of a commit the object database (.git/objects) may contains four types of objects:

* A blob object is the content of a file. Blob objects have no file name, time stamps, or other metadata.
* A tree object is the equivalent of a directory (structure). It contains a list of file names, each with some type bits and the name of a blob or tree object that is that file, symbolic link, or directory's contents. This object describes a snapshot of the source tree.
* A commit object links tree objects together into a history. It contains the name of a tree object (of the top-level source directory), a time stamp, a log message, and the names of zero or more parent commit objects.
* Branch and tag objects are a references to a particular commit and some additional meta-data. Once created, tags do not change.
* HEAD-s are symbolic references to the latest state of branches, or in special cases a specific commit without a branch ("detached head.")

### Fetch and Push.

Fetch and push are the mechanism by which means remote git repositories synchronize. That is, when you execute *git fetch (...)* you receive all the objects from the remote. Your working directory does not change however! In contrast push will publish you objects (blobs, trees, commits and branches) to a remote repository.

Clone fetches all objects:
![Git clone](http://git-scm.com/figures/18333fig0322-tn.png "clone")

Someone pushes to the remote:
![Git push](http://git-scm.com/figures/18333fig0323-tn.png "push")

You fetch the changes:
![Git fetch](http://git-scm.com/figures/18333fig0324-tn.png "fetch")

*git pull* is *git fetch; git merge;* It is advised to always provide remote and branch name as parameter to avoid unexpected results.

If a push fails (complaining it is unable to *fastforward*), this is a signal that your index is out of date. You should first fetch, then merge/rebase changes, then you can push. You can use *git push --force* to ignore this situation and just push you object and forcefully override the branch object('s HEAD) you are pushing. Use this with caution, other won't be able pull this branch, they will need *git fetch;git reset --hard HEAD*

### Shelve

Sometimes you need to capture and discard your current state of work, or even share or pass it to someone else.

##### Feature Branches

If you like to share what you are currently working on, you need to create a new branch, commit you changes there. Then you can push you branch to publish it or someone may pull from you. This sounds advanced, albeit **branching and merging is a lightweight and common operation** in git. E.g.:

```bash
$ git checkout -b ideaBranch
$ touch foo
$ git add --all
$ git commit -m "This might be a good idea."
$ git push origin ideaBranch
$ git checkout master
```

After you pushed you changes by switching back to the original branch (master) you see the precise state of before. Everyone is able now to fetch ideaBranch. We will examine branching and merging in the next chapter.

##### Stash and Pop

If you do not want or need to publish the changeset at hand, *git stash* is your friend. It can capture and restore what is in your staging area (cache). You do not need to commit or branch your changes.

```bash
$ touch z
$ git add z
$ git stash
Saved working directory and index state WIP on master: edcf391 Resolved.
HEAD is now at edcf391 Resolved.

$ git stash list
stash@{0}: WIP on master: edcf391 Resolved.

$ git stash show
 z | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

$ git stash pop
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   z
#
Dropped refs/stash@{0} (1a35ec1d8dbd6c95b87c0a17ae7106dff15aa206)
```

You can have multiple stashed changesets at once. The drawback of stash is that it is exclusive to your local repository You can't share your stashed changes.