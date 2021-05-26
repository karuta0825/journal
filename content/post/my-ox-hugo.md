+++
title = "ox-hugoの使い方"
author = ["karuta"]
publishDate = 2021-05-26T21:30:00+09:00
tags = ["hugo"]
draft = true
+++

## org-hugoで画像の貼る方法 {#org-hugoで画像の貼る方法}

まずはすでに画像パスがわかってる場合  

`org` ファイルに次のようにlinkパスを書いておくと、自動的に画像をコピーしてくれます。  

```org
#+attr_html: :width 500
[[/Users/karuta/Dropbox/org/img/_today.org_20210526_222951_wAJFn0.png]]
```

{{< figure src="/images/_today.org_20210526_222951_wAJFn0.png" width="500" >}}  

つぎにorg-babelによってコードを評価したあとに画像が挿入される場合  
たとえば、planumlを使用していて、コードを評価した結果の画像を表示したければ、  
いつものように記述するだけでよいです。  

`:exports both` を指定することで画像だけではなく、ソースコードも出力させることができます。  

```plantuml
Entity01 }|..|| Entity02
```

{{< figure src="/images/my.png" >}}
