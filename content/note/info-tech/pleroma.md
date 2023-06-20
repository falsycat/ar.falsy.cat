---
title: Pleroma
tags: [note, info-tech, web]
---

## 概要
- ActivityPubに対応したlightweight(自称)なSNS
- 単体で見るとlightweightには思えないけど，mastodonと比べたら確かにlightweight

## DB肥大化問題
- 長期間Pleromaを稼働させ続けると，DBのレコード数がやばいことになる
- DBのレスポンスがくそ長くなり，最終的にタイムアウトで500になる
- オブジェクトの寿命とか設定してみたけど特に意味はなかった

### 解決法
- ローカルアカウントそれ自体の情報以外の情報を削除する
- pleromaを停止して，postgresで次のSQLを実行する
	- 自動化しても良いかもしれない
- 追記: **フォロー/フォロワー情報も削除されてしまったので改善が必要！！！**
```SQL
TRUNCATE TABLE activities CASCADE;  # 全アクティビティの削除
DELETE FROM users WHERE not local;  # 全リモートユーザーの削除
VACUUM FULL;
VACUUM ANALYZE;
```