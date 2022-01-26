---
title: 华为
description: 华为SDK
published: true
date: 2022-01-25T09:02:16.459Z
tags: 
editor: markdown
dateCreated: 2022-01-25T09:02:14.345Z
---

# 广告

该组件实现了华为小游戏的4种广告展示(横幅、插屏、视屏、开屏)

:::tip 组件路径

CommonSDK/platform/huawei/AdsFunc.js

:::

:::tip 数据优先级

服务器数据 > 缓存 > 本地存储

:::

## API

### 索引

- `init` 拉取广告数据并初始化广告
- `initBannerNode` 初始化横幅广告节点
- `addBannerNativeRenderer` 添加横幅广告的原生渲染器
- `deleteBannerNativeRenderer` 删除一个横幅广告的原生渲染器
- `showBanner` 显示横幅广告
- `hideBanner` 隐藏横幅广告
- `addInsertNativeRenderer` 添加原生插屏广告的渲染器
- `deleteInsertNativeRenderer` 删除一个原生插屏广告的渲染器
- `showInsert` 展示插屏广告
- `setInsertAdVisible` 设置当前插屏广告的可见性
- `showVideo` 显示视屏广告
- `showOpenAd` 显示开屏广告
- `NativeAd` 原生广告类
- `openAd` 开屏广告实例
- `nativeAdBase` 原生广告加载类实例
- `bannerVerticalAlign` banner垂直对齐方式
- `bannerPriority` banner展示优先级
- `insertPriority` 插屏展示优先级
- `nativeBannerStyle` 原生banner样式
- `nativeInsertStyle` 原生插屏样式
- `videoStatus` 视屏广告状态

### 方法

<font size=4>**init()**</font>

从服务器拉取广告位数据，然后初始化横幅、插屏、视屏、开屏广告

</br>

<font size=4>**initBannerNode(node)**</font>

初始化横幅广告节点高度为父节点的包围盒高度

<font color=gray>**参数列表**</font>

- `node` [cc.Node][cc.Node] 横幅广告插入的父节点

</br>

<font size=4>**addBannerNativeRenderer(renderer)**</font>

向组件的的横幅广告原生渲染器数组中添加一个条目

<font color=gray>**参数列表**</font>

