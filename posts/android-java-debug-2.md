<!--
.. title: Android Java 層 Debug 工具介紹 (2)
.. slug: android-java-debugging-2
.. date: 2014/02/09 20:36:56
.. tags: Android, debugging, Eclipse, apktool
.. link:
.. description:
.. type: text
-->

在系列文的[第一篇文章][]中，我已經介紹過 Log Viewer 與
Profiler，而這次所要介紹的內容則是 Debugger，以及一些 Reverse Engineering 工具。

[第一篇文章]: android-java-debugging-1.html

## Remote Debugging

對於 Android App 開發者來說，在 Android 上 debug 是在自然不過的事了。
您只需要準備好專案，點一下 `Debug` 按鈕，IDE 就自動進入 debug 模式，接著無論是
下中斷點、單步執行，或是查看變數內容……等，一切皆任君差遣。

1. 但如果不是透過 IDE 啟動的程式執行到一半，出現了預期之外的狀況，這時您還能不
   能透過 Debugger 進行 debug 呢？
2. 若是執行的程式沒有建立專案，甚至沒有 Source Code 時，Debugger 還能有所作為嗎？
3. 又或著是系統廠 RD 最想要的功能，能不能對系統 Service 進行 debug？

上述三個問題的答案都是 YES，當然其中也會有一些前提必須滿足，像是 debug 的對象必
須具有 debuggable flag，或著手機本身 image 為 Engineer build。在前一篇文章中我也
提過了，不需要太擔心這個條件無法滿足，因為下一個章節就會來解決這件事。:)

我在這裡所要介紹的技巧，其實就和對 App 進行 debug 本質上是一樣的，只不過操作的
過程比較手動一些。我會以 Eclipse 進行以下的示範，但其實使用任何一款支援 Remote
Debugging 的 debugger 皆可，甚至連 Android plugin 都不需要安裝。

![Select debug port](/galleries/android-java-debug/debug_port.png)

首先到任何一個看得見這畫面的地方，不管是 Eclipse 內建的 DDMS 也好，或著獨立的
Android Device Monitor 也好，總之只要是這個畫面都好。

對著想要進行 debug 的 process 點一下。在點選之前，最後一欄的文字本來會是 `8600`
之類，但點選之後就會變成 `8600 / 8700`。

這些數字是其實是 Port Frowarding 所開在本機的 port，透過這些 port，就可以和手機
內特定 process 對應的 JVM 進行溝通。

在點選之前的 port 是以流水號方式從 8600 開始編號，而只要是被選取的 process
就會額外準備一組 port 8700。因為數字是固定的，因此在後續設定 debugger 時會比較方
便，所以這個步驟其實並不是必要的。

![Create debug configure](/galleries/android-java-debug/debug_config.png)

接下來，在 `Debug Configurations` 中建立一個新的 `Remote Java Application`，
右邊的 `Project` 則視您 debug 的對象選擇，若是沒有對應的專案則請保持空白，
`Port` 則填上在前一步驟看到的數字。因為所有我打算進行 debug 的 process 都會事先被
我設定好 port 8700，因此我只需要準備一個 Debug Configuration 即可。

最後按下 `Debug` 按鈕，順利的話就能看到 debugger 成功 attach，可以開始 debug 了！

.. 為何可以這樣做? jdwp
.. apktool
