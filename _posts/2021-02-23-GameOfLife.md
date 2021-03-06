---
layout: post
title:  "[JavaScript]2生物ライフゲーム/Two Camps Game of Life"
date:   2021-02-23 12:00:00 +0900
description: 以前なんとなく調べて出てきたのが、ライフゲームというものです。webフロントの実装練習として作成してみました。ここで実装しているライフゲームは、2色(=2生物)のライフゲームです。
categories: jekyll update
tags: 技術ネタ
---

[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/f4380449f672383002d8)

**目次**
- TOC
{:toc}

# はじめに
以前なんとなく調べて出てきたのが、ライフゲームというものです。  
その概要は下記"ライフゲームの説明"とwikipediaの[当該記事](https://ja.wikipedia.org/wiki/%E3%83%A9%E3%82%A4%E3%83%95%E3%82%B2%E3%83%BC%E3%83%A0)を参照していただくとして、webフロントの実装練習として作成してみました。  
[実装したライフゲームの実行サイト](https://hagiayato.github.io/MyLifeGame/)  

# ライフゲームの説明

## 概要
[ライフゲーム(wikipedia)](https://ja.wikipedia.org/wiki/%E3%83%A9%E3%82%A4%E3%83%95%E3%82%B2%E3%83%BC%E3%83%A0)  
ライフゲームは、生命の誕生、生存、死亡をマス目でシミュレーションするゲームです。  
ゲームと言ってもクリア、ゲームオーバー条件はなく、自由にマスに生命を配置し、その変化を楽しみむものです。  
## セルの生死ルール
※上記wikipedia記事より引用  

 - 誕生…死んでいるセルに隣接する生きたセルがちょうど3つあれば、次の世代が誕生する。
 - 生存…生きているセルに隣接する生きたセルが2つか3つならば、次の世代でも生存する。
 - 過疎…生きているセルに隣接する生きたセルが1つ以下ならば、過疎により死滅する。
 - 過密…生きているセルに隣接する生きたセルが4つ以上ならば、過密により死滅する。

### 独自機能　"2生物"
ここで実装しているライフゲームは、2色(=2生物)のライフゲームです。  
セルの生死追加ルール

- 生存、過疎、過密…2種の生物それぞれで判定を行う。
- 誕生…2種の生物それぞれで判定を行う。どちらの生物も誕生できるときは、ランダムにどちらかが誕生する。

※1色だけ使えば、普通のライフゲームとして遊べます。  
なぜ2生物にしたのかは、単純な自分の興味と他の方がやっていないからです。  
ライフゲームで2つの生物を戦わせてみたらどうなるのか、気になりますよね…  
### 操作説明
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/9f046239-ef3a-daa8-2aec-719f9350f274.png)

- クリアボタン…全生物を消す
- 開始/停止ボタン…ライフゲーム開始/停止
- 入力色(ラジオボタン)…入力色(生物)の選択
- FPSレンジ操作…FPS・実行周期の変更　*※2021/2/26機能追加*
- グリッドのマスをクリック…入力色(ラジオボタン)で設定した色の生物を配置
  配置しているマスをクリックした場合は生物を消す。
- グリッド上でドラッグ…入力色(ラジオボタン)で設定した色の生物を一括配置

# リンク
### 実装の参考
- [canvasでドット絵用のキャンバスを作成する [1マス=1ドット]](https://www.petitmonte.com/javascript/canvas_dot_picture.html)  
  セル表示、色塗り機能はこちらのサイトのコードをもとに実装させていただいております。

### 製作者関係
- [このwebアプリの実行サイト](https://hagiayato.github.io/MyLifeGame/)
- [このwebアプリのソースコード(github)](https://github.com/HagiAyato/MyLifeGame)
