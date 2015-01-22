+++
date = "2014-05-16T19:13:28+08:00"
title = "Clojure/Clojurescript Emacs 開發環境"
tags = ["clojre", "clojurescript", "emacs", "develop"]
categories = ["computer"]
+++

簡單的 clojure/clojurescript 開發環境。

# 基本功能安裝<a id="sec-1" name="sec-1"></a>

推薦從 emacs 24 起，自帶的 package 系統來安裝。

首先加入更多 package 的安裝來源 [melpa](http://melpa.milkbox.net)
[marmalade](http://marmalade-repo.org/)

    (defvar marmalade '("marmalade" .  "http://marmalade-repo.org/packages/"))
    (defvar gnu '("gnu" . "http://elpa.gnu.org/packages/"))
    (defvar melpa '("melpa" . "http://melpa.milkbox.net/packages/"))
    (add-to-list 'package-archives marmalade)
    (add-to-list 'package-archives melpa t)
    (package-initialize)

安裝 clojure-mode：
`M-x package-install` `clojure-mode`

這樣就有基本的代碼高亮和縮進功能了。

<!--more-->

# 強力插件: CIDER (Clojure IDE and REPL)<a id="sec-2" name="sec-2"></a>

[CIDER-github](https://github.com/clojure-emacs/cider)

## 安裝<a id="sec-2-1" name="sec-2-1"></a>

`M-x package-install` `cider`

## REPL (交互式編程環境)<a id="sec-2-2" name="sec-2-2"></a>

[REPL-wiki](https://zh.wikipedia.org/wiki/%25E8%25AF%25BB%25E5%258F%2596%25EF%25B9%25A3%25E6%25B1%2582%25E5%2580%25BC%25EF%25B9%25A3%25E8%25BE%2593%25E5%2587%25BA%25E5%25BE%25AA%25E7%258E%25AF)

### 安裝：<a id="sec-2-2-1" name="sec-2-2-1"></a>

推薦使用[leiningen](http://leiningen.org/) 來管理你的 clojure project.

`lein new myproject`

安裝 [cider-nrepl](https://github.com/clojure-emacs/cider-nrepl)
在 `~/.lein/profiles.clj` 加入以下兩行

    {:user
     {:plugins [[cider/cider-nrepl "0.7.0-SNAPSHOT"]]}}

### 使用：<a id="sec-2-2-2" name="sec-2-2-2"></a>

接下來在你的 emacs 執行 `M-x cider-jack-in`
沒有意外的話，會出現一個 repl 的 buffer，關掉是 `cider-quit` 。

幾個必用的 emacs function , 把他們綁在你喜歡的 key 上吧。
`cider-eval-last-sexp` , `cider-eval-defun-at-point` ,
`cider-switch-to-repl-buffer` , `cider-jump`

## Browser REPL (for clojurescript)<a id="sec-2-3" name="sec-2-3"></a>

[Austin-github](https://github.com/cemerick/austin)
[專案範例](https://github.com/cemerick/austin/tree/master/browser-connected-repl-sample)
在 `~/.lein/profiles.clj` 加入以下兩行

    {:user
     {:plugins [[com.cemerick/austin "0.1.4"]]}}

在你的 cljs 檔案裡的 namespace 新增：

    (:require [clojure.browser.repl])

在 REPL 的環境裡：

    (def repl-env (reset! cemerick.austin.repls/browser-repl-env
                          (cemerick.austin/repl-env)))
    (cemerick.austin.repls/cljs-repl repl-env)

接下來在新的 REPL 環境裡：

    (js/alert "hello browser")

你的 browser 應該會有反應。

## 自動補全<a id="sec-2-4" name="sec-2-4"></a>

[company-mode-github](https://github.com/company-mode/company-mode)

### 安裝：<a id="sec-2-4-1" name="sec-2-4-1"></a>

`M-x package-install` `company`

開啟：
`M-x global-company-mode`

預設開啟：在你的 init.el 加入這行。

    (global-company-mode)

### 使用：<a id="sec-2-4-2" name="sec-2-4-2"></a>

必須在你的 repl 開啟的時候才有效！

`M-n`, `M-p` 上下選擇候選鍵。

![img](//company-mode.github.io/images/company-elisp.png)

# 其他插件推薦<a id="sec-3" name="sec-3"></a>

[rainbow-delimiters](https://github.com/jlr/rainbow-delimiters)

[evil](https://gitorious.org/evil/pages/Home)

[ido](http://www.emacswiki.org/emacs/InteractivelyDoThings)

# 截圖<a id="sec-4" name="sec-4"></a>

![img](/img/emacs-clojure-development.png)
