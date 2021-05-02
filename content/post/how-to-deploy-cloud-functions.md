+++
title = "Cloud Functionsつかってみる"
author = ["karuta"]
date = 2021-05-02T18:14:00+09:00
publishDate = 2021-05-02T16:00:00+09:00
tags = ["GCP"]
draft = false
summary = "deployとルーティングについて"
+++

## GCPアカウントを変更する {#gcpアカウントを変更する}

以下をshellで叩くと、認証画面に遷移するので任意のアカウントを選択して変更する  

```sh
gcloud auth login
```


## Cloud Functionsのregion設定 {#cloud-functionsのregion設定}

regionを変更する場合は、 `gcloud config set` で変更できる。  

```nil
gcloud config set functions/region asia-east2
```

リージョン詳細はこちら  
<https://cloud.google.com/functions/docs/locations?hl=ja>  


## デプロイ方法 {#デプロイ方法}

これではうまくいかないことがわかった。  

```sh
gcloud functions deploy sample2 --runtime nodejs12 --trigger-http
```

これでうまくいった。 `entry-point` にindex.jsの関数名をつかえばよい。  

```sh
gcloud functions deploy sample2 --entry-point helloWorld --runtime nodejs12 --trigger-http
```


## Routingを使用する {#routingを使用する}

特定のルートに対してどのようなHTTPメソッドが叩かれたときに、どういう処理をさせるかというルーティング制御は  
`express` をインストールして以下のように書けばよい。  

```js
const express = require('express');
const app = express();
app.get("/...", function (req, res) { ... })
app.post("/...", function (req, res) { ... })
```
