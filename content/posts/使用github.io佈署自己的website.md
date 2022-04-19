---
title: 使用github.io佈署自己的website"
date: 2019-10-05T17:28:06+08:00
draft: false
description: "github.io"
tags: [
    "github"
]
---

Github有提供可以呈現靜態檔案的伺服器
只有靜態檔案，所以動態網頁是無法呈現的

使用方法如下:

----
1.Create a repository

  前往 github 創一個新的 repository 名稱必須和使用者一樣 ( 使用者名稱/使用者名稱.github.io )
舉例:
	Nigel-wei-zhe/Nigel-wei-zhe.github.io

!!!  要設定為 Public !!!

----
2.在本地端建立資料夾
  
  創好 repository 後 可以選擇在本地端clone一個資料夾或者自己創一個透過git指令上傳
這邊示範自己建資料夾git上傳

首先在桌面創建一個資料夾 page
並在資料夾裡隨意新增一個 index.html
隨便寫點內容

index.html:

	<!DOCTYPE html>
	<html>
		<body>
			<h1>Hello World</h1>
			<p>I'm hosted with GitHub Pages.</p>
		</body>
	</html>

存檔


接著透過上方路徑列開啟cmd

	C:\Users\Nigel\Desktop\page>

開始添加git指令:

	echo "# my first page" >> README.md
	git init
	git add .
	git commit -m "first commit"
	git remote add origin https://github.com/(你的名稱)/(你的名稱).github.io.git
	git push -u origin master

上傳完之後，幾分鐘後應該就能在 https://(你的名稱).github.io/ 上  看到自己的網頁了~


----
