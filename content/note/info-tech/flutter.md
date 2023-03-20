---
title: flutter
tags: [note, info-tech, development, software, library]
---

## 概要
- マルチプラットフォーム GUIアプリケーション フレームワーク
	- iOS/Android，Web，Windows/Linux/Mac，組み込み
- Google製
- 使用言語はDart

## インストール
### Arch Linux

- [install-archlinux](note/info-tech/install-archlinux.md)の直後から，`flutter doctor`がオールグリーンになるまで
- 1時間ぐらいは覚悟したほうがいい
- 特にandroid-studioがクソでかいので[qemu](note/info-tech/qemu)イメージのリサイズをする羽目になった
- [参考文献](https://dev.to/nabbisen/flutter-3-on-arch-linux-shi-mefang-1m2j)
- 追記: [qemu](note/info-tech/qemu)上だとパフォーマンスがゴミすぎてまともに使えなかった X(
	- ハードウェアアクセラレーションとか頑張ればいけるのかもしれないけど，諦めてホストのMacbookに直接入れた

#### 手順
1. 依存のインストール
```bash
pacman -S base-devel xorg-server xterm i3-wm noto-fonts git clang cmake ninja chromium
visudo  # いい感じに設定 & リログ

git clone https://aur.archlinux.org/flutter.git
cd flutter
makepkg -sci  # JDKはデフォルトを選択
cd ..

git clone https://aur.archlinux.org/android-studio.git
cd android-studio
makepkg -sci
cd ..

usermod -aG flutterusers user  # 設定後にリログ
```

2. Android Studioの設定
	1. 初期設定は適当に
	2. Android StudioからFlutterプラグインをインストール＆再起動
	3. Flutterプロジェクトを作成
		- flutter SDKのパス設定を忘れずに (`/opt/flutter`)
	4. `Android SDK Command line tools`をインストール

3. flutter doctor
```bash
export CHROME_EXECUTABLE=chromium  # 必要なら永続化する
git config --global --add safe.directory /opt/flutter
flutter doctor --android-licenses
flutter doctor  # 完了
```


## 感想
- メジャーバージョンが同じでも後方互換性は乏しい
	- 過去のプロジェクトをビルドしようとしてもよくわからないエラーが大量に出てくる