# thesis_template_ou_es

- 大阪大学基礎工学部システム科学科機械科学コース 卒業論文
- 大阪大学大学院基礎工学研究科機能創成専攻非線形力学領域 修士論文

用 LaTeX テンプレートです．

----

## 使い方

### リポジトリの複製

以下に `kisokou` というGitHubユーザーが `master_thesis` という名前でこのリポジトリを複製する手順を示します．

```bash
# 1. GitHubで master_thesis という新しいリポジトリを作成する

# 2. このリポジトリをその名前でcloneする
git clone git@github.com:ryo-ARAKI/thesis_template_ou_es.git master_thesis  # SSHを利用
cd master_thesis

# 3. 自身のリモートリポジトリを登録する
git remote set-url origin git@github.com:kisokou/master_thesis.git

# 4. 自身のリモートリポジトリを更新する
git push origin HEAD
```

### 最初のコンパイル

`thesis/` ディレクトリにある `main.tex` をコンパイルすることで修士論文の形式にあったPDFが生成されます．
このテンプレートは `uplatex` で作成されているので，それに応じた設定でコンパイルしてください．
`latexmk` コマンドを使用する方は，私の使っている `.latexmkrc` ファイルが [ここ](https://gist.github.com/ryo-ARAKI/8a256ef600325b0344bbc3990818b691) にあるので使ってください．

### テンプレートへの修正の反映

このテンプレートが更新されているとき，以下のように修正点を自身のリポジトリに反映させてください．

```bash
# 1. このテンプレートのリポジトリを登録する
git remote add upstream git@github.com:ryo-ARAKI/thesis_template_ou_es.git

# 2. テンプレートの最新状態を取得する
git fetch upstream

# 3. 自分がmasterブランチにいることを確認し，テンプレートの最新状態をmergeする
git switch master && git merge upstream/master

# 4. 自身のリモートリポジトリを更新する
git push origin HEAD
```

### 卒論/修論の切り替え

`thesis/main.tex` をコンパイルすると修士論文の形式でPDFが生成されます．
卒業論文（特別研究）を執筆する場合，このファイルを以下のように修正してからコンパイルしてください．

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

----

## コンテンツ

### `abstract/`

- 修論概要用のファイル
- モノクロ書式であったり修論より図のサイズが小さくなりがちであることに注意し，
  - 画像をグレースケールにする
  - ラベルや凡例のフォントサイズを大きくする
    などに注意して図を作成する

### `slide/`

- Beamerで作成された口頭発表スライド用のファイル

### `thesis/`

- 卒論・修論用のファイル
- `main.tex` をコンパイルすることで， `thesis/text/` 以下の章ごとに分割した tex ファイルが読み込まれる
- Overleaf や CloudLaTeX などで執筆する際はこのディレクトリのみアップロードすれば良い

#### `thesis/pics/`

- 画像用ディレクトリ
- このディレクトリにおいた画像を `abstract/` や `slide/` 以下からも参照可能

#### `thesis/text/`

- 章ごとに分割した tex ファイル用ディレクトリ
- 修論では `abstract.tex` （英語 1 ページの概要）が必要で `chap1_introduction.tex` （コンパクトな緒言）は不要
  - 卒論はその逆で，英語の概要無しでコンパクトな緒言をつける

#### `thesis/sample/`

- 上に述べた卒論/修論のスタイルでコンパイルした PDF
  - `main_batchelor.pdf` 卒業論文（特別研究）
  - `main_master.pdf` 修士論文

----

## 参考文献の管理について

このテンプレートでは `biblatex` を利用して参考文献を管理しています．
また，その形式はPhysical Review Fluidsに準じています．

### `bib_articles.bib` ：Mendeleyによる文献情報の管理

`bib_articles.bib` はMendeleyで自動作成した `.bib` ファイルの例です．
これをLaTeXファイルのプリアンプルで

```latex
\addbibresource{../bib_articles.bib}
```

のように読み込むことで文献を引用することができます．
手で文献情報を管理するよりも圧倒的に楽なので，ぜひこのようにして参考文献を管理してください．

### `bib_textbooks.bib` ：手作業による文献情報の管理

`bib_textbooks.bib` は，書籍や先輩の修士論文などMendeleyで管理しづらい参考文献をまとめたファイルです．
出版社のウェブサイトやGoogle Booksを使うと書籍の参考文献情報を `.bib` ファイルで出力できるので，それらをこのファイルにまとめておくと便利です．

### `mystyle.sty` ：雑誌名の短縮形の管理

このテンプレートでは参考文献の雑誌名を短縮形で表示します．
正式名称と短縮形の変換は `mystyle.sty` に記述されています．
たとえば，

```latex
\step[
  fieldsource=journal,
  match={Annual Review of Fluid Mechanics},
  replace={Annu. Rev. Fluid Mech.}]%
```

は `Annual Review of Fluid Mechanics` という雑誌を `Annu. Rev. Fluid Mech.` という短縮形で表示するように定義しています．
現状の `mystyle.sty` では流体力学に関係する雑誌名をある程度網羅しているつもりですが，他に引用する雑誌がある場合は自身で `\step[]` 要素を増やして対応してください．

----

## 便利なパッケージ

このテンプレートでは[mystyle.sty](./mystyle.sty)に様々なパッケージを読み込んでいます．
中でもきわめて便利なパッケージをいくつか紹介します．

### [`physics` パッケージ](http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/physics/physics.pdf)

物理学で使う様々な記号や記法がサポートされています．
このパッケージを使うとNavier-Stokes方程式が，

```latex
% 普通に書く
\begin{equation}
  \frac{\partial \bm{u}}{\partial t} + (\bm{u} \cdot \bm{\nabla}) \bm{u} = -\bm{\nabla} p + \frac{1}{\mathrm{Re}} \nabla^2 \bm{u}
\end{equation}

% physicsパッケージを使って書く
\begin{equation}
  \pdv{\vb*{u}}{t} + \qty(\vb*{u} \vdot \grad) \vb*{u} &= - \grad{p} + \frac{1}{\Re} \laplacian{\vb*{u}}
\end{equation}
```

と書け，微分量やベクトル演算子がかなり楽に扱えます

### [`empheq` パッケージ](https://mirror.ibcp.fr/pub/CTAN/macros/latex/contrib/mathtools/empheq.pdf)

連立方程式をきれいに書くためのパッケージです．
例を示すと，

```latex
% alignパッケージを使って書く
\begin{align}
\left\{
  \begin{array}{ll}
    \div{\vb*{u}} &= 0 \\
    \partial_i u_i &= 0
  \end{array}
\right.
\end{align}

% empheqパッケージを使って書く
\begin{empheq}[left=\empheqlbrace]{align}
  \div{\vb*{u}} &= 0 \\
  \partial_i u_i &= 0
\end{empheq}
```

のようになり，簡単に書けることが分かります．

[連立方程式を一番美しく書けるempheq](https://muscle-keisuke.hatenablog.com/entry/2015/11/23/122725)という記事に使い方がよくまとまっています．

### [`siunitx` パッケージ](https://ctan.tetaneutral.net/macros/latex/contrib/siunitx/siunitx.pdf)

SI単位や単位付き数値を簡単に扱うためのパッケージです．

```latex
加速度の単位は\si{m \per s^{-2}}です．
重力加速度は\SI{9.81}{\meter \per \second^{-2}}です．
```

のように使います．
