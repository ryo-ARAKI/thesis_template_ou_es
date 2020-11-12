# thesis_templete_ou_es

- 大阪大学基礎工学部システム科学科機械科学コース 卒業論文
- 大阪大学大学院基礎工学研究科機能創成専攻非線形力学領域 修士論文

用LaTeXテンプレート

## `abstract/`

- 修論概要用のファイル
- モノクロ書式である，本文より図のサイズが小さくなりがちであることに注意し，
  - 画像をグレースケールにする
  - ラベルや凡例のフォントサイズを大きくする
  などに注意して図を作成する

## `slide/`

- 口頭発表スライド用のファイル(Beamer)

## `thesis/`

- 卒論・修論用のファイル
- `main.tex` をコンパイルすることで， `thesis/text/` 以下の章ごとに分割したtexファイルが読み込まれる
- OverleafやCloudLaTeXなどで執筆する際はこのディレクトリのみアップロードすれば良い

### `thesis/pics/`

- 画像用ディレクトリ
- このディレクトリにおいた画像を `abstract/` や `slide` 以下からも参照可能

### `thesis/text/`

- 章ごとに分割したtexファイル用ディレクトリ
- 修論では `abstract.tex` （英語1ページの概要）が必要で `chap1_introduction.tex` （コンパクトな緒言）は不要
  - 卒論はその逆で，英語の概要無しでコンパクトな緒言をつける
