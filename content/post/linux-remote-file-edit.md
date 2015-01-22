+++
date = "2014-05-15T18:47:07+08:00"
title = "Linux 遠程文件編輯"
tags = ["linux", "remote"]
categories = ["computer"]
+++


大部分都是 ssh
連線過去使用那邊的環境來修改檔案，如果遠程環境沒有稱手的編輯器可是一件很惱人的一件事，所以找了一些方法在本地編輯文件。

# SSH Filesystem<a id="sec-1" name="sec-1"></a>

[sshfs](http://fuse.sourceforge.net/sshfs.html)
是將遠程的文件系統掛載在本地，之後就可以在本地編輯了，也會同步更新上去。

<!--more-->

## Example:<a id="sec-1-1" name="sec-1-1"></a>

下面的命令會將遠程的家目錄掛載在你本地的 `~/dir` 。

    sshfs user@yourdomain:/home/user ~/dir

之後就可以隨心所欲的編輯 `~/dir` 之下的東西了，當然不侷限於來編輯，像是
gimp、
mplayer 什麼的都可以！

# Emacs TRAMP<a id="sec-2" name="sec-2"></a>

[TRAMP](https://www.gnu.org/software/tramp/) 是在 Emacs
之下來遠程編輯文件的東西。

## Example:<a id="sec-2-1" name="sec-2-1"></a>

在 Emacs 之下 `M-x find-file` 後輸入 `/ssh:user@yourdomain` 然後 Enter
鍵，就會看到你的家目錄會以 `dired-mode`
的形式開啟，之後選擇你的檔案來編輯！

# 總結<a id="sec-3" name="sec-3"></a>

如果本地環境允許的話就安裝 `sshfs` 吧！這樣方便許多 `Emacs TRAMP`
只能用來編輯文件，而 `sshfs` 則不只用來編輯文件，用來看遠程的 pdf
或影音檔或 copy 檔案都很方便！
