# Individual files

Files that are not yet indexed you can remoge with *git clean*:

```bash
$ touch oops

$ git status
# On branch lolz
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   z
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       oops

$ git clean
fatal: clean.requireForce defaults to true and neither -n nor -f given; refusing
 to clean

$ git clean -n
Would remove oops

$ git clean -f
Removing oops

$ git status
# On branch lolz
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   z
#
```

Files that are indexed, you can revert your changes in the working tree with *git checkout*:

```bash
czigolag@YLDNW0400173CLU ~/git/2 (master)
$ cat x
4

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ echo "dsalkfnlkn" > x

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   x
#
no changes added to commit (use "git add" and/or "git commit -a")

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ cat x
dsalkfnlkn

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ git checkout x

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ git status
# On branch master
nothing to commit, working directory clean

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ cat x
4

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ echo "asajlkfbjkl" > x

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   x
#
no changes added to commit (use "git add" and/or "git commit -a")

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ git checkout x

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ git status
# On branch master
nothing to commit, working directory clean

czigolag@YLDNW0400173CLU ~/git/2 (master)
$ echo x
x
```

We have seen before *checkout* is used to switch branches. Switching branches will not alter any of your local changes in the working copy. If git would have to do so, it will fail to switch to that branch. You can stage/stash/commit your changes, then use clean and reset to make the checkout possible.

```bash
$ git checkout origin/lolz
error: Your local changes to the following files would be overwritten by checkou
t:
        z
Please, commit your changes or stash them before you can switch branches.
Aborting
```

# Staging area (cache)

reset mixed, hard

# Commit

amend

reset soft, hard, keep

# Merge / Pull

reset merge

merge abort

rebase abort
