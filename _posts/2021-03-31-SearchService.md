---
layout: post
title:  "[検索機能]検索機能におけるURLの特徴と活用例"
date:   2021-03-31 23:59:00 +0900
description: 複数のサイトの検索を、同じページからできるようにした検索ポータル,およびそれを簡単に作れる理由である検索サービスのURL構造
categories: jekyll update
tags: 技術ネタ
---

**目次**
- TOC
{:toc}

# はじめに
世の中にはGoogle,Yahoo等検索サービスがたくさんあります。  
さらに、検索サービス以外のwebサービスでも、Youtube,Twitter等それぞれの中での検索機能を持っているものがたくさんあります。  
それらの多くにはあるURLの特徴があります。  

# URLの特徴
Googleで"Qiita"を検索する場合、"Qiita"を入力欄に入れたうえで検索処理を実行します。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/e9f8fb24-956d-0728-52f4-4144fba53c6a.png)  
その結果は以下のように検索結果ページに遷移し表示されます。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/7c98d684-ce76-5c7c-a7ff-1a7490e64a33.png)  
そのページのURLは下記のとおり

```
https://www.google.co.jp/search?q=qiita&sxsrf=… ※以下省略
```

URLの中に検索ワード"Qiita"が入っています。ここで入っている"qiita"の役割はもちろん検索ワードであり、  
これを"Java"に変えてみると…"Java"の検索結果が表示されます。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/b8a55731-7999-83c7-ceed-5c90512acdb0.png)
これはyahoo,youtube,twitter等でも同じです。  

```
Google
https://www.google.com/search?q=[検索文]
Yahoo
https://search.yahoo.co.jp/search?p=[検索文]
bing
https://www.bing.com/search?q=[検索文]
wikipedia
https://ja.wikipedia.org/w/index.php?search=[検索文]

Youtube
https://www.youtube.com/results?search_query=[検索文]
niconico
https://www.nicovideo.jp/search/[検索文]

twitter
https://twitter.com/search?q=[検索文]
facebook
https://www.facebook.com/search/top?q=[検索文]
```

## この特徴は何者か
各検索機能のURLにある"q=[検索文]"のような部分はクエリストリング（クエリ文字列、URLパラメータ、リクエストパラメータ）です。  
クエリストリングによって表示する検索ワードを検索機能に渡しています。  
HTTPの2メソッド、GET/POSTのうち、クエリストリングはGETメソッドのみ入ります。

各検索機能でGETメソッドを使っている理由は、サイトの閲覧履歴に検索結果を残すためです。  
[こちらも参照：HTTPとは？GETとPOST？](https://qiita.com/norichang/items/7dcb2aedbb67fab341cc)    
検索結果のページは履歴から再閲覧・ブラウザバックで再表示できると便利ですよね。  

## この特徴の活用例
この特徴は、検索ポータル(ポータルサイト)を作るときに活用できます。  
検索ポータルは、インターネットに検索でアクセスするときの入り口となるWebサイトで、  
URLの特徴を生かすことで、複数のサイトでの検索を1つのフォームで切り替え実行できます。  
仕組みはクエリストリングの前につけるURLを検索サイトにより切り替えるだけ。  
[当該コード](https://github.com/HagiAyato/HagiAyato.github.io/blob/master/MySearch/script/script.js)  
###[実装例](https://hagiayato.github.io/MySearch/)  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/9f33a5cd-9741-80c6-7e2c-720b24a789b2.png)    
※検索サイトは、javascriptを改変することで自分好みに追加・改変可能です。  

# まとめ
各検索機能のURLにはクエリストリングがつき、ここに検索ワードが入ります。  
これによってサイトの閲覧履歴に検索結果を残すことが可能になります。  
