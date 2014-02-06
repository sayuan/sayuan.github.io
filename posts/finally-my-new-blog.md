<!--
.. title: 終於，新居落成
.. slug: finally-my-new-blog
.. date: 2014/01/29 21:05:42
.. tags: static blog generator, nikola, mathjax, markdown, CJK-space-fix
.. link:
.. description:
.. type: text
-->

## 塵埃落定

嚷著說要寫 blog 也差不多拖了一、兩年了，除了單純的因為我懶以外，找不到合適的
static blog generator 也是一大主因。為了讓 blog
能完全在自己的掌控之中，我必須選一個自己看得懂、改得動的語言所實作的
generator，因此我首先關注的是以 Python 實作的 [Pelican][]。

確認了 Pelican 有所有我需要的功能：支援 markdown 語法、能夠顯示 LaTex
語法、syntax highlight 當然也是必要的，還有其他 blog 必備的 tag, RSS, ……等等。
然後最後是，選一個看得順眼的 theme ……。糟糕，怎麼找不到合適的？

我這個人除了懶以外，另一個缺點是龜毛，而且常常是龜毛在我沒有能力做得更好的地方。
我開始嘗試改寫 theme，當然沒有美術細胞的我，即使投入了不少時間，
卻仍然做不出能看的東西，間接導致我的部落格生涯遲遲無法展開。

終於，不久前耳聞了另一套 Python 實作的 generator：
[Nikola][]，照慣例掃了一遍所有的 theme，終於看到一個讓我眼睛為之一亮的
theme: [zen][]，也就是各位現在正在看著的 theme 了。
終於呀，原來相比起 generator 的功能，我真正需要的只是一個好看的 theme。 :)

[Pelican]: http://blog.getpelican.com/
[Nikola]: http://getnikola.com/
[Zen]: http://www.damian.oquanta.info/posts/nikolas-zen-theme-finally-released.html

接下來就展示一下 Nikola 在數學公式和 code 的寫法以及其顯示在網頁上的效果吧。

## Math

顯示數學公式其實就只是使用了 [MathJax][]，沒有什麼特別的地方。

* inline math: $e^{ix} = \cos x + i\sin x$

    對應的寫法: `$e^{ix} = \cos x + i\sin x$`

* display math: $$\sqrt{1+\sqrt[^p\!]{1+a^2}}$$

    對應的寫法: `$$\sqrt{1+\sqrt[^p\!]{1+a^2}}$$`

## Syntax Highlight

Syntax highlight 則是 [CodeHilite][] 和 [Fenced Code Blocks][] 的功勞。

```java
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

對應的寫法：

<pre>```java
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```</pre>

[MathJax]: http://www.mathjax.org/
[CodeHilite]: http://pythonhosted.org/Markdown/extensions/code_hilite.html
[Fenced Code Blocks]: http://pythonhosted.org/Markdown/extensions/fenced_code_blocks.html

## CJK-space-fix

最後來個置入式行銷介紹一下我自己開發的 [CJK-space-fix][]。

很多人在寫 markdown 或著其他格式的檔案時，會習慣在不超過 column 80 的位置
換行。例如：
<pre>
很多人在寫 markdown 或著其他格式的檔案時，會習慣在不超過 column 80 的位置
換行。例如：
</pre>

這在 Python-Markdown 會被處理成如下
<pre>
`<p>`很多人在寫 markdown 或著其他格式的檔案時，會習慣在不超過 column 80 的位置
換行。例如：`</p>`
</pre>

然後顯示在瀏覽器上時，就會在 "位置" 和 "換行" 之間有一個多餘的空白，像是這樣：
<pre>
很多人在寫 markdown 或著其他格式的檔案時，會習慣在不超過 column 80 的位置 換行。例如：
</pre>

這在許多以空白作為單字分隔的語言中都不是問題，但是在中文卻會顯得很突兀。

有些人的解決方式是編輯 markdown 時故意不換行；
也有些人是在編輯文章時，故意選在標點符號的位置換行。
當然也有其他人和我一樣用程式解決，但其他人都是在 "markdown 轉 html" 這段
做處理。我一直認為這是屬於瀏覽器的問題，而瀏覽器的問題就該在瀏覽器上被解決，
雖然短時間內各家瀏覽器都不會有解決方案，至少我可以自己寫段 javascript
來處理好這件事，於是這支 script 就誕生了。

[CJK-space-fix]: https://github.com/sayuan/CJK-space-fix/

## What's next?

老實說，Nikola 也不是個讓我完全滿意的 generator，雖然說是支援
markdown，但找不到針對 markdown 的說明文件，很多功能我也都沒能試出來。
但要是再這樣挑三揀四，我想我大概永遠也沒有辦法開始 blogging 吧。
所以還是就先這樣吧！後續還有很多問題想要處理，像是站內搜尋、轉換至 HTML5、增加適當的 meta 標籤……等等。
不過我想最大的問題應該是我能堅持 blogging 多久吧？
