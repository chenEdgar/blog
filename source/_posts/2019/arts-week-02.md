---
title: ARTS-week-02
date: 2019-04-14 00:00
commends: true
tags:
  - ARTS
categories:
  - ARTS
---

目的是培养主动思考，坚持学习，主动输出的习惯<br /> Algorithm 每周至少做一个 leetcode 的算法题，进行编程训练和学习<br />Review 每周阅读并点评至少一篇英文技术文章，学习英文；如果你的英文不行，你基本上无缘技术高手<br /> Tip 总结归纳工作中的知识点。学习至少一个技术技巧<br />Share 分享一篇有观点有思考的文章，培养你的影响力<br /><br />
<a name="Algorithm"></a>
## Algorithm
[LeetCode 02 Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)<br />**题目**<br />You are given two** non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order **and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.<br /><br />You may assume the two numbers do not contain any leading zero, except the number 0 itself.<br />**Example**:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
<!--more-->
哈，算法与数据结构不分家。虽然是一道简单的题目，也花费了三个晚上的时间解决。<br />首次通过的解法：
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
function ListNode(val) {
   this.val = val;
   this.next = null;
}

/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
// 1. 返回值是链表, head 的val为l1.val + l2.val
// 2. 需要遍历两条链表， 终止遍历条件是l1 == null || l2 == null'
// 3. (l1.val + link2.val) >= 10，需要将向下移动一位

var addTwoNumbers = function(l1, l2) {
  let link1 = l1
  let link2 = l2
  let curNodeVal = 0
  let carry = 0
  let sumLinkList = null
  
  while(link1 !== null || link2 !== null) {
    if (link1 === null) {
      curNodeVal = link2.val + carry
    } else if (link2 === null) {
      curNodeVal = link1.val + carry
    } else {
      curNodeVal = link1.val + link2.val + carry
    }
    
    let newNodeVal = 0
    if (curNodeVal >= 10 ) {
      newNodeVal = curNodeVal % 10
      carry = 1
    } else {
      newNodeVal = curNodeVal
      carry = 0
    }

    if (sumLinkList) {
      let endNode = sumLinkList
      while (endNode.next !== null) {
        endNode = endNode.next
      }
      endNode.next = new ListNode(newNodeVal)
    
    } else {
      sumLinkList = new ListNode(newNodeVal)
    }
    
    link1 = link1 && link1.next
    link2 = link2 &&  link2.next
  }
  
  if (carry === 1) {
    let endNode = new ListNode(carry)
    if (sumLinkList.next) {
      let lastNode = sumLinkList
      while (lastNode.next) {        
        lastNode = lastNode.next
      }
      lastNode.next = endNode
    } else {
      // only one node
      sumLinkList.next = endNode
    }
  }
  
  return sumLinkList
}



