# latex-template

LaTeX（ラテフ）は、レポートや学術論文などの文書作成に適したフリーの組版制御ソフトです。数式や図表の自由な配置編集や、自動的な目次や索引の作成、相互参照の構築など、文書作成のさまざまな機能を備えています。
このレポジトリはlatexを使った論文作成のためのテンプレートです。

---

## 1. 環境設定

VS CodeはLaTeX環境としておすすめです。「LaTeX Workshop」によりリアルタイムPDFプレビュー、自動補完、エラー表示が可能で、効率的に作業が進むからです。
さらに、軽量で動作が速く、Gitや他ツールとの統合も優れています。カスタマイズ性が高く、初心者から上級者まで幅広く対応可能。クロスプラットフォーム対応でどのOSでも一貫した環境が構築できます。

参考
- [【自研究室向け】LaTeX+VSCode環境構築 2023年版](https://qiita.com/fuku_uma/items/e5ad46125a9612320273)
- [LaTeX Workshop を使いこなす](https://qiita.com/Yarakashi_Kikohshi/items/a9357dd469320ffb65a0)

---

### 1.1 VSCodeとLatexのインストール

**MacOSの場合**  
homebrewでいずれもインストールできます。ターミナルから以下のコードを実行してください。

```bash
# vscodeのインストール
brew install visual-studio-code --cask
# latexのインストール
brew install --cask mactex-no-gui
sudo tlmgr update --self --all
sudo tlmgr paper a4
```

MacOSでhomebrewを使っていない人はいますぐ使えるようになってください。  
これが使えるようになると、今後の全ての環境構築が圧倒的に楽になります。  
- [【macOS版】初心者でもわかる！Homebrewのインストール手順を徹底解説](https://zenn.dev/inablog/articles/5e790c9fbdad20)
- [2024年版 Homebrew完全ガイド：macOSのパッケージマネージャーを使いこなす](https://qiita.com/yu_uk/items/73654985fb1caeab4cec)


**Windowsの場合**  
動作確認をしていないので、以下の資料を読んでインストールしてください。  
[【大学生向け】LaTeX完全導入ガイド Windows編 (2022年)](https://qiita.com/passive-radio/items/623c9a35e86b6666b89e)

---

### 1.2 Latexmkrcの設定

(スキップしても動作する可能性あり。設定しておけば安心。)  
ターミナルで以下を実行する。

```bash
# ホームディレクトリに移動
cd ~
# .latexmkrcファイルの作成
touch .latexmkrc
# 作成した.latexmkrcファイルを編集
opent .latexmkrc
```

テキストエディタ等で開かれた.latexmkrcファイルに、以下のコマンドをコピペして保存する。

```bash{filename=".latexmkrc"}
# 通常の LaTeX ドキュメントのビルドコマンド
$latex = 'uplatex %O -kanji=utf8 -no-guess-input-enc -synctex=1 -interaction=nonstopmode %S';
# pdfLaTeX のビルドコマンド
$pdflatex = 'pdflatex %O -synctex=1 -interaction=nonstopmode %S';
# LuaLaTeX のビルドコマンド
$lualatex = 'lualatex %O -synctex=1 -interaction=nonstopmode %S';
# XeLaTeX のビルドコマンド
$xelatex = 'xelatex %O -no-pdf -synctex=1 -shell-escape -interaction=nonstopmode %S';
# Biber, BibTeX のビルドコマンド
$biber = 'biber %O --bblencoding=utf8 -u -U --output_safechars %B';
$bibtex = 'upbibtex %O %B';
# makeindex のビルドコマンド
$makeindex = 'upmendex %O -o %D %S';
# dvipdf のビルドコマンド
$dvipdf = 'dvipdfmx %O -o %D %S';
# dvipd のビルドコマンド
$dvips = 'dvips %O -z -f %S | convbkmk -u > %D';
$ps2pdf = 'ps2pdf.exe %O %S %D';

# PDF の作成方法を指定するオプション
## $pdf_mode = 0; PDF を作成しない。
## $pdf_mode = 1; $pdflatex を利用して PDF を作成。
## $pdf_mode = 2; $ps2pdf を利用して .ps ファイルから PDF を作成。
## pdf_mode = 3; $dvipdf を利用して .dvi ファイルから PDF を作成。
## $pdf_mode = 4; $lualatex を利用して .dvi ファイルから PDF を作成。
## $pdf_mode = 5; xdvipdfmx を利用して .xdv ファイルから PDF を作成。
$pdf_mode = 3;

# PDF viewer の設定
$pdf_previewer = "start %S";  # "start %S": .pdf に関連付けられた既存のソフトウェアで表示する。

## Windows では SyncTeX(PDF をビューアーで開いたまま中身の更新が可能で更新がビューアーで反映される機能) が利用できる SumatraPDF 等が便利。
## ぜひ SyncTeX 機能のあるビューアーをインストールしよう。
## SumatraPDF: https://www.sumatrapdfreader.org/free-pdf-reader.html
## $pdf_previewer = 'SumatraPDF -reuse-instance';
```

---

### 1.3 VSCodeの設定

初めてVSCodeを使う時は、日本語に設定しておくと楽。
[Visual Studio Code（VSCode）の設定をしてみた](https://qiita.com/TS1engineer/items/1b54f65ee87cb49582f5)

1. 左の「拡張機能」タブから「Latex-Workshop」をインストール
2. 左下の歯車マークから「設定」を開き、右上の「設定(JSON)を開く」をクリック
3. settings.jsonが開かれるので、本レポジトリの同名ファイルの中身をコピペする。
Windowsの場合は[こちら](https://qiita.com/fuku_uma/items/e5ad46125a9612320273#:~:text=VSCode%E3%81%AE%E8%A8%AD%E5%AE%9A-,Windows%E3%81%AE%E5%A0%B4%E5%90%88,-Mac%E3%81%AE%E5%A0%B4%E5%90%88)を参考にする。

---

## 2. 運用方法

### 2.1 本レポジトリのダウンロード

本レポジトリ「latex-template」をダウンロードする方法は大きく2つ。

### 2.2 latexのコンパイル

main.texをコンパイルしてPDFファイルを作成する方法は大きく2つ。
1. latex-workshopタブから実行する
   1. 任意のtexファイルを開く
   2. 左のタブに「TEX」と表記されたlatex-workshopのタブをクリックして開く
   3. 「コマンド」内の「LaTeXプロジェクトをビルド」をクリックでPDFを更新
   4. 「LaTeX PDFを表示」をクリックしてPDFを開く
2. texファイルを保存して自動更新する
   1. 任意のtexファイルを開く
   2. 「control + S」でファイルを保存する

settings.jsonの設定で、保存時に自動でPDFが保存される。  
動作が重いときは、settings.jsonの"latex-workshop.latex.autoBuild.run"を"off"にする。  
もしくは、main.texを\documentclass[report, 12pt, a4paper, draft]{jsbook} にしてdraftモードを有効にし、画像の出力を省略する。


---

## 3. 各ディレクトリの説明

```markdown
latex-template
├── main.tex                   # メインファイル（全体をまとめる）
├── preamble
│   ├── packages.tex           # 使用するパッケージ
│   ├── settings.tex           # ドキュメント設定（章構成、引用スタイルなど）
│   └── macros.tex             # カスタムコマンド・マクロ定義
├── frontmatter
│   ├── title.tex              # タイトル
│   ├── abstractEN.tex         # 英文要旨
│   ├── abstractJP.tex         # 和文要旨
│   └── contents.tex           # 目次・図表目次
├── mainmatter                 # 各章ごとの内容
│   ├── chapter1.tex
│   ├── chapter2.tex
│   ├── chapter3.tex
│   ├── chapter4.tex
│   └── chapter5.tex
├── backmatter
│   ├── citations.tex          # 参考文献リスト
│   ├── references.bib         # bibtexファイル
│   ├── appendix.tex           # 付録
│   └── acknowledgements.tex   # 謝辞
├── output
│   └── main.pdf            　　# 最終出力物
├── figure                     # 図専用のディレクトリ
│   └── figure_sample.png
├── table                      # 表専用のディレクトリ
│   ├── table_sample1.tex
│   └── table_sample2.tex
├── log                        # ログファイルや中間生成物
├── template                   # テンプレート関連
├── settings.json              # settings
└── README.md
```

---

