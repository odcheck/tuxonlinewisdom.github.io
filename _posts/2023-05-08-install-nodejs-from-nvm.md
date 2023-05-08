---
title: 'NVM is more love then Ubuntu Repo'
date: 2023-05-08
categories: [IT]
tags: [node, nvm, nodejs, ubuntu]
---
> nodejs from ubuntu repo is outdate as hell
{: .prompt-warning }

The only thing that works for me, is grep the install.sh form [here](https://github.com/nvm-sh/nvm#install--update-script){:target="_blank"}

like so
```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```
reload your bashrc
```shell
source ~/.bashrc
```
{: .nolineno }
list all avaiable versions
```shell
nvm list-remote
```
{: .nolineno }
install like this for e.g.
```shell
nvm install lts/hydrogen
```
{: .nolineno }
and tell your system to use the version
```shell
nvm use v18.13.0
```
{: .nolineno }

that's all about it.






