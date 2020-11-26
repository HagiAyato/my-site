---
layout: post
title:  "PdfSharpでPDFを結合する"
date:   2020-11-27 00:09:00 +0900
categories: jekyll update
---
[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/7e2dc668a446acec560e)

<h1>はじめに</h1>
PDFを結合するプログラムを日本語で調べると、出てくる多くはiTextSharpを使う方法です。<br/>
これでもいいのですが、無料版のライセンスがAPGLであり商用ソフトを作る場合には支障をきたします。<br/>
そこで今回は、MITライセンスのpdfSharpを用いてPDFを結合してみます。<br/>
※ライセンスの違いは以下の記事を参照<br/>
　[オープンソースライセンス、どれなら使っても良いの？？](https://qiita.com/fate_shelled/items/a928709d7610cee5aa66)
<h1>準備</h1>
まずはC#のプロジェクトをvisual studioで作成します。<br/>
次にそのプロジェクトにPdfSharpをインストールします。<br/>
　１．プロジェクト　＞　NuGet パッケージの管理を開く<br/>
　２．検索欄に"pdfSharp"を入力する<br/>
　３．右側"インストール"ボタンをクリックする<br/>

<h1>コード実装</h1>
いよいよコードを実装します。<br/>
まずはライブラリをコードにインポートします。

```C#
using PdfSharp.Pdf;
using PdfSharp.Pdf.IO;
```
つついて実際に処理を実装します。<br/>
１．結合後PDFのオブジェクトを作成

```C#
// PDFオブジェクト作成
PdfDocument document = new PdfDocument()
```
２．結合するPDFを開く

```C#
// file：結合するファイルのパス
// PdfDocumentOpenMode.Import：PDFを読み取りモードで開く
// 結合するPDFオブジェクトを作成
PdfDocument inputDocument = PdfReader.Open(file, PdfDocumentOpenMode.Import)
```
３．結合するPDFの全ページを結合後PDFに追加する

```C#
// 頁全件ループ
foreach (PdfPage page in inputDocument.Pages)
{
    // PDF頁を追加
    document.AddPage(page);
}
// 結合するPDFを閉じる
inputDocument.Close();
```
４．２，３を結合するPDFの数だけ繰り返す<br/>
５．PDFを保存し閉じる

```C#
// PDF保存
document.Save(selectedPath);
// PDFを閉じる
document.Close();
```
このようにして実際に作成したコードは以下の中の関数"pdfMerge"です。<br/>
[PDFmerger/IOpg.cs](https://github.com/HagiAyato/PDFmerger/blob/main/PDFmerger/IOpg.cs)<br/>
以下補足<br/>
・結合するファイルのパスはListにまとめておき、foreachを回して上記処理２～４を繰り替えすのがおすすめです。<br/>
・PDFオブジェクト作成時はusing句を使うことで、確実に処理終了時の解放ができます。<br/>
・例外処理(try-catch等)もお忘れなく。<br/>
<h1>ライセンス表記</h1>
PdfSharpはMITライセンスのライブラリで、使用する際はライセンスの表記が必要です。<br/>
ソースコード中やreadmeなどにライセンス表記を入れましょう。

```C#
/*
 * PdfSharpライセンス表記
 * Creator of PDFsharp is empira Software GmbH
 * Kirchstrase 19 53840 Troisdorf Germany
 * http://www.empira.de
 * PDFsharp (R) is a registered trademark of empira Software GmbH
 * Released under the MIT license
 * http://www.pdfsharp.net/PDFsharp_License.ashx?AspxAutoDetectCookieSupport=1
 */
```
