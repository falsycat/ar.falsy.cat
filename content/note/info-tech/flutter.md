---
title: flutter
tags: [note, info-tech, development, library]
---

## 概要
- flutterはマルチプラットフォーム GUIアプリケーション フレームワーク
	- iOS/Android，Web，Windows/Linux/Mac，組み込み
- Google製
- 使用言語は[Dart](note/info-tech/dart.md)

## 環境構築
- dart + flutterをインストール
- VSCodeにflutter用の拡張機能を追加

## 豆知識
### ウィジェットツリー
- `main`関数から`runApp`にウィジェットツリーを渡すことでメインループが始まる
- ウィジェットはStatelessなものとStatefullなものに大別できる
- Statefullなウィジェットが更新（`setState`）されると，そのウィジェットとその子孫のツリーが全て再構成（`build`）される
	- パフォーマンス悪そうに見えるけれど，ウィジェットツリーの変更部分のみをシステム内部のエレメントツリーに反映することで画面更新を行なっているので，最適化はされている
	- HTMLレンダラみたいな感じ

### 画面遷移
- Navigatorが現在の画面の状態スタックを持つ
	- pushで画面遷移
		- コルーチンのawaitで，遷移先がpopされた時の値を受け取れる
	- popで前の画面に戻る
		- ユーザーからの戻るボタン押下でも勝手にpopされ得る
		- 呼び出し元へ返す値を引数に設定できる
```dart
// push (遷移後の画面がpopされるまでyield)
final ret = await Navigator.of(context).push(
  MaterialPageRoute(
    builder: (context) => Widget(),
  ),
);

// pop
Navigator.of(context).pop("hello");
```