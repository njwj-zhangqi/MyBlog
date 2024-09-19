---
title: "Emacs init.el配置"
date: 2024-08-30
lastmod: 2024-09-19T09:21:45+08:00
draft: true
---

## 本地模板Local {#本地模板local}

```emacs-lisp
(require 'package)
(setq package-archives '(("gnu"    . "https://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")
                        ("nongnu" . "https://mirrors.tuna.tsinghua.edu.cn/elpa/nongnu/")
                        ("melpa"  . "https://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/")))
(package-initialize)

(when (not package-archive-contents)
  (package-refresh-contents))

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
 '(inhibit-startup-screen t)
 '(org-agenda-files nil)
 '(package-selected-packages
   '(org-pomodoro org-protocol-jekyll org-download pangu-spacing org-roam-ui org-roam-server org-roam doom-themes ws-butler writeroom-mode winum which-key volatile-highlights vim-powerline vi-tilde-fringe uuidgen undo-tree treemacs-projectile treemacs-persp treemacs-icons-dired toc-org term-cursor symon symbol-overlay string-inflection string-edit-at-point spacemacs-whitespace-cleanup spacemacs-purpose-popwin spaceline space-doc restart-emacs request rainbow-delimiters quickrun popwin pcre2el password-generator paradox overseer org-superstar open-junk-file nameless multi-line macrostep lorem-ipsum link-hint info+ indent-guide hungry-delete hl-todo highlight-parentheses highlight-numbers highlight-indentation hide-comnt helm-xref helm-themes helm-swoop helm-purpose helm-projectile helm-org helm-mode-manager helm-make helm-descbinds helm-comint helm-ag google-translate golden-ratio flycheck-package flycheck-elsa flx-ido fancy-battery eyebrowse expand-region evil-visualstar evil-visual-mark-mode evil-unimpaired evil-tutor evil-textobj-line evil-surround evil-numbers evil-nerd-commenter evil-mc evil-matchit evil-lisp-state evil-lion evil-indent-plus evil-goggles evil-exchange evil-args eval-sexp-fu elisp-slime-nav elisp-demos elisp-def editorconfig dumb-jump drag-stuff dotenv-mode dired-quick-sort diminish devdocs define-word column-enforce-mode clean-aindent-mode centered-cursor-mode auto-highlight-symbol auto-compile all-the-icons aggressive-indent ace-link ace-jump-helm-line))
 '(word-wrap t))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )

(use-package all-the-icons
 :if (display-graphic-p))


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

; 引入字体
(set-frame-font "霞鹜文楷等宽-16" nil t)

;设置默认启动目录
(setq default-directory "~/Emacs")
(setq default-directory "~/Emacs")

; 安装yasnipet
(require 'yasnippet)
(yas-global-mode 1)

(setq system-time-locale "C")
; 设置文件编码规则
(setq default-buffer-file-coding-system 'utf-8-unix)
; 设置org文件导出编码格式
(setq org-export-coding-system 'utf-8)
(setq org-log-coding-system 'utf-8)
(prefer-coding-system 'utf-8)
(set-default-coding-systems 'utf-8)
(set-terminal-coding-system 'utf-8)
(set-keyboard-coding-system 'utf-8)
(setq buffer-file-coding-system 'utf-8)
(setq default-buffer-file-coding-system 'utf-8)


(setq org-hugo-base-dir "~/Hugo/")
                                        ; 设置hugo导出的位置

(setq org-hugo-section "posts")
(setq org-hugo-front-matter-format "yaml")

(require 'org-hugo-auto-export-mode)

(use-package ox-hugo
  :ensure t)

; 关闭自动缩进
(electric-indent-mode -1)

; TODO记录时间和日志
(setq org-log-done 'note)
; 设置TODO的工作流
(setq org-todo-keywords
       '((sequence "SOMEDAY(s)" "TODO(t)" "HALF(h)" "PENDING(p)" "|" "DONE(d)" "CANCEL(c)")
        (sequence "WANT_BUY(W)" "BUYED(B)" "WATING(T)" "GETTED(G)")))

(setq org-time-stamp-custom-formats
      '("<%Y-%m-%d %a>" . "<%Y-%m-%d %a %H:%M>"))

;; 定义一个函数来插入当前时间到文件中
(defun now()
  "在光标位置插入当前时间。"
  (interactive)
  (insert (format-time-string "%Y-%m-%d %H:%M")))

;; 定义一个函数来插入当前缓冲区的文件名到文件中
(defun name()
  "在光标位置插入当前缓冲区的文件名。"
  (interactive)
  (if (buffer-file-name)
      (insert (file-name-sans-extension (file-name-nondirectory (buffer-file-name))))
    (insert "<无文件名>")))

; 设置Capture存储文件
;(setq org-default-notes-file  "~/Emcas/GTD/notes.org")


; 配置org-roam
(use-package org-roam
  :ensure t
  :custom
  (org-roam-directory "~/Emacs/org-roam/")
  :bind (("C-c n l" . org-roam-buffer-toggle)
         ("C-c n f" . org-roam-node-find)
         ("C-c n g" . org-roam-graph-show)
         ("C-c n i" . org-roam-node-insert)
         ("C-c n c" . org-roam-capture)
         ("C-c n d" . org-roam-dailies-capture-today))
;  :config
 ; (org-roam-db-autosync-enable))
)

; 设置org-capture和org-agenda的快捷键
(global-set-key (kbd "C-c c") 'org-capture)
(global-set-key (kbd "C-c a") 'org-agenda)

;; 配置 org-capture 模板
(setq org-capture-templates
      '(("c" "create TODO item" entry
         (file+headline "~/Emacs/GTD/task.org" "Tasks") ; 条目添加task.org的Task标题下
         "* TODO %?\n  Added: %U")
        ("s" "create SOMEDAY item" entry
         (file+headline "~/Emacs/GTD/someday.org" "Plans")
         "* SOMEDAY %?\n  Added: %U")
        ("w" "create WANT_BUY item" entry
         (file+headline "~/Emacs/GTD/shopping.org" "Shoppings")
         "* WANT_BUY %?\n  Added: %U")
        ("n" "create Inbox note" entry
         (file+headline "~/Emacs/GTD/inbox.org" "Notes"); 条目添加inbox.org的Notes标题下
         "* %?\n  Added: %U")))

;; 配置 org-agenda从哪些文件读取TODO
(setq org-agenda-files
      '("~/Emacs/GTD/task.org"  "~/Emacs/GTD/project.org"  "~/Emacs/GTD/someday.org" "~/Emacs/GTD/inbox.org"   "~/Emacs/GTD/shopping.org"))

(setq org-refile-targets
      '((my-refile-list :maxlevel . 2))) ; 所有议程文件允许最大3级标题

;; 指定你的GTD文件列表
(setq my-refile-list
      '("~/Emacs/GTD/task.org" "~/Emacs/GTD/inbox.org"
        "~/Emacs/GTD/finished.org" "~/Emacs/GTD/resource.org"
        "~/Emacs/GTD/trash.org"  "~/Emacs/GTD/shopping.org"
        "~/Emacs/GTD/project.org" "~/Emacs/GTD/someday.org"))


;; 禁用备份文件
(setq make-backup-files nil)

;; 禁用自动保存文件
(setq auto-save-default nil)

;(require 'pangu-spacing)

;; 开启 pangu-spacing 模式
;(pangu-spacing-mode 1)
;; 如果你希望在特定模式下启用 pangu-spacing，可以这样做：
;(add-hook 'org-mode-hook 'pangu-spacing-mode)
;(add-hook 'markdown-mode-hook 'pangu-spacing-mode)

;; 可以设置在保存文件时自动调整空格
;(add-hook 'before-save-hook 'pangu-spacing-before-save)

(org-babel-do-load-languages
 'org-babel-load-languages
 '((dot . t)   ; 启用DOT语言支持
   (plantuml . t))) ; 启用PlantUML支持

;(require 'doom-modeline)
;(doom-modeline-mode 1)

; 设置快速打开init.el
(defun open-init-file ()
  "Open the Emacs init file."
  (interactive)
  (find-file "~/.emacs.d/init.el"))

; 配置org-download
(require 'org-download)
;; 设置默认的截图保存目录
(setq org-download-image-dir "~/Emacs/images")
;; 启用Org Mode中的自动插入图片链接
(setq org-download-heading-lvl nil)
(setq org-download-timestamp "%Y-%m-%d-%H-%M-%S-%a_")
(setq org-download-link-format "[[file:%s]]")
;(setq org-download-screenshot-method "screencapture -i %s") ; macOS
;; 如果你使用的是Linux，可以使用下面的命令
; (setq org-download-screenshot-method "import -window root %s") ; Linux
;; Window通过自带的截图工具Snippet Tools
(setq org-download-screenshot-method "powershell -ExecutionPolicy RemoteSigned -File ~/Emacs/scripts/take-screenshot.ps1")
(setq org-download-screenshot-file "/tmp/screenshot.png")

;; 启用org-download
;(org-download-activate)

;启用自动换行
(setq truncate-lines t)

; 打开番茄钟
(require 'org-pomodoro)

;; 添加自定义命令到 org-agenda-custom-commands
;(setq initial-buffer-choice (lambda () (org-agenda nil "a")))

; 设置默认打开文件
(setq initial-buffer-choice
      (lambda ()
        (delete-other-windows)  ; 删除其他窗口
        (find-file "~/Emacs/README.org")))  ; 打开你的 home.org 文件


; 自定义快捷插入模板，获取org-roam中的Node内容
(defun my/org-roam-insert-node-content ()
  "Interactively select an Org-roam node and insert its content (excluding metadata) at point."
  (interactive)
  (let* ((node (org-roam-node-read))  ; 选择节点
         (file-path (org-roam-node-file node))  ; 获取文件路径
         (content (with-temp-buffer
                    (insert-file-contents file-path)
                    (goto-char (point-min))
                    ;; 跳过最多前三行以 : 开头的元数据和 #+ 开头的元数据
                    (let ((lines-skipped 0))
                      (while (and (not (eobp)) (< lines-skipped 4))
                        (cond
                         ((looking-at-p "^\\(:.*\\|#+.*\\)")
                          (forward-line)
                          (setq lines-skipped (1+ lines-skipped)))
                         (t (goto-char (point-max))))))
                    (buffer-substring-no-properties (point) (point-max)))))  ; 获取内容
    (insert content)))  ; 插入内容到当前光标处


(global-set-key (kbd "C-c n t") 'my/org-roam-insert-node-content)

```


