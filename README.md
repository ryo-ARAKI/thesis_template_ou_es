# thesis_template_ou_es

- 大阪大学基礎工学部システム科学科機械科学コース 卒業論文
- 大阪大学大学院基礎工学研究科機能創成専攻非線形力学領域 修士論文

用 LaTeX テンプレート

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
- `main.tex` をコンパイルすることで， `thesis/text/` 以下の章ごとに分割した tex ファイルが読み込まれる
- Overleaf や CloudLaTeX などで執筆する際はこのディレクトリのみアップロードすれば良い
- デフォルトだと修論用のスタイルになっているので，卒論を書く人は `main.tex` において以下の三点を修正すること

1. `\usepackage{hyoshi_master}` でなく `\usepackage{hyoshi_bachelor}` を使う

```LaTeX
% ===========================================
% 原稿設定
% ===========================================
\usepackage[normalem]{ulem}  % 卒論の二行組タイトルに下線をつける
% 表紙用スタイルファイル
\usepackage{hyoshi_bachelor}  % 卒論用
% \usepackage{hyoshi_master}    % 修論用
```

2. 英語アブストラクト（ `thesis/text/abstract.tex` ）を読み込まない

```LaTeX
% ===========================================
% 概要（英語） *****修士論文のみ（卒論は緒言）*****
% ===========================================
\pagenumbering{roman}
% \input{./text/abstract.tex}
% \clearpage
```

3. 緒言（ `thesis/text/chap1_introduction.tex` ）を読み込む

```LaTeX
% ===========================================
% 緒言 *****卒業論文のみ？（修論は英語概要）*****
% ===========================================
\pagenumbering{arabic}  % 以降算用数字でページ番号を記述
\input{./text/chap1_introduction.tex}
```

### `thesis/pics/`

- 画像用ディレクトリ
- このディレクトリにおいた画像を `abstract/` や `slide/` 以下からも参照可能

### `thesis/text/`

- 章ごとに分割した tex ファイル用ディレクトリ
- 修論では `abstract.tex` （英語 1 ページの概要）が必要で `chap1_introduction.tex` （コンパクトな緒言）は不要
  - 卒論はその逆で，英語の概要無しでコンパクトな緒言をつける

### `thesis/sample/`

- 上に述べた卒論/修論のスタイルでコンパイルした PDF
  - `main_batchelor.pdf` 卒業論文（特別研究）
  - `main_master.pdf` 修士論文

## コンパイルについて

私の使っている `.latexmkrc` ファイルは [ここ](https://gist.github.com/ryo-ARAKI/8a256ef600325b0344bbc3990818b691) にあります．
必要なら自由に使ってください．
