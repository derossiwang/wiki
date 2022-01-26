---
title: 微信
description: 微信SDK
published: true
date: 2022-01-25T08:55:26.801Z
tags: 
editor: markdown
dateCreated: 2022-01-25T08:55:24.645Z
---

# 微信广告

该组件实现了微信的3种广告展示(横幅、插屏、视屏)

:::tip 组件路径

CommonSDK/platform/weixin/AdsFunc.js

:::

:::tip 数据优先级

服务器数据 > 缓存 > 本地存储

:::

## 通用广告API

<font size=4>**init()**</font>

初始化微信游戏广告设置, 不需要手动调用。

</br>

## 横幅广告API

### 索引

- `initBannerNode` 初始化横幅广告节点
- `showBanner` 展示一条横幅广告
- `hideBanner` 隐藏一条横幅广告
- `bannerVerticalAlign` 横幅广告垂直对齐方式

</br>

<font size=4>**initBannerNode(node)**</font>

初始化横幅广告节点高度为父节点的包围盒高度

<font color=gray>**参数列表**</font>

- `node` [cc.Node][cc.Node] 横幅广告插入的父节点

</br>

<font size=4>**showBanner(opt)**</font>

展示ADConfig中的banner广告，如有多个ID，则会显示第一个成功加载的。如提供了`isNew`属性，则会强制拉取新Banner并展示第一个拉取成功的。

<font color=gray>**参数列表**</font>

- **`opt`** [Object][Object]
  - `isNew` [Boolean(可选)][Boolean] 是否为新广告
  - `verticalAlign` [String(可选)][String] 垂直对齐方式

::: tip 无法展示特定banner

新SDK**无法**像原来那样通过传入key和pos属性来显示特定的banner。方法会从头遍历ADConfig的bannerId数组，然后显示第一个成功的banner。

:::

::: tip banner轮转

如需要banner自动轮转，请在ADConfig中配置`bannerAdRotate`属性。如配置为true则轮转时间为默认的90s，否则请配置数字

```json
"bannerAdRotate": "true" // 90s后切界面时轮转
```

```json
"bannerAdRotate": "30" // 30s后切界面时轮转
```

:::

</br>

<font size=4>**hideBanner()**</font>

隐藏当前展示的横幅广告

</br>

<font size=4>**使用示例**</font>

```typescript {4}
// 首先定位banner节点才能正常显示
DBT.AdsFunc.initBannerNode(this.bannerNode);
if (DBT.CCGlobal.platform === DBT.CCConst.PLATFORM.WEIXIN) {
    DBT.AdsFunc.showBanner();
}
setTimeout(() => {
    DBT.AdsFunc.hideBanner();
}, 500)
```



## 视屏广告API

### 索引

- `showVideo` 展示一条视屏广告

<font size=4>**showVideo(opt)**</font>

展示视屏广告数组中填充率最高的广告

<font color=gray>**参数列表**</font>

- **`opt`** [Object][Object]
  - `isToast` [Boolean(可选)][Boolean]是否可toast提示出错提示
  - `key` [String(可选)][String] 视屏广告key 
  - `name` [String(可选)][String] 视屏广告名称(用于统计)
  - `success` [Function][Function] 成功回调
  - `fail`  [Function][Function] 失败(玩家手动关闭了视屏)回调
  - `error`  [Function][Function] 报错(无网或其他异常状态)回调

::: tip 流程改变

新SDK**无需**先`createVideoAd`再`loadVideoAd`传入回调. 视屏广告会在游戏加载时自动初始化，业务层仅需调用`showVideo`展示即可.

:::

::: tip 自动统计

方法内部已实现视屏广告在不同状态下的自动统计，无需像旧SDK那样通过`loadVideoAd`传入回调进行统计，回调执行业务层逻辑即可。

:::

::: tip 出错回调

**error回调**：组件会在视屏加载错误时会执行传入的error回调，并传入一个Object类型的参数。业务层需要根据传参的code属性判断出错的类型，并执行提示或跳转分享。

:::

#### 使用示例

```typescript
// game.ts
private watchVideo(e, tag) {
    ...
    DBT.AdsFunc.showVideo({
        isToast: true,
        key: "shuzihuarongdao",
	    name: "multiple",
        success: () =>{
            this.giveReward();
        },
        fail: () =>{...},
        error: () => {
            DBT.Share.shareGameMsg({
                key: "NDGTHRD",
                success: () => {this.giveReward()},
                fail:() => {...}
            })
        }
    })
}
```

</br>

## 插屏广告API

### 索引

- `showInsert` 展示一条插屏广告
- `setInsertAdVisible` 设置当前插屏广告的可见性

</br>

<font size=4>**showInsert(opts)**</font>

在检查插屏可否展示后，展示插屏广告数组中填充率最高的广告

<font color=gray>**参数列表**</font>

- **`opts`** [Object][Object]
  - `key` [String][String] 广告key
  - `scene` [Array][Array] 展示场景

:::warning 插屏默认不展示情况

1. 默认插屏广告在前15s无法展示
2. 与上一次展示间隔时间(30s)不足，不能展示
3. 非可展示情况下不能展示
4. 有广告/视频处于播放状态,不能展示

:::

</br>

<font size=4>**setInsertAdVisible(b)**</font>

设置当前插屏广告的可见性

<font color=gray>**参数列表**</font>

- `b` [Boolean][Boolean] 插屏广告的可见性

</br>



[cc.Node]: https://docs.cocos.com/creator/2.3/api/zh/classes/Node.html?h=node
[Array]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
[Function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function
[Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
[String]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[Boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean

