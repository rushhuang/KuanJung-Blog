---
toc: true
layout: post
description: Take a note about favicon and apple-touch-icon.
categories: [markdown, tutorial, quick notes, 隨筆]
title: About Favicon
hide: false
search_exclude: false
---
## About blog icon
在快速部屬完部落格後，如果這時候切換到其他分頁，就會看到自己部落格的分頁旁的小圖示還是預設的 fastpages 的縮圖。圖示如下：

![Fastpages favicon](https://raw.githubusercontent.com/fastai/fastpages/master/images/favicon.ico)
<span class="italic" style="display:block; text-align:center; font-size:14px; margin-top:1em;">以上圖示取自 [fastpages 的 github](https://github.com/fastai/fastpages)</span>

看了有點礙眼XD

簡單 Google 了一下發現這是網頁會使用的 favicon，有興趣的話，網路上有其他更多更詳盡關於 favicon 的介紹，這邊就不多贅述了。

關於在用 fastpages 搭建的部落格上，要改變 favicon 的設定，依據找到的[討論文](https://forums.fast.ai/t/how-do-i-add-a-logo-next-to-the-fastpages-blog-name/69904/6)，發現是要去修改部落格根目錄下的 `_includes/favicons.html`。

關於 favicon 的製作方式，只要輸出大小在 `48 X 48` 左右的 `ico` 檔，應該是沒問題，我自己是使用網路上找到的 [favicon 產生器](https://realfavicongenerator.net/) 來製作，只要把你想拿來做成 favicon 的圖丟給它，網站會自己產生支援各種瀏覽器的 favicon 檔案如下：

```command-line
android-chrome-192x192.png
android-chrome-256x256.png
apple-touch-icon.png
favicon-16x16.png
favicon-32x32.png
favicon.ico
mstile-150x150.png
safari-pinned-tab.svg
site.webmanifest
```

關於各種瀏覽器支援的 favicon 格式可參閱[這篇討論文](https://stackoverflow.com/questions/48956465/favicon-standard-2021-svg-ico-png-and-dimensions)。

得到相關檔案後，就可以把它們丟進部落格根目錄下的 `images/` 資料夾。

以及可以用來加入 `_includes/favicons.html` 檔案中的程式碼。依據原 favicon 產生時所需的 [Liquid filter](https://jekyllrb.com/docs/liquid/filters/) 相對路徑表示法 (`href="{{ "{{" }} "images/apple-touch-icon.png" | relative_url }}"`) 修改後如下： <!-- Escape Liquid tag in Jekyll blog post -->
```html
<link rel="apple-touch-icon" sizes="180x180" href="{{ "images/apple-touch-icon.png" | relative_url }}">
<link rel="icon" type="image/png" sizes="32x32" href="{{ "images/favicon-32x32.png" | relative_url }}">
<link rel="icon" type="image/png" sizes="16x16" href="{{ "images/favicon-16x16.png" | relative_url }}">
<link rel="manifest" href="{{ "images/site.webmanifest" | relative_url }}">
<link rel="mask-icon" href="{{ "images/safari-pinned-tab.svg" | relative_url }}" color="#5bbad5">
<meta name="msapplication-TileColor" content="#da532c">
<meta name="theme-color" content="#ffffff">
```

<span class="italic" style="display:block; text-align:center; font-size:14px; margin-top:1em;">以上程式碼為將相對路徑取代後結果</span>

其中值得注意的是關於 `apple-touch-icon`，它是用來當作 iOS 裝置把網頁加入主畫面時所呈現的圖示，圖示大小建議在 `180 X 180` 左右。在我做這些更動前，把部落格加入主畫面後，iOS 系統會自己以網頁縮圖來當作圖示，很醜，所以讓我興起了想要修改 `favicon` 及 `apple-touch-icon` 的想法。

## 結語
今天的紀錄就先到這裡，簡單記錄一下關於更改以 fastpages 部屬部落格修改 `favicon` 和 `apple-touch-icon` 的方法。

