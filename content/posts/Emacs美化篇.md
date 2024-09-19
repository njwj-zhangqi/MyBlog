---
title: "Emacs美化篇"
date: 2024-09-11T14:31:00+08:00
lastmod: 2024-09-19T09:22:50+08:00
draft: true
---

强烈推荐优先引入霞鹜文楷字体和doom-one主题，能让Emacs编辑体验上升一个台阶。


## 引入霞鹜文楷字体 {#引入霞鹜文楷字体}


### 下载字体文件 {#下载字体文件}

Windows首先从 [霞鹜文楷Github Release](https://github.com/lxgw/LxgwWenKai/releases) 下载最新的字体文件，然后复制到 `C:\Windows\Fonts` 目录下，即可安装完成。


### 添加字体配置 {#添加字体配置}

修改 `init.el`

```emacs-lisp
; 设置字体
(set-frame-font "霞鹜文楷等宽-16" nil t)
```


## 安装doom-one主题 {#安装doom-one主题}

由于doom-one主题是在doom-themes主题下，因此需要先安装doom-themes主题。安装步骤如下：

1.  `M-x` package-install
2.  输入doom-themes
3.  修改 `init.el` 配置
    ```emacs-lisp

    (use-package doom-themes
     :ensure t
     :config
     ;; Global settings (defaults)
     (setq doom-themes-enable-bold nil  ; if nil, bold is universally disabled
            doom-themes-enable-italic t) ; if nil, italics is universally disabled
     (load-theme 'doom-monokai-octagon t)
     (doom-themes-treemacs-config))
    (custom-set-variables
     ;; custom-set-variables was added by Custom.
     ;; If you edit it by hand, you could mess it up, so be careful.
     ;; Your init file should contain only one such instance.
     ;; If there is more than one, they won't work right.
     '(package-selected-packages
       '(doom-themes ws-butler writeroom-mode winum which-key volatile-highlights vim-powerline vi-tilde-fringe uuidgen undo-tree treemacs-projectile treemacs-persp treemacs-icons-dired toc-org term-cursor symon symbol-overlay string-inflection string-edit-at-point spacemacs-whitespace-cleanup spacemacs-purpose-popwin spaceline space-doc restart-emacs request rainbow-delimiters quickrun popwin pcre2el password-generator paradox overseer org-superstar open-junk-file nameless multi-line macrostep lorem-ipsum link-hint info+ indent-guide hungry-delete hl-todo highlight-parentheses highlight-numbers highlight-indentation hide-comnt helm-xref helm-themes helm-swoop helm-purpose helm-projectile helm-org helm-mode-manager helm-make helm-descbinds helm-comint helm-ag google-translate golden-ratio flycheck-package flycheck-elsa flx-ido fancy-battery eyebrowse expand-region evil-visualstar evil-visual-mark-mode evil-unimpaired evil-tutor evil-textobj-line evil-surround evil-numbers evil-nerd-commenter evil-mc evil-matchit evil-lisp-state evil-lion evil-indent-plus evil-goggles evil-exchange evil-args eval-sexp-fu elisp-slime-nav elisp-demos elisp-def editorconfig dumb-jump drag-stuff dotenv-mode dired-quick-sort diminish devdocs define-word column-enforce-mode clean-aindent-mode centered-cursor-mode auto-highlight-symbol auto-compile all-the-icons aggressive-indent ace-link ace-jump-helm-line)))
    (custom-set-faces
     ;; custom-set-faces was added by Custom.
     ;; If you edit it by hand, you could mess it up, so be careful.
     ;; Your init file should contain only one such instance.
     ;; If there is more than one, they won't work right.
     )

    (use-package all-the-icons
     :if (display-graphic-p))


    (setq custom-file "~/.emacs.d/lisp/init-theme.el")
    (load custom-file)

    (require 'doom-themes)

    ;; Global settings (defaults)
    (setq doom-themes-enable-bold t    ; if nil, bold is universally disabled
          doom-themes-enable-italic t) ; if nil, italics is universally disabled

    ;; Load the theme (doom-one, doom-molokai, etc); keep in mind that each theme
    ;; may have their own settings.
    (load-theme 'doom-one t)

    ;; Enable flashing mode-line on errors
    (doom-themes-visual-bell-config)

    ;; Enable custom neotree theme (all-the-icons must be installed!)
    (doom-themes-neotree-config)
    ;; or for treemacs users
    (setq doom-themes-treemacs-theme "doom-colors") ; use "doom-colors" for less minimal icon theme
    (doom-themes-treemacs-config)

    ;; Corrects (and improves) org-mode's native fontification.
    (doom-themes-org-config)
    ```
