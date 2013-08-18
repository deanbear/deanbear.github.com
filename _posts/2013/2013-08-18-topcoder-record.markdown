---
layout: post
title: TopCoder竞赛笔记
date: 2013-08-18 17:11:59
categories:
- 技术流/techgangster 
tags:
- TopCoder
- Programming
- algorithm
---
讀書的時候，在NIT埋頭搞了一年多的ACM，後面轉學了，到ZJUT的時候又稍微玩了個把月拿了個校一等獎就去實習了，後面的兩年就沒再接觸過編程競賽了。今年搬家和新室友住一起，其中一個是ACMer，參加過WorldFinal，工作之後還有在堅持玩競賽。所以我這把年紀才開始玩TopCoder就是由他帶起的。

讀書的時候也有聽說TopCoder，並且伴着許多傳說，比如“XXX在上面贏了XX萬美刀的獎金”，“XXX憑着TopCoder的成績拿了多少多少萬年薪”之類的。當然，每個行業都有這樣的天才人物。我這種小脆皮根本和這樣的傳說搭不上邊，當然沒有啥好說的。但既然上了這條賊船，讓自己變的更強大也是理所應當的。這樣也表明自己弱雖弱，但有一顆上進的心嘛。並且做做編程算法是肯定有好處的，因爲編程本身就是另外一種思考方式。

TopCoder的賽制啊判分標準之類的我還不熟，待以後玩利落了再來八一八。現在一個月2-3次的比賽，一场2小时左右(SRM,Single Round Match)，頻率和时间還是很适合大部分工作了的程序员的。我現在還在Division 2，也就是菜鳥的範疇中，努力升級至Div1中> <

我在Topcoder上寫過的代碼都會託管在github上，[點擊這](https://github.com/deanbear/TopCoder)。並且在這篇文章會定期更新代碼思路。

Get fun from programming. May the force be with you.

***

###SRM588 2013/08/12

房間裏只有壹人解出兩題。我只做出壹題。略難，加上手太生不夠麻利。卡在第二題，對我來說第三題其實更容易得手。

- KeyDungeonDiv2: 
  
  送分题，在此不表。
- GUMIAndSongsDiv2:

   這道題目有點意思，壹直想著用背包(DP)，但是由于前後選擇有依賴，相當于是有狀態的，所以不知如何下手。比賽結束後嘗試用dfs搜索的辦法，把所有的狀態枚舉搜索了壹遍，答案是正確的，但是過不了系統測試，超時了。本想剪枝優化壹下，但是除了歌的長度(duration)還有歌曲音調(tone)變化限制，剪枝未遂。後面看了壹些建議：從songs中，取出兩首的tone作爲上下限(上下限界定完，這樣在這個界限中的切歌最優耗費壹定是MaxTone-MinTone)，再篩選出所有符合這個上下限的歌按duration從小到大排序(貪心在這裏是ok的，因爲在規定時間內，歌曲越多越好)，算出給定時間在這個tone界限中能放的歌曲，最後對比所有組合，取最大。時間複雜度爲O(n^3)。
   
   PS: 比賽時我在的房間只有壹個人最後成功了，而且還是暴力破解，枚舉所有情況的。在進行系統測試時，壹個來自天朝的少年nickname爲"China_xijingping"的還在叫囂說"Brute force is cheating , it can not pass"之類的話，然後那個人就華麗麗麗的pass了…當時我覺得丟人丟到國外的感覺。

- GameInDarknessDiv2:

  這道題其實也比較容易，用bfs或者dfs可以輕松搞定。只要明白Alice的下壹步以及Alice當前壹步，都需要考慮，這樣Bob才不會跟Alice撞到壹起。先把Alice的移動全部標記到壹個狀態數組[step][y][x]，後續Bob每次進行dfs的時候，就可以對比Alice狀態數組，同時記錄Bob自己的狀態數組[step][y][x]，把第n步移動到[yn][xn]的位置都標記上，以免反複的進行dfs。最後只要Bob能堅挺的完成所有step，那麽Bob就贏了。
  
  這題目就是寫起來比較麻煩。手慢則來不及了。

[看代碼點擊我](https://github.com/deanbear/TopCoder/tree/master/SRM/SRM588)

###SRM587 2013/08/01

這場比賽也很慘，本來可以命中三題的，但是第二題用dp沒過系統測試，第三題寫好來不及提交時間就到了。不開心。> <

- InsertZ : 這題考驗智力水平是不是適合當程序員。
- JumpFurther :

  這題我當時想用dp做，還華麗的寫出了個狀態轉移方程。但是系統測試證明我是錯的。其實是一個數學公式。能達到的總數是一定的，只要某段求和爲badstep，則可以總數減一繞過去。否則返回總數。我討厭數學，真的。

- ThreeColorabilityEasy :

  也是數學題，只要4個組合成的矩形構成不是3:1的情況就Yes，否則爲No。
  
[看代碼點擊我](https://github.com/deanbear/TopCoder/tree/master/SRM/SRM587)
   
   

