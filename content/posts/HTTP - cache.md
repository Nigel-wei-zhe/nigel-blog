---
author: "Nigel"
title: "HTTP - cache"
date: 2020-01-15T11:11:40+08:00
description: "HTTP-cache's study"
draft: false
tags: [
	"html5"
]
---
## 序
---
快取(cache)，聽過也大概知道有甚麼作用，但其中的原理還有 Header 中的一些相關配置就不是這麼的了解
所以整理了一下資料讓自己更清楚。

## 快取(Cache) 是甚麼
---
今天要瀏覽一個網頁，流程會是這樣 

> **瀏覽器** -- 請求 --> **伺服器** -- 提供HTML、images...等相關資源 --> **瀏覽器**

所以每次想要瀏覽一個網頁，就要從網頁伺服器，下載頁面、 圖片等等...的資源，假設今天那個網頁不常更新，內容其實都一樣，這樣每次下載一樣的東西，流量不就是浪費了嗎?
這時候 快取(Cache) 就派上用場了。

快取(Cache) 就是把比較不常變動的資源儲存起來在瀏覽器的快取中，當使用者今天要拜訪這個網頁時，就能快速把資料取出來。
可以節省流量，也因為不用再下載，也可以節省時間。

## Expires 
---
那麼要怎麼讓瀏覽器知道，這個頁面要快取呢?
可以在 HTTP Response Header 裡面添加 Expires
Expires 是 HTTP 1.0 的 Header

	Expires: Tue, 12 Jan 2021 14:41:30 GMT

瀏覽器收到這個Response，就會把資源快取下來，當下一次瀏覽器要再次瀏覽這個網頁，瀏覽器會檢查自己本身的時間，去比對是否有過期，超過 Expires 的時間，如果沒有超過，瀏覽器就不會發送 Request ，直接從 快取 中拿取資料。

那麼會有一個問題，瀏覽器比對是根據自己本身的時間，假設自己本身時間被改過，那麼就會失準。

## Cache-Control: max-age
---
為了解決這個問題 HTTP 1.1 堆出了 新的 Header，用法如下

	Cache-Control: max-age=10

意思是這個請求的到期時間是10秒，在10秒之內重新整理，都是從快取裡面拿資料，超過10秒之後，才會重新送新的 Request。

以上兩個，都是著重在 Response 的 新鮮度 (freshness) ，只要時間還沒到期，就去快取裡面拿資料，過期才發送 Resquest
，那麼如果一個 Header 同時有 Expires 和 Cache-Control: max-age 會優先參考 max-age。

## last-modified & if-modified-since
---
前面兩個有提到如果過期之後就是發送一個新的 Request ，那麼可能有一種情況新鮮度過期了，但去跟伺服器請求資料發現，資料還是沒更新跟快取中的還是一樣，那在這情況之下，有辦法就直接找快取拿資料嗎?

答案是有的，如下:

	Server 給的 Response :

	last-modified: Tue, 22 Oct 2019 18:15:00 GMT
	cache-control: max-age=10

那麼經過了11秒，新鮮度過期了發送了一個 Request 

	client  發的 Request :

	if-modified-since: Tue, 22 Oct 2019 18:15:00 GMT // 把當初收到的 last-modified 傳回去

這時候伺服器收到，就會確認 last-modified 的日期 是否有更改過，如果有新的就傳新的，沒有的話 Server會回傳 Status code: 304,表示你可以繼續沿用快取。

last-modified 是 指檔案的編輯時間，假設你今天打開這個檔案甚麼都不改然後存檔，編輯時間就會被更改，但實際上內容還是一樣

## etag & if-none-match
---
為了更加確認，檔案真的不一樣了，而不是單純的參考編輯時間，所以又出現了這個 Header。  Etag 可以想像是，把目前檔案裡的內容編成一個數值，如果檔案內容不變，etag的值不會變，但如果改變了就會有一個新的etag值。
流程基本上跟 last-modified 一模一樣。

## Cache-Control: no-store & no-cache
---

	no-store: 完全不使用快取                             // 永遠不用快取
	no-cache: 每次都會發送 Request，確認是否有新的檔案    //  永遠檢查快取

## 參考資料
---
[循序漸進理解 HTTP Cache 機制](https://blog.techbridge.cc/2017/06/17/cache-introduction/)

[彻底弄懂 Http 缓存机制 - 基于缓存策略三要素分解法](https://mp.weixin.qq.com/s/qOMO0LIdA47j3RjhbCWUEQ)

[HTTP缓存控制小结](https://imweb.io/topic/5795dcb6fb312541492eda8c)