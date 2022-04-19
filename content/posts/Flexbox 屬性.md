---
author: "Nigel"
title: "Flexbox 屬性"
date: 2019-12-25T15:47:49+08:00
description: "css - Flexbox"
draft: false
tags: [
	"css3",
	"sass"
]
---
# display: flex

flex: 主要是 main axis 與 cross axis 構成

 main axis  > 左右向

 cross axis > 上下向

那麼有一些設定屬性，如下。

## flex-direction

> 設定主軸 (main axis) 的方向

	.container {
	  display: flex;
	  flex-direction: row; // 橫向
	  flex-direction: row-reverse; // 橫向，反序排列
	  flex-direction: column; // 主軸變直向
	  flex-direction: column-reverse; // 主軸變直向, 反序排列
	}

## justify-content

> 與主軸 (main axis) 的對齊方式

	.container {
	  display: flex;
	  justify-content: flex-start; // 靠左
	  justify-content: flex-end; // 靠右
	  justify-content: center; // 置中
	  justify-content: space-between; // 貼齊父容器，每個子元素的間格一致
	  justify-content: space-around; // 與父容器的間格為，每個元素間格的一半
	  justify-content: space-evenly; // 每個元素與父容器都是相同的間格
	}

## align-items

> 交叉軸 (cross axis) 的對齊方式

	.container {
	  display: flex;
	  align-items: flex-start; // 靠上
	  align-items: flex-end; // 靠下
	  align-items: stretch; // 填滿整個容器
	  align-items: baseline; // 依容器的基準線對齊
	  align-items: center; // 依容器的中線對齊
	}

**!!!注意!!!  align-items IE 只支援 11 (含)以上。**

## align-self

> 設定單一元素的對齊方式，會覆寫父層align-items的設定

	.container {
	  display: flex;
	  align-items: flex-end; //靠下
	  .item1 {
		align-self: flex-start; // 只有這個 item1 靠上
	  }
	}


---
# 參考資料
[Summer。桑莫。夏天 - 圖解 Flexbox 基本屬性](https://cythilya.github.io/2017/04/04/flexbox-basics/)