---
title: qemu
tags: [note, info-tech, tool, virtualization]
---

## 概要
- コマンドラインベースのVirtualBoxと思っている
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

### ディスクイメージの作成
```bash
qemu-img create -f qcow2 sda.qcow2 16G
```

### ディスクイメージのリサイズ
```bash
# ホストOSで実行
qemu-img resize sda.qcow2 +16G

# ゲストで実行
cfdisk /dev/sda  # いい感じに
e2fsck -f /dev/sda2
resize2fs /dev/sda2
```

### archのlive cdを起動
```bash
qemu-system-x86_64 \
  -m 4G  \
  -cdrom ../iso/archlinux-2023.02.01-x86_64.iso  \
  sda.qcow2
```
- [関連: ArchLinuxのインストール方法](note/info-tech/install-archlinux.md)