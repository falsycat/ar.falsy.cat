---
title: dart言語
tags: [note, info-tech, development, programming-language]
---

## 概要
- Google製プログラミング言語
- [flutter](note/info-tech/flutter.md)のための言語
- 日本語資料少なめ
- オブジェクト指向

## 特徴
- undefined behaviorは無い
- Null safety
	- 型名に?を付ければNull許容型になる
	- Null許容型に対してはNullチェックをしないとコンパイラがキレる
- 整数値以外は参照型
- GC（mark & sweep）搭載
	- デストラクタは無さそう，そもそもmark & sweepでデストラクタは信頼できない
- コンストラクタが書きやすい
	- わざわざメンバ変数と同じ名前の引数を書いて，代入して，，，ということをしなくてもいい
- 静的解析が強め

## 文法
- 大体は既存のやつと同じ
- 文末セミコロン必須
- 関数呼び出しの実引数リストでもケツカンマ許容

### 変数修飾子
- 型が自明な場合，型名は省略できる
	- 省略できる場合は省略することが推奨される

```dart
// コンパイル時定数
const int x = 0;
const x = 0;

// 再代入不可能変数
final int x = 0;
final x = 0;

// 再代入可能変数
var int x = 0;
var x = 0;

// 遅延初期化変数
late int x;
late final int x;
```

#### final: 再代入不可能変数
- 値型の変数に対しては，値の変更を禁止する
- 参照型の変数に対しては，参照先の変更のみを禁止する
- dartでは，参照先のオブジェクトの変更を禁止することはできない

#### late: 遅延初期化
- 変数の初期化を遅延させることができる
- 実質的にはNull safetyの無いNull許容型
- `late final`修飾子によって複数回の代入をコンパイルエラーにできる
	- ただし静的解析の精度は微妙なので，絶対に2回目の代入ができなくなるわけではない

### Null safety
- Null許容型に対しては，Nullを扱いやすくするための演算子が使える
- 関数の中で，変数に対して一度nullチェックをした場合，以降，その変数はNull許容型でないものとして扱える
```dart
(T? x) {
  x ?? T();  // x が null ならば 0 それ以外ならば T()
  x?.method();  // x が null ならば methodを呼ばずnullを返す それ以外ならば methodを呼ぶ
  x!.method();  // x が nullでない ことを前提として methodを呼ぶ（実行時にnullだった場合runtime error）
};
(T? x) {
  if (x == null) {
    return;
  }
  x.method();  // x!.method(); とする必要がない
};
(T? x) {
  x.method();  // Nullチェックしてないのでコンパイルエラー
};
```

### コンストラクタ
- C++と比べてかなり書きやすい

```dart
class A {
  final int x;
  final int y;
  final int z;

  A(this.x, this.y, this.z);
  A(this.x, {required this.y, this.z = 1});
  A.empty() :
    this.x = 0, this.y = 0, this.z = 0;
}

void main() {
  final a1 = A(0, 1, 2);
  final a2 = A(0, y: 1);
  final a3 = A.empty();
}
```
