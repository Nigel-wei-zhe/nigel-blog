---
title: "使用Hugo"
date: 2019-10-03T20:09:38+08:00
draft: false
description: "Hugo"
tags: [
    "html5",
    "css3"
]
---

**建置環境:Windows-64bit**

----
## 安裝Hugo

前往:
	https://github.com/gohugoio/hugo/releases

下載對應的版本

在 C:\ 底下建立 一個新資料夾 命名 Hugo
裡面再建立一個子資料夾 命名 bin

把剛剛下載的檔案 全部解壓縮 放入 C:\Hugo\bin

使用 CMD 下指令 確認版本號 

	C:\Hugo\bin>hugo version

再去 控制台 -> 編輯系統環境變數 

環境變數 -> 使用者變數的 Path 把剛剛的

	C:\Hugo\bin

新增進去

使用 CMD 去確認 有新增成功

	C:\>hugo version	

有跳出版本訊息 才算成功

----
## 新增一個新的 Site

指令 

	hugo new site [Site名稱]

線上選取一個主題: 
	https://themes.gohugo.io/

選取主題後，底下作者都有教怎麼安裝
請參考

新增第一篇文章試試看

指令

	hugo new posts/my-first-post.md

會在	   \content\posts  找到我們新增的第一篇文章

這時候下指令

	hugo server -D

就會在 http://localhost:1313/ 看到成果