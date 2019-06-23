---
layout: post
title: "Finish merge after resolving conflicts"
description: "解完衝突後，如果想繼續merge，該做什麼"
date: 2019-06-14
tags: [git, command line, cli]
comments: true
share: true
---

## 正確的合併分支訊息

通常 `merge branch` 時，如果不幸有衝突，要先解完衝突，才能繼續合併。

如果單純用命令列的指令來操作，有以下步驟

1. `git add <conflict_file_name>`
2. `git commit -m "resolve conflicts"`
3. `git push <remote_name> <branch_name>`

可是，這個 `commit log` 的 `message` 就會變成 'resolve conflicts'
而不是預設的 `Merge <branch_name> to <branch_name>`這種訊息

所以如果想要保有預設的 merge message, 再解決完衝突之後

1. `git add <conflict_file_name>`
2. `git merge --continue`
3. `git push <remote_name> <branch_name>`

這個 `commit` 的 `description`也會描述是哪些檔案發生衝突，非常好用。
