---
title: "Unable to retrieve a connection's remote IP address under IISNode"
date: 2019-11-08T10:09:08+08:00
draft: false
description: "express retrieve a connection's remote IP address under IISNode"
draft: false
tags: [
    "NodeJs"
]
---
# 狀況
---

在 IIS 底下安裝 IISNode 模組，並在後端架設一個 Node.exe
要在 Node.exe 上獲取遠端連接的IP位址會失敗。
因為 IISNode 像是一個 reverse proxy 多個源頭進來，但 Node.exe 只會看到一個位址
就是 IISNode 所有的 client 連進來都看不到。
另外 IISNode 與 Node.exe 之間的連接是走命名的方式，不是走 TCP，所以在
Node.exe 無法取到 IP address

# 解決
---

在 IISNode 的 web.config 上添加

	<configuration>
  		<system.webServer>

    		<!-- ... -->

    		<iisnode enableXFF="true" />

  		</system.webServer>
	</configuration>


這樣 client 連進來 IISNode 要拋給 Node.exe 就會添加 一個 X-Forwarded-For request header
把外部進來 IP　再傳遞下去

	const http = require('http')
	  http.createServer(function (req, res) {
	  const xff = req.headers['x-forwarded-for']
      // ...
    }).listen(process.env.PORT)




# 參考連結
---
[github_issues](https://github.com/tjanczuk/iisnode/issues/94)