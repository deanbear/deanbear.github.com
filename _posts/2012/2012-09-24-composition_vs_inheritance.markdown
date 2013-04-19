---
author: Bear
comments: true
date: 2012-09-24 22:32:32
layout: post
slug: composition_vs_inheritance
title: 组合与继承:物尽其用，各取所需。
wordpress_id: 45
categories:
- 技术流/TechGangster
tags:
- Java
- OOP
- 组合与继承
---

    上两个星期团队对应用做了一个重构改造，主要是增加代码复用性以及减少重复编码成本。理所当然的，OOP听起来就是为这个目的而产生的。OOP的全称有几个人拼的齐?科普一把:Object Oriented Programming.在大陆翻译是面向对象程序设计，在台湾翻译成物件导向程式设计。不知道是不是耳濡目染听多了，我认为这个词大陆翻译的比较正。

这个改造不是我做的，在看改造完的代码的时候，虽然觉得写的都挺合情合理的，但总觉得很怪异，又不知道该怎么表达。某天晚饭吃火锅的时候，和其他人聊起来我的看法，老蒋直接抛给我一句:"你的意思就是组合比继承更适合"，虎躯一震的感觉马上出来了，只怪自己书读的不够说不出来这么抽象的语句。所以我的想法就是，虽然继承是OOP的精髓所在，但是，作为杀手锏，没有必要每次都出，组合反而更加灵活适用。

接着我就翻了翻 Thinking in Java ，找到了两处关于 composition(组合) vs. inheritance(继承) ，也算是比较权威的解释了，什么时候用组合什么时候用继承，心里有个数。内容如下。
<!-- more -->
**Part One**


> 

> 
> Choosing composition vs. inheritance
> 
> 
Both composition and inheritance allow you to place subobjects inside your new class (composition explicitly does this—with inheritance it’s implicit). You might wonder about the difference between the two, and when to choose one over the other.

Composition is generally used when you want the features of an existing class inside your new class, but not its interface. That is, you embed an object so that you can use it to implement features in your new class, but the user of your new class sees the interface you’ve defined for the new class rather than the interface from the embedded object. For this effect, you embed private objects of existing classes inside your new class.

Sometimes it makes sense to allow the class user to directly access the composition of your new class; that is, to make the member objects public. The member objects use implementation hiding themselves, so this is a safe thing to do. When the user knows you’re assembling a bunch of parts, it makes the interface easier to understand. A car object is a good example:

Because in this case the composition of a car is part of the analysis of the problem (and not simply part of the underlying design), making the members public assists the client programmer’s understanding of how to use the class and requires less code complexity for the creator of the class. However, keep in mind that this is a special case, and that in general you should make fields private.

When you inherit, you take an existing class and make a special version of it. In general, this means that you’re taking a general-purpose class and specializing it for a particular need. With a little thought, you’ll see that it would make no sense to compose a car using a vehicle object—a car doesn’t contain a vehicle, it is a vehicle. The is-a relationship is expressed with inheritance, and the has-a relationship is expressed with composition.


上面一坨英文的中心思想就是:



	
  * 组合是一个显性的写法，你想要一个类的特性，就直接把它作为自己的类的成员对象。想让人访问则用public，否则用private或protected即可，非常灵活方便类与类之间没有羁绊(这是高端词汇)

	
  * 继承则是一个隐性的写法，往往是在通用的基类之上添加或修改一些属性或方法，成为一个特例。

	
  * 组合表达"含有某功能"，而继承表达"是某物的一种版本"


区别听起来组合的思想比组合高级一些，更抽象而且有哲学范儿。而组合则是很随意很灵活的一个过程性思维，但特管用。具体什么时候用哪个，则认真读一下Part two。

**Part Two**


> 

> 
> Composition vs. inheritance revisited
> 
> 
In object-oriented programming, the most likely way that you’ll create and use code is by simply packaging data and methods together into a class, and using objects of that class. You’ll also use existing classes to build new classes with composition. Less frequently, you’ll use inheritance. So although inheritance gets a lot of emphasis while learning OOP, it doesn’t mean that you should use it everywhere you possibly can. On the contrary, you should use it sparingly, only when it’s clear that inheritance is useful. One of the clearest ways to determine whether you should use composition or inheritance is to ask whether you’ll ever need to upcast from your new class to the base class. If you must upcast, then inheritance is necessary, but if you don’t need to upcast, then you should look closely at whether you need inheritance. The Polymorphism chapter provides one of the most compelling reasons for upcasting, but if you remember to ask “Do I need to upcast?” you’ll have a good tool for deciding between composition and inheritance.



这段我觉得写的特棒。虽然继承在面向对象语言中绝对是重中之重，考试必考。但这不代表你在任何时候任何场景都必须用它。比如说你有一个独门武功，你就不分场合不分对手的一直用，结果刚好某个对手就是你克星专拆你的绝招，那你死定了。所以说绝招不要随便放，得等到决定胜负一招定天下时用才能看出功夫的奥义。用的多不如用的少，用的少不如用的妙。所以当你要用继承关系时，你扪心自问一把:"我需要向上转型吗?"如果答案是肯定的，则大胆用着，如果发现其实这个类没有那么通用不会遇到要向上转型的情景，则尽量用组合吧。当然，话也不能太绝对，一切以场景为主见机行事见招拆招，肯定不会错。

最后重复本文最关键的一句话：**不必拘泥于组合方式还是继承方式，由这个类是否需要向上转型而定，就这么简单。**