## 本地模板Com {#本地模板com}

更新时间: 2024-09-19

```elisp
(require 'package)
(setq package-archives '(("gnu"    . "https://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")
                        ("nongnu" . "https://mirrors.tuna.tsinghua.edu.cn/elpa/nongnu/")
                        ("melpa"  . "https://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/")))
(package-initialize)

(when (not package-archive-contents)
  (package-refresh-contents))

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
 '(inhibit-startup-screen t)
 '(org-agenda-files nil)
 '(package-selected-packages
   '(wordcount-section graphviz-dot-mode org-bullets beancount org-preview-html org-pomodoro org-protocol-jekyll org-download pangu-spacing org-roam-ui org-roam-server org-roam doom-themes ws-butler writeroom-mode winum which-key volatile-highlights vim-powerline vi-tilde-fringe uuidgen undo-tree treemacs-projectile treemacs-persp treemacs-icons-dired toc-org term-cursor symon symbol-overlay string-inflection string-edit-at-point spacemacs-whitespace-cleanup spacemacs-purpose-popwin spaceline space-doc restart-emacs request rainbow-delimiters quickrun popwin pcre2el password-generator paradox overseer org-superstar open-junk-file nameless multi-line macrostep lorem-ipsum link-hint info+ indent-guide hungry-delete hl-todo highlight-parentheses highlight-numbers highlight-indentation hide-comnt helm-xref helm-themes helm-swoop helm-purpose helm-projectile helm-org helm-mode-manager helm-make helm-descbinds helm-comint helm-ag google-translate golden-ratio flycheck-package flycheck-elsa flx-ido fancy-battery eyebrowse expand-region evil-visualstar evil-visual-mark-mode evil-unimpaired evil-tutor evil-textobj-line evil-surround evil-numbers evil-nerd-commenter evil-mc evil-matchit evil-lisp-state evil-lion evil-indent-plus evil-goggles evil-exchange evil-args eval-sexp-fu elisp-slime-nav elisp-demos elisp-def editorconfig dumb-jump drag-stuff dotenv-mode dired-quick-sort diminish devdocs define-word column-enforce-mode clean-aindent-mode centered-cursor-mode auto-highlight-symbol auto-compile all-the-icons aggressive-indent ace-link ace-jump-helm-line))
 '(word-wrap t))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )

(use-package all-the-icons
 :ensure t
 :if (display-graphic-p))


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

; 引入字体
(set-frame-font "霞鹜文楷等宽-16" nil t)

;设置默认启动目录
(setq default-directory "~/Emacs")


; 安装yasnipet
(use-package yasnippet
  :ensure t
  :config
(yas-global-mode 1))


(setq system-time-locale "C")
; 设置文件编码规则
(setq default-buffer-file-coding-system 'utf-8-unix)
; 设置org文件导出编码格式
(setq org-export-coding-system 'utf-8)
(setq org-log-coding-system 'utf-8)
(prefer-coding-system 'utf-8)
(set-default-coding-systems 'utf-8)
(set-terminal-coding-system 'utf-8)
(set-keyboard-coding-system 'utf-8)
(setq buffer-file-coding-system 'utf-8)
(setq default-buffer-file-coding-system 'utf-8)


(setq org-hugo-base-dir "~/Hugo/")
                                        ; 设置hugo导出的位置

(setq org-hugo-section "posts")
(setq org-hugo-front-matter-format "yaml")


;(use-package org-hugo-auto-export-mode
;  :ensure t)


(use-package ox-hugo
  :ensure t)

; 关闭自动缩进
(electric-indent-mode -1)

; TODO记录时间和日志
(setq org-log-done 'note)
; 设置TODO的工作流
(setq org-todo-keywords
       '((sequence "SOMEDAY(s)" "TODO(t)" "HALF(h)" "PENDING(p)" "|" "DONE(d)" "CANCEL(c)")
        (sequence "WANT_BUY(W)" "BUYED(B)" "WATING(T)" "GETTED(G)")))

(setq org-time-stamp-custom-formats
      '("<%Y-%m-%d %a>" . "<%Y-%m-%d %a %H:%M>"))

;; 定义一个函数来插入当前时间到文件中
(defun now()
  "在光标位置插入当前时间。"
  (interactive)
  (insert (format-time-string "%Y-%m-%d %H:%M")))

;; 定义一个函数来插入当前缓冲区的文件名到文件中
(defun name()
  "在光标位置插入当前缓冲区的文件名。"
  (interactive)
  (if (buffer-file-name)
      (insert (file-name-sans-extension (file-name-nondirectory (buffer-file-name))))
    (insert "<无文件名>")))

; 设置Capture存储文件
;(setq org-default-notes-file  "~/Emcas/GTD/notes.org")


; 配置org-roam
(use-package org-roam
  :ensure t
  :custom
  (org-roam-directory "~/Emacs/org-roam/")
  :bind (("C-c n l" . org-roam-buffer-toggle)
         ("C-c n f" . org-roam-node-find)
         ("C-c n g" . org-roam-graph-show)
         ("C-c n i" . org-roam-node-insert)
         ("C-c n c" . org-roam-capture)
         ("C-c n s" . org-roam-tag-add)
         ("C-c n d" . org-roam-dailies-capture-today))
  :config
  (org-roam-db-autosync-enable)

)

; 设置org-capture和org-agenda的快捷键
(global-set-key (kbd "C-c c") 'org-capture)
(global-set-key (kbd "C-c a") 'org-agenda)


;; 配置 org-capture 模板
(setq org-capture-templates
      '(("c" "create TODO item" entry
         (file+headline "~/Emacs/GTD/task.org" "Tasks") ; 条目添加task.org的Task标题下
         "* TODO %?\n  Added: %U")
        ("s" "create SOMEDAY item" entry
         (file+headline "~/Emacs/GTD/someday.org" "Plans")
         "* SOMEDAY %?\n  Added: %U")
        ("w" "create WANT_BUY item" entry
         (file+headline "~/Emacs/GTD/shopping.org" "Shoppings")
         "* WANT_BUY %?\n  Added: %U")
        ("n" "create Inbox note" entry
         (file+headline "~/Emacs/GTD/inbox.org" "Notes"); 条目添加inbox.org的Notes标题下
         "* %?\n  Added: %U")))

;; 配置 org-agenda从哪些文件读取TODO
(setq org-agenda-files
      '("~/Emacs/GTD/task.org"  "~/Emacs/GTD/project.org"  "~/Emacs/GTD/someday.org" "~/Emacs/GTD/inbox.org"   "~/Emacs/GTD/shopping.org"))

(setq org-refile-targets
      '((my-refile-list :maxlevel . 2))) ; 所有议程文件允许最大3级标题

;; 指定你的GTD文件列表
(setq my-refile-list
      '("~/Emacs/GTD/task.org" "~/Emacs/GTD/inbox.org"
        "~/Emacs/GTD/finished.org" "~/Emacs/GTD/resource.org"
        "~/Emacs/GTD/trash.org"  "~/Emacs/GTD/shopping.org"
        "~/Emacs/GTD/project.org" "~/Emacs/GTD/someday.org"))


;; 禁用备份文件
(setq make-backup-files nil)

;; 禁用自动保存文件
(setq auto-save-default nil)

;(require 'pangu-spacing)

;; 开启 pangu-spacing 模式
;(pangu-spacing-mode 1)
;; 如果你希望在特定模式下启用 pangu-spacing，可以这样做：
;(add-hook 'org-mode-hook 'pangu-spacing-mode)
;(add-hook 'markdown-mode-hook 'pangu-spacing-mode)

;; 可以设置在保存文件时自动调整空格
;(add-hook 'before-save-hook 'pangu-spacing-before-save)

(org-babel-do-load-languages
 'org-babel-load-languages
 '((dot . t)   ; 启用DOT语言支持
   (plantuml . t))) ; 启用PlantUML支持

;(require 'doom-modeline)
;(doom-modeline-mode 1)

; 设置快速打开init.el
(defun open-init-file ()
  "Open the Emacs init file."
  (interactive)
  (find-file "~/.emacs.d/init.el"))

; 配置org-download
(require 'org-download)
;; 设置默认的截图保存目录
(setq org-download-image-dir "~/Emacs/images")
;; 启用Org Mode中的自动插入图片链接
(setq org-download-heading-lvl nil)
(setq org-download-timestamp "%Y-%m-%d-%H-%M-%S-%a_")
(setq org-download-link-format "[[file:%s]]")
;(setq org-download-screenshot-method "screencapture -i %s") ; macOS
;; 如果你使用的是Linux，可以使用下面的命令
; (setq org-download-screenshot-method "import -window root %s") ; Linux
;; Window通过自带的截图工具Snippet Tools
(setq org-download-screenshot-method "powershell -ExecutionPolicy RemoteSigned -File ~/Emacs/scripts/take-screenshot.ps1")
(setq org-download-screenshot-file "/tmp/screenshot.png")

;; 启用org-download
;(org-download-activate)

;启用自动换行
(setq truncate-lines t)

; 打开番茄钟
(use-package org-pomodoro
  :ensure t)

;; 添加自定义命令到 org-agenda-custom-commands
;(setq initial-buffer-choice (lambda () (org-agenda nil "a")))

; 设置默认打开文件
(setq initial-buffer-choice
      (lambda ()
        (delete-other-windows)  ; 删除其他窗口
        (find-file "~/Emacs/README.org")))  ; 打开你的 home.org 文件


; 自定义快捷插入模板，获取org-roam中的Node内容
(defun my/org-roam-insert-node-content ()
  "Interactively select an Org-roam node and insert its content (excluding metadata) at point."
  (interactive)
  (let* ((node (org-roam-node-read))  ; 选择节点
         (file-path (org-roam-node-file node))  ; 获取文件路径
         (content (with-temp-buffer
                    (insert-file-contents file-path)
                    (goto-char (point-min))
                    ;; 跳过最多前三行以 : 开头的元数据和 #+ 开头的元数据
                    (let ((lines-skipped 0))
                      (while (and (not (eobp)) (< lines-skipped 4))
                        (cond
                         ((looking-at-p "^\\(:.*\\|#+.*\\)")
                          (forward-line)
                          (setq lines-skipped (1+ lines-skipped)))
                         (t (goto-char (point-max))))))
                    (buffer-substring-no-properties (point) (point-max)))))  ; 获取内容
    (insert content)))  ; 插入内容到当前光标处


(global-set-key (kbd "C-c n t") 'my/org-roam-insert-node-content)

;;; org-download
(use-package org-download
  :ensure t)

;(setq org-download-screenshot-method "flameshot gui --raw >%s")
(setq org-download-method 'directory)
(setq-default org-download-heading-lvl nil)
(setq-default org-download-image-dir "./images")
(defun dummy-org-download-annotate-function (link)
  "")
(setq org-download-annotate-function
      #'dummy-org-download-annotate-function)


(setq org-roam-capture-templates
      '(("d" "default" plain
         "%?"
         :if-new (file+head "${slug}-%<%Y%m%d%H%M%S>.org"
                            "#+title: ${title}\n#+date: %U\n#+filetags: \n\n")
         :unnarrowed t)
("e" "Emacs" plain
         "%?"
         :if-new (file+head "${slug}-%<%Y%m%d%H%M%S>.org"
                            "#+title: ${title}\n#+date: %U\n#+filetags: :Emacs: \n\n")
         :unnarrowed t)
("p" "Photo" plain
         "%?"
         :if-new (file+head "${slug}-%<%Y%m%d%H%M%S>.org"
                            "#+title: ${title}\n#+date: %U\n#+filetags: :Photo: \n\n")
         :unnarrowed t)
("f" "Fit" plain
         "%?"
         :if-new (file+head "${slug}-%<%Y%m%d%H%M%S>.org"
                            "#+title: ${title}\n#+date: %U\n#+filetags: :Fit: \n\n")
         :unnarrowed t)
("t" "Treking" plain
         "%?"
         :if-new (file+head "${slug}-%<%Y%m%d%H%M%S>.org"
                            "#+title: ${title}\n#+date: %U\n#+filetags: :Treking: \n\n")
         :unnarrowed t)
("k" "Info" plain
         "%?"
         :if-new (file+head "${slug}-%<%Y%m%d%H%M%S>.org"
                            "#+title: ${title}\n#+date: %U\n#+filetags: :PKM: \n\n")
         :unnarrowed t)
))

;(use-package org-protocol
;  :ensure t)

; 顶部菜单栏
(menu-bar-mode 0)
; 顶部工具栏
(tool-bar-mode 0)

; 打开beancount配置
;(add-to-list 'load-path "~/.emcas.d/elpa/beancount-0.9")
(use-package beancount
  :ensure t)

(add-to-list 'auto-mode-alist '("\\.beancount\\'" . beancount-mode))

; 开启graphviz配置
(use-package graphviz-dot-mode
:ensure t
:config
(setq graphviz-dot-indent-width 4))

;(use-package company-graphviz-dot)


; 开启图片展示功能
;(auto-image-file-mode t)

;(add-to-list 'load-path "~/.emacs.d/site-lisp/dictionary-overlay/")
;(require 'dictionary-overlay)
```
