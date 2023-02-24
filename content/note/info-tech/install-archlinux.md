---
title: ArchLinuxのインストール
tags: [note, info-tech, linux]
---

## 概要
- [ArchLinux](https://archlinux.org)のインストール手順を記録する
- Live Environmentの起動方法については触れない

<!-- more -->

## 前提
- [qemu](note/info-tech/qemu.md)上の仮想マシン
- BIOS
- GPT
- x86_64
- デュアルブートなし
- できるだけシンプル，ミニマリスティックに

## 手順
### 1. 事前準備

```bash
loadkeys jp106      # キーボード設定
ping google.com     # インターネット疎通確認
timedatectl status  # 時間の確認 (この時点ではUTC)
```

### 2. パーティショニング
```bash
cfdisk /dev/sda       # 先頭1MiBをBIOS bootに，残りをLinuxに設定
mkfs.ext4 /dev/sda1   # フォーマット
mount /dev/sda1 /mnt  # /mntへマウント
```

### 3. インストール
```bash
vim /etc/pacman.d/mirrorlist                    # 日本のmirrorを指定しておく
pacstrap -K /mnt base linux linux-firmware vim  # Wi-Fiで10分くらい
```

- 執筆時点で有効な日本のmirror
	- `http://mirrors.cat.net/archlinux/$repo/os/$arch`
	- `https://mirrors.cat.net/archlinux/$repo/os/$arch`

### 4. 初期設定
```bash
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt  # 以下仮想rootで作業
```
#### 時計関係
```bash
ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime  # TZを東京に
hwclock --systohc
```

#### 言語関係
- `/etc/locale.gen`を編集して，`en_US.UTF-8 UTF-8`をアンコメント
- `locale-gen`
- `/etc/locale.conf`を作成して`LANG=en_US.UTF-8`を追記-
- `/etc/vconsole.conf`を作成して`KEYMAP=jp106`を追記

#### カスタマイズ
- `/etc/hostname`にホスト名を設定
- `passwd`でrootパスワードを設定

#### ブートローダのインストール
```bash
pacman -S grub/
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

以上．