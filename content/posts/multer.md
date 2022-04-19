---
title: "multer"
date: 2019-11-24T16:08:57+08:00
draft: false
description: "Multer is a node.js middleware for handling multipart/form-data"
draft: false
tags: [
    "javascript",
    "NodeJs",
    "vuejs"
]
---
# 介紹
---
>Multer 是一個 node.js 的中間件，"只"用於處理 multipart/form-data 類型的數據，主要用於上傳

安裝:

	npm install --save multer

# 參數
---

## req.file 的屬性

Key|Description|Note
:-:|:-:|:-:
fieldname|表單上面的名稱|
originalname|電腦上顯示的檔案名稱|
encoding|編碼|
mimetype|文件的mime 類型|
size|文件大小 (位元組) |
destination|路徑|DiskStorage
filename|保存在 destination 的名稱|DiskStorage
path|完整路徑|DiskStorage
buffer|存放檔案的內存|MemoryStorage

## multer(opts) 的  opts

Key|Description
:-:|:-:
dest or storage|存放位置
fileFilter| 過濾 (函式)
limits|限制數據
preservePath|保存完整文件路徑

>storage

	const upload = multer({ dest: 'uploads/' })
	// 存放在 uploads 資料夾裡

	or

	const storage = multer.diskStorage({
	  destination: function (req, file, cb) {
        cb(null, 'uploads/')
      },   // 存放在 uploads 資料夾裡
      filename: function (req, file, cb) {
    	cb(null, file.originalname)
	  }    // 設定檔案的名稱，沒有設定的話是隨機並且沒有副檔名
	})

	const upload = multer({ storage: storage })

存於內存:

	const storage = multer.memoryStorage()
	const upload = multer({ storage: storage })

>limits

   fieldNameSize – 欄位名最大尺寸。預設值：100 bytes

   fieldSize – 欄位值最大尺寸。預設值：1MB

   fields – 非檔案欄位的最大數量。預設值：Infinity

   fileSize – multipart 表單中，檔案的最大尺寸。預設值：Infinity

   files – multipart 表單中，檔案最大數量。預設值：Infinity

   parts – multipart 表單中，最大元件(fields files)數量。預設值：Infinity

   headerPairs – 預設值：2000

範例:

	const upload = multer({
	  limit: {
        fileSize: 1000000 // 限制上傳檔案的大小為 1MB = 1000000 bytes
	  }
	})

>fileFilter

過濾函示，直接上範例

	const onlyImage = function (req, file, cb) {
	  const reg = /^image\/*/   // 正規驗證 image 類型的檔案
	  if (reg.test(file.mimetype)) {

		// 若接受該檔案，呼叫 cb() 並帶入 true
    	cb(null, true)

	  } else {

	  	// 自訂一個屬性 fileValidationError 加到 req 中
    	req.fileValidationError = `上傳檔案格式錯誤` 


    	// 若不接受該檔案，呼叫 cb() 並帶入 false, 錯誤訊息可帶可不帶
    	cb(null, false, new Error('上傳檔案格式錯誤'))
	  }
	}

	const upload = multer({ fileFilter: onlyImage })


## multer(opts) 後面接的方法

>.single(fieldname)

接受 "一個" 名稱為 "fieldname" 的資料。 資料存在 req.file

>.array(fieldname[, maxCount])

接受 "數個" 名稱為 "fieldname" 的資料，maxCount 限制最大數量。 資料存在 req.files

>.fields(fields)

接受 "數組" 名稱不同 的資料。 資料存在 req.files

	[
	  { name: 'avatar', maxCount: 1 },
	  { name: 'gallery', maxCount: 8 }
	]

>.any()

接受一切上傳的資料。資料存在 req.files

>.none()

只接受文本域


# 範例
----
html:

	<form action="/profile" method="post" enctype="multipart/form-data">
	  <input type="file" name="avatar">
	</form>

		or
	
	<input type="file" ref="files">

	...

	 const uploadFile = this.$refs.files.files[0]
	 const formData = new FormData()
	 formData.append('avatar', uploadFile)


server:

	const express = require('express')
	const multer  = require('multer')
	const upload = multer({ dest: 'uploads/' })

	const app = express()

	app.post('/profile', upload.single('avatar'), function (req, res, next) {
	  // req.file is the `avatar` file
	  // req.body will hold the text fields, if there were any
	})

	app.post('/photos/upload', upload.array('photos', 12), function (req, res, next) {
	  // req.files is array of `photos` files
	  // req.body will contain the text fields, if there were any
	})



# 參考連結
----
[Multer](https://github.com/expressjs/multer)