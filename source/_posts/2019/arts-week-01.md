---
title: ARTS-week-01
date: 2019-04-06 00:00
commends: true
tags:
  - ARTS
categories:
  - ARTS
---

目的是培养主动思考，坚持学习，主动输出的习惯<br /> Algorithm 每周至少做一个 leetcode 的算法题，进行编程训练和学习<br />Review 每周阅读并点评至少一篇英文技术文章，学习英文；如果你的英文不行，你基本上无缘技术高手<br /> Tip 总结归纳工作中的知识点。学习至少一个技术技巧<br />Share 分享一篇有观点有思考的文章，培养你的影响力<br /><br />
<a name="Algorithm"></a>
## Algorithm
[LeetCode 01 tow sum](https://leetcode.com/problems/two-sum/)

题目：<br />Given an array of integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have exactly one solution, and you may not use the same element twice.<br />Example
```
Given nums = [2, 7, 11, 15], target = 9
Because nums[0] + nums[1] = 2 + 7 = 9, return [0, 1].
```

<!--more-->

参考：
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  for (let i = 0; i < nums.length - 1; ++i) {
    for(let j = i + 1; j < nums.length ; ++j) {
      if (nums[i] + nums[j] === target) {
        return [i, j]
      }
    }
  }
};

twoSum([2,7,11,15], 9)
```

**补充**<br />上面是我给出的解决方案，凭直觉给出的暴力(brute force)解决方案，时间复杂度是Ο(n)。查看[solution](https://leetcode.com/problems/two-sum/solution/)可知，以时间复杂度为参考，借助hash table的实现是更优解，时间复杂度为O(n)。<br />JavaScript的Object对象时基于hash table设计的，因此可以很遍历的基于Object对象实现快速的查询操作。

```javascript
// hash table
var twoSum = function(nums, target) {
 const map = {
 //	num: indexInNums
 }
   
 for (let i = 0; i < nums.length; ++i) {   
   const matchIndex = map[target - nums[i]]
   if (matchIndex >= 0) {
      return [i, matchIndex]
   }
   map[nums[i]] = i
 }
}

twoSum([2,7,11,15], 9)
```

两种实现方式的对比截图<br />
![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1554626569571-57aadb4a-4ab6-48bf-aa35-6f54e7d2ced6.png#align=left&display=inline&height=562&name=image.png&originHeight=1124&originWidth=1316&size=589162&status=done&width=658)<br />基于测试结果可知
1. 基于hash table运行时间消耗是两重for 循环的一半
1. hash table的实现其空间复杂度是O(n)，本题内存占用为35.5M，内存占用超过77%的算法实现，因此还有优化空间。

### 参考
[js对象与hash table](https://segmentfault.com/a/1190000007692754)

<a name="Review"></a>
## Review
[what is a URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL#Absolute_URLs_vs_relative_URLs)
> 什么是相对url和绝对url。之前还有一点的误解。

以当前域名是 `http://twofeet.cn/blog` 为前提开始下面的内容。<br /> `/about.html` 属于绝对url，真实的地址是 `http://twofeet.cn/about.html` ， `about.html` 是相对url，真实地址是 `http://twofeet.cn/blog/about.html` 

<a name="Tips"></a>
## Tips
<a name="14bb08dc"></a>
### Vue相关
布尔型prop可以采用简写的形式。如属性 `modal`  控制弹窗是否有遮罩层，可以有下面两种写法。

