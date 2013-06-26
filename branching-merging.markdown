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

To publish a branch, you need to push it to a remote:
```bash
$ git push origin lolz
$ git push origin lolz:lolz # Lolcal_Branch:Remote_Branch
```

You can remove a branch:

```bash
$ git branch -d lolz # Locally
$ git push origin :lolz # Remote
```

Without a branch referencing to thhem, commits (and corresponding objects) are garbage collected by local git repos over time.

# Branching Strategy

### Merge

### Rebase