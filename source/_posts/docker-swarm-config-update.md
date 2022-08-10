---
title: docker-swarm-config-update
date: 2022-08-11 00:40:26
tags:
---

# 如何不停止 Docker swarm 服務修改 config 

在使用 Docker swarm 部屬環境時，我們會在 compose file 中使用 `configs` 來讓服務可以動態調整參數。
```yml
# docker-compose.yml
configs:
  http_config:
    file: ./httpd.conf
```
但是當我們需要修改設定時會發現 `docker stack deploy` 並不會偵測到 config 檔案變更而幫我們更新服務設定，必須要停止所有服務重新啟動才會更新，停止所有服務只因為其中一個服務需要更新非常不合理，應該只有修改 config 的服務自己重啟就好。

為了解決這個問題我們必須要讓 docker 偵測到服務有變更需要更新，這邊我們可以使用 `configs` 中的 `name` 來幫 config 檔設定別名，當我們的 config 變更後別名跟著變動就可以讓 docker 偵測到服務需要重新啟動。
```yml
# docker-compose.yml
configs:
  http_config:
    file: ./httpd.conf
    name: http_config_20220811 # config 修改後變更別名，例如在後面加入日期
```

雖然修改別名能夠解決問題，但是這樣每次改 config 就要同時修改 compose file 也是很不方便，所以我們用環境變數調整 `name` 的值讓他可以動態改變，在原本的 name 後面接上檔案的 hash，這樣只要內容有變更 hash 值就會一起變動，只需要在 config 修改後將 `HTTP_CONFIG_HASH` 設定成新的 hash 就好。


```sh
# update-hash.sh 
#!/bin/sh
export HTTP_CONFIG_HASH=$(shasum httpd.conf -a 512 | cut -c1-16)
```
部屬環境或是 config 修改完成要重新啟動服務時執行 `source update-hash.sh`

```yml
# docker-compose.yml
configs:
  http_config:
    file: ./httpd.conf
    name: http_config_${HTTP_CONFIG_HASH}
```

# 參考
[Updating Docker Swarm Configs and Secrets Without Downtime](https://www.youtube.com/watch?v=oWrwi1NiViw)
[update-hash.sh ](https://github.com/BretFisher/dogvscat/blob/master/hash-config-secret.sh)


