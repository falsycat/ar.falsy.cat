---
title: ObsidianとQuartzによるセカンドブレインデジタルガーデンの構築
tags: [note, info-tech, web]
---

## 概要
- [Quartz](https://github.com/jackyzha0/quartz)で[Obsidian](note/info-tech/obsidian.md)のVaultを公開する
- 「*セカンドブレインデジタルガーデン*」という御大層な言葉は[Quartz](https://github.com/jackyzha0/quartz)の紹介文からの引用

<!--more-->

## 初期設定
1. [Quartz](https://github.com/jackyzha0/quartz)をforkする
2. GitHub Actionsを有効化
3. repoの設定で`workflow permission`を`read and write permissions`へ変更
	- これしないとdeployに失敗する
4. repoをローカルにclone
5. `data/config.yaml`をいい感じに編集
	- `author`など
6. `config.toml`をいい感じに編集
	- `baseURL`など
7. pushする
8. deployが終わったらGitHub Pagesのドメイン設定をする

## 記事の執筆
1. ローカルrepoの`content/`ディレクトリをVaultとしてObisidianで開く
	- `content/templates/`は弄ってはいけない
2. 記事を書く
3. pushする

## ローカルプレビュー
- まだ[qemu](note/info-tech/qemu.md)上のマシンへのOSインストール作業ができていないので，また今度試す
- なるべくホストマシンは汚したくない(切実)

## 所感
- 扱いやすい[Obsidian](note/info-tech/obsidian.md)で執筆して，[Quartz](https://github.com/jackyzha0/quartz)でいい感じに公開ができた
- 執筆のためにリポジトリをcloneしなければならないため，記事数が増えた時の複数PCの同期コストが問題になりそう
	- ブランチ分けてPullRequest活用すれば解決する？
		- 記事書くたびにPR作るのはクソめんどくさそう