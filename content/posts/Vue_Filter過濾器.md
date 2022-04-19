---
title: "Vue_Filter過濾器"
date: 2019-10-04T19:50:39+08:00
draft: false
description: "vuejs"
tags: [
    "vuejs"
]
---

用於處理一些頁面上資料的呈現


用法:  值後面加上 | (pipe) 可以串入多個Filter，有順序之分(左至右)

	{{ value | A | B | C }}

 	A 執行完 會B 再換 C

範例:

替金額加上$，和千分位符號  程式碼如下

	<div id="app">
		<div>{{ price | currency }}</div>
	</div>


	new Vue({
		el: '#app',
		data: {
			price: 999999
		}
		filter: {
		  currency (number) {
		  	const n = Number(number)
		  	return `$${n.toFixed(0).replace(/./g, (c, i, a) => {
    		  const currency = (i && c !== '.' && ((a.length - i) % 3 === 0) ? `, ${c}`.replace(/\s/g, '') : c);
    		  return currency
			})}`
		  },
		  priceFormat (value) {
		  	return `$${value}`
		  }
		},
	})


也可以套用在 V-bind

	<div id="app">
		<div :data-value="value | A | B | C"></div>
	</div>



使用 Vue.Filter() 全域註冊

Vue.Filter('自訂名稱', 執行的函式)

範例:

	<div id="app">
		<div>{{ msg | test('hi') }}</div>
	</div>

	Vue.Filter('test', function (value, arg) {
	  return `${value}~${arg}`
	})
	new Vue({
	  el: '#app',
	  data: {
	  	msg: 'Nigel'
	  }
	})

	顯示: Nigel~hi
