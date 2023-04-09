---
title: 2人の幼女と悪魔とチェス盤
tags: [note, info-tech, logical]
---

## 概要
- 「2人の幼女とチェス盤の部屋」という次のような論理問題を解説する
	- 以下の手順の後，幼女Bが任意の整数$x\left(0\leq x<64\right)$を求められるようにするには，幼女Aはどのような操作を行うべきか
		1. 悪魔が8x8チェス盤の各マスに1個ずつ，合計0個以上64個以下のポーンをランダムに配置する
		2. 悪魔は幼女Aにチェス盤を見せ，任意の数字$x\left(0\leq x<64\right)$を伝える
		3. 幼女Aは，チェス盤に対して次のいずれかの操作のうち可能であるものを1回だけ必ず行う
			- 任意のマスからポーンを1個だけ取り除く
			- 任意のマスにポーンを1個だけ追加する
		4. 悪魔は幼女Bにチェス盤を見せる

## 問題の簡潔化
- $f(g(b,x))=x$とできるような写像$f,g$を求めよ
	- $B=\left\\{0,1\right\\}$
	- $b\in B^{64}$
	- $x\in B^6$
	- $f: B^{64} \rightarrow B^6$
	- $g: B^{64} \times B^6\rightarrow B^{64}$
		- $b$と$g(b,x)$は1ビットだけ異なる

## 解答
- $f(b)=f_0\oplus f_1\oplus f_2 \oplus \dots \oplus f_{63} \quad\left(f_i=i b_i\right)$
- $b'=g(b,x) \implies b'_m \neq b_m\quad\left(m=x\oplus f(b)\right)$
- [チェス盤が16x16の場合のプログラム](https://wandbox.org/permlink/XLo1pGURvrU4Y4Jj)

## 解説
- $x=f(b)\oplus m$となるような$m\in B^6$は必ず存在する
- 盤面の各マスに$m$の値を割り当てることで，1マスの操作だけで$m$を表現できる
	- 盤面のマス目の数も，$m$がとりうる値の数も64
	- $f(g(b,x))=f(b)\oplus m=f(b)\oplus f\_m\oplus m(1-b\_m)$

## 応用
- 長さ$2^N$の任意のビット列について，任意の1ビットだけを反転させることで，長さ$N$のビット列を表現できる

## 参考文献
- [# 超難問論理クイズ「2人の幼女とチェス盤の部屋」が本当に難しすぎた - 明日は未来だ！](https://sist8.com/chess2you)
- [幼女問題まとめ - GItHub Gist](https://gist.github.com/catupper/5678658)
- [Impossible Escape? - DataGenetics](http://datagenetics.com/blog/december12014/index.html)