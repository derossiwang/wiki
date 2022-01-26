---
title: QQ
description: 手Q SDK
published: true
date: 2022-01-25T08:57:10.146Z
tags: 
editor: markdown
dateCreated: 2022-01-25T08:57:08.092Z
---

# 手Q广告

该组件实现了QQ的4种广告展示(横幅、插屏、视屏、格子)

:::tip 组件路径

CommonSDK/platform/qq/AdsFunc.js

:::

:::tip 数据优先级

服务器数据 > 缓存 > 本地存储

:::

## 通用广告API

<font size=4>**init()**</font>

初始化QQ游戏广告设置。该方法会初始化4种广告，对banner广告添加从服务器拉取的轮转时间，最后添加切换前后台时的插屏显示监听

</br>

## 横幅广告API

### 索引

- `initBannerNode` 初始化横幅广告节点
- `showBanner` 展示一条横幅广告
- `hideBanner` 隐藏一条横幅广告

<font size=4>**initBannerNode(node)**</font>

初始化横幅广告节点

<font color=gray>**参数列表**</font>

- `node` [cc.Node][cc.Node] 横幅广告插入的父节点

</br>

<font size=4>**showBanner()**</font>

展示横幅广告

</br>

<font size=4>**hideBanner()**</font>

隐藏当前展示的横幅广告

</br>

## 插屏广告API

### 索引

- `showInsert` 展示一条插屏广告

<font size=4>**showInsert(opts)**</font>

展示一条插屏广告

<font color=gray>**参数列表**</font>

- **`opts`** [Object][Object]
  - `key` [String][String] 广告key
  - `scene` [Array][Array] 展示场景

## 视屏广告API

### 索引

- `showVideo` 展示一条视屏广告
- `videoStatus` 视屏广告状态

<font size=4>**showVideo(opt)**</font>

展示一条视屏广告，默认切换间隔不得小于1s。

<font color=gray>**参数列表**</font>

- **`opt`** [Object][Object]
  - `isToast` [Boolean(可选)][Boolean]是否为toast广告
  - `key` [String(可选)][String] 视屏广告key 
  - `name` [String(可选)][String] 视屏广告名称
  - `success` [Function][Function] 成功回调
  - `fail`  [Function][Function] 失败回调
  - `error`  [Function][Function] 报错回调

<font size=4>**videoStatus**</font>

视屏广告状态

## 格子广告API

### 索引

- `createCustomGridAd` 创建并显示最大支持个数的格子广告
- `hideCustomGridAd` 隐藏并销毁显示的格子广告

<font size=4>**createCustomGridAd(opt)**</font>

根据屏幕方向尽可能多地创建并显示格子广告(横向1-4，纵向1-5)

<font color=gray>**参数列表**</font>

- **`opt`** [Object][Object]
  - `node` [cc.Node][cc.Node] 广告所在节点
  - `size` [Number(可选)][Number] 格子广告单元大小
  - `orientation` [String(可选)][String] 屏幕方向

<font size=4>**hideCustomGridAd()**</font>

隐藏并销毁显示的格子广告



[cc.Node]: https://docs.cocos.com/creator/2.3/api/zh/classes/Node.html?h=node
[Array]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
[Function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function
[Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
[String]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[Boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/G

