+++
date = "2013-08-25T04:10:14+08:00"
title = "產生一組不重複整數的集合(Ruby)"
tags = ["ruby", "alogrithm"]
categories = ["computer"]
+++

先用 Ruby 寫以前上 Android 中猜數字範例中用到的算法：

# Normal Way - 1<a id="sec-1" name="sec-1"></a>

    def get_uniq_nums(size, range)
      ary = []
      begin
        r = rand(range)
        if ary.member?(r)
          next
        else
          ary << r
        end
      end while( ary.length < size )
      return ary
    end

<!--more-->

記得之前教的不是用 member
的方法來判斷，當初沒有提到用到集合的概念寫，好像是檢查前面幾個數字的迴圈吧，那陀
Java 程式碼已經忘光了。

這是產生 4 個不重複 1~9 的數字，放在一個陣列裡面   
`get_uniq_nums(4, (1...10))`   

變成一個數字，先 join 把他連在一起變成字串，在轉回數字。   
`get_uniq_nums(4, (1...10)).join.to_i`   

# Normal Way - 2<a id="sec-2" name="sec-2"></a>

    def get_uniq_nums(size, range, ary = [])
      if size.zero?
        ary
      elsif ary.member?(r = rand(range))
        get_uniq_nums(size , range, ary)
      else
        get_uniq_nums(size - 1, range, (ary << r))
      end
    end

試了別種寫法，很像叫尾遞迴的方法，跟普通遞迴好像差別在多用一個參數在存值，在
Emacs lisp
很像還要多用一個函數才能不影響原來的接口。順便一提，弄不出一個函數的普通遞迴方法。

以下是普通遞迴版失敗品：

    def get_uniq_nums(size, range)
      if size.zero?
        []
      elsif get_uniq_nums(size, range).member?(r = rand(range))
        get_uniq_nums(size, range)
      else
        get_uniq_nums(size - 1, range) << r
      end
    end

# Set Way<a id="sec-3" name="sec-3"></a>

放狗一搜，找到了其他方法：

-   [How do I generate a list of n unique random numbers in
    Ruby?](http://stackoverflow.com/questions/119107/how-do-i-generate-a-list-of-n-unique-random-numbers-in-ruby)

> Set implements a collection of unordered values with no duplicates.

    require 'set'
    
    def rand_n(n, max)
      randoms = Set.new
      loop do
        randoms << rand(max)
        return randoms.to_a if randoms.size >= n
      end
    end

好吧&#x2026;原來 Ruby 內建了 Set
的資料型態，第一次發現有內建集合的程式語言，當初應該要想到 Java
中有沒有這東西。
上面是用集合內不重複元素的特性，所以在加入元素時天生就會檢查有沒有重複，最後在轉成陣列。

看來以後可以玩玩看交集、聯集、差集之類的，還有子集合判斷之類的。

# Range Way - 1<a id="sec-4" name="sec-4"></a>

> A Range represents an interval&#x2014;a set of values with a beginning
> and
> an end.

    range = 0...1000000
    how_many = 10000
    
    # first way
    # Array::sample Choose a random element or n random elements from
the array.
    range.to_a.sample(how_many)
    
    # second way
    (range).sort_by{rand}[0...how_many]

直接從 Range 裡用內建的方法隨機挑，行數完敗上面那兩個。

# Range Way - 2<a id="sec-5" name="sec-5"></a>

突然想到如果要在生成時就篩選掉不想要數字的話，要怎麼做？

仔細一想很簡單，直接在在範圍裡改。

    # Delete 2 from the range of rand
    (1..4).reject { |x| x==2 }.to_a.sample(how_many)

# Benchmark them<a id="sec-6" name="sec-6"></a>

## Part 1<a id="sec-6-1" name="sec-6-1"></a>

    require 'benchmark'
    
    range = 0...1000000
    how_many = 10000
    
    ## Range way - 1
    Benchmark.realtime do
      range.to_a.sample(how_many)
    end
    # => 0.076334817
    
    ## Set Way
    Benchmark.realtime do
      rand_n(how_many, range)
    end
    # => 0.01060032
    
    ## Normal way - 1
    Benchmark.realtime do
      get_uniq_nums(how_many, range)
    end
    # => 3.565261117

## Part 2<a id="sec-6-2" name="sec-6-2"></a>

    range = 0...1000000
    how_many = 1000000
    
    ## Set Way
    Benchmark.realtime do
      rand_n(how_many, range)
    end
    # => 11.305328646
    
    ## Range way - 1
    Benchmark.realtime do
      range.to_a.sample(how_many)
    end
    # => 0.112987391

Range Way 完敗。 還有沒有實現 Set Way 和 Normal Way 的篩選的功能。
