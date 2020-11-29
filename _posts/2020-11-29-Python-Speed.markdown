---
layout: post
title:  "[Python]所要時間で見るDataFrameの強さと弱点"
date:   2020-11-29 00:10:00 +0900
categories: jekyll update
---
[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/b226c12f489f22eb2a20)

<h1>はじめに</h1>
Pythonではpandas.DataFrameで二次元の表データを扱うことができます。<br/>
他言語の配列相当であるlist,tuple以上に表データを扱いやすいのですが、その処理速度も基本的にはlist,tuple以上に速いのです。<br/>
そんなDataFrameの強さと弱点を実際にプログラムを動かしながら見ていきましょう。<br/>
<p>実行環境・条件</p>
実行環境<br/>
・windows10 Home 64bit<br/>
条件<br/>
・使用データ：10000行のCSVデータ<br/>
・使用データの列：index,学生ID,A-E 5教科の点数(0-10000)<br/>
　※ある試験を受けた学生10000人の成績一覧をモデルとしています<br/>
<h1>DataFrameの強さ</h1>
DataFrameの強さは簡単な処理で、かつ高速でデータを処理できる点です。
<h5>平均値を求める場合</h5>
後ろに列を追加して、平均値を代入する処理を実装します。<br/>
listだと下記の処理を組むことになります。

```python
for idx, row in enumerate(list):
	row.extend('0')
	row[7] = str((float(row[2]) + float(row[3]) + float(row[4]) + float(row[5]) + float(row[6]))/5.0)
```
他の言語と書き方が似ています。<br/>
これでもいいのですが…DataFrameで実装すると以下の1行で済みます。

```python
# オリジナル
df['average'] = (df['subjectA'] + df['subjectB'] + df['subjectC'] + df['subjectD'] + df['subjectE'])/5
# 編集後
df['average'] = (df[['subjectA', 'subjectB', 'subjectC', 'subjectD', 'subjectE']].sum(axis=1))/5
```
※編集リクエスト者：[siruku6](https://qiita.com/siruku6)さん<br/>
1行分操作のイメージで書けるためコーディングミスのリスクが少ないです。
<h5>ソートする場合</h5>
上記の平均値降順でソートを行う場合、listだと下記の処理を組むことになります。

```python
list = sorted(list, key=lambda x: x[7], reverse=True)
```
ソートに関しては、listでも1行で実装できますね。<br/>
これをDataFrameで実装するとこちらも1行で済みます。

```python
df.sort_values('average', ascending=False)
```
<h5>条件で絞り込みをする場合</h5>
平均点が50点以上のデータのみを絞り込む場合、listだと下記の処理を組むことになります。

```python
list2 = []
for idx, row in enumerate(list):
	if 50 <= float(row[7]):
		list2.append(row)
```
平均算出時と同様に、forループを使います。<br/>
これをDataFrameで実装すると、…予想がつくと思いますが1行で済みます。

```python
df2 = df[50 < df['average']]
```
<h5>各処理の速度は…</h5>
これら各処理の速度を計測し、10回平均を取ると以下の通りとなります。

| 処理名 | 10回平均所要時間(list)[sec] | 10回平均所要時間(DataFrame)[sec] |
|:--|--:|--:|
| 平均計算 | 0.764768385887146<br/>コード変更後 : 0.007805347442626953 | 0.01179955005645752 |
| ソート | 0.030899477005004884 | 0.011399650573730468 |
| 絞り込み | 0.04529948234558105 | 0.006699275970458984 |

DataFrameによる実装はコードが簡潔なだけでなく、その速度が速いこともわかります。
<h1>DataFrameの弱点</h1>
DataFrameの弱点はforループです。<br/>
もし平均値をforループで作成する場合は下記のコードを使います。

```python
for idx in range(len(df)):
	df.iat[idx, 6] = str((float(df.iat[idx, 1]) + float(df.iat[idx, 2])
		+ float(df.iat[idx, 3]) + float(df.iat[idx, 4]) + float(df.iat[idx, 5])/5.0))
```
その所要時間は10回平均2.33[s]で、listの場合よりも遅いのです。<br/>
従ってDataFrameを扱う際は、極力forを使わないことが望ましいです。
<h3>どうしてもDataFrameでforを使うなら</h3>
それでもDataFrameでforを使う場面はあります。<br/>
そんなときは、forを使う部分のみlistやndarrayにする、あるいは下記投稿のような方法を使うことで処理を高速化できます。<br/>
[[Python3 / pandas] DataFrameをどうしても1行ずつ処理したいときの速度改善策](https://qiita.com/siruku6/items/0633db690283a0f525ad)
<h2>サンプルデータ作成について</h2>
今回使ったサンプルデータは、下記URLのコードで作成しました。<br/>
[make10000data.py](https://github.com/HagiAyato/PythonTests/blob/main/make10000data.py)

