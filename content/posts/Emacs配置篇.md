---
title: "Emacs配置篇"
date: 2024-09-11T14:35:00+08:00
lastmod: 2024-09-19T09:22:57+08:00
draft: true
---

## 前言 {#前言}

前提：Windows下的Emacs配置，默认放在 `C:\Users\{User}\AppData\Roaming\.emacs.d`
AppData是隐藏目录，需要在 “查看”中勾选“隐藏的项目”来打开。


### Windows设置home环境变量 {#windows设置home环境变量}

为了保持Linux、Windows、Mac OS下配置文件的统一，需要在Windows下设置 `home` 环境变量，变量值为 `C:\Users\{User}`

以下配置都将以 `C:\Users\{User}\.emacs.d` 作为最终配置文件夹，请务必检查。

如果没有新建过 `~/init.el` 文件，默认是不存在的。新建txt文档，改成 `init.el` ，使用Emacs打开。
注意： `init.el` 与 `.emacs` 是冲突的，如果在 `home` 下存在 `.emcas` 文件，请删除。


## 插件配置 {#插件配置}

由于Emacs插件的下载地址都在国外，下载速度很慢，因此首先替换插件下载源，将以下代码放在 `init.el` 最上面。

```emacs-lisp
  ;; 设置插件管理器源
  ;使用清华大学的镜像源
  (require 'package)
  (package-initialize)
  (setq package-archives '(("gnu"    . "https://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")
                           ("nongnu" . "https://mirrors.tuna.tsinghua.edu.cn/elpa/nongnu/")
                           ("melpa"  . "https://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/"))
      ;; 使用use-package
(unless (package-installed-p 'use-package)
     (package-refresh-contents)
     (package-install 'use-package))
(eval-when-compile
      (require 'use-package))
```


## 文件格式配置 {#文件格式配置}

```emacs-lisp

  ;; 设置文件编码规则
  (setq default-buffer-file-coding-system 'utf-8-unix)
  ;; 设置org文件导出编码格式
  (setq org-export-coding-system 'utf-8)
(prefer-coding-system 'utf-8)
(set-default-coding-systems 'utf-8)
(set-terminal-coding-system 'utf-8)
(set-keyboard-coding-system 'utf-8)
(setq buffer-file-coding-system 'utf-8)
(setq default-buffer-file-coding-system 'utf-8)

```


## ox-hugo配置 {#ox-hugo配置}

以下是ox-hugo插件的配置

```emacs-lisp
(setq org-hugo-base-dir "D:/Workspace/Hugo/")

;; 设置默认的Hugo站点配置文件（如果你的站点配置文件不是默认的config.toml）
(setq org-hugo-section "posts")  ; 默认的Hugo内容部分

  ;; 设置默认的Hugo Front Matter变量
(setq org-hugo-front-matter-format "yaml")  ; 或者 "toml" 或 "json"
;(setq org-hugo-export-with-toc t)           ; 是否导出带有目录的文件
;(setq org-hugo-export-with-section-numbers nil) ; 是否导出带有章节编号的文件
(use-package ox-hugo
  :ensure t)  ; 确保ox-hugo包已安装
```


## 模块化配置 {#模块化配置}

在 `init.el` 文件中只需要引入其他配置文件，将具体的配置分别放在各自的文件中。

创建一个 `~/lisp/hello.el` 文件，代码如下：

```emacs-lisp
;; 定义一个hello-world函数
(defun hello-world())
(interactive)
(message "Hello, Emacs"))

;; 导出本模块
(provide 'hello)
```


## 时间和文件名配置 {#时间和文件名配置}

```emacs-lisp
;; 定义一个函数来插入当前时间到文件中
(defun now()
  "在光标位置插入当前时间。"
  (interactive)
  (insert (format-time-string "%Y-%m-%d %H:%M")))

;; 定义一个函数来插入当前缓冲区的文件名到文件中
(defun file()
  "在光标位置插入当前缓冲区的文件名。"
  (interactive)
  (if (buffer-file-name)
      (insert (file-name-sans-extension (file-name-nondirectory (buffer-file-name))))
    (insert "<无文件名>")))
```
