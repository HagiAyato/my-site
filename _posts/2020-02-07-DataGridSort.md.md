---
layout: post
title:  "[DataGrid,DataGridView等]ソートの落とし穴と対処"
date:   2021-02-07 10:00:00 +0900
description: DataGrid,DataGridViewのソートには、データ型による落とし穴があります。---その説明と対処法について
categories: jekyll update
tags: 技術ネタ
---

[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/05cb5bcc22f832a9a308)

**目次**
- TOC
{:toc}

# はじめに
Microsoft提供のフレームワークには、DataGrid(wpf),DataGridView(.net)等のコントロールがあります。  
これはデータを表形式で表示・編集できる、とても便利なものです。  
そんなDataGrid,DataGridViewのソートには、データ型による落とし穴があります。  

# 落とし穴
下記のような、ファイル一覧をDataGridViewで表示するアプリケーションがあります。  
ファイルサイズは、表記を分かりやすい単位に変換して表示しております。  
参考：[【C#】容量を表すバイト単位の数値を単位付きの読みやすい文字列に変換する関数](https://baba-s.hatenablog.com/entry/2018/12/25/154000)  
![2021-01-31SortBefore.JPG]({{site.baseurl}}/media/2021-01-31SortBefore.JPG)  
ここでファイルサイズで昇順ソートをかけてみると、上から  
「file2⇒file3⇒file1」の順になるべきです。  
しかし実際は  
「file1⇒file2⇒file3」という順になるのです…!  
![2021-01-31SortAfter.JPG]({{site.baseurl}}/media/2021-01-31SortAfter.JPG)  
### なぜこうなるの?
その原因は、ソートの仕様にあります。  

実は、ファイルサイズを表記を分かりやすい単位に変換すると変換後のデータは文字列になります。  
そしてその状態でDataGridViewに表示するということは、DataGridViewに文字列としてデータが入るのです。  
なのでファイルサイズでソートをかけた際、文字列としてソートが行われます。  

文字列としてソートをすると、先頭の1文字から順番に並び替えが行われるため、  
本当は一番サイズが大きい1.87MBが、先頭になります。  
***※バグではありません。***  

この事象は、数値を文字列に変換した際だけでなく日付を文字列に変換して表示した場合も同じことが起きます。Excelのフィルタでで文字列をソートした場合も同じです。  
(となると、この落とし穴は.netあるあるかもしれません)  
# 対処法
対処法は、下記2つのことを行うことです。  

### 1. 非表示列として、元データを追加
文字列に変換する前の元データ(数値、日付等)を非表示列の列としてDataGrid,DataGridViewに追加します。  
非表示列なので、ユーザからの見た目は変わりません。  

### 2. 文字列データをソートする際、元データ列でソートする
文字列データをソートする際に、元データ列でソートを書けるようにコードを書きます。  

```cs
        /// <summary>
        /// 列ヘッダクリック時処理(カスタムソート用)
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void dataGridView1_ColumnHeaderMouseClick(object sender, DataGridViewCellMouseEventArgs e)
        {
            // クリックした列を判別
            switch (e.ColumnIndex)
            {
                case 4:
                    // ファイルサイズ(文字)列
                    // 現在のファイルサイズ(文字)列の並びを取得
                    SortOrder mode = dataGridView1.Columns[4].HeaderCell.SortGlyphDirection == SortOrder.Ascending ? SortOrder.Descending : SortOrder.Ascending;
                    ListSortDirection direction = mode == SortOrder.Ascending ? ListSortDirection.Ascending : ListSortDirection.Descending;
                    // ファイルサイズ(数値)列基準でソートを実施
                    dataGridView1.Sort(dataGridView1.Columns[3], direction);
                    dataGridView1.Columns[4].HeaderCell.SortGlyphDirection = mode;
                    break;
                default:
                    // それ以外の列の場合は、ファイルサイズ(文字)列のソート順表記消去
                    dataGridView1.Columns[4].HeaderCell.SortGlyphDirection = SortOrder.None;
                    return;
            }
        }
```
処理の流れ
列ヘッダをクリック⇒その列か判別：ファイルサイズ(文字列データ)列の場合⇒  
現在の並び順を取得⇒その反対順で***元データ基準ソート***⇒  
ファイルサイズ(文字列データ)列の並び順更新  

ソートをこのように実装したうえで、ファイルサイズで昇順ソートをかけてみると、上から  
「file2⇒file3⇒file1」の順になります。  
![2021-01-31SortAfter2.JPG]({{site.baseurl}}/media/2021-01-31SortAfter2.JPG)  
本来のファイルサイズ順でソートができました。  

今回はDataGridViewを例にしましたが、DataGrid等でも同じ方法で対処可能です。  

# まとめ
DataGrid,DataGridViewをソートする際には、データ型に注意してください。  
また、どうしても数値を文字列で表示したい場合は上記方法で本来のサイズでのソートを実装しましょう。  
