# What is grammatical-edit.el ?
grammatical-edit.el is a plugin that provides grammatical edit base on tree-sitter.

## Installation
1. Install tree-sitter first: https://emacs-tree-sitter.github.io/installation/
2. Clone or download this repository (path of the folder is the `<path-to-grammatical-edit>` used below).

In your `~/.emacs`, add the following two lines:
```Elisp
(add-to-list 'load-path "<path-to-grammatical-edit>") ; add grammatical-edit to your load-path
(require 'grammatical-edit)
```

## Enabled in the specified programming language
Not all programming languages ​​are suitable for parenthesis auto-completion.
You can add grammatical-edit.el to the programming language mode like below:

```Elisp
(dolist (hook (list
               'c-mode-common-hook
               'c-mode-hook
               'c++-mode-hook
               'java-mode-hook
               'haskell-mode-hook
               'emacs-lisp-mode-hook
               'lisp-interaction-mode-hook
               'lisp-mode-hook
               'maxima-mode-hook
               'ielm-mode-hook
               'sh-mode-hook
               'makefile-gmake-mode-hook
               'php-mode-hook
               'python-mode-hook
               'js-mode-hook
               'go-mode-hook
               'qml-mode-hook
               'jade-mode-hook
               'css-mode-hook
               'ruby-mode-hook
               'coffee-mode-hook
               'rust-mode-hook
               'qmake-mode-hook
               'lua-mode-hook
               'swift-mode-hook
               'minibuffer-inactive-mode-hook
               'typescript-mode-hook
               ))
  (add-hook hook '(lambda () (grammatical-edit-mode 1))))
```

Then binding below grammatical-edit.el commands with below keystrokes:

```Elisp
(define-key grammatical-edit-mode-map (kbd "(") 'grammatical-edit-open-round)
(define-key grammatical-edit-mode-map (kbd "[") 'grammatical-edit-open-bracket)
(define-key grammatical-edit-mode-map (kbd "{") 'grammatical-edit-open-curly)
(define-key grammatical-edit-mode-map (kbd ")") 'grammatical-edit-close-round)
(define-key grammatical-edit-mode-map (kbd "]") 'grammatical-edit-close-bracket)
(define-key grammatical-edit-mode-map (kbd "}") 'grammatical-edit-close-curly)
(define-key grammatical-edit-mode-map (kbd "=") 'grammatical-edit-equal)

(define-key grammatical-edit-mode-map (kbd "%") 'grammatical-edit-match-paren)
(define-key grammatical-edit-mode-map (kbd "\"") 'grammatical-edit-double-quote)
(define-key grammatical-edit-mode-map (kbd "'") 'grammatical-edit-single-quote)

(define-key grammatical-edit-mode-map (kbd "SPC") 'grammatical-edit-space)
(define-key grammatical-edit-mode-map (kbd "RET") 'grammatical-edit-newline)

(define-key grammatical-edit-mode-map (kbd "M-o") 'grammatical-edit-backward-delete)
(define-key grammatical-edit-mode-map (kbd "C-d") 'grammatical-edit-forward-delete)
(define-key grammatical-edit-mode-map (kbd "C-k") 'grammatical-edit-kill)

(define-key grammatical-edit-mode-map (kbd "M-\"") 'grammatical-edit-wrap-double-quote)
(define-key grammatical-edit-mode-map (kbd "M-'") 'grammatical-edit-wrap-single-quote)
(define-key grammatical-edit-mode-map (kbd "M-[") 'grammatical-edit-wrap-bracket)
(define-key grammatical-edit-mode-map (kbd "M-{") 'grammatical-edit-wrap-curly)
(define-key grammatical-edit-mode-map (kbd "M-(") 'grammatical-edit-wrap-round)
(define-key grammatical-edit-mode-map (kbd "M-)") 'grammatical-edit-unwrap)

(define-key grammatical-edit-mode-map (kbd "M-p") 'grammatical-edit-jump-right)
(define-key grammatical-edit-mode-map (kbd "M-n") 'grammatical-edit-jump-left)
(define-key grammatical-edit-mode-map (kbd "M-:") 'grammatical-edit-jump-out-pair-and-newline)
```

### Make tree-sitter to support elisp

```
1. git clone https://github.com/Wilfred/tree-sitter-elisp
2. gcc ./src/parser.c -fPIC -I./ --shared -o elisp.so
3. cp ./elisp.so ~/.tree-sitter-langs/bin (~/.tree-sitter-langs/bin is path of your tree-sitter-langs repo)
(tree-sitter-load 'elisp "elisp")
(add-to-list 'tree-sitter-major-mode-language-alist '(emacs-lisp-mode . elisp))
```
### Make tree-sitter to support vue

```
1. git clone https://github.com/ikatyang/tree-sitter-vue.git
2. gcc ./src/parser.c ./src/scanner.cc -fPIC -I./ --shared -o vue.so
3. cp ./vue.so ~/.tree-sitter-langs/bin (~/.tree-sitter-langs/bin is path of your tree-sitter-langs repo)
(tree-sitter-load 'vue "vue")
(add-to-list 'tree-sitter-major-mode-language-alist '(web-mode . vue))
```

### Make tree-sitter to support Typescript

```
1. git clone https://github.com/tree-sitter/tree-sitter-typescript.git
2. gcc ./tsx/src/parser.c ./tsx/src/scanner.cc -fPIC -I./ --shared -o typescript.so
3. cp ./typescript.so ~/.tree-sitter-langs/bin (~/.tree-sitter-langs/bin is path of your tree-sitter-langs repo)
(tree-sitter-load 'typescript "typescript")
(add-to-list 'tree-sitter-major-mode-language-alist '(typescript-mode . typescript))
```

More config about tree-sitter can refer to [my profile](https://github.com/manateelazycat/lazycat-emacs/blob/master/site-lisp/config/init-tree-sitter.el)