```
循环套循环，结果可想而知。差！

测试结果<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1555002239240-1bbfbc54-13f3-467c-87c1-9976916bc900.png#align=left&display=inline&height=199&name=image.png&originHeight=398&originWidth=1308&size=162507&status=done&width=654)

做题的收获：<br />**链表**
1. 学习了链表，链表是比数组稍微复杂一点的数据结构。有单链表、双向链表、循环链表和双向循环链表这么几类
1. 链表暂用不连续的内存空间，数组则是占用连续的内存空间
1. 单单就插入和删除操作，链表的执行时间复杂度为O(1)。
1. 在指定在某个节点前插入一个节点，双向链表的效率更高，时间复杂度为O(1)，单链表是O(n)。但双链表占用更多的内存空间
1. 思想：以时间换空间，以空间换时间

** 其他**
1. 需要学习写伪代码，一种思维练习方式
1. 对算法的学习已练习为主，遇到不懂的看书、看专栏、看参考答案
1. 如何找到循环的终止条件，找退出的临界点

**疑问**<br />用链表实现加法运算的意义在哪，是否真实存在这种需求<br />**<br />**加餐**
1. 如何用链表实现LRU(least recently used 最近最少使用)缓存淘汰策略
1. 假设字符串通过单链表存储，如何判断该字符串是回文


<a name="Review"></a>
## Review
1、[What are Stack and Queue?](https://medium.com/javascript-in-plain-english/javascript-what-are-stack-and-queue-79df7af5a566)<br />文中用JavaScript语言基于数组(Array)和链表(linked list)分别实现了栈(stack)和队列(queue)，实现浅显易懂。<br />但是不明白的数组和栈、队列、链表的关系，按[队列、堆栈与数组、链表的关系与区分](https://www.cnblogs.com/zhishan/p/3207932.html)一文中所说，似乎明白了一点。
> 队列、栈是线性**数据结构**的典型代表，数组、链表是常用的两种**数据存储结构**；
> 队列和栈均可以用数组或链表的存储方式实现它的功能！



<a name="b2cba5b5"></a>
## Tip  
分享的是中后台管理项目单页应用中面包屑交互与开发中的一些坑。前端框架是nuxt.js。<br />面包屑设计的目的是帮助用户在网站中导航，让用户知道自己当前在哪，可以去哪里。一般分为[三类](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%8C%85%E5%B1%91%E5%AF%BC%E8%88%AA)：路径型，位置型，属性型。

项目中踩过的坑总结：
> 面包屑实现是维护一份属性json数据，通过遍历json匹配当前route的path，找到面包屑的路径

1、假设有一个应用列表(A) -> 应用详情(B) -> 更细粒度的详情(C)这么一个三层嵌套的页面场景。A跳转B，通过query传递AId，在B页面通过AId获取到详情；同理C通过query获取BId获取C页面渲染的数据。进入到C页面时，面包屑为**A > B > C**。当点击B返回C时，会发现AId丢失了。<br />2、假设常规路径面包屑为**A > B > C**，但需求希望在在A和B路径之间加一层**X**，x是动态生成的(有点类似属性型面包屑)。<br />3、侧边栏目录没有对应的页面，展示在路径型面包屑中，对应的面包屑节点不可点(因为是目录，点了没有地方跳转)。面包屑告诉我可以去哪里，去没有给我一条路。体验特别差。

解决方案<br />针对1：全局监听路由，维护更新path-query映射表似乎能解决。针对项目现有实现是针A->B改为从vuex总获取，因为末尾层级的页面的query传参不受影响。改动最小。

针对2：在保证原面包屑逻辑通用性条件下，将通过path获得的面包屑路径初始化为链表，针对这条链表进行节点的动态插入。因为实现原因，最终将动态节点从当前版本中去除。

针对3：应该重新思考业务模块组合，交互流程是否合适。

关于面包屑设计的一些个人看法：面包屑是一种辅助导航工具，可以让交互变得更友好。但应该仔细考虑是否需要面包屑。是不是因为设计上的疏忽，导致交互上的缺陷，需要用面包屑来救场。能不用面包屑就不用。


**参考**<br />1. [面包屑设计](https://cdc.tencent.com/2009/07/06/%E9%9D%A2%E5%8C%85%E5%B1%91%E8%AE%BE%E8%AE%A1/)
<a name="d41d8cd9"></a>
## 
<a name="Share"></a>
## Share
本周分享的是一部跑步主题的动漫——[强风吹拂](https://movie.douban.com/subject/30238385/)，讲述十名同住一室的大学生，在队长灰二策划下开始训练，到获得参加箱根驿传并取得第十名(下赛季种子选手名最低名次)成绩的过程。

我为什么跑步，在之前的一篇[跑步杂书说](https://www.jianshu.com/p/2c9782b85e66)有提到，为了更好的聆听自己的声音、帮助自己恢复、获得“撞墙”时生理与心理上的体验。一直认为跑步是一个人独处的好时机，不会有任何工作、生活压力困扰；可以感受自己的呼吸与心跳。平常路跑时可以感受迎面跑来的陌生人对自己说句加油的愉悦，比赛时赛道志愿者的加油呐喊与冲刺到终点时战胜自己的满足感等，所有的这些让我一直在跑。我的目标是UTMB。

通过强风吹拂这部动漫，让我看到了很多不曾看到、体会到的内容。<br />1、没有跑过接力赛，不能真的体会到接近虚脱的队友将接力棒交给自己那一刻的心情<br />2、没有一同训练经历，只能局限在自身的痛与乐，无法感受到共同进步、提高的乐趣<br />3、接力赛需要根据不同人的特点安排交接棒，有人定性好，抗干扰能力强；有人适合腿部任性好，适合上下坡路段；有人速度快，需要安排做突进选手<br />4、团队赛需要上帝视角，时刻关注比赛时间与目标的偏差，调整比赛的节奏；每一棒的选手都需要调整自己的状态，专注于比赛<br />5、“一个都不能少”是相信也是期许，如果打心底认同目标，自然会努力提升的——动漫中的王子是一个参考<br />6、真正的强大，所守护的都不是个人的东西，如火影中的羁绊、强风吹拂中的团队奋斗的目标

现在在补充一句我为什么跑步，为了感受那一份爱的纯粹。


