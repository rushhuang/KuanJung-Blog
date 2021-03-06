---
toc: true
layout: post
description: My very first blog post talking about fastpages and ssh tunnelling.
categories: [markdown, tutorial]
title: First Blog Post
hide: false
search_exclude: false
---
## 前言
有鑑於自己的記憶力一直都不是很好，常常忘記事情，因此想說開個 blog 來記錄一下遇到的一些事情以及解決方法，順便紀錄自己看到的一些有趣的東西。

## 正文

### [fastpages](https://github.com/fastai/fastpages)
為了要建 blog，簡單搜尋了一下快速搭建 blog 的工具，除了常見的 Hexo、Hugo 之類的，也有發現 fastpages 這個工具，由於它
原生支援 jupyter notebook，想說好像挺方便的就來玩看看。

跟著[教學步驟](https://github.com/fastai/fastpages#hiding-a-blog-post)走基本上不會遇到太大的問題。但我自己是沒仔細看教學步驟說的要把 `New repository secret` 所新增的 private key 名稱設定成指定的 `SSK_DEPLOY_KEY`。因此在第一次搭建的時候沒有搭建成功，最後砍掉重練。不過第二次注意到後就沒問題，搭建過程也算快速。

### MacOS 從 terminal 打開 Docker
由於 blog 是部屬在 Github Pages 上，其中也存在「一個小時只能 build 十次」([GitHub Pages sites have a soft limit of 10 builds per hour.](https://docs.github.com/cn/pages/getting-started-with-github-pages/about-github-pages)) 的限制。就算沒有這樣的限制，把修改好的東西一次 push 到 GitHub 上感覺也是一個好習慣(?)，所以我們就先在本機端測試一下網站的效果。

把 GitHub 上的 repository clone 到家裡的 Mac Mini 上後就開始測試啦。跟著[教學文件](https://github.com/fastai/fastpages/blob/master/_fastpages_docs/DEVELOPMENT.md)的腳步，下了 `make server`。

```
...
...
...
docker.errors.DockerException: Error while fetching server API version: 500 Server Error for http+docker://localhost/version: Internal Server Error ("b'dial unix docker.raw.sock: connect: connection refused'")
[36767] Failed to execute script docker-compose
make: *** [server] Error 255
```

噴出了一堆 error message...

趕快 Google 一波壓壓驚，查了一下發現原來是機器上的 Docker Desktop 沒開。由於是遠端進去的，所以也不能直接點 Docker Desktop 圖示來開啟。

迅速 Google 了一下，找到[有人說](https://stackoverflow.com/questions/54437744/how-to-start-docker-from-command-line-in-mac)用 `open -a Docker` 的方式就可以開了，試了一下，用 glances 看，真的有開起來。

這時候下 `make server` 應該就不會有問題了 (雖然我是照著 `Makefile` 中 `make server` 每個指令一個一個下的)。

### 利用 SSH 建立 SOCKS proxy server
這時候會開啟一個 local server，由於是開在遠端機器的本機端(有點饒口)，所以我們可以利用 `ssh -D 6666 username@server_ip` 的方式開啟 SOCKS proxy，接著進到手邊電腦瀏覽器設定 proxy 的頁面，在「手動設定 Proxy」選項下的「SOCKS 主機」後填入 `localhost`，並在「埠」的欄位填上剛剛指定的 `6666`，就完成了。

這時候隨便找個 check ip 的網站應該就可以發現 ip 的確有換了。

### Live view 
接著點進 `make server` 程序最後提供的本機端網址([0.0.0.0:4000/KuanJung-Blog](0.0.0.0:4000/KuanJung-Blog)))，就能看到自己的網站了。

## 後話
這次的紀錄先到這邊，希望自己可以常常更新XD

