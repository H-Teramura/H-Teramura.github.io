---
title: "Javaでゲームを作る（とりあえず触ってみる編）"
date: 2018-03-24 13:45 +0900
categories: java e-game
---
### Javaも触ってみようかなと思って
こんばんは、Ikubakuです。これからJavaでゲームを作る話を不定期で書いていこうと思います。というのも、色々面白いJavaのライブラリなどがあってちょっと触ってみたいなと思い、練習がてら簡単なゲームを作ってみようかなと思ったからです。

#### Javaで書かれたライブラリやプロジェクト（メモとして）
- Synthesijer (<http://synthesijer.github.io/web/>)
Javaを用いた高位合成ツールで、Javaを書くとHDLを出力してくれる。
- Play Framework (<https://www.playframework.com/>)
Java, ScalaでWeb Appを作ることができる。

### LWJGL
Javaにはgraphicsというグラフィックライブラリがすでにありますが、ゲームが作れるほど高速ではないらしいです。そんなわけでゲーム制作用のライブラリである[LWJGL](https://www.lwjgl.org/)を使うことにしました。

LWJGLはゲーム内のもののクラスが用意されているようなタイプのライブラリ（ゲームエンジンと呼ばれたりする）とは違ってOpenGLなどの低いレベルのライブラリとの架け橋になるようなもの[^1]なので、ゲームを動作させる仕組みの部分は自分で実装する必要がありそうです。
> LWJGL is a Java library that enables cross-platform access to popular native APIs useful in the development of graphics (OpenGL, Vulkan), audio (OpenAL) and parallel computing (OpenCL) applications. This access is direct and high-performance, yet also wrapped in a type-safe and user-friendly layer, appropriate for the Java ecosystem.

> LWJGL is an enabling technology and provides low-level access. It is not a framework and does not provide higher-level utilities than what the native libraries expose. As such, novice programmers are encouraged to try one of the frameworks or game engines that make use of LWJGL, before working directly with the library.

（<https://www.playframework.com/> より引用）

[^1]:1,OpenCLも使えるらしい

### 環境構築
とりあえずOpenJDKかOracle JDKを準備しておきます（パスを通すなど。IDEを使うほうが楽そうではある？）。それから[ここのページ](https://www.lwjgl.org/customize)を使って必要なモジュールをダウンロードします。

#### カスタマイズ
今回はReleaseのZIPバンドルでGetting Startedを選んでみました。Contentsの内容がPresetによって変わるので用途に合わせて選んでやる必要がありそうです。DOWNLOAD ZIPを押すとダウンロードが始まります（そして気長に待つ）。

ダウンロードしたら適当な場所に展開しておきます（ディレクトリを作って展開しないと散らかるので注意）。

### サンプルコードを動かす
とりあえず[ここ](https://www.lwjgl.org/guide)にあるコードを動かしてみます。普通にコンパイルするのですが、JavaプログラムでJARファイルからクラスをインポートする方法をよくわかっていなかったのでメモがてら。

まずHelloWorld.javaというファイルにサンプルコードを書いて保存してやります。で、コンパイルのやり方ですが、LWJGLのクラスをインポートしたいのでjavacのオプションとして先程LWJGLを展開したパスを与えてやります[^2]。

```
$ javac -cp "/path/to/lwjgl/*:." HelloWorld.java
```

実行時も同様に

```
$ java -cp "/path/to/lwjgl/*:." HelloWorld
```

-cpというのがクラスパスを指定するオプションでコロンでファイルパスを区切って書きます。この場合はLWJGLを展開したディレクトリの中の全ファイルとカレントディレクトリ内のclassファイルが検索対象になります。

こうするとLWJGLを展開したディレクトリとカレントディレクトリ（ソースコードを置いた場所を想定している）の中からクラスを検索されて、ライブラリの読み込みとエントリポイントのあるクラスの検索ができるというわけです。

真っ赤なウィンドウが表示されたら成功です。

[^2]:2,あるいはjavacがデフォルトでクラスを検索するディレクトリにコピーしても良い

### おわりに
今回は環境の準備だけやりました。これから少しずつLWJGLを使っていこうと思います（Javaの勉強もしながら）。そういえばIDEでやってないけれど使ったほうがやりやすいのかなあ。

では、また。

*****
脚注
