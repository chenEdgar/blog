---
title: ARTS-week-03
date: 2019-04-22 00:00
commends: true
tags:
  - ARTS
categories:
  - ARTS
---
目的是培养主动思考，坚持学习，主动输出的习惯<br /> Algorithm 每周至少做一个 leetcode 的算法题，进行编程训练和学习<br />Review 每周阅读并点评至少一篇英文技术文章，学习英文；如果你的英文不行，你基本上无缘技术高手<br /> Tip 总结归纳工作中的知识点。学习至少一个技术技巧<br />Share 分享一篇有观点有思考的文章，培养你的影响力<br /><br />
<a name="Algorithm"></a>
## Algorithm
leetcode 3 [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string, find the length of the **longest substring** without repeating characters.<br />**Example 1:**
```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**
```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, 
             "pwke" is a subsequence and not a substring.
```
<!--more-->

**解决方法**<br />解决思路：<br />将字符串转为数组，遍历整个数组，将所有不重复的字符串片段存储在bridge中，在循环中找到字符串长度最大的字符串片段。返回
```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  // 不是字符串 返回0
  if (!s) return 0
  
  let maxStrIndex = 0,
      minStrIndex = 0,
      loopLimit = 1,
      bridge = {}
  
  const arr = s.split('')
  for (let i = 0, len = arr.length; i < len; i++) {
   
    // 至少循环一次
    for(let j = minStrIndex; j < loopLimit + i; j++) {
      
      // 没有存储则初始化字符串存储的[]
      if(!bridge[j]) {
        bridge[j]  = []  
      }
      
      // 当前字符串不在[bridge[j]]中，则追加
      if(bridge[j].indexOf(arr[i]) === -1) {
        bridge[j].push(arr[i])
      } else {
        // 当前字符与bridge中的字符重复时，将更新循环的下限
        // 跳出当次循环
        minStrIndex = j
        continue
      }
      
      // 对比找到当前bridge中字符长度最长的索引 
      if (bridge[j].length > bridge[maxStrIndex].length) {
        maxStrIndex = j
      }
    }
  }

// 最后一个测试用例，如果将下面的打印出来，会报错 Output Limit Exceeded
// console.log('没有重复字符的字符串的对象', bridge)
// console.log('最长字符串在bridge中的索引', maxStrIndex)
// console.log('最长字符串为', bridge[maxStrIndex])
// console.log('最长字符串', bridge[maxStrIndex])
  
  return bridge[maxStrIndex].length
};

