# Versioning

In this chapter we examine operations to add and remove to and from the repository and how to stage, commit these changes.

### Staging Area

Git tracks each file in the working tree for changes. Before you commit, you must stage a set of changes to the staging area. Only changes in the staging area can be committed.

![Staging area](http://git-scm.com/figures/18333fig0201-tn.png)

Once an already staged file change, you need to re-stage it.

``` bash
# git init .
Initialized empty Git repository in /home/czigolag/git/.git/

czigolag@yldnw0400173clu ~/git
# touch .gitignore

czigolag@yldnw0400173clu ~/git
# git status
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
# rm .gitignore

czigolag@yldnw0400173clu ~/git
# git status
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)

czigolag@yldnw0400173clu ~/git
# touch .gitignore

czigolag@yldnw0400173clu ~/git
# git status
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
# git add --all

czigolag@yldnw0400173clu ~/git
# echo "*~" >> .gitignore

czigolag@yldnw0400173clu ~/git
# git status
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

If git encounters a ''.gitignore'', it will apply its contents to ignore specific files/directories completely. The rules apply from the directory they are defined in. Example:

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

Git limitation: git can't track empty directories. Convention is to add an empty file named ''empty'' or ''.gitignore''.

### Commit

### Push and Pull

### Shelve