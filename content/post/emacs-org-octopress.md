+++
date = "2013-08-23T19:57:41+08:00"
title = "Org-mode + Octopress + Github 來搭建 Blog"
tags = ["octopress", "github", "org-mode", "blog"]
categories = ["computer"]
+++


-   優點
    -   免費網域、免費託管、免費流量
    -   版本管理，不用擔心備份！
    -   Org-mode or Markdown 撰寫效率好
-   缺點
    -   技術門檻要求較高   
            需要懂一些 Git, Github, Org-mode 或 Makrdown，更進階要客製化
Blog 的話，可能還要
        懂些許 Ruby (jekyll)
    -   Org-mode 的 code block 沒有 markdown's code block 的 title url
        功能。



<!--more-->

# Org-mode<a id="sec-1" name="sec-1"></a>

> Org mode is for keeping notes, maintaining TODO lists, planning
> projects, and
> authoring documents with a fast and effective plain-text system.   
> **<http://orgmode.org/>**

Org-mode 是建立於 Emacs(編輯器)
之上的插件，是一種輕量級的標記語言可以用來做時間管理、筆記、生成 Html
&#x2026; ，同類型的流行的還有 Markdown，這篇文章基本上就是
Emacs + org-mode 寫的，之後在透過插件
[org-octopress](https://github.com/yoshinari-nomura/org-octopress)
生成給 Octopress 用。

## Install Emacs(24.x)<a id="sec-1-1" name="sec-1-1"></a>

我只會在 Linux 平台上用 Package 裝。

一些流行的 Linux distribution 的 Package Manager 安裝方法。

    pacman -S emacs          # Archlinux
    apt-get install emacs    # Ubuntu
    yum install emacs        # Fedora

## Install org and org-octopress<a id="sec-1-2" name="sec-1-2"></a>

用 Emacs 裡的 Package Manager 安裝：

    # 在家目錄建一個 .emacs.d 資料夾後，在裡面建 init.el
    mkdir ~/.emacs.d
    touch ~/.emacs.d/init.el

在 init.el 添加：

    (add-to-list 'package-archives
      '("marmalade" . "http://marmalade-repo.org/packages/"))
    
    (add-to-list 'package-archives
      '("melpa" . "http://melpa.milkbox.net/packages/") t)
    
    (package-initialize)

開啟 Emacs 鍵入 `M-x package-install org RET` ，把 org 換成
org-octopress 後安裝。

## Org-octopress Setup<a id="sec-1-3" name="sec-1-3"></a>

以下是從
[org-octopress](https://github.com/yoshinari-nomura/org-octopress) 的
README 裡擷取 Basic Settings 的片段。

添加在 init.el。

-   Emacs Settings:

    (require 'org-octopress)
    (setq org-octopress-directory-top       "~/octopress/source")
    (setq org-octopress-directory-posts     "~/octopress/source/_posts")
    (setq org-octopress-directory-org-top   "~/octopress/source")
    (setq org-octopress-directory-org-posts "~/octopress/source/blog")
    (setq org-octopress-setup-file          "~/org-sty/setupfile.org")

-   Octopress Settings:

In octopress/<sub>config</sub>.yml, you must set the permelink
attribute:   
`permalink: /blog/:year-:month-:day-:title.html`

# Octopress<a id="sec-2" name="sec-2"></a>

[Octopress](http://octopress.org/) 是一套 Blog 的框架，所以一開始你的
Blog 就有一個簡潔的外觀，功能上有支援 Twitter, Facebook, Delicious
等等，也可以用來產生靜態 Blog 後放在 Github
上，預設是用 Markdown 來撰寫文章。

## Install and Use Octopress<a id="sec-2-1" name="sec-2-1"></a>

要先安裝 [Ruby](http://www.ruby-lang.org/en/) 和
[Git](http://gitscm.com/)。   
官方的方法： [Octopress Setup](http://octopress.org/docs/setup/)

# Github<a id="sec-3" name="sec-3"></a>

首先有個 [Github](https://github.com/) 的帳號後，建立一個 Repository 為
username.github.io，之後去你的 octopress 的根目錄鍵入 `bundle exec rake
setup_github_page` 輸入剛剛建完給你的 url。

官方文檔: [GithubHelp](https://help.github.com/)

# 基本流程<a id="sec-4" name="sec-4"></a>

1.  開啟 Emacs 鍵入 `M-x org-octopress RET` ，會到 org-octopress
    的界面鍵入 `w`
       和標題，開始撰寫文章。
2.  寫完後，鍵入 `C-c C-e P x octopress` 來生成靜態網頁
3.  在你的 octopress 根目錄鍵入 `bundle exec rake gen_deploy`
4.  也可以把 source branch 下 push 上去做版本管理 `git push -u origin
    source`

文章打到一半或要做確認的時候用(需先生成靜態網頁) `bundle exec rake
preview` ，之後在
<http://localhost:4000/> 可以看你的 Blog。
