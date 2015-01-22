+++
date = "2013-08-27T19:32:07+08:00"
title = "阿姆斯壯數 (Ruby)"
tags = ["ruby", "alogrithm"]
categories = ["computer"]
+++

寫一些簡單的演算法來熟悉 Ruby。

# Armstrong number<a id="sec-1" name="sec-1"></a>

-   [阿姆斯壯數 -
    WiKi](https://zh.wikipedia.org/wiki/%25E6%25B0%25B4%25E4%25BB%2599%25E8%258A%25B1%25E6%2595%25B0)

指一 N 位数，其各个数之 N 次方和等于该数。   

例如 153、370、371 及 407
就是三位數的水仙花数，其各个数之立方和等于该数：   

<!--more-->

# Source code

不曉得型別轉來轉去算不算壞習慣&#x2026;。   

有用到 lazy 這個 enumerator，如果沒用 lazy 的話就會當在那裡了，lazy
感覺很像是一個一個求值後在判斷在存值，沒有使用的話則一次全部求值後在做事。   

懶的想怎麼做優化了，怕到時候改一改可讀性就沒現在這個好了，先留這個作筆記。

    class Integer
      def armstrong_num? # may be have more better name..
        sum = 0
        digits = self.to_s.length
        digits.times { |n| sum += (self.to_s[n].to_i ** digits) }
        return sum == self
      end
    end
    
    # 三位數的所有阿姆斯壯數
    (100...1000).select{ |x| x.armstrong_num? }
    # => [153, 370, 371, 407]
    
    # 四位數的第一個阿姆斯壯數
    (1000...10000).select{ |x| x.armstrong_num? }.first(1)
    # => [1634]
    
    # 前 15 個阿姆斯壯數
    (1..Float::INFINITY).lazy.select{ |x| x.armstrong_num? }.first(15)
    # => [1, 2, 3, 4, 5, 6, 7, 8, 9, 153, 370, 371, 407, 1634, 8208]
    
    # 前三個阿姆斯壯數，從三位數開始
    (100..Float::INFINITY).lazy.select{ |x| x.armstrong_num? }.first(3)
    # => [153, 370, 371]

