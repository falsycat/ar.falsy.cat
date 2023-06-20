---
title: C/C++のsanitizerの使い方
tags: [note, info-tech, development, programming-language, howto]
---

## 概要
- バグを検知するコードを埋め込むための，sanitizerと呼ばれる機能がある
- このページではsanitizerの使い方を説明する

## 使い方

### コンパイル時にsanitizerを埋め込む
- 種類ごとにオプションが異なる
- XXXにはSanitizer名をカンマ区切りで羅列する
	- 代表的なSanitizer名については後述

```bash
g++ -fsanitizer=XXX a.cc
gcc -fsanitizer=XXX a.c
```

#### 代表的なSanitizer
- [ここ](https://gcc.gnu.org/onlinedocs/gcc/Instrumentation-Options.html)で`-fsanitizer=`を検索すると一覧が見れる
- `thread`は`address`や`undefined`と同居できない

|名前|説明|
|:--|:--|
|`address`|[Address Sanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer)|
|`undefined`|[Undefined Behavior Sanitizer](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html)|
|`thread`|[Thread Sanitizer](https://github.com/google/sanitizers/wiki#threadsanitizer)|

### 実行時にsanitizerの挙動を指定する
- sanitizerが埋め込まれたバイナリに対して，実行時に，sanitizerの挙動を環境変数で指定することができる
- 詳細は各sanitizerの説明ページを参照

## 所感
- `thread`が強すぎる
	- `thread`は実際に[Nf7](https://git.falsy.cat/nf7/nf7)のデバッグで使ってる
		- sanitizerがなければ気づけなかったcondition raceがかなりあった
			- 格好つけてロックフリーで書いたせい
- `thread`が`address`や`undefined`と一緒に使えないのが痛い
	- どちらともを使うには，`thread`でビルド，テストした後に，オプションを変えてビルドし直し，同じテストを実行しなければならない