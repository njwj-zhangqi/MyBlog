---
title: "org-roam使用"
date: 2024-08-31T14:02:00+08:00
lastmod: 2024-09-19T09:23:43+08:00
categories: ["Emacs"]
draft: true
---

## org-roam配置 {#org-roam配置}

```emacs-lisp
(use-package org-roam
  :ensure t
  :custom
  (org-roam-directory "~/Emacs/org/roam/")
  :bind (("C-c n l" . org-roam-buffer-toggle)
         ("C-c n f" . org-roam-node-find) ; 查找Node
         ("C-c n g" . org-roam-graph-show) ;展示graph vie
         ("C-c n i" . org-roam-node-insert) ;插入链接
         ("C-c n c" . org-roam-capture) ;新建Node
         ("C-c n d" . org-roam-dailies-capture-today)) ;开启org-roam日记功能
  :config
  (org-roam-db-autosync-enable))
```

配置指定的目录，以及绑定对应的快捷键。


### 安装org-roam-ui {#安装org-roam-ui}

org-roam-ui会在本地启动一个Web页面，用于展示图谱和Node

安装命令： `M-x package-install org-roam-ui`
使用: `M-x org-roam-ui-mode RET`


### 开启org-roam日记功能 {#开启org-roam日记功能}

```emacs-lisp
("C-c n d" . org-roam-dailies-capture-today)) ;开启org-roam日记功能
```

在上面的配置中已经包含，实际上只需要绑定一个快捷键即可。


## org-roam快捷键 {#org-roam快捷键}

| 快捷键  | 功能                |
|------|-------------------|
| C-c n c | 创建一个Node        |
| C-c n i | 插入一个链接，如果不存在则创建Node |
| C-c n f | 查找Node            |
|         |                     |
