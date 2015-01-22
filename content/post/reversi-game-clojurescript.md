+++
date = "2014-05-11T19:10:27+08:00"
title = "黑白棋 (Clojurescript)"
tags = ["html5", "game", "clojure", "clojurescript"]
categories = ["computer"]
+++

一個簡單的單機網頁(html5)黑白棋遊戲。

[Try it Online](https://xuhaojun.github.io/reversi/)

<!--more-->

[Source code](https://github.com/XuHaoJun/reversi)


# 實現算法<a id="sec-1" name="sec-1"></a>

每次下棋對其八個鄰近方格做掃描，如果是相反顏色的棋子，就往其方位向前找到另一個相同顏色的棋子，若有找到則翻棋，沒有則遍歷下一個方位。

# 電腦(AI)下棋算法<a id="sec-2" name="sec-2"></a>

暫時隨機，在看用哪種好。

# Clojurescript 使用心得<a id="sec-3" name="sec-3"></a>

一堆括號阿！！每次都要讓函數回傳有意義的值，Debug
起來也很容易，一個函數影響的範圍就只有他的參數而已，沒有隱示參數(全域變數、成員變數)的話就很好測試，每個函數就盡量小小的做一件事，不過到使用
[phaser](https://github.com/photonstorm/phaser) (javascript html5 game
framework)那層就一堆副作用囉!(set! xxx yyy)。

# 截圖<a id="sec-4" name="sec-4"></a>

![img](/img/reversi-game.png)
