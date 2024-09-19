---
title: "Org-mode的TODO使用"
date: 2024-08-30T16:48:00+08:00
lastmod: 2024-09-19T09:23:32+08:00
draft: true
---

任何标题都可以在前面加上 `TODO` 来变成一个TODO Item。


## DONE-this is a todo {#done-this-is-a-todo}

-   `C-c C-t`  `S-Right` `S-Left` : 在"标题"=&gt;"TODO"=&gt;"DONE"状态间切换
-   `C-c / t` : 将TODO进行树状图展示

-   `M-x org-agenda t` :使用org-agenda展示
-   `S-M-RET` : 插入一个新的TODO


## TODO相关配置 {#todo相关配置}


### 设置状态和工作流 {#设置状态和工作流}

通过org-todo-keywords设置多种状态和不同的工作流

```emacs-lisp
(setq org-todo-keywords
      '((sequence "TODO(t)" "PROCESSING(p)" "|" "DONE(d)" "CANCEL(c)")
        (sequence "WANT(w)" "Buyed(b)" "TRANSPORTING(T)" "GET(g)")))
```

其中的"|"用来区分完成状态的。在"|"之前，表示未完成状态，不会置灰，在"|"之后，表示完成状态，会置灰。


### 添加时间戳日志 {#添加时间戳日志}

当状态从未完成状态，包括TODO和PROCESSING，切换到完成状态（DONE、CACNEL）时，产生一个时间戳，用来记录完成时间点。

```emacs-lisp
; 第一种格式，只记录时间
(setq org-log-done 'time)
; 第二种格式，记录时间，还有完成的笔记
(setq org-log-done 'note)
```


### 单独设置状态的时间戳和日志 {#单独设置状态的时间戳和日志}

由于time和note会将每个状态转换时都只记录时间或者都记录笔记，实际上创建状态不需要记录Note，DONE的状态才需要，
因此需要单独定义每个状态是否记录日志和时间

```emacs-lisp
(setq org-todo-keywords
      '((sequence "TODO(t!)" "PROCESSING(p!)" "|" "DONE(d@/!)" "CANCEL(c@/!)")
        (sequence "WANT(w)" "Buyed(b)" "TRANSPORTING(T)" "GET(g)")))
```

其中 `@` 代表记录日志, `!` 代表记录时间戳， `@/!` 表示两种都记录。


## TODO使用 {#todo使用}


### 设置TODO优先级 {#设置todo优先级}

;\*\*\* TODO [#A] 测试标题

A,B,C三个优先级，默认优先级为B


### 复选框 {#复选框}

待办事项下的复选框，不会被统计到全局的待办事项中，因此可以当作小任务或者步骤。

```org
* TODO 旅行
** TODO 买票
   - [X] 定闹钟
   - [ ] 付钱
** TODO 出发
```
