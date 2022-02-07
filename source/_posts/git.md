---
title: git
date: 2022-01-28 13:11:58
tags: git
---

# Git 指令筆記

-----
* Git
  * 還原上一次 commit 並且刪除所有變更

    `git reset --hard HEAD~1`

  * 還原上一次 commit 並且保留所有變更

    `git reset --soft HEAD~1`

  * push 時遇到 `! [rejected] develop -> develop  (would clobber existing tag)` 修復方法

    `git fetch --tags -f`

-----