---
author: "Nigel"
title: "Shallow Copy & Deep Copy"
date: 2019-12-18T09:44:32+08:00
description: "the difference between a deep copy and a shallow copy"
draft: false
tags: [
	"NodeJs",
	"javascript"
]
---
# Data Type (型別)
---
首先在JS中,可分為 **Primitive Type (基本型別)** 跟 **Non-Primitive Type (非基本型別)**

* Primitive: Number、 String、 Boolean、 Null、 Undefined
* Non-Primitive: Object、 Array、 Function、 Date、 Regx

兩者差異在於，給值方式的不同

那麼可以分為 **By value (值)**  跟  **By reference (參考位置)**

1. Primitive Type 是 By value

	用 **Number** 舉例:

		var a = 1
		var b = a
		b = 2

		console.log(a); // Output: 1
		console.log(b); // Output: 2

		// 修改 b 時不會修改到 a

2. Non-Primitive Type 是 By reference

	用 **物件(Object)** 舉例:

		var obj1 = { name: 'obj1', id: 123 }
		var obj2 = obj1
		obj2.name = 'obj2'
	
		console.log(obj1); // Output: { neme: 'obj2', id: 123 }
		console.log(obj2); // Output: { neme: 'obj2', id: 123 }

		// 修改 obj2，把 obj1 也改了

# Shallow Copy (淺拷貝)
---

那麼 Shallow Copy 指的就是上面那個情況，可以發現在修改 obj2 的時候，把 obj1 也改了。
因為 var obj2 = obj1 只是把"參考位置"賦予給 obj2 ，兩個物件彼此是共用同一個"參考位置"，而位置都指向同一個"值"，
當修改 obj2 時就會去"參考位置"把"值"替換掉，導致影響到原來的資料

# Deep Copy (深拷貝)
---

所以在處理 Non-Primitive Type By reference 時，就要去賦予新的"參考位置"讓彼此不要相互影響
具體作法可以採用ES6的函式`Object.assign()`，先建立一個空物件把所有屬性拷貝進去，會跟原始物件長的一模一樣，但參考位置是各自獨立的

用上面例子修改

		var obj1 = { name: 'obj1', id: 123 }
		var obj2 = Object.assign({}, obj1)
		obj2.name = 'obj2'
	
		console.log(obj1); // Output: { neme: 'obj1', id: 123 }
		console.log(obj2); // Output: { neme: 'obj2', id: 123 }

		// 修改 b 時，就沒有影響到 a 了

那麼要注意 `Object.assign()` 只能複製 "第一層" ，如果物件裡面的屬性中又包含一個物件，那麼就會漏掉

	var obj1 = { name: 'obj1', id: 123, obj: { a: 0}}
	var obj2 = Object.assign({}, obj1)
	obj2.name = 'obj2'
	obj2.obj.a = 999;

	console.log(obj1); // { name: "obj1", id: 123, obj: Object { a: 999 } }
	console.log(obj2); // { name: "obj2", id: 123, obj: Object { a: 999 } }
	console.log(obj1 === obj2); // false
	console.log(obj1.obj === obj2.obj); // true


如果資料格式剛好是 `JSON ` 格式就可以使用`JSON.stringify`把物件轉成字串，在使用`JSON.parse`把字串轉成新的物件，這樣就可以達成完全的**Deep Copy**，但前提是 `JSON ` 格式