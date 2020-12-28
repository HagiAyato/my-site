---
layout: post
title:  "[PDFmerger]生まれて初めてのソフト公開v0.1"
date:   2020-12-28 10:00:00 +0900
description: PDFファイル結合ソフト、PDFmergerを暫定公開
categories: jekyll update
tags: 技術ネタ
---
**目次**
- TOC
{:toc}

# 公開の経緯  
[PdfSharpでPDFを結合する](https://qiita.com/hagii-x/items/7e2dc668a446acec560e)  
この記事が約500回表示をいただいております。  
多くの方から見ていただく中でコードだけ公開するままはどうかと思い、仮ですが実行ファイルを公開します。  

# PDFmergerについて  
MITライセンスのライブラリ、PdfSharpを用いてPDFの結合を行うwindowsアプリケーションです。  

### 作成理由  
 - MITライセンスのPDF編集ライブラリを使ってみたいという興味  
 - 過去に使ったPDF結合ソフトに結合設定の保存機能がなく、結合対象のPDFの一部のみ修正した際に必ず結合設定をするという手間がかかったため  
※結合設定…結合するPDFファイル、結合する順番の設定  

### 特徴  
 - PDFファイルの結合設定を.datファイルに保存する機能があります。  
   PDFを結合しなおす際にこの.datファイルを読み込むことで、結合設定をすぐに復元できます。

### DLリンク  
[PDFmerger リリース](https://github.com/HagiAyato/PDFmerger/releases)
同じリポジトリで、ソースコードも確認可能です。
### 以下、ソフトのreadme  
<hr/>
<h1>PDFmerger</h1>
PDFファイルの結合アプリケーションです。
<h2>インストール方法</h2>
<ol type="1">
  <li>[リリースページ](https://github.com/HagiAyato/PDFmerger/releases/)
  から"Release_PDFmerger.zip"をダウンロードする</li>
  <li>ダウンロードした"Release_PDFmerger.zip"を、任意のフォルダに解凍する</li>
</ol>
<h4>必須環境</h4>
<ul>
  <li>Framework: .NET Framework 4.6.1</li>
</ul>
<h2>使い方</h2>
<ol type="1">
  <li>アプリケーション"PDFmerger.exe"を開く</li>
  <li>PDFファイルの結合構成を行う
    <ul>
      <li>"+追加"ボタン…結合するPDFを、結合PDFリストの一番下に追加する(複数選択可能)</li>
      <li>"▲一番上へ"ボタン…選択中のPDFを、結合PDFリストの一番上に移動する</li>
      <li>"△一行上へ"ボタン…選択中のPDFを、結合PDFリストの一行上に移動する<br />
        ※選択中のPDFのうち、一番上のPDFを基準にします。
      </li>
      <li>"△一行下へ"ボタン…選択中のPDFを、結合PDFリストの一行下に移動する<br />
        ※選択中のPDFのうち、一番下のPDFを基準にします。
      </li>
      <li>"▼一番下へ"ボタン…選択中のPDFを、結合PDFリストの一番下に移動する
      </li>
      <li>"-削除"ボタン…選択中のPDFを、結合PDFリストから削除する</li>
    </ul>
  </li>
  <li>出力ファイル名・パスを決定する(下記いずれかの方法)<br />
    1.出力ファイルパス欄に、直接入力<br />
    &nbsp;※パスを入力しない場合は、アプリケーション"PDFmerger.exe"と同じフォルダに出力されます。<br />
    2."出力ファイル変更"ボタンを押して、ダイアログで名前を決定する<br />
    3."結合・出力"ボタンを押した際に決定する(この段階では出力ファイルパス欄を空欄にする)
  </li>
  <li>"結合・出力"ボタンを押して、結合したPDFを出力する</li>
</ol>
<h3>拡張機能</h3>
<h4><b>◆結合設定書き出し/読み込み機能◆</b></h4>
<p>
  現在の結合PDFリストと出力ファイルパスの設定をファイルに書き出し/読み込みする機能です。<br />
  上部メニュー"ファイル"から起動します。<br />
  拡張子…".dat"<br />
<ul>
  <li>ファイル&gt;結合設定&gt;結合設定読み込み…既に存在する結合設定ファイルを読み込む<br />
    &nbsp;※アプリケーションに現状入力されている設定は破棄されます。
  </li>
  <li>ファイル&gt;結合設定&gt;結合設定読み込み…結合設定ファイルを作成・名前を付けて保存する</li>
</ul>
</p>
<h4>PDFファイルドロップ機能</h4>
<p>
  アプリケーションにPDFファイルをドラッグアンドドロップすると、<br />
  ドラッグアンドドロップしたPDFファイル全てを結合PDFリストの一番下に追加します。
</p>
<h2>補足情報</h2>
<h4>開発環境</h4>
<ul>
  <li>OS: Windows10</li>
  <li>ソフト: Microsoft Visual Studio Community 2017</li>
</ul>
<h4>使用ライブラリ</h4>
・PDFsharp version="1.50.5147"
<h4>著作権</h4>
Copyright (C) 2020 HA Works
<h4>問い合わせ・規約</h4>
商用以外の利用は無制限・無料で可能です。<br />
商用利用について、もしくは問題発生時などは下記アドレスにお問い合わせください。
haworks.eng☆gmail.com※☆→@
<h4>ライセンス表記(MITライセンス)</h4>
Creator of PDFsharp is empira Software GmbH<br />
Kirchstrase 19 53840 Troisdorf Germany<br />
www.empira.de<br />
PDFsharp (R) is a registered trademark of empira Software GmbH<br />
Released under the MIT license<br />
http://www.pdfsharp.net/PDFsharp_License.ashx

