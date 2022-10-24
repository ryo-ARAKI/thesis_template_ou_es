# thesis_template_ou_es

このリポジトリは

- 大阪大学基礎工学部システム科学科機械科学コース 卒業論文
- 大阪大学大学院基礎工学研究科機能創成専攻非線形力学領域 修士論文

用非公式 LaTeX テンプレートです．

----

## 使い方

以下の手順に従わず，ファイル一式を単純にダウンロードしてももちろん使用できますが，Git(Hub)を用いて差分管理しながら論文を執筆することを強く推奨します．
Git(Hub)の勉強については[私が以前作成した資料](https://github.com/ryo-ARAKI/Saturday_LT/blob/master/git_tutorial/git_tutorial.md)と[スライド](https://github.com/ryo-ARAKI/Saturday_LT/blob/master/git_tutorial/git_tutorial.pdf)がありますが，断然おすすめなのは慶應大の渡辺先生の[GitHub演習](https://github.com/kaityo256/github)です．

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
    % 緒言 *****卒業論文のみ（修論は英語概要）*****
    % ===========================================
    \pagenumbering{arabic}  % 以降算用数字でページ番号を記述
    \input{./text/chap1_introduction.tex}
    ```

----

## コンテンツ

### `abstract/`

- 修論概要用のファイル
- モノクロ書式なこと，修論より図のサイズが小さくなりがちなことに注意し，
  - 画像をグレースケールにする
  - ラベルや凡例のフォントサイズを大きくする

  などに注意して図を作成する

### `slide/`

- Beamerによる発表スライド用のファイル

### `thesis/`

- 卒論/修論用のファイル
- `main.tex` をコンパイルすることで， `thesis/text/` 以下の章ごとに分割した tex ファイルが読み込まれる
- Overleaf や CloudLaTeX などで執筆する際はこのディレクトリのみアップロードすれば良い
  - その場合も `mystyle.sty` や `.bib` ファイルは必要である
  - `main.tex` 内のパスを適切に書き換えること

#### `thesis/pics/`

- 画像用ディレクトリ
- このディレクトリにおいた画像を `abstract/` や `slide/` 以下からも参照可能になっている

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
また，その書式はPhysical Review Fluidsに準じています．

### `bib_articles.bib` ：Mendeleyによる文献情報の管理

`bib_articles.bib` はMendeleyで自動作成した `.bib` ファイルの例です．
これをLaTeXファイルのプリアンプルで

```latex
\addbibresource{../bib_articles.bib}
```

のように読み込むことで文献を引用することができます．
手で文献情報を管理するよりも圧倒的に楽なので，ぜひこの方法で参考文献を管理してください．

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

### 日本語文献と英語文献での場合分け

[BibLaTeX で日本語文献と英語文献の混在を扱う(2018年版)](http://granular.blog39.fc2.com/blog-entry-76.html)という記事を参考に，最終著者前の区切りを英語文献のときは `, and` ，日本語文献のときは `, ` としています．
日本語文献の定義は， `.bib` ファイルで `langid={Japanese}` というフィールドを記述することで可能です．
`bib_textbooks.bib` にいくつか日本語の文献を定義しているので参考にしてください．

----

## `latexdiff` を用いた差分管理

Git(Hub)を用いて論文を執筆することで `.tex` の差分は管理できますが， `.pdf` 上の変更点は比較することができません．
また，指導教員に添削をお願いする際も最新版のPDFを渡すだけではどこが変更されたのか分かりづらく，負担になってしまいます．
より快適に原稿の更新と添削のサイクルを回すため， `latexdiff` を用いたPDF上での差分表示を推奨します．
いま，修正前の `old.tex` と修正後の `new.tex` があったとき，

```latex
latexdiff -e utf8 -t CFONT --flatten old.tex new.tex > diff.tex
latexmk diff.tex
```

のようにすれば，変更前の箇所が青色・小さいフォントサイズで，変更後の箇所が赤色・大きなフォントサイズで表示されたPDFが得られます．
使用しているオプションは以下のとおりです．

- `-e utf8` 文字エンコーディングの指定
- `-t CFONT` 差分表示の指定．デフォルトだと打ち消し線と下波線での表示になるが，見づらいのでこちらがおすすめ
- `--flatten` `input` などで読み込んでいる別の `.tex` ファイルを正しく制御するために必要

文章に大きな修正を加えた際，作成した `diff.tex` がうまくコンパイルできないことがあります．
そのような場合はデフォルトで `--math-markup=2` となっている数値を下げるなどすれば「おおらかに」修正点を取り扱ってくれるようです．
また，参考文献周りでエラーが出る場合，差分ファイル中の参考文献を `.bbl` ファイルの内容で置き換えるとよいです．

- 参考
  - [Overleaf: Using Latexdiff For Marking Changes To Tex Documents](https://www.overleaf.com/learn/latex/Articles/Using_Latexdiff_For_Marking_Changes_To_Tex_Documents)
  - [にっき♪：latexdiff](http://abenori.blogspot.com/2016/06/latexdiff.html)

### Gitと `latexdiff` の連携

上記の例ではわざわざ `old.tex` と `new.tex` という2つのファイルを準備していましたが，これはいかにも面倒です．
そこで，Gitを使った差分管理と連携するためのツールとして `latexdiff-vc` があります．
先の例で `main.tex` というファイルの一つ前のコミットとの差分を見たいとすると

```latex
latexdiff-vc -e utf8 -t CFONT --flatten --git --force -r HEAD^ main.tex
```

で差分ファイルが出力されます．
`-r` 以降に差分をとる対象を記述します．
この例では `HEAD^` で直近のコミットを指定していますが，コミットハッシュやブランチ名も利用できます．
例えば，デフォルトの`master` ブランチの他に `work` や自分の名前でブランチを作っておき，普段はそこでcommitを積み重ねて先生に見てもらう段階で `master` ブランチとの差分PDFを作成し，プルリクエストを出してマージする，のようなワークフローが考えられます．
さらに教員の添削を反映するためのブランチを作っても良いですが，やりすぎるとわけが分からなくなってしまうので注意しましょう．

- 参考：[Gitで管理しているLaTeXのdiffをpdfで見る(TeXLive2015版)](https://nekketsuuu.github.io/entries/2017/01/27/latexdiff-vc.html)

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

- 参考：[連立方程式を一番美しく書けるempheq](https://muscle-keisuke.hatenablog.com/entry/2015/11/23/122725)

### [`siunitx` パッケージ](https://ctan.tetaneutral.net/macros/latex/contrib/siunitx/siunitx.pdf)

SI単位や単位付き数値を簡単に扱うためのパッケージです．

```latex
加速度の単位は\si{m \per s^{-2}}です．
重力加速度は\SI{9.81}{\meter \per \second^{-2}}です．
水の同粘性系数は\(\nu = 1.0 \times 10^-6\, \si{m^2/s}\)である．
```

のように使います．

- 参考：[単位：実験AのためのLaTeX小技集](https://uec.medit.link/latex/units.html)

----

## 役立つリンク集

### [Detexify](http://detexify.kirelabs.org/classify.html)

手（マウス）書きでLaTeXの記号を探せる．
論文や教科書で出てきた見たことない記号を入力する際にとても便利です．

### [svgnames Colors](https://www.latextemplates.com/svgnames-colors)

`xcolor` パッケージに `svgnames` オプションをつけて読み込んだ際に利用できる色名の一覧です．
なお，本テンプレートでは `xcolor` パッケージをオプション無しで読み込んだのち，documentclassのオプションとして `svgnames` を導入しています．

### その他

- [self_checklist.md](./self_checklist.md)
  - 論文を先生に見てもらう前にチェックすべきことをまとめてあります．項目が多いですが，先生の時間を形式の添削に費やすのはもったいないのできちんと確認しましょう．
- [akira-okumura：修士論文 LaTeX テンプレート](https://github.com/akira-okumura/MasterThesisTemplate)
  - 名古屋大学の奥村先生による修論用のLaTeXテンプレートです．非常に充実しているのでぜひ目を通してください．このテンプレートで扱えていない内容として，
    - §5 剽窃について
    - §6 色覚多様性と作図

    はかならず読んでおきましょう．
- [Qiita: LaTeXにおける正しい論文の書き方](https://qiita.com/birdwatcher/items/5ec42b35d84d3ee2ffbb)
- [Qiita: アカデミックヤクザにキレられないためのLaTeX論文執筆メソッド](https://qiita.com/suigin/items/10960e516f2d44f6b6de)
  - 一部タイトルが不穏当ですが，非常によくまとまっているので論文を書き始める前に一通り目を通しておきましょう．
- [LaTeXのTipsや備忘録](https://github.com/ryo-ARAKI/TIL/blob/master/latex_tips.md)
  - 私がLaTeXを使っていてぶつかった問題点とその解決策をまとめています．
- [StackOverflow: Answer to 'What commands are there for horizontal spacing?'](https://tex.stackexchange.com/a/74354)
  - 水平スペースにもいろいろな種類があるので適切なものを使いましょう．
