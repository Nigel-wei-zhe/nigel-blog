---
title: "Build Express"
date: 2019-10-16T14:12:25+08:00
draft: false
description: "Build Express"
tags: [
    "nodejs"
]
---
#介紹
---
express是建立在node.js的http模組上，另外包裝，並提供
一些中介。

不免俗 Hello world 範例:

	const express = require('express')
	const app = express()

	app.get(`/`, function (req, res) {
	  res.send(`Hello World!`)
	})
	
	app.listen(3000, function () {
  	  console.log(`Example app listening on port 3000!`)
	})

或者 可以直接用產生器

全域安裝

	npm install express-generator -g

裝完透過

	express -h

可以看到

	Usage: express [options][dir]
	Options:
    -h, --help          output usage information
        --version       output the version number
    -e, --ejs           add ejs engine support
        --hbs           add handlebars engine support
        --pug           add pug engine support
    -H, --hogan         add hogan.js engine support
        --no-view       generate without view engine
    -v, --view <engine> add view <engine> support (ejs|hbs|hjs|jade|pug|twig|vash) (defaults to jade)
    -c, --css <engine>  add stylesheet <engine> support (less|stylus|compass|sass) (defaults to plain css)
        --git           add .gitignore
    -f, --force         force on non-empty directory

到要開專案的路徑底下(這邊選用 ejs 模板)

	express --view=ejs myapp

資料結構:

	.
	├── app.js
	├── bin
	│   └── www
	├── package.json
	├── public
	│   ├── images
	│   ├── javascripts
	│   └── stylesheets
	│       └── style.css
	├── routes
	│   ├── index.js
	│   └── users.js
	└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug

	7 directories, 9 files