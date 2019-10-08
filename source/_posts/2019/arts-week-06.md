---
title: ARTS-week-06
date: 2019-05-03 00:00
commends: true
tags:
  - ARTS
categories:
  - ARTS
---
目的是培养主动思考，坚持学习，主动输出的习惯<br /> Algorithm 每周至少做一个 leetcode 的算法题，进行编程训练和学习<br />Review 每周阅读并点评至少一篇英文技术文章，学习英文；如果你的英文不行，你基本上无缘技术高手<br /> Tip 总结归纳工作中的知识点。学习至少一个技术技巧<br />Share 分享一篇有观点有思考的文章，培养你的影响力

<a name="Algorithm"></a>
## Algorithm
[LeetCode 6 ZigZag conversion](https://leetcode.com/problems/zigzag-conversion/)

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`<br />Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**
```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

背景知识：<br />[zigzag](https://zh.wikipedia.org/wiki/%E9%8B%B8%E9%BD%92%E5%BD%A2) 锯齿形，形状似锯子的形状![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1557676616338-985422c0-b16d-4237-a139-9f271d085bf0.png#align=left&display=inline&height=89&name=image.png&originHeight=178&originWidth=1106&size=52406&status=done&width=553)

(图片来自[维基百科](https://zh.wikipedia.org/wiki/%E9%8B%B8%E9%BD%92%E5%BD%A2))<br />**分析**

1. 通过看图可以看出形状是有规律的
2. 通过加example 1 的输入转换为锯齿形 结合 example 2 易得出他们的关系 2(numRows - 1) * circle = strLen - remainder。 其中circle是循环的次数，remainder是循环外的字符数。

 <br />想用二维数组实现，后面卡住了。

看了solution后得到启示。<br />一行一行遍历，以numRows作为第一层循环，circle作为第二层循环的步长
```javascript
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
  if (numRows === 1) return s
  
  let retStr = '',
      strLen = s.length,
      circleLen = 2 * numRows - 2
  
  for (let i = 0; i < numRows; i++) {
    for (let j = 0; j < strLen; ) {
      retStr = retStr.concat(s.substr(i + j, 1))
      
      // 去除第一行和最后一行；
      if (i !== 0 && i !== numRows - 1 && j + circleLen - i < strLen) {
         retStr = retStr.concat(s.substr(j + circleLen - i, 1))
      }
      j += circleLen
    }
  }
  
  return retStr
};
```

运行结果<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1557681384209-44dbc0d1-a660-4ca6-9370-a3c3eb384b92.png#align=left&display=inline&height=411&name=image.png&originHeight=822&originWidth=1388&size=378193&status=done&width=694)


<a name="Review"></a>
## Review
1  [A Gentle Introduction to tmux](https://hackernoon.com/a-gentle-introduction-to-tmux-8d784c404340)  tmux一款终端复用工具, 详见tip

<a name="Tip"></a>
## Tip
工具一：<br />一个终端复用的工具 [tmux](https://github.com/tmux/tmux/wiki)，他主要的功能包括分屏、保护现场和会话共享等。<br />1 分屏效果<br />可以在一个tab上查看所有任务相关的进程<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1557670876103-b65e7801-6663-424f-99fd-364bf36d8989.png#align=left&display=inline&height=452&name=image.png&originHeight=904&originWidth=1140&size=264161&status=done&width=570)

2 保护现场<br />终端命令关闭时会话会终端，或者通过ssh登录服务器想新开一个窗口执行其它操作时还得重新操作。tmux的保护现场功能完美解决这个问题

[![Video MP4 (680x488).mp4 (1.79MB)](https://cdn.nlark.com/yuque/0/2019/jpeg/163562/1557672212995-58c6d6e4-1080-45dd-b87c-dc0474a9c5e0.jpeg?x-oss-process=image/resize,h_450)](https://www.yuque.com/deepexi-company/arts/sngit5?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22Video+MP4+%28680x488%29.mp4%22%2C%22size%22%3A1874034%2C%22percent%22%3A0%2C%22id%22%3A%22mRWRQ%22%2C%22videoId%22%3A%22fe18208fd9754f55bbec45d0660593da%22%2C%22coverUrl%22%3A%22https%3A%2F%2Fcdn.nlark.com%2Fyuque%2F0%2F2019%2Fjpeg%2F163562%2F1557672212995-58c6d6e4-1080-45dd-b87c-dc0474a9c5e0.jpeg%22%2C%22aliyunVideoSrc%22%3Anull%2C%22taobaoVideoId%22%3A%22225990119973%22%2C%22uploaderId%22%3A163562%2C%22authKey%22%3A%22YXBwX2tleT04MDAwMDAwMTImYXV0aF9pbmZvPXsidGltZXN0YW1wRW5jcnlwdGVkIjoiMjlhNTQ0ZjZlYjA1MDViMDIwNmYyMzI1ZDY2OGIxOTIifSZkdXJhdGlvbj0mdGltZXN0YW1wPTE1NTc2ODI3NDY%3D%22%2C%22docUrl%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fdeepexi-company%2Farts%2Fsngit5%22%2C%22card%22%3A%22video%22%7D#mRWRQ)
3 会话共享<br />[共享会话](https://louiszhai.github.io/2017/09/30/tmux/#%E4%BC%9A%E8%AF%9D%E5%85%B1%E4%BA%AB)给了链接，没有去实现

更多关于tmux

1. [tmux实用入门](https://hackernoon.com/a-gentle-introduction-to-tmux-8d784c404340)
1. [tmux中文手册](https://hackernoon.com/a-gentle-introduction-to-tmux-8d784c404340)

工具二：<br />[feedly](https://feedly.com/i/welcome), 定制化你的阅读内容<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1557673204050-7e876454-5009-447b-9f73-fa4f7ef06de2.png#align=left&display=inline&height=767&name=image.png&originHeight=1534&originWidth=2534&size=933523&status=done&width=1267)

<a name="Share"></a>
## Share
[W3C新技术汇总：Web技术的现在与未来](https://mp.weixin.qq.com/s?__biz=MzUxMzcxMzE5Ng==&mid=2247491186&idx=1&sn=235f648fccaf0e2769fa5044418a8b4d&chksm=f951ab31ce262227a867bdaeaa9d967f2be0272108ef51cfdd9fd7c5118dbcb7201b56ded254&mpshare=1&scene=2&srcid=05090EIW4SEAUAWYJrESqW58&from=timeline&as)<br />文中提到小城程序引用如下
>  Web 中文兴趣组与小程序研讨会
> 在本地社区方面，W3C 正在尝试使用熟识的本地语言（中文）讨论技术想法和独特的 Web 需求，目前中文兴趣组策划的小程序 / 快应用研讨会将于近日举行，其主题包括：
> - 小程序和快应用解决了哪些 Web 还没有解决的问题，如何解决的<br />
> - 小程序和快应用存在的问题，包括开发中遇到的问题和使用中遇到的问题<br />
> - 不同小程序 / 快应用 API 之间的差异、跨平台开发框架以及下一代移动 Web 应用的标准化方向<br />
> - 新场景的 API (AR and AI)<br />

这里的主题很有意思。涵盖了过去、现在和将来。如果能站在过去(小程序还没出现之前)预见小程序的出现，便能获取小程序带来的红利。站在现在思考过去(小程序多样化)能够促进人去思考，同时也能去发现未解决的问题。