```html
// 简洁版
<dialog modal></dialog>

// 多写几个字
<dialog :modal="true">
```
对于自定义的组件，使用简洁版prop写法时，定义组件时需要声明[prop的类型](https://vuejs.org/v2/guide/components-props.html#Prop-Validation)和初始值，否则不生效。如
```javascript
....
props: {
	modal: {
  	  type: Boolean,
      default: true  
  }
}
....
```

HTML 元素 `input` type 为 `checkbox` 或者 `radio` 时，其 `checked` 属性同样支持两种写法。

```html
<input type="radio" checked="checked"><input>
或者
<input type="radio" checked><input>
```


<a name="0686f383"></a>
### nuxt axios module
> axios的proxy和baseURL不能共存，proxy为false时，设置的baseURL才生效


下面说的都是引子，和axios无关。[axios-module点击这里](https://axios.nuxtjs.org/options#baseurl)<br />先从当前部署方式说起<br />业务中客户端请求后端服务统一通过kong代理转发，由kong代理到各个微服务。web应用同样通过kong代理到目标地址。客户端通过kong代理地址访问web应用，确保了后端API服务和应用在同一个源，解决了跨域问题。

改造前物理部署图<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1554471440901-2a61dfc7-52be-4b2e-a7bf-79d5cd0718fa.png#align=left&display=inline&height=776&name=image.png&originHeight=1552&originWidth=2248&size=563380&status=done&width=1124)<br />网关kong和后端services都部署在外网服务器，用户通过kong代理访问cdn上的web应用和后端services。如用户登录接口访问为 `http://www.kong-server.com/user-center/user/login` 其中 `user-center` 就是用户中心的上下文，在kong新建route，配置paths项为 `/user-center` 。这样所有来自客户端的请求路径匹配 `/user-center` 的请求都会被空转发到对应upstream的target地址(即后端服务地址)  `http://www.target-service.com/user-center/user/login ` 

后面考虑安全原因，后端服务部署在内网服务器，服务统一经过跳机与kong通信。更改后的部署方式如下

改造后物理部署图<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/163562/1554471096941-f2a7509c-4c10-40e5-bcac-6c8353092696.png#align=left&display=inline&height=831&name=image.png&originHeight=1662&originWidth=1756&size=628931&status=done&width=878)

由于kong新部署在一台新的主机，又不想给每一个service配置route。因此新配置一个route的paths为 /`collect-service` , `strip` 项设置为 `true` , 这样所有来自客户端的请求中匹配`/collect-service`的请求都将被转发到目标服务器中。同样已用户登录接口为例：<br />客户端请求为. `http://www.kong-server.com/`**`collect-service/user-center`**`/user/login `  ,注意请求中多了 `collect-service` 。这个请求经过代理后将被转发到 `http://www.target-service.com/user-center/user/login`<br /> 

改造前后对客户端访问是无差别的，为了少写几个配置，所以增加了一个统一的上下文 `/collect-service` 访问kong匹配拦截。统一修改请求路径的上下文在axios中可以设置 `[baseURL](https://axios.nuxtjs.org/options#baseurl)=http://www.kong-server.com/collect-service ` , 但是设置后baseURL仍然是'/'。为什么设置不成功呢。于是找到了[nuxt-axios-module](https://axios.nuxtjs.org/options#baseurl), 重新读了一遍。阅读文档可知，baseURL的默认值为 `http://[HOST]:[PORT][PREFIX]`  **在proxy为false时baseURL才生效**。好了问题出在proxy上，原来是代码判断出了问题。饶了一圈，答案很简单--多读文档。
<a name="d41d8cd9"></a>
## 
<a name="Share"></a>
## Share
文章出处 
1. [the journey to devops.pdf](https://blog.scottlogic.com/bjedrzejewski/assets/white-papers/the-journey-to-devops.pdf)
1. [the-journey-to-devops.html](https://blog.scottlogic.com/2019/03/25/the-journey-to-devops.html)

目前在公司的产品部做DevOps平台，参考"the journey to devops"文中提到的评估devops流程成熟度中提到的五点，对比现在有devops平台，更能认识到目前产品的不成熟。

评估devops成熟度的五点：
1. 开发和运维为了产品质量，携手共进
1. 成熟的发布体系: CI/CD、频繁的迭代、多环境等
1. 有效的测试：自动化测试、阶段测试、监控等
1. 一切自动化的文化形成
1. 不变的是变化，拥抱变化。给成员学习时间、花时间不断改进工作流

文中提到的如何开始devops的第五点中提到文化的改变——关注敏捷开发流程、快速且高效的反馈机制建设、持续学习与自动化文化建设。团队目前也有一些实践。如清晰的定义工作“完成”的概念，开发联调完不教完成，经过测试在测试环境测试通过才叫完成；分支协作开发和code review；尽早的涉及业务，在mock阶段保证mock数据的真实性；项目初期尽早的简历持续集成环境，保证后面的功能开发能够持续集成等。对于自动化测试和监控是目前欠缺的，但也在开发计划中。
