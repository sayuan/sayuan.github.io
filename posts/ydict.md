<!--
.. title: ydict - node.js 實作
.. slug: ydict
.. date: 2014/01/30 15:07:52
.. tags: ydict, nodejs
.. link:
.. description:
.. type: text
-->

## What is "ydict"

身為一名 command line 魔人，儘可能的將所有在電腦上的操作在 command line
之內完成，是一件理所當然的事情，就連查字典也不例外，而 ydict
就是這樣的工具。

![ydict](/galleries/misc/ydict.png)

ydict 的資料來自於 [Yahoo 字典][]，事實上 ydict
所作的事情就只是以使用者的輸入詞在 Yahoo 字典上查詢，然後 parsing
出重要的資訊，並以適合 terminal 的格式顯示在螢幕上。

但其實 ydict 並不是 "一個" 工具，事實上很多人都曾開發自己的實作，
而各實作也有各自的分支，我現在已經找不出最早是由誰開發的了。
在眾多版本之中，我使用了最長時間的是 [freehaha 實作的 Python 版本][freehaha]，
其次則是 [FourDollars 的 Perl 版本][fourdollars]，在此先向兩位作者致上感謝。

使用 ydict 這工具對我來說已經到了不可或缺的地步，但幾乎每隔一段時間 Yahoo
字典就會改版，而接下來的幾天在作者尚未更新之前，我就會沒有 ydict 可使用。
而另一方面，我也會希望能針對自己的需求，對 ydict 進行修改。

## My works

我也確實試過自己動手修改，但後續要繼續與原作者的版本接軌卻反而成了一件麻煩事。
而在先前嘗試修改的經驗裡，我覺得必須能容易的更新 parsing 規則，才能夠快速的針對
Yahoo 字典的改版做出更新。正巧最近我剛學了一點 javascript 與
node.js，我想如果能像 jQuery 一樣使用 CSS selector 進行
parsing，事情也許會簡單很多，於是 [ydict.js][] 就此誕生。

ydict.js 的一個主要設計考量是，parsing 與 display
必須分離，parsing 的部份只會回傳處理後的 json，而 display 只是單純的將 josn
檔依照格式顯示在螢幕上， 因此在任何一方修改都不會影響到另一方。
另外我也把 parsing 的部份包成 module，讓其他 project
可以直接引用，雖然我覺得這個功能完全只是雞肋。:p

此外，我也已經將 ydict.js 上傳 npm，因此只要執行下述指令即可完成安裝，
希望各位會喜歡。

    [sudo] npm install -g ydict.js

## What else?

我的好友 Andrew 與 Jeff 也和我一樣依賴 ydict，因此在去年 Yahoo
字典改版，各家實作卻都尚未支援之前，他們也都各自開發了自己的實作。

首先是 [Andrew 的 shell script 版][andrew]，使用 w3m 的超簡短作弊寫法，
麻雀雖小卻是五臟俱全。(**使用前請先安裝 w3m 套件。**)

另外就是 [Jeff 開發的 LiveScript 版][jeff]，和 ydict.js 一樣使用 [cheerio][]
來處理 parsing，並且同樣也已經上傳 npm，因此只要執行下述指令即可安裝：

    [sudo] npm install -g jydict

[Yahoo 字典]: http://tw.dictionary.yahoo.com/
[freehaha]: https://github.com/freehaha/ydict
[fourdollars]: http://fourdollars.blogspot.tw/2008/05/vim-ydict.html
[ydict.js]: https://github.com/sayuan/ydict.js/
[andrew]: https://github.com/yongjhih/rc/blob/master/bin/andict
[jeff]: https://github.com/JeffChien/jydict
[cheerio]: https://github.com/MatthewMueller/cheerio
