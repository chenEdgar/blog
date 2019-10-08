---
title: ARTS-week-05
date: 2019-05-05 00:00
commends: true
tags:
  - ARTS
categories:
  - ARTS
---
目的是培养主动思考，坚持学习，主动输出的习惯<br /> Algorithm 每周至少做一个 leetcode 的算法题，进行编程训练和学习<br />Review 每周阅读并点评至少一篇英文技术文章，学习英文；如果你的英文不行，你基本上无缘技术高手<br /> Tip 总结归纳工作中的知识点。学习至少一个技术技巧<br />Share 分享一篇有观点有思考的文章，培养你的影响力

<a name="Algorithm"></a>
## Algorithm
[LeetCode 05 Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)<br />Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

<!--more-->
**Example 1:**
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**
```
Input: "cbbd"
Output: "bb"
```

**brute force**<br />1 判断是否是回文<br />2 找到字符创s中的所有回文<br />3 找到回文字符串最长的那个
```javascript
function isPalindromic(s) {
  return s === s.split('').reverse().join('')
}

/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  let lp = ''
  if (!s) {
    return lp  
  }
  for(let i = 0; i < s.length; i++) {
    for (let j = 1; j < s.length + 1; j++) {
      let strChunk = s.substr(i, j)
      if (isPalindromic(strChunk)) {
        lp = strChunk.length > lp.length ? strChunk : lp
      }
    }
  }
  
  return lp
  
};
```
当执行如下用例。测试执行时间为6s左右s="civilwartestingwhetherthatnaptionoranynartionsoconceivedandsodedicatedcanlongendureWeareqmetonagreatbattlefiemldoftzhatwarWehavecometodedicpateaportionofthatfieldasafinalrestingplaceforthosewhoheregavetheirlivesthatthatnationmightliveItisaltogetherfangandproperthatweshoulddothisButinalargersensewecannotdedicatewecannotconsecratewecannothallowthisgroundThebravelmenlivinganddeadwhostruggledherehaveconsecrateditfaraboveourpoorponwertoaddordetractTgheworldadswfilllittlenotlenorlongrememberwhatwesayherebutitcanneverforgetwhattheydidhereItisforusthelivingrathertobededicatedheretotheulnfinishedworkwhichtheywhofoughtherehavethusfarsonoblyadvancedItisratherforustobeherededicatedtothegreattdafskremainingbeforeusthatfromthesehonoreddeadwetakeincreaseddevotiontothatcauseforwhichtheygavethelastpfullmeasureofdevotionthatweherehighlyresolvethatthesedeadshallnothavediedinvainthatthisnationunsderGodshallhaveanewbirthoffreedomandthatgovernmentofthepeoplebythepeopleforthepeopleshallnotperishfromtheearth"<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1556900629047-183e6e8d-b6f4-479f-be68-c105e53f255a.png#align=left&display=inline&height=275&name=image.png&originHeight=550&originWidth=1410&size=107590&status=done&width=705)

LeetCode执行结果Time Limit Exceeded。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1556900669759-fb013809-f28f-41a8-baf0-0ec84462fe10.png#align=left&display=inline&height=283&name=image.png&originHeight=566&originWidth=1300&size=75329&status=done&width=650)<br />结论是暴力解法直观却未必行的通。


<a name="Review"></a>
## Review
1 [The Best Questions to Ask at Your Performance Review](https://medium.com/s/story/the-best-questions-to-ask-at-your-performance-review-5aba3fb86528)<br />[扩展] [马蜂窝张矗：我对技术团队绩效考核管理的几点思考](https://juejin.im/post/5caaaf72f265da24c3126460)<br />本篇文章的目的在于帮助员工更好的**准备**绩效考核评审。避免在雇主问及"你还有什么想问的吗"时面面相觑，无话可说。<br />绩效评审的目的对雇主来说是知道你在做什么；对于雇员来说，是让雇主知道你现在的工作、接下来努力的方向、以及和雇主的关系(_我的理解是让雇主知道你希望被怎么管理_)。如何在绩效评审中实现这些信息互通呢，首先需要雇员问自己几个问题，明确自己的立场：公司真正重视的是什么？自身的角色如何适应公司的业务？员工的核心价值是什么(what are the core values of the people work there)？我所做的工作如何影响公司目标的实现。

在明确立场后，就可以提出自己的问题了。下面是几个参考。<br />1 我的表现与您的期望匹配吗?<br />目的在与明确评价的标准

2 您还有其他评价标准评估我做的事吗<br />有些绩效考核可能是用像时间管理、生产率等比较模糊值去衡量，但你的雇主可能有你没注意到的具体的考核点。如你回复邮件的用语比较粗鲁，这也是减分的点。

3 您认为我的优势是什么？我的弱势是什么<br />平和的问雇主你有哪些需要提高点，你的雇主会很乐意给你提供帮助的。这些需要提高的点就是你接下来努力提升的方向

4 进阶到下一个层次我需要掌握什么技能或特质<br />不进则退。有目标才能提升

5 公司对员工的职业发展有什么预算吗<br />利用公司的资源提升自己是一个好的选择

6 我们来谈谈薪资吧<br />你认为你值得这份工资，就提出来吧

<a name="Tip"></a>
## Tip
1 计算一段程序的时间开销<br />[console.time(label)](https://developer.mozilla.org/en-US/docs/Web/API/Console/time) 与 console.timeEnd(label)结合。timeEnd的label与time的label是同一个，用于标识这个timer的开始于结束。效果见**Algorithm的执行代码**

<a name="Share"></a>
## Share
调整算法学习策略<br />先前的算法学习是基于LeetCode，做题时遇到不会的就去查知识点、看算法导论学习相应的算法和数据结构知识。这样容易陷入一个陷阱——可能做了十几二十题都是同一个数据结构或者同一类算法可以解决的。这样一会造成长时间停滞不前，二呢在做算法题时没有一个视野在有限的知识里选择合适的算法与数据结构。因此五一开始调整了学习策略。<br />新的学习方式以极客时间王铮的[数据结构与算法之美]()课程为主，辅以《数据结构与算法JavaScript描述》《算法导论》两本书，以及每周的LeetCode算法题。新的学习方式兼顾了知识结构的完整性，保证了知识广度的扩展；同时兼顾了一定量的练习。

两篇笔记：[栈](https://www.yuque.com/suihan-mfioc/backlog/pir2ag) 和 [链表](https://www.yuque.com/suihan-mfioc/backlog/pir2ag)。笔记内容主要是记录知识要点、算法应用场景和一些思考题
