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

Fetch and push are the mechanism by which means remote git repositories synchronize. That is, when you execute *git fetch (...)* the 


### Shelve