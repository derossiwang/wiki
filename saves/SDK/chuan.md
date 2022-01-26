---
title: 最长串
description: 
published: true
date: 2022-01-26T01:24:03.771Z
tags: 
editor: markdown
dateCreated: 2022-01-26T01:24:01.832Z
---

描述：这是一个类似染色但并非染色的问题。
给定一个二维数组表示一个岛的地图，其中不同的地势高度分别用不同的数字表示。
求出在同一高度下，最长的路是多长。

---

例如：给定4*4的二位数组
```
0,1,2,1
0,0,1,2
1,0,0,1
0,0,0,0
```
其中最长的路是：
![在这里插入图片描述](https://img-blog.csdnimg.cn/6bfbb560dc14416bac910946424f6ad2.png)

---

```js
let n = 10;
let m = 10;
//定义一个二维数组
let map = [];
let book = [];
for (let i = 0; i < n; i++) {
    map.push([]);
    book.push([]);
}


for (let i = 0; i < n; i++) {
    for (let j = 0; j < m; j++) {
        map[i][j] = Math.floor(Math.random() * 4);
        book[i][j] = 0;
    }
}

let len = [];
let longest = [];
let dir = [[1, 0], [-1, 0], [0, 1], [0, -1]];
for (let i = 0; i < n; i++) {
    for (let j = 0; j < m; j++) {
        dfs(i, j);
    }
}


function dfs(x, y) {
    if (x >= n || y >= m || x < 0 || y < 0) return;
    book[x][y] = 1;
    len.push([x, y]);
    if (len.length > longest.length) {
        for (let i = 0; i < len.length; i++)
            longest[i] = len[i];
    }
    for (let i = 0; i < 4; i++) {
        let tox = x + dir[i][0]
        let toy = y + dir[i][1]
        if (tox >= n || toy >= m || tox < 0 || toy < 0) continue;
        if (map[tox][toy] == map[x][y] && book[tox][toy] != 1) {
            dfs(tox, toy);
            book[tox][toy] = 0;
        }
    }
    len.pop();
}

console.log(map, longest);
```

运行结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/675e7661b9b348a48d92a83adcb82134.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ04tRHVzdA==,size_20,color_FFFFFF,t_70,g_se,x_16)
