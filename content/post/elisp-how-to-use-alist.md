+++
title = "elispの連想配列の操作方法を整理する"
author = ["karuta"]
publishDate = 2021-06-12T00:00:00+09:00
draft = false
+++

## 連想配列とはなにか？ {#連想配列とはなにか}

コンスセルを要素とする配列のこと。コンスセルとは、 `(値1 . 値2)` のようにドットでペアをつくるデータ構造コンスセルの左側の値を取得する方法は、 `car` であり、右側を取得する方法は、 `cdr` となる。  

この左側をkeyして右側をvalueとして利用したのが、emacs-lispの連想配列である。  

<!--more-->  


## Get {#get}

-   keyからコンスセルを取得する  
    
    `assq`, `assoc` を利用する  
    
    ```elisp
    (setq alist '((one . 1)))
    (assq 'one alist) 
    ; => (one . 1)
    ```

-   値からコンスセルを取得する  
    
    `rassq`, `rassoc` を利用する  
    
    ```elisp
    (setq alist '((one . 1)))
    (rassq 1 alist) 
    ; => (one . 1)
    ```

-   keyからコンスセルのvalueを取得する  
    
    ```elisp
    (setq alist '((one . 1)))
    (assoc-default 'one alist) ; => 1
    ```


## Set {#set}

valueを変更する  

```elisp
(setq alist '((one . 1)))
(setf (cdr (assoc 'one alist)) 11) ; => x
alist 
; => ((one . 11))
```


## 追加する {#追加する}

先頭に追加する  

```emacs-lisp
(setq alist '((one . 1)))
(add-to-list 'alist '(two . 2))
; => ((two . 2) (one . 1))
```

後ろから追加する  

```elisp
(setq alist '((one . 1)))
(append alist '((two . 2)))
; => ((one . 1) (two . 2))
```


## 削除する {#削除する}

これはイミュータブルである。ちょっと癖があるが、削除したいものをしているするために、 `assco` を利用しないといけない。  

```emacs-lisp
(setq alist '((one . 1) (two . 2)))
(delete (assoc 'one alist) alist)
; => ((two . 2))
```