// 测试失败用例
//" " 期望输出1
```

遇到的报错信息<br />[Output Limit Exceeded](http://poj.org/faq.htm)  引用原文的解释
> Your program has produced too much output. Currently the limit is twice the size of the file containing the expected output. The most common cause of this result is that your programs falls into an infinite loop containing some output operations.

输出的内容超过了期望输出内容的大小两倍的限制

**算法分析**<br />测试用例执行完的时间和执行结果如下，执行时间慢于80%的JavaScript提交，内存占用高于95%的JavaScript提交。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1555838658636-ac6e15bf-d0c3-412b-950d-d2122d774ce4.png#align=left&display=inline&height=515&name=image.png&originHeight=1124&originWidth=1366&size=551822&status=done&width=626)<br />时间复杂度：第一层循环为O(n) ，第二层循环为O(n) ，总的时间复杂度为O(n)<br />空间复杂度：需要一个中间变量bridge存储值，复杂度为O(n)

**更优解法**<br />solution提供的更优解是采用**滑动窗口算法，**滑动窗口算法解决的是在某些场景下将嵌套的循环改为单层循环，从而减少时间复杂度。

先提供参考<br />**参考**<br />[Window Sliding Technique](https://www.geeksforgeeks.org/window-sliding-technique/)<br />[Sliding Window algorithm template to solve all the Leetcode substring search problem.](https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/sliding-window-algorithm-template-to-solve-all-the-leetcode-substring-search-problem)<br />[什么是「滑动窗口算法」（sliding window algorithm），有哪些应用场景？](https://www.zhihu.com/question/314669016)
<a name="d41d8cd9"></a>
## 
<a name="Review"></a>
## Review
专题 持续交付([continuous delivery](https://www.atlassian.com/continuous-delivery))

CI和CD的区别是什么，持续交付的价值是什么。这个专题解决了我这两个疑问。

1、CI和CD的区别是什么<br />CI，continuous integration，持续集成即开发者将功能分支持续的合并到主分支，测试用例通过并保证主分支功能正常，解决了将一大坨代码合并到主分支可能带来的功能故障问题、定位问题的复杂度问题。

CD 分为持续交付(continuous delivery) 和 持续部署(continuous deployment)。<br />持续交付建立在CI的基础上，持续交付解决了交付的难题——每个交付的特性通过自动化测试用例后，可以在任何时候发布新特性，保证了客户可以快速的体验新特性。<br />持续部署在持续交付的基础上进一步做到自动化，发布完全自动化，不需要人为点击"发布"按钮。这样没有发布日一说，开发并经过流水线的测试后就会部署到线上，可以更快的让用户体验到的功能特性，接受反馈。同时解放了开发人员，让开发更关注与软件开发。

> 从现有的知识看持续部署，这更像是一个软件交付的"桃花源"。在具备一条完整CI流水线前提下，考虑商业目的，产品的发布都不可能做到持续部署。有个案例补充就很棒了。


2、持续交付的价值是什么<br />第一点CI与CD的区别有提到一些价值。<br />下面列举一些微观价值<br />1、需求设计转换为线上产品所需的时间 - 敏捷开发，快速试错<br />2、终端用户遇到的bug数量 - 功能的健壮与用户体验<br />3、用户对新功能粘度 - (开发的功能是用户需要的，还是拍脑袋想出来的)<br />4、新功能交付的频率 - 敏捷开发

商业价值<br />持续交付能快速的响应市场变化；能够提高团队生产力——繁重的测试、部署工作都自动化了；功能频发可预测的交付给用户，快速的满足用户的需求，在用户获取与留存的马拉松中有节奏的已不变应万变。


其他参考<br />[持续集成理论和实践的新进展](http://insights.thoughtworkers.org/continuous-integration/) - ThoughtWorks这家咨询公司的文章可以多读读
<a name="Tip"></a>
## Tip
分享两个本周学到的item2的使用<br />1、如何让iterm2 在任何界面呼入呼出？<br />效果如下图<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1555866761214-83312c8b-61ea-45e7-adab-b447fc85f20c.png#align=left&display=inline&height=283&name=image.png&originHeight=1216&originWidth=2870&size=472373&status=done&width=667)<br />配置参考[知乎的回答]()

2、item2中快速的在单词中切换<br />效果如下图<br />![Large GIF (970x430).gif](https://cdn.nlark.com/yuque/0/2019/gif/163562/1555867190545-194fa948-cd22-4572-8c55-ee306e4661fe.gif#align=left&display=inline&height=331&name=Large%20GIF%20%28970x430%29.gif&originHeight=430&originWidth=970&size=841875&status=done&width=746)<br />单词间切换的快捷键设置依据mac本身的快捷键设置 `option + <-` 向左跳一个单词， `option + ->` 向右跳一个单词。 item这个两个组合键有其他的功用，但目前貌似没有用到。

目前只给hotkey window 设置了这个快捷键。设置方式<br />item2 -> preferences -> profiles。 <br />
![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1555867850391-aa9bfcaf-529d-4383-b96c-6e1f0ea427f6.png#align=left&display=inline&height=355&name=image.png&originHeight=1270&originWidth=2668&size=928941&status=done&width=746)

双击修改界面<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1555867917361-7817710b-f7e1-497d-99e5-0c89ef89beb4.png#align=left&display=inline&height=445&name=image.png&originHeight=1136&originWidth=1904&size=746488&status=done&width=746)
<a name="d41d8cd9-1"></a>
## 
<a name="Share"></a>
## Share
> 做一个主动输出价值的人，而不是被安排的人

上周和成员聊过后，产生了本周分享的这个观点。做一个主动输出价值的人，而不是被安排的人。<br />其实，公司的每个人都应该问自己一个问题，如果1年2年或者5年后，从公司离职了，会获得一份自己期望薪资的工作吗？或者离职后是否具备了你想要的能力，让你有机会开始新的旅程。如果没想，现在开始好好想想。如果你有答案了，恭喜你，你领先了多数人。

我眼中的主动输出价值的人是这样的：<br />主动的提供帮助；发现问题的同时提供解决方案；喜欢有价值的交流而不是八卦、抱怨；有责任心等。<br />被安排的人是这样的：<br />消极的接受；工作上完成分配的任务就好；即使不喜欢被安排又不去争取主动。

上面是个人的一些观点，不喜欢的忽略就好。

