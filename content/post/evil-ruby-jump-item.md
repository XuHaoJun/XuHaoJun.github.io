+++
date = "2013-10-19T19:55:09+08:00"
title = "Ruby block match and jump (emacs evil-mode)"
tags = ["emacs", "evil-mode", "ruby"]
categories = ["computer"]
+++


# Description<a id="sec-1" name="sec-1"></a>

Emacs evil-mode `%` 功能加上 Ruby block 的配對，例如將光標放在 `class
Foo` 上後鍵入 `%` 可以跳轉至相符的 `end` 。

<!--more-->

# Example<a id="sec-2" name="sec-2"></a>

![img](/img/evil-ruby-jump-item.gif)

# Source Code<a id="sec-3" name="sec-3"></a>

    ;; Require package: (evil)
    (evil-define-motion evil-ruby-jump-item (count)
      :jump t
      :type inclusive
      (cond ((string-match ruby-block-beg-re (current-word))
             (ruby-end-of-block count))
            ((string-match ruby-block-end-re (current-word))
             (ruby-beginning-of-block count))
            (t
             (evil-jump-item count))))
    
    (add-hook 'ruby-mode-hook
              (lambda ()
                (define-key evil-normal-state-local-map "%" 'evil-ruby-jump-item)
                (define-key evil-motion-state-local-map "%" 'evil-ruby-jump-item)))

