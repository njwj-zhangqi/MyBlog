---
title: "Emacs配置篇"
lastmod: 2024-08-29T17:45:17+08:00
categories: ["Emacs"]
draft: true
---

## 前言 {#前言}

前提：Windows下的Emacs的默认配置，放在 `C:\Users\{UserName}\AppData\Roaming\.emacs.d` 目录下，以下操作都基于此目录，用 `~` 表示

如果没有新建过 `~/init.el` 文件，默认是不存在的。新建txt文档，改成 `init.el` ，使用Emacs打开。


## 插件配置 {#插件配置}

使用清华大学的镜像源：

```emacs-lisp
;; 设置插件管理器源
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

这是注释

```emacs-lisp
;; 设置文件编码规则
(setq default-buffer-file-coding-system 'utf-8-unix)
;; 设置org文件导出编码格式
(setq org-export-coding-system 'utf-8)
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
