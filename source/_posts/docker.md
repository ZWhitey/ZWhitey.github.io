---
title: docker
date: 2021-07-19 11:36:46
tags: docker
---

# Docker 指令筆記

-----
* Docker
  * 複製檔案到 container
  `docker cp <src-path> <container>:<dest-path> `
  範例：`docker cp ./sample.txt 1cea5baea09b:/sample_folder`

  * 連線到 container bash
  `docker exec -it <container> /bin/bash`
  範例：`docker exec -it 1cea5baea09b /bin/bash`

-----