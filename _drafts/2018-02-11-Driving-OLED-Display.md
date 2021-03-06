---
title: "FPGAをはじめてみる"
date: 2017-10-11 22:00:00 +0900
categories: FPGA
---
このサイトを立ててから1ヶ月半近く更新していませんでした。このままだと自分までブログの存在を忘却してしまいそうなのでなにか書くことにしました。ということで最近触り始めたFPGAについて書きます。

FPGAというのは内部のデジタル回路を再構成できるICのことで、回路をプログラムしてやる[^1]ことでいってみれば自作のデジタルICを作ることができます。たとえば7セグ表示のビンゴマシーンは主要な部分をデジタル回路で作ることができる[^2]のでFPGAを用いて作ることができますし、時間をかければCPUを自作することだってできます。また回路を自由に構成できるだけでなく、FPGAはマイコンよりも相対的に多くの入出力ポートを備えています。なんだかマイコンとは異なる魅力がありそうです。そんなわけで私がFPGAに入門した話を何回か書いていこうと思います。

使っているFPGAボードはマルツエレックのMAX10-FBです。IntelFPGA(Altera)のMAX10(10M08SAE144C8GES)を搭載しています。開発環境はQuartus Prime 17.0 Lite Editionを使用しています。
[^1]: 正確にはハードウェア記述言語で書かれた回路の「仕様」をFPGAの内部配線情報に変換するというステップを踏んでおり、別に文字で回路図そのものを書くのではない
[^2]: ランダムな番号を作り出すところをどうするかという問題はありますが

## Lチカ以前
マイコンなどの入門ならLEDを点滅させる「Lチカ」から始めるのが定番ですが、ここではLEDを点灯させるところから始めたいと思います。というのは、FPGAで時間で状態が変わるものを作ることはマイコンで同じことをやるよりも少し道のりが長いからです。

プログラミング言語にはVHDLを使います。またVHDLの練習関係のソースコードは[GitHub: vhdl-study](https://github.com/H-Teramura/vhdl-study)にアップすることにします。(まだソースコード用のCSSを書いてないのでここにソースコードを載せられないというのは内緒)

### LEDを点灯する(wiring01)
まずはFPGAボードの赤色LEDを点灯させてみようと思います。ソースコードは先程示したリポジトリのwiring01というディレクトリにあります。
