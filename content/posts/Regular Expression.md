---
title: "Regular Expression"
date: 2019-10-08T15:22:42+08:00
draft: false
description: "RegExp"
tags: [
    "javascript"
]
---
# 介紹
----
Regular Expression (RegExp) 正規表達式
用來判斷字串是否有符合格式
線上測試Reg格式的網址:https://regexr.com/


# RegExp宣告
----
以下用js示範
直接例項化:

	var reg = new RegExp(pattern [, flags])

隱式建立:

 	var reg = /pattern/flags

pattern 是一個字串，填入正規表示式
flags 是一個可選的字串，包含屬性 'g'（global ）、'i' （ignoreCase）和 'm'（multiline）


# RegExp 物件方法
----
test:
  檢索字串中是否存在指定的值。返回值是 true 或 false

	var reg = new RegExp('a')
	console.log(reg.test('abc'))

	OUTPUT: true

exec:
  檢索字串中的指定值。返回值是被找到的值。如果沒有發現匹配，則返回 null

	var reg = new RegExp('a')
	console.log(reg.exec('abc'))

	OUTPUT: a

replace:
  替換與正規表示式匹配的子串

	var str = 'hi'
	console.log(str.replace(/hi/, 'yo'));
	
	OUTPUT: yo


# 範例
----
RegExp|說明|範例
:-:|:-:|:-:
`/^09\d{8}$/`|手機號碼|"0912345678"
`/^.*@gmail\.com$/`|gmail|"123@gmail.com"
`/^[A-Z]\d{9}$/`|身分證字號|"A123456789"
`/^\d{4}-\d{2}-\d{2}$/`|西元生日格式|"1993-08-07"
`/^U[0-9a-f]{32}$/`|LineID|
`/^[1-9][0-9]{4,9}$/`|QQ號|"10583600"
`/^\d $/`|是否是數字|
`/[\u4e00-\u9fa5]/`|是否存在中文|



# 參考來源
----
https://codertw.com/前端開發/231904/
