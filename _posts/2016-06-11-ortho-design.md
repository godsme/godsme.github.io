---
layout: post
title: "变化驱动：正交设计"
date:   2016-06-10 19:39:14
time: 2016年06月10日 星期六
categories: software design
location: 深圳,中国
---

一个出发点
===






两个问题
===

一旦人们开始进行进行模块化拆分，就必须解决如下两个问题:


<img src="https://godsme.github.io/img/module.png" width="300px" />

三方关系
===







可问题在于,如何才能做到?
---


￼所谓**内聚性**，关注的是一个软件单位内部的关联紧密程度。因而高内聚追求的是*关联紧密的事物应该被放在一起*，并且*只有关联紧密的事物才应该被放在一起*。简单说，就是Unix的设计哲学：

>Do One Thing, Do It Well。


2. 而当我们定义模块之间的API时，需要让双方尽可能**低耦合**。





四个策略
===








但在另外一些场景下，我们则无法清晰的判定：一个模块是否真的包含多重变化原因，或多重职责。比如如下代码:

``` cpp
{
};

{
  {
    {
      { 
        SWAP(students[x], students[x-1]);
      } 
    }
}
```






<img src="https://godsme.github.io/img/dup3.png" width="300px" />


如果两个模块之间是**部分重复**的，则发出了一个重要的信号：这两个模块都至少存在两个变化原因,或两重职责。


<img src="https://godsme.github.io/img/dup4.png" width="300px" />


<img src="https://godsme.github.io/img/dup2.png" width="300px" />




### 策略二：分离不同的变化方向



```cpp
{
  {
    {
      {
  }
```


```cpp
{
  {
    {
      {
  }
```


<img src="https://godsme.github.io/img/change_direct.png" width="300px" />




另外，如果两个模块有**部分代码**是重复的，往往意味着**不同变化方向**。






<img src="https://godsme.github.io/img/couple.png" width="300px" />


* 首先，**客户**和**实现**模块的数量，会对耦合度产生重大的影响。它们数量越多，意味着 API 变更的成本越高，越需要花更大的精力来仔细斟酌。

而具体到策略**缩小依赖范围**，它强调:
2. API 也应该**高内聚**，而不应该强迫API的客户依赖它不需要的东西。

### 策略四：向着稳定的方向依赖










总结
---


由此得到了**两个问题**：模块划分必然要解决如何划分,以及模块间如何协作(API 定义)的问题。



我们已经在多个系统的设计和开发中，以这四个原则来驱动我们的软件设计，不仅让我们的系统在保持简单的同时，具备所有必要的灵活性。也让设计和开发活动变得高度有章可循，让团队生产率得以大幅提升。
