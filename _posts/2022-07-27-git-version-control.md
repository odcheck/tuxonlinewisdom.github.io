---
title: 'Git branching and stuff' # Title in the Post as H1
date: 2022-07-27
categories: [IT] # categories
tags: [it, git, scm, branch] # always in small letters
external_links:
    target: _blank # target of external links
external_url: '' # URL
image:
  path: # points to the image on cloudinary cdn starting with /
  alt: # description 
---
## Create new feature-branch
1) Ensure you are on master and you have the latest code
```
git checkout master
```
2) Ensure you have the latest code
```
git fetch
git status
```
```
git pull
# or
git pull --ff-only # This prevents automatic merge commits from just pulling
```
3) Create new feature-branch
```
git checkout -b feature/<short-description-alphanumeric-lowercase-with-dashes>
```
### Commit & Push
1) Check which changes you have made
```
git status
```
2) Selectively add new files not tacked yet by git / removed files
```
git add <path-spec>
```
3) Selectively add and review changes to existing (tracked files)
```
git add -p .
# or
git add -p <path-spec>
```
4) Create a commit with a reasonable commit message \
When using a CLI editor, after saving and closing the message file git will proceed with the commit automagically!

To abort: Simply safe an empty file and the commit get’s aborted
```
git commit -m "<reasonable-commit-message>"
# or if you want to use an editor
git commit
# and with more helpeful output
git commit -v
```
5) *optional* Fix files changes to included in the previous commit (ONLY if NOT PUSHED yet)

    1. add files / changes as noted previously
    2. instead of a normal commit, do:

```
git commit --amend -m "<reasonable-commit-message>"
```
or if you want to use an editor
```
git commit --amend
# and with more helpeful output
git commit --amend -v
```
6) *optional* fix for remote changed commits (Usually should not happen on feature-branch) \

WARNING: Rebase can have destructive consequences, only do this if you known what you are doing!

**make sure you have NO unchanged files / changes**
```
git pull --rebase
```
7) Do the final push (after one / many commits)
```
git push
```
If this is your first push, it will fail, because git does not yet know where to put the branch
on the remote repo. \
Git will output an example on how to fix this based on the local branch name, e.g
```
git push --set-upstream origin <your-feature-branch-name>
```
### Sync from “mainline”
0) Ensure your branch is backed Up before sync by committing & pushing
```
git commit ...
git push
```
1) Update repo with latest remote data
```
git fetch
```
2) Check what changed
```
git log --graph --oneline --decorate HEAD..origin/master
# For more details
git log --graph HEAD..origin/master
```
3a) Normal merge
```
git merge origin/master
# opon merge conflicts:
git merge --abort # to cancel merge
# use editor like vim and git add to resolve conflicts
git merge --continue # to resume merge after resolution
```
3b) Rebase (advanced) \
WARNING: Rebase can have destructive consequences, only do this if you known what you are doing!
```
git rebase -i origin/master
# an editor will open and show which commits will be rebased
# Additional rebase behaviour can be set there, but this is strongly discuraged during sync!
# after saving and closing the rebase plan file the rebae is executed one commit at a time
# upon getting a conflict
git rebase --abort # to cancle rebase
```
```
git status # this will show 
# what rebase operation was executed last, that failed
# what rebase opteration will happen next
# what files contain conflicts
# use editor like vim and git add to resolve conflicts
git rebase --continue # to continue the rebase process after resulution
git rebase --skip # in case the rebase does not continue because the commit is now empty after resulution
# This might happen if your changes were already made by another on the master branch
```
### Close Pull Request + Merge to “mainline”
AFTERWARDS, if no pipeline with automatic versioning exists:
```
git checkout master
git pull
git status
git tag | sort -V | tail
git tag <appropriate-new-tag-on-merge-commit>
git push origin <previously-created-tag>
```

That's it so far. 