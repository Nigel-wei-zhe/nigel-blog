---
title: "Vee-Validate v3.0.11"
date: 2019-10-29T16:11:36+08:00
draft: false
description: "VeeValidate is a template-based validation library for Vue.js"
draft: false
tags: [
    "NodeJs",
    "vuejs"
]
---
# 介紹
----
>利用Vue.js基礎模板來驗證表單的模組，內建一些驗證規則，也可自行新增

# 設置
----
**安裝**:

>npm

	npm install vee-validate --save

>CDN

	<!-- jsdelivr cdn -->
	<script src="https://cdn.jsdelivr.net/npm/vee-validate@latest/dist/vee-validate.js"></script>
	<!-- unpkg -->
	<script src="https://unpkg.com/vee-validate@latest"></script>

**套用**:

>所有規則套用中文訊息

	import { ValidationProvider, ValidationObserver, extend } from 'vee-validate'
	import * as rules from 'vee-validate/dist/rules'
	import tw from 'vee-validate/dist/locale/zh_TW'

	for (let rule in rules) {
  	  extend(rule, {
        ...rules[rule], // add the rule
        message: tw.messages[rule] // 把 message 加進去並中文化
      })
    }

    extend('telRegExp', {
  	  validate: value => {
      const reg = /^09\d{8}$/
      return reg.test(value)
      },
      message: '手機號碼 格式錯誤'
    }) // 自訂手機號碼規則

    Vue.component('ValidationProvider', ValidationProvider)
    Vue.component('ValidationObserver', ValidationObserver)

>使用 ValidationProvider 包裝 inputs 

	<validation-provider rules="required" v-slot="{ errors }">
  		<input v-model="value" name="myinput" type="text" />
  		<span>{{ errors[0] }}</span>
	</validation-provider>

# 使用驗證
---

**內建規則**

    "alpha": "{_field_} 須以英文組成",
    "alpha_dash": "{_field_} 須以英數、斜線及底線組成",
    "alpha_num": "{_field_} 須以英數組成",
    "alpha_spaces": "{_field_} 須以英文及空格組成",
    "between": "{_field_} 須介於 {min} 至 {max}之間",
    "confirmed": " {_field_} 不一致",
    "digits": "{_field_} 須為 {length} 位數字",
    "dimensions": "{_field_} 圖片尺寸不正確。須為 {width} x {height} 像素",
    "email": "{_field_} 須為有效的電子信箱",
    "excluded": "{_field_} 的選項無效",
    "ext": "{_field_} 須為有效的檔案",
    "image": "{_field_} 須為圖片",
    "oneOf": "{_field_} 的選項無效",
    "integer": "{_field_} 須為整數",
    "length": "{_field_} 的長度須為 {length}",
    "max": "{_field_} 不能大於 {length} 個字元",
    "max_value": "{_field_} 不得大於 {max}",
    "mimes": "{_field_} 須為有效的檔案類型",
    "min": "{_field_} 不能小於 {length} 個字元",
    "min_value": "{_field_} 不得小於 {min}",
    "numeric": "{_field_} 須為數字",
    "regex": "{_field_} 的格式錯誤",
    "required": "{_field_} 為必填",
    "required_if": "{_field_} 為必填",
    "size": "{_field_} 的檔案須小於 {size}KB"

**用法**

>在 ValidationProvider 中添加 rules 屬性後面添加驗證規則，v-slot會把結果傳出來 [關於 Scoped Slot Data](https://logaretm.github.io/vee-validate/guide/validation-provider.html#scoped-slot-data)

	<ValidationProvider rules="required|email" v-slot="{ errors }"></ValidationProvider>

>有些規則直接套用屬姓名就好，有些是後面需要帶參數的

	<ValidationProvider rules="required|min:3" v-slot="{ errors }"></ValidationProvider>
	<ValidationProvider rules="required|between:3,10" v-slot="{ errors }"></ValidationProvider>
	<ValidationProvider rules="required|oneOf:coffee,tea,beer,milk" v-slot="{ errors }"></ValidationProvider>

# ValidationProvider 與 ValidationObserver
---

**ValidationProvider**:

>比較針對 每一個單一 input 去做驗證

**ValidationObserver**:

>對整張表單，檢查每一項input 是否都通過驗證

範例:

	<template>
	  <ValidationObserver ref="observer" v-slot="{ invalid }" tag="form" @submit.prevent="submit()">
	    <TextFieldWithValidation rules="required" v-model="first" />

	    <TextFieldWithValidation rules="required" v-model="second" />

	    <button :disabled="invalid">Submit</button>
	  </ValidationObserver>
	</template>

	<script>
	export default {
	  methods: {
	    async submit() {
	      const isValid = await this.$refs.observer.validate();
	      if (!isValid) {
	        // ABORT!!
	      }

	      // 🐿 ship it
	    }
	  }
	};
	</script>


# 參考連結
---
* [VeeValidate官網](https://logaretm.github.io/vee-validate/guide/)
* [カバの樹](https://www.kabanoki.net/4955/)