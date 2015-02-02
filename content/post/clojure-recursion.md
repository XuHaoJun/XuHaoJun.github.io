+++
date = "2014-05-10T19:43:37+08:00"
title = "Clojure 遞迴測試"
tags = ["clojure"]
categories = ["computer"]
+++


[Clojure Recursive
Looping](http://clojure.org/functional_programming#Functional%2520Programming--Recursive%2520Looping)

# 傳統遞迴<a id="sec-1" name="sec-1"></a>

## Source<a id="sec-1-1" name="sec-1-1"></a>

    (defn deepable-recur? [deep-length]
      (if (= 0 deep-length)
        true
        (deepable-recur? (dec deep-length))))

<!--more-->

## Test<a id="sec-1-2" name="sec-1-2"></a>

一個很蠢的測試函式：

    (defn deep-test [start end step deep-fn]
      (doseq [length (range start end step)]
        (if (deep-fn length) (println length "Deep Done!"))))

    (deep-test 5000 10000 1000 deepable-recur?)
    ;;; output->
    ;; 5000 Deep Done!
    ;; 6000 Deep Done!
    ;; 7000 Deep Done!
    ;; 8000 Deep Done!
    ;; StackOverflowError 
    ;; clojure.lang.Numbers$LongOps.combine (Numbers.java:394)

# Clojure recur special operator<a id="sec-2" name="sec-2"></a>

## Source<a id="sec-2-1" name="sec-2-1"></a>

    (defn deepable-recur? [deep-length]
      (loop [len deep-length]
        (if (= 0 len)
          true
          (recur (dec len)))))

## Test<a id="sec-2-2" name="sec-2-2"></a>

    (deep-test 60000000 80000000 2000000 deepable-recur?)
    ;;; output->
    ;; 60000000 Deep Done!
    ;; 62000000 Deep Done!
    ;; 64000000 Deep Done!
    ;; 66000000 Deep Done!
    ;; 68000000 Deep Done!
    ;; 70000000 Deep Done!
    ;; 72000000 Deep Done!
    ;; 74000000 Deep Done!
    ;; 76000000 Deep Done!
    ;; 78000000 Deep Done!
    ;; nil

# Clojure trampoline<a id="sec-3" name="sec-3"></a>

## Source<a id="sec-3-1" name="sec-3-1"></a>

    (defn deepable-recur? [deep-length]
      (if (= 0 deep-length)
        true
        #(deepable-recur? (dec deep-length))))

## Test<a id="sec-3-2" name="sec-3-2"></a>

比上面那個慢多了。

    (trampoline deepable-recur? 70000000)
    ;;; output->
    ;; true

[Clojure Recursive
Looping](http://clojure.org/functional_programming#Functional%2520Programming--Recursive%2520Looping)

# 傳統遞迴<a id="sec-1" name="sec-1"></a>

## Source<a id="sec-1-1" name="sec-1-1"></a>

    (defn deepable-recur? [deep-length]
      (if (= 0 deep-length)
        true
        (deepable-recur? (dec deep-length))))

## Test<a id="sec-1-2" name="sec-1-2"></a>

-   一個很蠢的測試函式：

    (defn deep-test [start end step deep-fn]
      (doseq [length (range start end step)]
        (if (deep-fn length)
          (println length "Deep Done!"))))
    (deep-test 5000 10000 1000 deepable-recur?)
    ;;; output->
    ;; 5000 Deep Done!
    ;; 6000 Deep Done!
    ;; 7000 Deep Done!
    ;; 8000 Deep Done!
    ;; StackOverflowError   clojure.lang.Numbers$LongOps.combine
(Numbers.java:394)

# Clojure recur special operator<a id="sec-2" name="sec-2"></a>

## Source<a id="sec-2-1" name="sec-2-1"></a>

    (defn deepable-recur? [deep-length]
      (loop [len deep-length]
        (if (= 0 len)
          true
          (recur (dec len)))))

## Test<a id="sec-2-2" name="sec-2-2"></a>

    (deep-test 60000000 80000000 2000000 deepable-recur?)
    ;;; output->
    ;; 60000000 Deep Done!
    ;; 62000000 Deep Done!
    ;; 64000000 Deep Done!
    ;; 66000000 Deep Done!
    ;; 68000000 Deep Done!
    ;; 70000000 Deep Done!
    ;; 72000000 Deep Done!
    ;; 74000000 Deep Done!
    ;; 76000000 Deep Done!
    ;; 78000000 Deep Done!
    ;; nil

# Clojure trampoline<a id="sec-3" name="sec-3"></a>

## Source<a id="sec-3-1" name="sec-3-1"></a>

    (defn deepable-recur? [deep-length]
      (if (= 0 deep-length)
        true
        #(deepable-recur? (dec deep-length))))

## Test<a id="sec-3-2" name="sec-3-2"></a>

比上面那個慢多了。

    (trampoline deepable-recur? 70000000)
    ;;; output->
    ;; true

