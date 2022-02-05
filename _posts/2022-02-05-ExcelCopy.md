---
layout: post
title:  "[Excel]いろいろな方法で、数値を含むセルをコピーしよう"
date:   2022-02-05 15:00:00 +0900
description: Excelの数字を含む値を、色々な方法で正しくコピーしましょう。
categories: jekyll update
tags: 技術ネタ
---
[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/6fbe58a3c53f33560bad)  

**目次**
- TOC
{:toc}


# はじめに
先日、こちらのツイートが話題になりました。  

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">さっきマネージャーとの打ち合わせ中にやってしまいました不覚 <a href="https://t.co/ckHjofDrYE">pic.twitter.com/ckHjofDrYE</a></p>&mdash; DECO*27 (@DECO27) <a href="https://twitter.com/DECO27/status/1484464478016049157?ref_src=twsrc%5Etfw">January 21, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>  

Excelで"DECO\*27"という文字をコピーしようとしたら、DECO\*28,DECO\*29…と数字が増えてしまったという事象です。  
Excelで文字列をコピーする方法は様々ですが、直感的に一番やりやすいのは、セルの右下をドラッグする方法です。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/5d9763ed-6e18-7f26-41c7-0ef002cf31c9.png)  

しかしこの方法では、文字列中の数値が増えていってしまうことがあります。  
そこで、色々な方法でこの事象を回避しましょう。  

# 対策
### 1. Ctrlキーを押しながらドラッグ

ドラッグをするときにCtrlキーを押していると、それだけで"DECO\*27"の27をそのままコピーできます。  
直感的にできる方法なので、私としては一番おすすめです。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/f0a0676e-1f69-0cf1-22d9-193040407f9a.png)  

### 2. オートフィルオプションを使う
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/b91fe6a8-35e5-6ddf-b9d1-df1cc9093dd8.png)  
セルをドラッグし終えた際に、右下に表示されるのがオートフィルオプションです。  
これをクリックして、セルのコピーを選択すると  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/fb028915-fc7b-72e6-f5da-3ce09ea475fb.png)  
"DECO\*27"の27をそのままコピーできました。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/f0a0676e-1f69-0cf1-22d9-193040407f9a.png)  

### 3. 値をして貼り付け
まずは"DECO\*27"と入力したセルを選択し、右クリック->コピーをクリックします。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/97d225fe-1e46-7e63-2718-d2f89bc8c2ac.png)  
その後貼り付けたい範囲を選択し、右クリック->値として貼り付けをクリックします。  
"DECO\*27"の27をそのままコピーできました。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/f0a0676e-1f69-0cf1-22d9-193040407f9a.png)  

### 4.ショートカットキーで貼り付け
ショートカットキーを使えば、マウス操作なしで"DECO\*27"の27をそのままコピーできます。  

1. Ctrl+D
"DECO\*27"と入力したい範囲のうち、一番上に"DECO\*27"と入力->そのセルを含めて、入力したい範囲全体をShiftキー+"↓"キー操作で選択  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/b8044578-cbbe-eed1-943c-44dcb8a755df.png)  
そしてCtrl+Dキーを押すと、"DECO\*27"の27をそのままコピーできました。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/f0a0676e-1f69-0cf1-22d9-193040407f9a.png)  

1. Ctrl+C->Ctrl+V
"DECO\*27"と入力したい範囲のうち、一番上に"DECO\*27"と入力->そのセルをコピー  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/97d225fe-1e46-7e63-2718-d2f89bc8c2ac.png)  
そのセルの下から、入力したい範囲全体をShiftキー+"↓"キー操作で選択  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/8707ce48-fdde-10ba-c57b-77cf636909d8.png)  
そしてCtrl+Vキーを押すと、"DECO\*27"の27をそのままコピーできました。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/655112/4393744d-7e55-2743-1382-fd2e4dd2416e.png)  

# 情報提供元
今回の記事で紹介した対策は、このツイートとそこに寄せられたリプライを元に紹介しております。  
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">対策<a href="https://t.co/t2c93A7ifJ">https://t.co/t2c93A7ifJ</a></p>&mdash; 七虹彩人(ayato-nananiji) (@ayato_nananiji) <a href="https://twitter.com/ayato_nananiji/status/1484501326038183938?ref_src=twsrc%5Etfw">January 21, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>  

# 宣伝
最後に、DECO\*27さんの公式チャンネル、SNSを掲載します。  
技術勉強の合間に、DECO\*27さんの楽曲をお楽しみください。
[Twitter](https://twitter.com/DECO27)  
[Youtube](https://www.youtube.com/c/DECO27Official)  

