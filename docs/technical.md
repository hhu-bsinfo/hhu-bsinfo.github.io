# Technical Guidance

## Introduction

### Scope

### Purpose

The main purpose of this document is to guide the development team in setting up a development environment for the DXRAM project. 
It also defines standards and best practices for the developers to follow using certain tools, third party libraries and policies.

## Development Environment

### Setup

#### Oracle JDK / Open JDK
Download the latest Java 8 Oracle JDK [jdk-8u202-linux-x64.tar.gz](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) and follow the instructions [here](https://wiki.ubuntuusers.de/Java/Installation/Oracle_Java/Java_8/) for installation. To put it in a nutshell, extract the *tar* (do it all as root via `sudo su`)

``` bash
sudo su
tar xzf jdk-8u202-linux-x64.tar.gz
```
move it into `/opt`

``` bash
mkdir /opt/Oracle_Java
mv jdk1.8.0_202 /opt/Oracle_Java
```
and update the system accordingly (replace *VERSION* with the one you downloaded, currently 202)

``` bash
update-alternatives --install "/usr/bin/java" "java" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/java" 1
update-alternatives --install "/usr/bin/javac" "javac" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/javac" 1
update-alternatives --install "/usr/bin/javaws" "javaws" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/javaws" 1
update-alternatives --install "/usr/bin/jar" "jar" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/jar" 1 

update-alternatives --set "java" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/java"
update-alternatives --set "javac" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/javac"
update-alternatives --set "javaws" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/javaws"
update-alternatives --set "jar" "/opt/Oracle_Java/jdk1.8.0_VERSION/bin/jar" 
```
Finally test the installation via

``` bash
$ java -version
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)
```

#### IDE

#### Other tools

### Build Automation with Gradle

### Distribution

### Debugging

## Git Workflow

To prepare the environment make sure **git** is installed and configured properly.

``` bash
sudo apt install git
```

It is highly recommended to work with SSH keys. This aproach will save your time alot.
An article about generating a new SSH key and adding it to the ssh-agent can be found [here](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
Afterwards [add](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account) your SSH key to your GitHub account and [test](https://help.github.com/en/articles/testing-your-ssh-connection) the connection.

To finish the configuration add your email and name in the global scope.
This information will appear in the commit history.

``` bash
git config --global user.email "your@email.com"
git config --global user.name "Your Name"
```

### Forks and Remote Repositories

First create a workspace directory in your home:

``` bash
cd && mkdir workspace && cd workspace
```

Now fork your own copy of [hhu-bsinfo/dxram](https://github.com/hhu-bsinfo/dxram) to your account.
Additionally it could be helpful to fork all other DXRAM repositories you are going to work with as well.

!!! tip
    If you are going to develop something within DXRAM (changing DXRAM code), there is no way to circumvent the **development** branch.
    However, in case you are developing an independent piece of software with DXRAM as dependency, working with the **master** branch might be an option.

Time to clone all forked copies:

``` bash
git clone --branch=development git@github.com:<you>/dxram.git
```

Adding the original repository [https://github.com/hhu-bsinfo/dxram.git](https://github.com/hhu-bsinfo/dxram.git) to *git*

``` bash
$ git remote add shared https://github.com/hhu-bsinfo/dxram.git
$ git fetch --all
Fetching origin
Fetching shared
From https://github.com/hhu-bsinfo/dxram
 * [new branch]        development -> shared/development
 * [new branch]        master      -> shared/master
 * [new tag]           0.3.1       -> 0.3.1
 * [new tag]           0.5.0       -> 0.5.0
 * [new tag]           0.6.0       -> 0.6.0
 * [new tag]           0.7.0       -> 0.7.0
 * [new tag]           v0.4.0      -> v0.4.0
```

allows you to get updates from the **shared** upstream, i.e. you want to keep `origin/development` up to date with `shared/development`.
Checkout a new branch

``` bash
git checkout -b shared_development shared/development
```

to create a local read-only copy of the *shared* upstream.
When it's time to get updates

``` bash
git checkout development
git merge shared_development --ff-only
```

make sure you are on the right branch and you do fast-forward merge only!

The *origin/development* branch can be used to provide a small bugfix, but the favored solution is to go with a new *origin/bugfix* or *origin/feature* branch. In both cases a **Pull request** is the appropriate strategy. The `git rebase` command will help you in case your *pull request* is outdated because of new commits from other contributors.

### Tips

It is a bad practice to commit some semi-finished changes (or have several different changes in one commit), but what to do in case you have to leave or switch the place which implies the need to commit and push changes upstream? Well, there is a simple solution to that. Just do it, but leave a special hint in the message which is often refered as *work in progress*:

``` bash
git add .
git commit -m 'WIP: whatever I started to do'
git push
```

Whenever the work is finished the last commit (WIP) should be replaced via

``` bash
git commit --amend
```

and the message `'WIP: whatever I started to do'` can be edited in the text-editor that opens automatically (e.g. *nano* or *vim*).
The drawback or complication of this workflow is that you will need to foce `git push -f` and in case of working with multiple workstation also `git pull --rebase` will be necessary. So, make sure you know what you are doing!

Some other advanced but helpful technics are for instance [stash](https://git-scm.com/docs/git-stash) and [cherry-pick](https://git-scm.com/docs/git-cherry-pick).

Best sources and documentation for git:

``` bash
git help <command>
```

and the official [docs](https://git-scm.com/doc).

## Development Guidelines

### Public APIs

### Internal APIs

### Development Conventions and Best Practices

## Testing and Deployment

### JUnit Tests

### extTests

### Configuration

### HHUBS Cluster sollipulli

### HHU Cluster HILBERT
