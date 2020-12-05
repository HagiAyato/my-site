---
layout: post
title:  "[小話]Googleアナリティクスと広告ブロッカー"
date:   2020-12-05 00:22:00 +0900
categories: jekyll update
---
[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/d9fd851263c595b5da2e)

## 発端  
先日私は、自分のサイトをGitHub Pagesで作成しました。  
[自分のサイト](https://hagiayato.github.io/my-site/)
そして、そのサイトのアクセス数の集計・解析のためGoogleアナリティクスを導入したのですが、  
自分でサイトにアクセスしても、それをGoogleアナリティクス側が拾ってくれませんでした。
![2020-12-05 182619.jpg]({{site.baseurl}}/media/2020-12-05 182619.jpg)
## 分析
真っ先に導入方法が間違えていないかを確認したのですが、どうも間違えてはいないようでした。  
その方法は以下の記事の通りです。  
[GitHub Pages で Google Analytics を使うシンプルな設定](https://qiita.com/memakura/items/2cfc8133e07fdc72c45f)
その後他の原因を疑っても結果は変わらず…  

しばらくすると、あるものに目が行きました。  
**広告ブロッカーが動作しているという表示**  
※どのブロッカーかは伏せます。

試しに広告ブロッカーを自分のサイトで無効にし、再度自分のサイトにアクセスすると…
![2020-12-05 184845.jpg]({{site.baseurl}}/media/2020-12-05 184845.jpg)  
今度はちゃんと、アクセスをGoogleアナリティクス側が拾ってくれました!
## 結論
**GitHub PagesにおけるGoogleアナリティクスは広告ブロッカーでブロックされ、ブロッカーが作動する環境からのアクセスを集計しない**  
今まではwebページを軽量で見たいということで、基本的にPCブラウザに広告ブロッカーを入れていました。  
ただ今回の件を考えると、広告ブロッカーはwebページの運営に支障をきたすということになるわけでして…  
少し複雑な気持ちになります。
### 補足
- QiitaにおいてもGoogleアナリティクスを導入していますが、自分のサイトと結果は変わりませんでした。
- 広告ブロッカーを無効にしなくても、ホワイトリストでGoogleアナリティクス関係のブロックを解除する方法もあるようです。ただし方法を調べ切れていないため今回は触れません。
- GitHub Pages側での広告ブロック対策は今後調査します。