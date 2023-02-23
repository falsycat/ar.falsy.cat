---
title: qemu
tags: [computer, virtualization]
---

- 個人的に，qemuはコマンドラインベースのVirtualBoxと思っている
- 今のところM2チップのMacbook ProでLinuxを使うための最善手
	- M1/M2向けVirtualBoxはまだ開発者プレビューしかなく，まともに使えなかった

<!--more-->

## インストール

### Mac
```bash
$ brew install qemu
```
- ハードウェアアクセラレーションが有効化されている他のビルドもあるらしいが未検証
	- 今後GPU使いたくなったら検証予定

## コマンド逆引き

### archのlive cdを起動
```bash
qemu-system-x86_64 \
  -m 4G  \
  -cdrom ../iso/archlinux-2023.02.01-x86_64.iso
```

## オプション一覧
```
-m 4G         # メモリサイズ指定
-cdrom a.iso  # ISOファイル指定
```