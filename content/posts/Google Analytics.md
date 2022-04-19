---
author: "Nigel"
title: "Google Analytics"
date: 2019-12-30T21:41:49+08:00
description: "hugo Internal Templates - Google Analytics "
draft: false
tags: [
	"google"
]
---
開發網站絕對不是為了自己開心，通常都有目的性，不論是分享資訊、廣告、賣東西
那麼就會有個問題出來了，究竟有多少人看過我的網站呢? 流量如何? 都是從哪裡連過來
所以就會套用網路分析工具，在自己的網頁中埋code，方便統計這些數據，從而優化自己網站，增加流量

# Google Analytics

那麼用自己的 blog 為例，目前引擎採用 hugo v0.58
根據官方的文件，是有 Internal Templates 只需要簡單添加幾行code就可以開通了

那麼第一步當然就是先去 Google Analytics 註冊開通，完成後應該會拿到一組 ##追蹤 ID## 

大概是長這樣

	UA-123xxxxxx-0

取得之後 就可以去 hugo 的 config.toml 裡 加入一行

	googleAnalytics = "UA-123xxxxxx-0" 

之後去你的 index 模板 加入

	{{ template "_internal/google_analytics.html" . }}


run hugo server

接著去 Google Analytics 後台 看 即時流量 應該會有 "1" 就表示成功了，可以追蹤到你的網頁了


那麼補充一下可以在你的網址中加入 UTM 更能清楚知道來自哪邊

	utm_source=FB // 活動來源
	utm_medium=social // 活動媒介
	utm_campaign=ZZZ // 活動名稱

