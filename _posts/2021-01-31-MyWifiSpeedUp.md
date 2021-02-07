---
layout: post
title:  "[無線LAN+Windows]おうちインターネットを速くしたいっ!!"
date:   2021-01-31 10:00:00 +0900
description: 限られた環境でおうちインターネット(wifi)を高速化する方法
categories: jekyll update
tags: 技術ネタ
---

[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/6e1ffa16103f788ebb72)

**目次**
- TOC
{:toc}

# はじめに
コロナ禍で昨年から弊社でもテレワークが始まり、その他私生活でZoom、Meetのようなオンライン会議システムを使い始めました。  
そこで起きていた問題がインターネット(無線LAN/wi-fi回線)の遅さ。  

 - テレワークでは、会社との通信が遅くテレワーク用ツールがフリーズする
 - オンライン会議は映像が途切れ途切れになる

というレベルです。  

この場合本来やるべきは、無線LANルータやプロバイダを変えること。  
ですが、諸事情あってすぐにそれらを変更できないのが私の現状です…  
そこで、無線LANルータやプロバイダを変えずにインターネットを高速にできる方法を色々試してみました。  
その中で有効だったものを3つ紹介します。  

# 1.受信ウィンドウ自動チューニングレベルを引き上げ  
受信ウィンドウ自動チューニングレベルを引き上げることで、通信の高速化を図るというものです。  
どうやら、Windowsによるネットワーク最適化機能を最大限使う設定らしい…  

方法：下記コマンドを、管理者として開いているコマンドプロンプトで実行  

```batch
rem Windows 10/8.1/7の場合
netsh interface tcp set global autotuninglevel=restricted
rem Windows Vistaの場合
netsh interface tcp set global autotuning=restricted
```

引用元：[Windowsで光回線の速度が出ない場合のチェックポイント(受信ウィンドウ自動チューニングレベル編)](https://freesoft.tvbok.com/web/network/autotuninglevel.html)  

簡単に実行できるよう、私の方でバッジファイルを作成しました。  
これを管理者として実行することで、簡単に設定変更が可能です。  
[Network_Speed_Up.bat](https://github.com/HagiAyato/MyWindowsBat-and-Reg/blob/main/Network_Speed_Up.bat)  

※サイトによっては、この機能を無効化(=disable)した方が高速になるという情報もあり。  

# 2.DNS設定
DNSサーバーは、インターネットのドメインとIPアドレスを変換するサーバです。  
PCのデフォルト設定は"自動"ですが、これを高速の物に手動設定します。  
なお、PCでなくルータで設定してもOKです。  

```
案1. Google Public DNS
　IPv4：優先DNSサーバ　8.8.8.8　代替DNSサーバ　8.8.4.4
　IPv6：優先DNSサーバ　2001:4860:4860::8888　代替DNSサーバ　2001:4860:4860::8844
案2. 1.1.1.1
　IPv4：優先DNSサーバ　1.1.1.1　代替DNSサーバ　1.0.0.1
　IPv6：優先DNSサーバ　2606:4700:4700::1111　代替DNSサーバ　2606:4700:4700::1001
```
参考：WikipediaのDNSサーバ名記事  
# 3.無線LANルータの設定
無線LANルータの設定のうち、"20/40MHz 共存方式"をONにします。  
無線LANルータが飛ばす電波の帯域(幅)を広げることで、インターネットの高速化を図ります。  
設定方法は無線LANルータ次第…説明書を読むか型番で調べれば出てくるはず。  
参考：[パソコンのWi-Fi(無線LAN)が遅い・途切れるときに試してほしい対処法  
](https://sittoku.net/slow-wifi-approach.html#2040MHz)  

# 上記の結果
上記対応の結果、おうちインターネットの速度は下記の通りになりました。  
使用ツール：[Google スピードテスト](https://www.google.com/search?q=%E3%82%B9%E3%83%94%E3%83%BC%E3%83%89%E3%83%86%E3%82%B9%E3%83%88)  
![2021-01-31SpeedTest.JPG]({{site.baseurl}}/media/2021-01-31SpeedTest.JPG)  
この測定は回線が混雑する深夜に行ったのですが、  
対応前の速度はダウンロードが2-4Mbpsだったのでその8-4倍程度になりました。  

# まとめ
無線LANルータやプロバイダを変えなくても、インターネットの高速化は可能!  
ぜひお試しください。  