- `renderer` [NativeAdRenderer](/JSDoc/commonUtils/NativeAdRender#NativeAdRenderer)

<font color=gray>**返回值**</font>

- [Number][Number] 新添加的渲染器index

</br>

<font size=4>**deleteBannerNativeRenderer(index)**</font>

删除组件的横幅广告原生渲染器数组中的指定条目

<font color=gray>**参数列表**</font>

- `index` [Number][Number] 横幅广告原生渲染器数组index

</br>

<font size=4>**showBanner(opt)**</font>

显示横幅广告，该方法优先显示原生Banner(此时会隐藏sdk的banner)

<font color=gray>**参数列表**</font>

- `opt` [Object][Object]
  - `priority ` [String(可选)][String]  native | sdk 展示优先级
  - `verticalAlign` [String(可选)][String] top | center | bottom 垂直对齐方式
  - `nativeStyle` [Number(可选)][Number] 渲染方式(渲染器数组index)
  - `isNew` [Boolean(可选)][Boolean] 是否为新广告
  - `isForce` [Boolean(可选)][Boolean] 是否强制显示

</br>

<font size=4>**hideBanner()**</font>

隐藏当前显示的横幅广告

</br>

<font size=4>**addInsertNativeRenderer(renderer)**</font>

向组件的的插屏广告原生渲染器数组中添加一个条目

<font color=gray>**参数列表**</font>

- `renderer` [NativeAdRenderer](/JSDoc/commonUtils/NativeAdRender#NativeAdRenderer) 原生渲染器

<font color=gray>**返回值**</font>

- [Number][Number] 新添加的渲染器index

</br>

<font size=4>**deleteInsertNativeRenderer(index)**</font>

删除组件的插屏广告原生渲染器数组中的指定条目

<font color=gray>**参数列表**</font>

- `index` [Number][Number] 横幅广告原生渲染器数组index

</br>

<font size=4>**showInsert(opt)**</font>

展示插屏广告

<font color=gray>**参数列表**</font>

- **`opts`** [Object][Object]
  - `key` [String][String] 广告key
  - `scene` [Array][Array] 展示场景

:::warning 插屏默认不显示情况

1. 与上一次展示间隔时间不足30s
2. 非可展示场景
3. 已有插屏显示

:::

</br>

<font size=4>**setInsertAdVisible(b)**</font>

设置当前插屏广告的可见性

<font color=gray>**参数列表**</font>

- `b` [Boolean][Boolean] 插屏广告的可见性

</br>

<font size=4>**showVideo(opt)**</font>

展示视屏广告数组的一条广告

<font color=gray>**参数列表**</font>

- **`opt`** [Object][Object]
  - `isToast` [Boolean(可选)][Boolean]是否为toast广告
  - `key` [String(可选)][String] 视屏广告key 
  - `name` [String(可选)][String] 视屏广告名称
  - `success` [Function][Function] 成功回调
  - `fail`  [Function][Function] 失败回调
  - `error`  [Function][Function] 报错回调

</br>

<font size=4>**showOpenAd(opt)**</font>

展示开屏广告

<font color=gray>**参数列表**</font>

- **`opt`** [Object][Object]
  - `render` [NativeAdRenderer](/JSDoc/commonUtils/NativeAdRender#NativeAdRenderer) 原生渲染器
  - `fail` [Function(可选)][Function] 失败回调

### 类   -  NativeAd

<font size=4>**constructor(name, id)**</font>

构造函数

<font color=gray>**参数列表**</font>

- **`name`** [String][String] 广告名
- `id` [Number][Number] 广告ID

</br>

<font size=4>**show(opt)**</font>

显示原生广告

<font color=gray>**参数列表**</font>

- **`opt`** [any][any] 广告参数

</br>

<font size=4>**reportShow(statLabel)**</font>

上报原生广告展示事件

<font color=gray>**参数列表**</font>

- **`statLabel`** [String][String] 统计时间名

</br>

<font size=4>**reportClick(statLabel)**</font>

上报原生广告点击事件

<font color=gray>**参数列表**</font>

- **`statLabel`** [String][String] 统计时间名

</br>

<font size=4>**hide()**</font>

隐藏原生广告

</br>

<font size=4>**setRendering(target)**</font>

设置原生广告渲染器

<font color=gray>**参数列表**</font>

- **`target`** [NativeAdRenderer](/JSDoc/commonUtils/NativeAdRender#NativeAdRenderer) 原生渲染器

</br>

<font size=4>**log(s)**</font>

打印日志

<font color=gray>**参数列表**</font>

- **`s`** [String][String] 日志信息

</br>

### 类   -  NativeOpenAd

继承[NativeAd](#类-nativead)，为原生开屏广告类

</br>

<font size=4>**show(fail)**</font>

显示原生开屏广告

<font color=gray>**参数列表**</font>

- **`fail`** [Function][Function] 失败回调

</br>

<font size=4>**reportShow()**</font>

上报原生开屏广告展示事件

</br>

<font size=4>**reportClick()**</font>

上报原生开屏广告点击事件

</br>

<font size=4>**_showRender()**</font>

??????????????

</br>

### 属性

<font size=4>**openAd**</font>

[NativeOpenAd](#类-nativeopenad) 原生开屏广告实例

<font size=4>**nativeAdBase**</font>

[nativeAdBase](#) 原生广告加载类实例

<font size=4>**bannerVerticalAlign**</font>

[String][String] top | center | bottom   banner垂直对齐方式

<font size=4>**bannerPriority**</font>

[String][String] banner展示优先级(native优先于sdk)

<font size=4>**insertPriority**</font>

[String][String] 插屏展示优先级

<font size=4>**nativeBannerStyle**</font>

[Number][Number] 原生banner样式。1代表老样式，2代表新样式

<font size=4>**nativeInsertStyle**</font>

[Number][Number] 原生插屏样式。1代表老样式，2代表新样式

<font size=4>**videoStatus**</font>

[Number][Number] 视屏广告状态。0代表隐藏，1代表显示



[cc.Node]: https://docs.cocos.com/creator/2.3/api/zh/classes/Node.html?h=node
[Array]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
[Function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function
[Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
[String]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[Boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/G
[Number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[any]: https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html#any