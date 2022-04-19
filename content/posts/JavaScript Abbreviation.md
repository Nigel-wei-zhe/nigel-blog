---
title: "JavaScript Abbreviation"
date: 2019-10-20T17:02:14+08:00
draft: false
description: "shorthand JavaScript coding techniques"
draft: false
tags: [
    "javascript"
]
---
* 三元運算子

當要寫 if else 判斷式時 一般會寫成

	const a = 7
	let result

 	if (a > 0) {
	  result = `a大於0`
 	} else {
	  result = `a小於0`
 	}

簡寫

	let result = a > 0 ? `a大於0` : `a小於0`


* 短路求值

當宣告一個變數給值時，想確認不是 null, undefined, 空值時
可能會這樣寫

	if (a !== null || a !== undefined || a !== '') {
	  let b = a
	}

簡寫

	let b = a || '值有誤'

* 物件屬性

如果宣告物件裡的屬性名稱和值相同名稱

	const obj = { x: x, y: y }

簡寫

	const obj = { x, y }


* 箭頭函式

直接舉例

	function sayHello(name) {
	  console.log('Hello', name)
	}

簡寫

	sayHello = name => console.log('Hello', name)


* 解構賦值簡寫方法

宣告引用解構時

	const observable = require('mobx/observable')
	const action = require('mobx/action')
	const runInAction = require('mobx/runInAction')
	const store = this.props.store
	const form = this.props.form
	const loading = this.props.loading
	const errors = this.props.errors
	const entity = this.props.entity

簡寫

	import { observable, action, runInAction } from 'mobx'
	const { store, form, loading, errors, entity:contact } = this.props
	//最後一個變數名為contact


* 物件陣列引用擴充

有一個物件或陣列要拿來合併或擴充

	const odd = [1, 3, 5]
	const nums = [2 ,4 , 6].concat(odd)

簡寫

	const odd = [1, 3, 5 ]
	const nums = [2 ,4 , 6, ...odd]

使用這個方法會重新產一個新的參考值，不會去改到原本參考值


* 強制引數簡寫

函示變數沒有值，跳例外處理
	
	function foo(bar) {
	  if(bar === undefined) {
		throw new Error('Missing parameter!')
	  }
	  return bar
	}

簡寫

	mandatory = () => {
	  throw new Error('Missing parameter!')
	}
	foo = (bar = mandatory()) => {
	  return bar
	}