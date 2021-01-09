---
layout: post
title:  "[.net、Java連携]C#.netで.jarを実行するンジャー"
date:   2021-01-09 13:00:00 +0900
description: C#.netでJava(.jarファイル)を実行する方法
categories: jekyll update
tags: 技術ネタ
---

[本記事は、Qiitaのこの記事と同一内容です。](https://qiita.com/hagii-x/items/a60d5df95b8e8fc5da10)

**目次**
- TOC
{:toc}

どうしてもJavaを使わないとできない処理をC#.netから起動する必要が出た場合、  
その実装に困りますよね…  
そこで参上!C#.netで.jarを実行するンジャー!!(ここまで茶番)  
# Java側のプログラム
java側のプログラムはmainメソッド(関数)を入れます。  
main関数のコマンドライン引数"args"でC#から値を受け取ります。  
下記サンプルプログラムでは、1つの引数でメッセージ：msgを受け取り、それを表示しています。  

```java:Sample.java
	public static void main(String[] args) {
		// TODO 自動生成されたメソッド・スタブ
		if (args.length <= 0) {
			System.out.println("出力メッセージなし");
		} else {
			System.out.println("出力メッセージ：" + args[0]);
		}
		// Enterキー入力待ち
		// 参考：https://stackoverflow.com/questions/26184409/java-console-prompt-for-enter-input-before-moving-on
		System.out.println("Press \"ENTER\" to exit...");
		Scanner scanner = new Scanner(System.in);
		scanner.nextLine();
	}
```

プログラムができたら、実行可能な.jarファイルを生成しましょう。  

# C#(.net)側のプログラム
C#側では、Processクラスのオブジェクトで.jarファイルを起動します。  
.jarファイルは、C#(.net)の実行ファイルが生成されるDebug/Releaseフォルダに配置するとファイル指定が楽です。  

```C#
// コマンドプロンプトを表示して実行する場合
Process.Start("java", "-jar (.jarファイル名orパス) (引数) (引数)…"))
// コマンドプロンプトを表示せずに実行する場合
Process.Start("javaw", "-jar (.jarファイル名orパス) (引数) (引数)…"))
```

.jarファイルの実行中にC#のプログラムを止めたい場合、WaitForExitメソッドを使いましょう。  

```C#
// 終了待ち
jar.WaitForExit();
```

.jarファイルの実行結果は、ExitCodeメソッドで受け取れます。  
※javaのmainメソッドが ```void main()``` なら、戻り値0で正常終了  

```C#
// 結果取得(0:正常終了)
jar.ExitCode();
```
オブジェクトを作成しますので、usingやclose,disposeなどによるオブジェクト解放をお忘れなく。  
参考：[確保したリソースを忘れずに解放するには？［C#／VB］](https://www.atmarkit.co.jp/ait/articles/1710/18/news022.html)  
実装例↓

```c#:ConnectJar.cs
        /// <summary>
        /// .jar実行
        /// </summary>
        /// <param name="msg">メッセージ</param>
        /// <returns>True:成功/False:失敗</returns>
        public static bool Excecute(string msg)
        {
            bool result = false;
            Process jar = null;
            try
            {
                // .jarをプロセスとして起動
                using (jar = Process.Start("java", "-jar Sample.jar " + msg))
                {
                    // 終了待ち
                    jar.WaitForExit();
                    // 結果取得(0:正常終了)
                    if (jar.ExitCode == 0) result = true;
                }
            }
            catch (Exception e)
            {
                MessageBox.Show("例外発生\n" + e.Message);
            }
            return result;
        }
```

あとはC#.netを実行するだけ…!  
サンプルコード全体は下記リポジトリにあります。  
[CSJarソースコード](https://github.com/HagiAyato/CSJar)

# 補足
 - 今回はC#で実装しましたが、VB.netでも同じ方法で.jarの実行ができます。
 - Processクラスを使うと、.jar以外にも様々なプロセスを実行できます。  
   [外部アプリケーションを起動する、ファイルを関連付けられたソフトで開く|dobon.net](https://dobon.net/vb/dotnet/process/shell.html)
