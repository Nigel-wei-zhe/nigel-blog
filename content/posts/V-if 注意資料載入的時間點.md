---
title: "V-if 注意資料載入的時間點"
date: 2019-10-14T16:28:40+08:00
draft: false
description: "vuejs"
tags: [
    "vuejs"
]
---
#狀況
----
Html:

	<div id="app">
		<h1 v-if="testData.array.length > 0"> 如果陣列有值顯示出來 </h1>
	</div>

Js:

	new Vue ({
	  el: '#app',
	  data: {
	  	testData: ''
	  },
	  created () {
	    const vm = this
    	vm.testData = {
      	  testArray: [
            {
              msg: 'hi'
            }
          ]
        }
	  }
	})


這時候去看console 會報錯

	TypeError: Cannot read property 'length' of undefined

就我的理解應該是一開始掛載 data 時，屬性建立時還沒有把 testArray 掛上去，當然也無法使用length

#解決辦法
----
	<div id="app">
		<h1 v-if="testData.testArray && testData.testArray.length > 0"> 如果陣列有值顯示出來 </h1>
	</div>

一開始就先檢查一次值是否存在，再執行後續動作

因為有接觸過一些專案，一開始我把判斷式都先刻好，但未注意到資料載入時間，有些可能是還需要透過API去後端拿資料
這樣可能就會造成一開始在掛載屬性報錯，所以要先了解先後順序~~

