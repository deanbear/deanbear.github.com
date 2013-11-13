---
layout: post
title: MacBook Pro雙硬盤SSD+HDD炮製Fusion Drive
date: 2013-11-09 18:41:15
categories:
- 技术流/techgangster
tags:
- Fusion Drive
- SSD
- MacBook Pro
---
###進化的開始

去年正式工作後拿了第一個月工資，就買了MacBook Pro。Mid 2012低配，i5 CPU，4G DDR3，500GB HD。拿來幹活的，日用基本還好，但是程序多開了或者開了大程序就很慢很卡。一直想換個SSD，但是SSD又貴，我又懶，絕配，就這麼熬了一年。

今年剛進公司的小朋友和我一樣的MBP，但是去年就換了128G SSD，8G DDR3。各種飛快刺激到我。恰好主管手上有一塊去年雙十一抽獎得到的但一直閒置在那兒的SAMSUNG 840 120G的SSD，我用500塊買到（市場價大概580-600），然後就開始着手加SSD。

分爲兩塊內容，硬件篇，以及軟件篇。

###硬件篇

**PART I 未雨綢繆**

最近一次用光驅還是什麼時候的事情？我最近一次用是在上半年，因爲借錢給艾未未，配合他完成了一個行爲藝術，稍稍對抗了一下當局。然後他的工作室送了T恤瓜子紀錄片之類的東西給我，還包括一張左小祖咒的新專輯CD [__这小小的葡萄我从来没吃过__](http://www.xiami.com/album/567432) 。我用MBP的光驅聽了幾天，還不錯。就再也沒有用過了。

所以我決定把光驅拆下來，換成硬盤位裝上磁盤。這樣就有120G+500G的硬盤空間了。原來打算把120G拿來裝Mac OS X，500G拿來放相片以及視頻等資料，但是後來發現了蘋果研發的很厲害的Fusion Drive就沒費腦子在想分區分盤了，這在下面的軟件篇會說。

那這個時候還剩一個問題，把SSD放在光驅位，還是把原生的日立HD拆下來放在光驅位，再把SSD放在硬盤位？不苛刻的來說，這都無所謂的，仁者見仁智者見智的事。但是硬要說哪個比較好，我搜索了一圈，認爲把SSD放在光驅位是比較好的選擇。

這是在MacRumors上的一個帖子討論[「ssd in optical drive bay?」](http://forums.macrumors.com/showthread.php?t=1220138) ，截取最有用的一個回覆，如下：

> For the record, the computer is not prevented waking from sleep. It's Hibernation mode that doesn't function properly.If you don't use Hibernation mode (which stores all the open program information on the SSD in a ~6GB file every time you close the clamshell) and only use sleep, putting the SSD in the optical bay makes the most sense. 

>If you put the SSD in the main bay, the HDD losses shock protection, making it vulnerable to damage if dropped. You also lose SMART protection. Unless you're an avid user of Hibernation mode, I don't recommend putting the SSD in the main bay. No, put it in the Optical bay drive, disable hibernation mode and you can (1) keep peace of mind about the safety of your HDD, (2) recover 6GB of space on your SSD (and space on an SSD is still precious, and (3) enjoy faster sleeping thanks to Hibernation mode being disabled.

> The only time I don't give this advice is if you have a SATA III-capable 2011 MBP where SATA III only works in the main bay. That's a function of when you bought your 2011 (earliest models only have SATA III enabled on the main bay afaik). Those owners should mount their SSD in the main bay to take advantage of the maximum speeds their SATA III SSD can offer. But this doesn't apply to owners of MBP's prior to April 2011.

總結來說，拿捏好以下幾個點，就可以明確要怎麼處理SSD和HD的位置擺放了。

A. MacBook的硬盤位是有保護機制的，能防震防摔。HD比SSD更需要這樣的保護機制（因爲Hard Drive是有讀寫機械磁頭以及磁盤的，而Solid-state Drive完全不一樣的結構雖然我也沒研究是怎樣的原理）。

B. 如果把SSD裝在光驅位上，又把系統裝在SSD上，那麼由於光驅位的緣故，是不能用Mac OSX的Safe Sleep的功能的，也就是如果沒電了，系統就不會把內存中的程序資料Dump到硬盤中去，下次開機時，未保存的東西都會沒掉。(如果採用Fusion Drive，我不確定系統還是不是全部裝SSD上，也不確定是否不能Safe Sleep，我直接禁用了)

C. 老款的MBP，光驅位的SATA串口鏈接速度只能達到3Gbit/s，但是SSD（比如我這塊SAMSUNG 840）可以到6Gbit/s，如果SSD是支持6Gbit/s，放在支持3Gbit/s的光驱位就显得很亏了。我的Mid2012的MBP硬盤位和光驅位都可以支持6Gbit/s，所以沒差別。(可以去左上角蘋果->關於本機->更多信息->系統報告->硬件->SATA/SATA Express瞭解機器情況)

想通以上幾點，你就可以得出HD放哪裏，SSD放哪裏。或者索性保留光驅，把HD換成SSD，再把HD變成移動硬盤好嘞。

**PART II 上房揭瓦**

目標是：原生HD不動，卸下光驅，裝上SSD。

準備以及工具：

A. 一塊SSD。（我用的SAMSUNG 840不推薦，除了價格便宜，有點過時了。推薦840 PRO或者840 EVO）

B. 一個光驱位硬盘托架(淘寶隨便搜索很多的，我買的是50塊左右的)。十字紋螺絲刀(買托架一般會贈送開機裝卸工具，沒有向老闆要或者買有的)

過程：

1. SSD與托架組裝。SSD四周可以旋螺絲的，用來避震的。托架應該有贈送這樣的螺絲。SSD放入托盤架然後鎖上，儘量安裝牢固。（見圖一）

2. 拆後蓋。注意三顆長螺絲以及剩下的短螺絲的位置，妥善存放。我隔壁的小朋友現在的後蓋上就少了一顆螺絲...

3. 卸光驅。先把連接電路的線給拆清楚，輕些。找準固定螺絲的位置。我這款Mid2012的，一共有三顆螺絲固定，I.風扇邊上， II. HD邊上， III.音響串線下方。 這三顆螺絲都挺不容易卸的，特別是第三顆。注意不要旋花了螺絲，不然比較麻煩。第三顆螺絲要先把音響部位拆一遍，才能看到底下的螺絲。然後就可以把光驅拖出來了。（見圖二、圖三、圖四）

4. 完善SSD。光驅上有兩個東西要拆下來給SSD，一個是電路連接口，拆下來給SSD。還有一個是旋螺絲的固定支架腳，也要卸下來給SSD。

5. 裝SSD。把3倒序，要注意把線線框框都給整理清楚。

6. 檢測。先別忙着裝後蓋。開機檢測是否識別SSD了，開機會提示無法讀取光驅，忽略先。打開「磁盤工具」，如果可以看到SSD的名字了，就算識別了。（見圖五）

7. 裝上後蓋。

以下爲對應實拍圖，以及壁紙的女神是，湯唯。

![](http://farm4.staticflickr.com/3699/10754988693_7e5d89457f_k.jpg)


###软件篇

**PART I 理论**

開始想換SSD時，我只是打算把SSD當成系統盤，把HD變成內置的外接硬盤就好了。後來無意發現了一年前Apple推出的 [Fusion Drive](http://en.wikipedia.org/wiki/Fusion_Drive)，感慨Apple挺牛逼的。用系統來實現了智能管理硬件這件事情。簡單的說，Fusion Drive就是用一塊SSD以及一塊HD，混合成一塊邏輯硬盤，也就是對操作系統來說，就是一塊硬盤。但是同時Mac OSX有一套算法機制，能智能識別出哪些文件以及應用以及資料該放在SSD或者HD上。這樣在保證了SSD的速度優勢的情況下，用HD彌補了空間劣勢。在SSD還是很貴的情況下，做到了一個很好的綜合權衡。Apple只推出了iMac以及Mac mini下的原装128G SSD + 1T HD的Fusion Drive。作为低配的MBP，自己DIY吧。已经用了三天，效果不错，用BlackMagic测试过，写150MB/s，读530MB/s。與840純SSD評測是一致的（當然和更高端的SSD寫速度還是有差距的）。

其实第一次听说要DIY Fusion Drive我是拒绝的，因为，你不能让我DIY，我就马上去DIY，第一我要调查一下，因为我不愿意DIY了以后发现功效没有，这样读者出来一定会骂我，根本没有这样的Fusion D日ve，就证明上面那个是假的。后来我也经过证实他们确实是有效高能的，我用了大概3天左右，感觉还不错，后来我在写这篇文章的时候没有添油加醋，因为我要让读者看到，我用完之后是这个样子，你们用完之后也会是这个样子！

*注意，我差點漏了一個信息，由於我只用Mac OS X這麼一個系統，所以不存在「Fusion Drive是否支持Boot Camp Windows以及Windows」這樣的困擾。所以沒有深究這樣的問題，請有需求用雙系統的朋友自重！

**PART II 實踐**

1. 備份。製作Fusion Drive需要先格式化掉磁盤。所以原來的系統資料要的話就必須備份。我用系統自帶的Time Machine備份到500G的WD移動硬盤。(略簡單，需過程自行搜索)，我的系統大概50G左右，耗時接近1小時。

2. 制作啟動U盤。官方鏈接[OS X 恢复磁盘助理](http://support.apple.com/kb/dl1433?viewlocale=zh_CN)。具體過程是用磁盤工具將下載下來的dmg拖入U盤即可。不明確自行搜索。

3. 關機，按住option開機，選擇U盤啓動。(如果還是選擇磁盤啓動的話，會無法完成第4步的格式化磁盤動作)

4. [Fusion Drive DIY](http://dr.ibuick.com/Gp2H.html) by ibuick ，按住這個教程來，三步，格式化SSD與HD(磁盤工具又立功了)->合併SSD和HD成爲一塊邏輯盤(diskutil coreStorage create Macintosh\ HD diskX diskXX)->建立系統分區(diskutil coreStorage createVolume $LogicHDUID jhfs+ MacintoshFD 100%)

5. 繼續用U盤安裝系統。成功後進入系統，非常快！淚流滿面。然後看到磁盤工具裏就是完整的一塊620GB的Macintosh HD了！關機！

6. 按option開機，選擇Time Machine導入，這時候鏈接剛才存儲備份的移動硬盤，開始還原，我用了半個小時，就完成了，一臺和原來一樣，但是速度更快的MBP。

7. 又差點忘記了，雖然是Fusion Drive，但是還是有SSD的成分！如果有SSD又想延長使用壽命的話，請開啓Trim！別問我爲什麼，因爲原生的Mac Fusion Drive是開啓的！我也不喜歡用Trim Enabler，因爲它對我是黑盒子，我並不知道它到底做了什麼。所以我用命令行開啓Trim。但是10.9 Mavericks開啓TRIM的命令行和之前的不一樣，找了好久才看到這個[macx上的帖子](http://www.macx.cn/thread-2106941-1-1.html)。
	
**命令行開啓Trim 開始**

输入以下指令：

i.为了安全，此步为备份驱动 （可能需要输入密码）

	sudo cp -r /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/ /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.BACKUP

ii.更新

	sudo perl -pi -e 's|(\x52\x6F\x74\x61\x74\x69\x6F\x6E\x61\x6C\x00{1,20})[^\x00]{9}(\x00{1,20}\x54)|$1\x00\x00\x00\x00\x00\x00\x00\x00\x00$2|sg' /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/MacOS/IOAHCIBlockStorage

iii.开trim

	sudo kextcache -system-prelinked-kernel

iv.清cache

	sudo kextcache -system-caches

v.重启系统。

**命令行開啓Trim 結束**
	
再給個鏈接，我上面的實踐過程都是參考[知乎上這幾位哥的回答](http://www.zhihu.com/question/20602523)而綜合而成的。謝謝他們的貢獻。

~~~~~~~大功告成的分割線~~~~~~~~~~


MBP變身Fusion Drive後，做啥都麻利了，心情也好了。所以我在微博上說，買SSD真的是能讓幸福感飆升的行爲之一。之前買iPad也有這個感覺。

後續缺點還是爆一下，那只有一個，因爲用了兩塊盤而且是Fusion Drive，不知道系統在背後搞什麼鬼(比如不活躍文件從SSD移動到HD等)，肯定有同時使用兩塊盤的時候，所以這幾天耗電量比原來的大了，持久度估計只有原來的3/4了。希望後續系統穩定下來了，找到我使用系統的規律後，電池使用時間能長回來（不懂原理真吃虧啊，摔！）

還有如果Fusion Drive完了，後悔了，還是希望用單純SSD和HD的，怎麼辦呢？後路我也搜索了一下了。只是沒有實踐過。請後悔的同學自重！

	diskutil cs delete $LUID

###接着就愉快的工作吧！別以爲換了SSD寫代碼的速度也會變快！這是妄想！請把腦子換成SSD腦子吧謝謝！





