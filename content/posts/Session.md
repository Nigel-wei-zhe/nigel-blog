---
author: "Nigel"
title: "Session"
date: 2019-12-06T15:23:37+08:00
description: "use express-session middleware on express"
draft: false
tags: [
	"NodeJs"
]
---
# Session 介紹
---
HTTP協議上本身是"無狀態"的,就是單純的傳送、接收，無法紀錄使用者的一些資訊，
所以 cookie 及 session 的這種機制就被發明出來了,那透一個情景來理解 Session
今天一位客人進入一間餐廳，服務生會發給他一張會員卡，上面會有一組會員ID
並在餐廳內部電腦記錄了，這個 ID 是哪位顧客持有的，並把基本資料 (姓名、電話) 跟這個 ID 綁定在一起
當下次這位顧客來到餐廳，出示他的會員卡，服務生就能透過會員的ID去查客人的基本資料
那麼 這裡面的 會員ID 就是 Session ID
藉由這個機制，就可以擴充HTTP協議本身是無狀態，讓一些新的應用產生

# express-session
---
NPM:

	npm install express-session

Example:

	var express = require('express')
	var session = require('express-session')

	app.use(session({
	  name: 'connect.sid' // 設置在cookie中,保存session的名稱,預設為'connect.sid'
	  store: ,// 默認存在內存中，可以改成 redis, mongodb 等
	  secret: 'keyboard cat', // 加密字串
	  resave: false, //每次請求要不要再重新發送 session 
	  saveUninitialized: true // 再沒有不論有沒有 session 每次請求都會發送 session cookie
	  cookie: { maxAge: 10 * 1000 } // 設定有效時間
	}))

	app.get('/', function(req, res, next) { 
	  var sess = req.session
	  if (sess.views) {
    	sess.views++
    	res.setHeader('Content-Type', 'text/html')
    	res.write('<p>views: ' + sess.views + '</p>')
    	res.write('<p>expires in: ' + (sess.cookie.maxAge / 1000) + 's</p>')
    	res.end()
	  } else {
    	sess.views = 1
    	res.end('welcome to the session demo. refresh!')
	  }
	})




# 參考資料連結
---
[session的介紹](https://yken919.pixnet.net/blog/post/45702341)

[express_cookie & session](https://wiki.jikexueyuan.com/project/node-lessons/cookie-session.html)

[express-session](https://github.com/expressjs/session)