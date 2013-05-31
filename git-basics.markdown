# Git Basics #

[Git](http://en.wikipedia.org/wiki/Git_(software%29) is a distributed revision control and source code management systems.

### Introduction ###

##### Local Version Control Systems #####
![Local Version Control Systems](http://git-scm.com/figures/18333fig0101-tn.png "Local Version Control Systems")

##### Centralized Version Control Systems #####
![Centralized Version Control Systems](http://git-scm.com/figures/18333fig0102-tn.png "Centralized Version Control Systems")

##### Distributed Version Control Systems #####
![Distributed Version Control Systems](http://git-scm.com/figures/18333fig0103-tn.png "Distributed Version Control Systems")

### Getting Started ###

##### Install Git Command Line #####

Install [package git on your Linux](http://git-scm.com/download/linux) or [mysysgit on Windows](https://code.google.com/p/msysgit/downloads/list).

![Git Bash](http://johnnycode.com/assets/images/2010-07-09-my-first-day-using-git-on-windows-7/Git-Bash-Committing-Changes.png "Git Bash")

##### Create Repository #####

> $ cd /d
  
> $ mkdir git
  
> $ git init epam1
  
> $ git init --bare epam2

##### Clone Repository #####

``` bash
git clone file:///d/git/epam2 epam3
Cloning into 'epam3'...
warning: You appear to have cloned an empty repository.
```

``` bash 
> $ git clone https://git.epam.com/gabor_czigola/git_example.git gitex1
> Cloning into 'gitex1'...
> Username for 'https://git.epam.com': gabor_czigola
> Password for 'https://gabor_czigola@git.epam.com'
```
  
  
> $ git clone git@git.epam.com:gabor_czigola/git_example.git gitex2
> Cloning into 'gitex2'...

### Comparison ###

* Stores snapshots, past is always accessible.
* Three way merge, resolves tree conflicts with an ease.
* Cheap branching and merging.
* Free as in free beer.
* Vivid ecosystem, Git is a [platform](http://git.epam.com) and a [network](http://github.com)!
* Became the standard in many environments.