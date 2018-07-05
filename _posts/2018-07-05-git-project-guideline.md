---
layout: post
title: "Git Project guideline"
description: "好的git管理專案工作流程會帶你上天堂"
date: 2018-07-05
tags: [git]
comments: true
share: true
---

---

這篇文章是看完thoughtbot上這篇git [project guideline](https://github.com/thoughtbot/guides/blob/master/protocol/git/README.md)上的一個整理。寫的很短，也歡迎大家直接看原文。


## 1. 管理Repo


1. `repo`中不要包含專屬你個人開發或機器相關的文件
2. `merge`後，把`local`和`remote branches` 刪除
3. 在`feature branch`上開發
4. 經常的`rebase`, 好包含`upstream`的變更
5. 用`pull request`來做`code reveiw`



## 2. 寫功能

#### 基於master, 先開一個local的feature branch

```git

get checkout master
git pull
git checkout -b <branch-name>

```

#### 沒事就fetch, rebase一下, 才能保持最新的狀態

```git
git fetch origin
git rebase origin/master
```


#### Resolve conflict, 確認功能沒問題，通過測試後，就可以stage changes

```git
git add --all
```


#### commit changes

```git
git status
git commit --verbose
```


#### 寫一個好的 commit 訊息

更多[guideline](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)可以看這裏

#### 如果不只有一個commit, 可以用git rebash interactively把他們變成更有意義的commits

```
git rebash -i origin/master
```

### git rebash 介紹
`git rebash` 是用來
* 編輯前次`commit`的訊息
* 把前面數次的`commit`變成一個
* 把不需要的`commit` 刪除或 `revert`


#### rebash commits against a branch

```
git rebash --interactive other-branch-name
```

#### rebash commits against a point in time

```
git rebash --interactive HEAD-7
```

詳細的介紹`git`上面有，[git rebash](https://help.github.com/articles/about-git-rebase/)


#### 最後share your branch

```
git push origin <branch name>
```

## 3. Review Code

對於別人的`pull reuqest`, 若有需要修改

```
git checkout <branch name>
./bin/setup
git diff staging/master..HEAD

```

在`branch`上修改，在自己的機器上做測試，`commit`和`push`
如果okay,就可以合併惹。


## 4. Merge


#### 可以用rebase interactively, 像是可以把移除空白格這種commit,和其他提交組合在一起。

```
git fetch origin
git rebase -i origin/master
```

#### force push branch, 這會讓github自動關閉你的pull request。

```
git push --force-with-lease origin <branch-name>
```

#### 查看新的commit log, 查看已經更改的文件，merge到master

```
git log origin/master..<branch name>
git diff --state origin/master
git checkout master
git merge <branch-name> --ff-only
git push
```

#### 刪除feature branch
```
git push origin --delete <branch name>
```

#### 刪除本地功能分支
```
git branch --delete <branch-name>
```


















