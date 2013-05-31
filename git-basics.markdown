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

``` bash
$ cd /d
$ mkdir git
$ git init epam1
$ git init --bare epam2
```

##### Clone Repository #####

``` bash
$ git clone file:///d/git/epam2 epam3
Cloning into 'epam3'...
warning: You appear to have cloned an empty repository.
```
``` bash 
$ git clone https://git.epam.com/gabor_czigola/git_example.git gitex1
Cloning into 'gitex1'...
Username for 'https://git.epam.com': gabor_czigola
Password for 'https://gabor_czigola@git.epam.com'
```
``` bash 
$ git clone git@git.epam.com:gabor_czigola/git_example.git gitex2
Cloning into 'gitex2'...
```

Public key based authentication is the most convenient. You should generate yourself a private-public key pair (or reuse an existing one.) Use *ssh-keygen* on [Windows](https://help.github.com/articles/generating-ssh-keys#platform-windows) or [Linux](https://help.github.com/articles/generating-ssh-keys#platform-linux), or [PuTTY](http://katsande.com/using-puttygen-to-generate-ssh-private-public-keys) to create a new key pair.
Copy-paste the public key to https://git.epam.com/keys and append your private key to *~/.ssh/id_rsa* .

### Comparison ###

* Stores snapshots, past is always accessible.
* Three way merge, resolves tree conflicts with an ease.
* Cheap branching and merging.
* Free as in free beer.
* Vivid ecosystem, Git is a [platform](http://git.epam.com) and a [network](http://github.com)!
* Became the standard in many environments.