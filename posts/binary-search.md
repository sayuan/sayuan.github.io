<!--
.. title: 程式競賽小技巧 - Binary Search
.. slug: binary-search
.. date: 2015-06-06 23:33:28 UTC+08:00
.. tags: programming contest, competitive programming, algorithm
.. link:
.. description:
.. type: text
-->

最近在 [Kaif][] 開了一個 [程式競賽][] 區，打算在上面提一些我在競賽中學到的技巧，
不過既然我有一個很久沒動筆的 Blog，不如就直接寫在這裡，再把連結貼到 Kaif 吧。

Binary Search 在程式競賽中，指的不是用來檢查元素在 sorted list 中位置的方法，
而是一種解題技巧。適用 Binary Search 的題目，通常會有兩個特性：

1. 目的是要求出某個變數 "滿足某個條件" 的最小值，
   且變數超出此值後也都會繼續滿足此條件。

2. 無法使用有效率的方法計算出答案，但只要給變數任意的值，
   都能容易的判斷出是否滿足條件。

在針對整數域時，我的 code 會像是這樣：

```.java
int lower = 0;
int upper = 1000000;                    // 某個大到一定滿足條件的值
while (lower < upper) {
    int mid = (lower+upper)/2;
    boolean satisfied = check(mid);     // 將 mid 代入檢查是否滿足
    if (satified) upper = mid;
    else lower = mid+1;
}
```

離開 `while` 迴圈時，`lower` 會與 `upper` 相等，並且就是所求答案。

那麼在實數域會有什麼不同呢？這就是我覺得有意思的地方了。
由於浮點數精確度的關係，是有可能發生 `mid` 等於 `lower` 的情況，導致形成無窮迴圈。

好在我們知道比較浮點數應該要允許一點誤差。通常我的習慣是加上一個常數
`Є`，於是 code 會長這樣：

```.java
public static final double EPSILON = 1e-8;

while (lower+EPSILON < upper) {
    // ...
}
```

使用這個技巧，只要你選擇了 "適當" 的 `Є`，程式就會是可以正確運行的。
但什麼情況下會出問題呢？

當你的 `lower` 很大，而 `Є` 很小時，同樣有可能發生 `lower+EPSILON==lower` 的情況。

那有沒有更好的方法？看看以下的 code 吧。

```.java
double lower = 0.0;
double upper = 1e30;
for (int times=0; times<50; times++) {      // 注意這行
    double mid = (lower+upper)/2;
    boolean satisfied = check(mid);
    if (satisfied) upper = mid;
    else lower = mid;
}
```

結果就是什麼都不要管，固定跑個足夠次數就好。:p

我自己習慣跑 50 次，但也看過其他參賽者使用 40, 100, 200 次。

[Kaif]: https://kaif.io
[程式競賽]: https://kaif.io/z/programming-contest
