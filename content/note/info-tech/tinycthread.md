---
title: tinycthread
tags: [note, info-tech, 'c-language', development]
---

[tinycthread](https://tinycthread.github.io) / [API doc](https://tinycthread.github.io/doc/tinycthread_8h.html)

## 概要
- スレッド関係の機能を提供するlightweightなライブラリ
	- `mtx`: mutex
	- `cnd`: condition variable
	- `thrd`: thread
	- `tss`: thread-specific storage
- C11
- zlib license
- マルチプラットフォーム
- CMake利用可能

## 導入方法
### CMake: FetchContent
```cmake
# ---- tinycthread ----
# repository: https://github.com/tinycthread/tinycthread
# license   : zlib

FetchContent_Declare(
  tinycthread
  GIT_REPOSITORY "https://github.com/tinycthread/tinycthread.git"
  GIT_TAG        "6957fc8383d6c7db25b60b8c849b29caab1caaee"
)
FetchContent_MakeAvailable(tinycthread)
```