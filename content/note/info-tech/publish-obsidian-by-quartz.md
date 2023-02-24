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

## カスタマイズ

### Recent Notesの表示数を変更する
1. `layouts/partials/recent.html`の`first 3 $notes`を変更する

### トップページにグローバルグラフを表示する
1. `data/graphConfig.yaml`の`enableGlobalGraph`を`true`にする

### 記事にRelated Notesを表示する
1. `layouts/partials/recent.html`を作成
2. `layouts/_default/single.html`の好きな位置に`{{partial "related.html" .}}`を挿入
3. `i18n/en.toml`に`related_notes`の翻訳を追加

layouts/partials/recent.html
```html
<div class="content-list">
  <h2>{{ i18n "related_notes" }}</h2>
  {{$notes := .Site.RegularPages.Related .}}
  {{partial "page-list.html" (first 3 $notes)}}
</div>
```

## 所感
- 扱いやすい[Obsidian](note/info-tech/obsidian.md)で執筆して，[Quartz](https://github.com/jackyzha0/quartz)でいい感じに公開ができた
- 執筆のためにリポジトリをcloneしなければならないため，記事数が増えた時の複数PCの同期コストが問題になりそう
	- ブランチ分けてPullRequest活用すれば解決する？
		- 記事書くたびにPR作るのはクソめんどくさそう