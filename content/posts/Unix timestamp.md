---
title: "Unix timestamp"
date: 2019-10-23T15:16:39+08:00
draft: false
description: "Unix timestamp 時間戳簡介並轉換"
draft: false
tags: [
    "javascript"
]
---

# 簡介
---
Unix timestamp (時間戳) 是指至格林威治時間 1970年01月01日00时00分00秒起
到現在的"總秒數"


# javascript 轉換
---

1. 1572480000 --> 2019-10-31 08:00:00 +0800

YYYY-MM-DD格式，使用主機時間
	
	function (timestamp = 1572480000) {
	  const month = new Date(timestamp * 1000).getMonth() < 10 ? 0 + (new Date(timestamp * 1000).getMonth() + 1) : new Date(timestamp * 1000).getMonth() + 1
      const date = new Date(timestamp * 1000).getDate() < 10 ? 0 + (new Date(timestamp * 1000).getDate()) : new Date(timestamp * 1000).getDate()
      const formatTime = `${new Date(timestamp * 1000).getFullYear()}-${month}-${date}`
      return formatTime
	}

2. 2019-10-31 08:00:00 +0800 --> 1572480000 

使用主機時間

	function () {
	  const timestamp = new Date('2019-10-31 08:00:00 +0800').getTime()
	  const result = Math.floor(timestamp / 1000)
	}

# 補充
---

	new Date('2019-10-31 00:00:00 +0000') // 有寫時區的話，會以給定時區的時間，回傳當地時區的時間
	new Date('2019-10-31')                // 沒寫時間的話，會以 UTC（+0）的 00:00 為時間，回傳當地時區的時間
	
