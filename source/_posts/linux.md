---
title: linux
date: 2022-01-05 01:49:03
tags: linux ssh
---

# linux 筆記

-----
複製 ssh key 時遇到權限問題先檢查以下設定有沒有問題
* SSH Key 權限
  * .ssh 資料夾 `700 (drwx------)`
  * public key (id_rsa.pub) `644 (-rw-r--r--)`
  * authorized_keys `644 (-rw-r--r--)`
  * private key (id_rsa) `600 (-rw-------)`
 
-----