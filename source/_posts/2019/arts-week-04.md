---
title: ARTS-week-04
date: 2019-04-29 00:00
commends: true
tags:
  - ARTS
categories:
  - ARTS
---
目的是培养主动思考，坚持学习，主动输出的习惯<br /> Algorithm 每周至少做一个 leetcode 的算法题，进行编程训练和学习<br />Review 每周阅读并点评至少一篇英文技术文章，学习英文；如果你的英文不行，你基本上无缘技术高手<br /> Tip 总结归纳工作中的知识点。学习至少一个技术技巧<br />Share 分享一篇有观点有思考的文章，培养你的影响力

<a name="Algorithm"></a>
## Algorithm
[LeetCode04 Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.<br />Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).<br />You may assume **nums1** and **nums2** cannot be both empty.

**Example 1:**
nums1 = [1, 3]nums2 = [2]The median is 2.0

**Example 2:**
> nums1 = [1, 2]
nums2 = [3, 4]The median is (2 + 3)/2 = 2.5

what, the overall run time complexity should be O(m+n). 好吧，我先补补算法分析再来做。暴力解法似乎行不通了。

<!--more-->

了解了[复杂度](https://www.yuque.com/suihan-mfioc/ldnedr/ns6uhp), 了解了基本的排序实现，最终在一周结束前用快排实现了结果。但复杂度上没有达到要求。看solution，使用的是[二分搜索算法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E7%B4%A2%E7%AE%97%E6%B3%95)实现。

```javascript
function quickSort(list) {
    if (list.length == 0) { return [] }
    let lesser = [],
        greater = [],
        privot = list[0];

    list.slice(1).forEach(it => {
       it < privot ? lesser.push(it) : greater.push(it)
     })
  
    return quickSort(lesser).concat(privot, quickSort(greater))
}

/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
  let newNums = nums1.concat(nums2);
  
  newNums = quickSort(newNums)
  let newNumsLen = newNums.length,
      isEvent = newNumsLen % 2 === 0,
      median = 0
  
  if (isEvent) {
    median = (newNums[newNumsLen / 2 - 1] + newNums[newNumsLen / 2]) / 2
  } else {
    median = newNums[Math.floor(newNumsLen / 2)]
  }
  return median
};
```

算法分析<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1556465402483-f6d86aaa-f475-4038-9e13-62fe59142e84.png#align=left&display=inline&height=620&name=image.png&originHeight=1240&originWidth=1334&size=505708&status=done&width=667)

参考维基百科<br />[快速排序](https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)<br />[二分搜索算法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E7%B4%A2%E7%AE%97%E6%B3%95)

<a name="wbaFM"></a>
## Review
[TDD Changed My Life](https://medium.com/javascript-scene/tdd-changed-my-life-5af0ce099f80)
> [TDD](https://zh.wikipedia.org/wiki/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91)， test-driven development，测试驱动开发，是一种编程方法论。其目的是取得快速反馈并使用“illustrate the main line”方法来构建程序——维基百科

作者用TDD带来的几点好处

1. 提到代码测试率，从而减少40%-80%的线上bug
1. 改了代码不用担心影响其他逻辑
  1. 接手别人的项目或者维护一个老旧的项目的时，往往担心该一行代码引发雪崩。如果有单元测试和功能测试罩着则可以免去后顾之忧
3. 节省开发者的时间
  1. 较少维护成本：代码开时间占软件开发的20-30%, 软件开发完成后很大一部分都在代码维护和功能迭代上面。随着代码几经转手或者开发时间久远，对定位和修复bug会带来很高的成本。而这些成本可以通过单元测试和功能测试减少。
  1. 快速反馈，快速定位问题
4. 想的更多了。组件、模块等如何更后效的解耦和组合，功能如何更易测试
4. 提升团队效率。TDD改变了以往流水线似的开发流程——功能开发、测试、有bug、回去完善代码、测试、又有bug...TDD让团队对代码的变动更有信心。运行出错的地方会定位到具体原因，一切都是可预知的。

两年前Neo和我提到TDD，当时也没怎么在意。再说前端项目追求块，TDD在开发前期需要花费大量的时间写测试用例。投入和产出似乎不成比例。接触过的开发知道的也只有后端核桃会写贯彻TDD这套。在前端实践中，更多的是开发后功能通过冒烟用例，更多的还在人力测试阶段。TDD还没有很好的实践。



<a name="Tip"></a>
## Tip

1. chrome快速切换页签

`command + 数字1-9` 可以快速切换到对应的页签，并且 `command + 9` 必定是定位在最后一个页签。为了快速的切换到目标页签，建议同一个窗口打开4-5个页签。多则乱。

2. <br />

分享一款vscode 插件[vscode-gitlens](https://github.com/eamodio/vscode-gitlens)。当前主要用通途在git 历史文件的查看看上，它提供了文件级、行级查看，多维度查询git commit记录以及对比分析等功能。下过如下。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1556473488692-4e4faaa0-7e5a-469a-96c0-4132ca51ee9d.png#align=left&display=inline&height=894&name=image.png&originHeight=1788&originWidth=2866&size=1633220&status=done&width=1433)

旁白：作为重度webstorm用户的我，在做临时性工作时，打开vscode永远是第一选择。快才是王道。

<a name="Share"></a>
## Share
> 我所在团队主要负责公司DevOps平台的建设。“协作流程落实计划”是一份分阶段落实团队协作规范的计划，最终目的是打造敏捷、高效的团队，形成一切自动化的团队文化。

本周分享的内容是基于上周写“协作流程落实计划”的一些感想。
<a name="VAW1X"></a>
### 感想一 计划的可执行性

1. 如何保证计划是可执行的
  1. 将计划划分为几个阶段，每个阶段设置具体关注的目标；
  1. 明确达成这个目标什么角色需要在何时怎么做某件事，并设置完成这件事的验收标准
  1. 找到利益相关方，就计划达成一致
2. 跟进反馈
  1. 验收设计的检查点
  1. 根据实际情况，修正计划。符合团队的才是最好的
3. 总结改进
  1. 阶段日期截止时，总结计划实施的情况
4. 其他
  1. 写可执行的任务之类，个人感觉是采用动宾结构能出效果

附上[协作流程落实计划](https://www.yuque.com/docs/share/7f2ee7b1-651e-4851-8a17-968d3010adb4)，有不同的想法和建议可以一起交流。

<a name="BcMnT"></a>
### 感想二 概设阶段前端做什么
首先明白软件设计采用自顶向下的设计模式，先有总体设计，才能做局部设计。概要设计就是一份设计蓝图，他关注需求的功能描述、数据库的数据关系描述等。一般有架构师进行设计。

那么，概设阶段前端能做什么。

1. 理解需求背景
1. 理解专业词汇、能用白话说清楚
1. 已有业界方案。试用同类型的产品、去体验功能和交互
1. 结合原型窜起功能闭环、梳理数据走向
1. 理解业务的价值、能给用户带来什么样的价值

后话：公司的概设规范分类在后端目录，看过之后有了感想二的疑问。后面还需要去实践。


