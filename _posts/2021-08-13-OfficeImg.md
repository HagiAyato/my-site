---
layout: post
title:  "[Word,Excel,Power Point]Officeのファイルから画像を取り出す処理をコードで自動化"
date:   2021-08-13 21:20:00 +0900
description: Officeのファイル(docx/xlsx/pptx)から画像を抜き出すコンソールアプリ
categories: jekyll update
tags: 技術ネタ
---

**目次**
- TOC
{:toc}

# はじめに
皆さんは、こういう話を聞いたことありますか?

- 最近のOffice(Word,Excel,Power Pointなど)のファイルの正体はzipファイル
- Officeのファイルについて、拡張子をzipにして解凍すると、使用画像を取り出せる

これは事実であり、詳細は下記記事に記載されています。  
[パワーポイント、ワードから画像を取り出す。](https://qiita.com/msht0511/items/4f5b1552c92dddbc763d)  
でも、いちいちファイルの拡張子を変えて、解凍して、画像を取り出す…というのは面倒!!  
そんなわけで、この処理を自動でおこなうC#コードを作りました。  

# 解説
ソースコートは下記リンクに貼ってあります。  
[Program.cs](https://github.com/HagiAyato/OfficeImg/blob/main/OfficeImg/OfficeImg/Program.cs)

#### 仕様

- ドラッグアンドドロップをしたOfficeファイルについて、使用画像を取り出す
- 複数ファイルのドラッグアンドドロップにも対応
- 取り出した画像は、ドラッグアンドドロップしたファイルと同じ階層に置く
- 対応拡張子は下記の通り
 - Word:".docx",".docm",".dotx",".dotm"
 - Power Point:".pptx",".pptm",".ppsx",".ppsm",".potx",".potm"
 - Excel:".xlsx",".xlsm",".xltx",".xltm"
 - Open Document:".ods",".odt",".odp"

#### 処理の流れ

1. ファイルの存在チェック
1. ファイルの拡張子チェック
1. ファイルを解凍
1. 解凍したフォルダから画像ファイルを取り出す
1. 解凍したフォルダ削除

###  ファイルの存在チェック
今回のプログラムでは、コマンドライン引数で処理対象ファイルのパスを受け取ります。(fname)  
それが実在しないファイルだと困るので、ファイルの存在チェックをします。  

```Program.cs
// ファイルの存在チェック
if (!File.Exists(fname))
{
    Console.WriteLine("ファイルが存在しません。");
    continue;
}
```

###  ファイルの拡張子チェック
ファイルが存在しても、処理に非対応のファイルでは困ります。  
なので、拡張子でファイルが処理に対応しているか確認します。  

```Program.cs
string type = "", extension = "";
extension = Path.GetExtension(fname);
switch (extension)
{
    case ".docx":
    /** 中略 **/
    case ".dotm":
        type = "word";
        break;
    case ".pptx":
    /** 中略 **/
    case ".potm":
        type = "ppt";
        break;
    case ".xlsx":
    /** 中略 **/
    case ".xltm":
        type = "xl";
        break;
    case ".ods":
    /** 中略 **/
    case ".odp":
        type = "";
        break;
    default:
        Console.WriteLine("対応のファイルではありません。");
        continue;
}
```

### ファイルを解凍

fnameはzipファイルでなく、コマンドライン引数で受け取ったOfficeのファイルパスです。  
解凍元ファイルの拡張子は、zipにせずOfficeのファイルのままでも問題ありません。  

```Program.cs
// ファイルを展開
/** 中略 **/
ZipFile.ExtractToDirectory(fname, unzipDir);
```

### 解凍したフォルダから画像ファイルを取り出す

.netには、フォルダ内の全ファイル・フォルダをコピーする関数がありません。  
なので自作する必要があります。  
**DirectoryUtil.Copy**がこれに当たり、**[このサイト](https://kan-kikuchi.hatenablog.com/entry/DirectoryProcessor)**の**CopyAndReplace**関数と処理は同じです。  

```Program.cs
// 解凍したフォルダから画像ファイルを取り出す
string mediaDir = unzipDir + "/" + type + "/media";
/** 中略 **/
DirectoryUtil.Copy(mediaDir, directoryName + "/" + fileName + extension + "_media");
```

### 解凍したフォルダ削除

最後に、解凍したフォルダを削除します。

```Program.cs
// zipファイルと解凍したフォルダ削除
Directory.Delete(unzipDir, true);
```

# 蛇足
~~本当は[PDFMerger](https://qiita.com/hagii-x/items/7f5d928f36b9cc68dc00)と同様に実行ファイルを公開したいのですが、  
Visual Studio Codeで実行ファイルを作成するとどうしても個人情報入りのファイルがないと実行できない状況となり、公開ができません。  
どうにかできないかな…~~  
⇒フレームワークを.net Coreから.net Frameworkに変更したことで、ソフトの公開ができました。  
[ソフトのDLリンク](https://github.com/HagiAyato/OfficeImg/releases/)  
抜き出した画像の著作権・肖像権に気を付けつつご利用ください。  
