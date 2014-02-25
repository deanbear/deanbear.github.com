---
layout: post
title: Head First Design Pattern讀書筆記
date: 2014-02-25 12:10:33
categories:
- 技术流/techgangster
tags:
- 設計模式
- 筆記
---
好久沒有發技術類的文章了，最近看的技術書是 [Head First Design Patterns](http://book.douban.com/subject/1400656/)，通俗易懂，適合Java以及廣大面向對象程序的程序員觀看學習。由於習慣裝逼看英文原版，所以Gang Of Four的那本Design Patterns實在是消化不了，所以就選了這本讀。這個是讀書筆記，順便給博客除除草，嚴肅得告訴大家，這個還是以技術爲基調的博客，是技術類博客！(無自信聲音漸弱...)

設計模式拖到現在才好好的學了一遍，這個東西重要當然是重要的，但是幹看一點用都沒有，其實這個和吉他和絃譜一樣的，首先你得知道和絃的名字，並且大概熟悉這個和絃是怎麼按的，下次再遇到的時候，就會心一笑，ㄟ這個不就是那個和絃嘛，更厲害一點的時候就是自己寫曲子的時候可以編入這個和絃。所以這本書就是告訴你偉大的前輩們觀察總結出來的設計模式名冊以及介紹，方便後人交流和使用。

設計模式本身就是針對面向對象而言的，一种设计模式一定是遵循了这些原则，才会变得通用。所以這本書總結了「OO Principles」，非常棒，摘抄一遍加深印象。

1. 封裝變量。(Encapsulate what varies.)
2. 組合優於繼承。(Favor composition over inheritance.)
3. 面向接口編程，而非實現。(Program to interfaces, not implementations.)
4. 爲交互對象間松耦合的設計而奮鬥不止。(Strive for loosely coupled designs between objects that interact.)
5. 類爲擴展而開，爲修改而關。(Classes should be open for extension but closed for modification.)
6. 依賴抽象類，而非具體類。(Depend on abstractions. Do not depend on concrete classes.)
7. 類儘量少與其他類接觸，保留少量就好。(Only talk to your friends.)
8. 高級組件調用低級組件。(Don't call us, we'll call you.)
9. 一個類只要負責做好一件事就可以了。(A class should have only one reason to change.)

接下來正式說說書中重點介紹的幾款常用模式。

**策略模式(the Strategy Pattern)**

將變量或者需要變化的方法封裝好，符合需求的能動態替換對應變量或方法，而不影響到其他部分。

簡單的用代碼來描述就是這樣：

	class Bear {
		@setter
		Role role;
		
		public void show() {
			role.play();
		}
		
		public static void(String[] args) {
			Bear i = new Bear();
			Guitarist guitarist = new Guitarist()
			i.setRole(guitarist);
			i.show();
			//我變，我變，我變變變。
			Programmer programmer = new Programmer();
			i.setRole(programmer);
			i.show();
		}
	}
	
	class Guitarist implements Role {
		@Override
		public void play() {
			System.out.println("Hey, Let's rock!");
		}
	}
	
	class Programmer implements Role {
		@Override
		public void play() {
			System.out.println("Damn, who wanna play this!");
		}
	}
	
就是說`role`這個是很容易變的，動態的改變它就能`show`出不一樣的`I`。這就是策略模式，整合了OO原則的前三條有沒有？自己好好感受一下。

**觀察者模式(the Observer Pattern)**

這個用的很廣泛。發佈——訂閱(Publisher-Subscriber)，這麼做的好處就是松耦合，可以增加多個訂閱者而不影響到發佈者，也可以修改發佈者的邏輯但是不需改變訂閱者。這就是OO原則第四條的體現。java中有內建的Observable類(供發佈者繼承)以及Observer接口(供訂閱者實現)，就是很標準的觀察者模式。

**装修模式(the Decorator Pattern)**

裝修模式的代碼作品是java.io，一層包裹著一層，還有就是http相關的wrapper，包裝器，和裝修模式是一樣的意思。

	class Bear {
		public void saySomething() {
			System.out.println("I'm bear.");
		}
	}
	
	class GuitaristBear extends Bear {
		@Override
		public void saySomething() {
			super.saySomething();
			System.out.println("And I'm a guitarist.");
		}
	}

裝修模式的中心思想就是OO原則的第5條，類不要更改，但是可以擴展，這樣的好處在於在不修改原類的基礎上，新需求新業務可以以擴展繼承來滿足，同時對老應用的其他引用模塊不會造成影響。

**工廠模式(the Factory Pattern)**

工廠模式首先將創建對象以及對象選擇封裝進了一個類，體現了OO原則第一點。然後工廠模式又分爲兩種，一種叫抽象工廠模式(abstract factory)，另外一種叫工廠方法模式(factory method)。兩者很相似，都是基於OO原則第五點創造的，工廠方法是由業務對象繼承父類的抽象方法，直接在本身實現子類方法的特定業務。而抽象工廠是定義好接口，有多個實現類，實現類作爲傳參，進入業務對象，所以抽象工廠本身就有工廠方法的模式，作爲傳參時也屬於策略模式。

工廠方法：

	abstract class RoleFactory {
		abstract void createRole();
	}
	
	class Bear extends RoleFactory {
		@Override
		public void createRole() {
			//Do sth. only I can do.
		}
		
		public void whoAmI() {
			//Different class invokes different createRole()
			createRole();
		}
	}

抽象工廠方法：
	
	//prepare I.
	public interface RoleFactory {
		void createCharater();
		void createSkill();
		void createAppearance();
	}
	
	//prepare II.
	public class GuitaristRoleFactory implements RoleFactory {
		@Override
		public void createCharater() {
			System.out.println("Humor, and outgoing.");
		}
		
		@Override
		public void createSkill() {
			System.out.println("Outstanding barrel guitarist.");
		}
		
		@Override
		public void createAppearance() {
			System.out.println("Ugly but gentle.");
		}
	}
	
	//Ready Go
	public class Bear {
		RoleFactory concreteRoleFactory;
		public Bear(RoleFactory concreteRoleFactory) {
			this.concreteRoleFactory = concreteRoleFactory;
		}
		public void whoAmI() {
			concreteRoleFactory.createCharater();
			concreteRoleFactory.createSkill();
			concreteRoleFactory.createAppearance();
		}
	}
	
工廠方法就像內嵌的裝備，而抽象工廠則更像可插拔外置裝備。但它們的核心思想都是反轉依賴(Dependency Inversion, DI)，針對抽象而非具象類編程。

**單例模式(the Singleton Pattern)**

單例的要點就是，保證類只有一個實例，並且提供一個全局統一(唯一)的訪問入口。書中提供了一個最好的雙重檢查鎖(double-checked locking)，面試的時候，你只要把這個扔出去回答singleton的問題，無敵了。

	public class Singleton {
		private volatile static Singleton uniqueInstance;
		private Singleton() {
		public static Singleton getInstance() {
			if (uniqueInstance == null) {				synchronized (Singleton.class) { 
					if (uniqueInstance == null) {
						uniqueInstance = new Singleton(); 
					}				}
			}
			return uniqueInstance;		}	
	}
	
**命令模式(the Command Pattern)**

我覺得這個模式很平常，不知道爲什麼要單獨拿出來講。Command對象裏藏着一個業務對象，command只暴露幾個基本的方法，比如execute()，在這幾個方法中實現業務邏輯。Client調用方就可以調用execute()實現業務請求了。多線程Thread就是這個模式。"run, Forrest run!"

**適配器模式(the Adapter Pattern)**

更好理解了，和名字一樣。港行的mbp插頭很大無法插入大陸的插頭，所以我會買一個適配器。還有就是國內和國外數碼產品偶爾電壓還不一樣，需要穩壓的適配器。B要適配A，則創造一個C實現A的接口，同時C中包含B，C的方法裏寫B的邏輯。

**外觀模式(the Facade Pattern)**

這個也很好理解，是OO原則第七點的體現。負責的底層調用就讓他們留在底層吧。我們只管調用封裝完美的API就好。

**模板模式(the Template Pattern)**

這個是我最早知道的模式了，因爲以前用C++的時候，STL就是各種算法的庫，只要投入參數，就可以得到結果，當時就覺得這樣的模式真太好用了。

父類定義好算法的流程以及框架，子類可以覆蓋父類中的某些流程，實現個性化的算法，也可以加上一些Hook，來做自己在大流程之下還需要做的事情，但大框架是不變的。所以OO原則第八條就是說的這個。

	public class playFolks {
		public void playASong() {
			playGuitar();
			sing();
			hook();
		}
		public void playGuitar() {
			System.out.println("by Martin");
		}
		public void sing() {
			System.out.println("NA-NA-NA-NA");
		}
		public void hook() {
		}
	}
	
	public class bearPlayGuitar extends playGuitar {
		@Override
		public void sing() {
			System.out.println("Guitar solo, keep silence");
		}
		@Override
		public void hook() {
			System.out.println("Thanks everyone!");
		}
	}
	
**迭代器模式(the Iterator Pattern)**

迭代器也不玄乎，實現迭代器接口，適配底層不同的容器，對上層保持一致透明。迭代功能單獨拆出來，不與容器混在一起，就是OO原則第9條所說的。

**複合模式(the Composite Pattern)**

將不同容器整合成樹狀結構，再與迭代器結合，對每一個子結構都能做到對上層用戶透明讀取。這裏的代碼是這本書裏寫的最妙的一段代碼了。反正用到的一定會寫，不會寫的一定不會用到。就這麼草草了事吧。

**狀態模式(the State Pattern)**

雖然說了很多，但是我只記得一句話了，狀態模式和策略模式是雙胞胎。。。

**代理模式(the Proxy Pattern)**

經常跟遠程調用扯在一起。你認爲是本地調用，但其實背後是遠程調用。同時代理也能做一些事先過濾。


好了，就這麼羅列幾條吧。最關鍵的點，設計模式只是把日常碰到的一些涉及起了名字，方便程序員之間的交流的，生搬硬套是沒有用的，也就是說讀了這本書只是告訴你命名，至於會不會用，還得看你自己了。


