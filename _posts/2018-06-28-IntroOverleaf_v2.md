---
title: OverLeaf v2 での文書作成
description: 好き嫌いはあるだろうが，オンラインの共同執筆がトレンドと信じるので，乗り遅れないようにOverLeaf v2の使い方を勉強する．
categories:
 - Tutorial
tags: LaTeX, OverLeaf
---

## OverLeaf v2とは

一言でまとめると，オンラインで使える LaTeX 原稿執筆環境である．オフラインの環境構築は「時間」と「複雑」のクロスミックスにすぎないため，ネット環境が安定であれば，OverLeafを利用するのは好都合であろう．かつ，去年(2017)同じオンラインLaTeXサービスである(ShareLaTeX)を[買収した](https://www.sharelatex.com/blog/2017/07/20/sharelatex-joins-overleaf.html)ので，両者の長所の融合となる[OverLeaf v2](https://www.overleaf.com/blog/641-try-out-overleaf-v2#.WzHXENgzZ24)がオンラインLaTeX執筆の最善選択である．

## オンラインでLaTeXする利点と欠点

### 利点

* 環境構築が不要　◎
* 共同執筆がしやすい　○
* バージョン管理しやすい　○
* PCのシステムに問わない　△

### 欠点

* ネット環境依存　
* セキュリティの懸念
* Debugの不自由
* 容量制限

## OverLeaf v2で文章作成

好き嫌いはあるだろうが，オンラインの共同執筆がトレンドと信じるので，乗り遅れないようにサービスの使い方を勉強する．

> ### Powerful collaboration features
>
> -- via overleaf blog
>
> Overleaf v2 offers an impressive collection of new and upgraded collaboration features. The collaborative editing is faster and smoother than in Overleaf v1, and it shows you where your collaborators cursors are as they type. The new track changes mode lets you see exactly what has been changed by your collaborators, and allows you to accept or reject each individual change. You can also comment on ranges of text in your document for precise communication.
>
> ![collaboration](https://www.filepicker.io/api/file/TPnpF9pXTOmAnle4ey0q)

まず，https://v2.overleaf.com/にアクセスしてサービスを起動する．beta版なので，現時点(2018/06/26)で Overleaf or ShareLaTeX のアカウントが必須，が，両者の既存プロジェクトが影響されないので，心配無用．

### 日本語文章作成

二つの方法を紹介する．一ツ目はXeLaTeXエンジン(コンパイラ)で文章作成する，もう一つは pLaTeX + dvipdf （≒ dvips + gs）という変換経路になり，日本で現在主流であろう．

#### XeLaTeX での日本語環境設定

1. Blank Projectを作る

2. main.texの頭の部分(\documentclass{article}と\begin{document}の間)を以下のコードを入力する

   ``` latex
   \documentclass[a4paper]{bxjsarticle}
   
   \usepackage{fontspec}
   \usepackage{zxjatype}
   
   \setjamainfont{ipam.ttf}
   \setjasansfont{ipag.ttf}
   \setjamonofont{ipag.ttf}
   ```

3. 「Menu」> 「Settings」> 「Compiler」から「XeLaTeX」に設定する

4. テンプレート[@ishigaki(https://qiita.com/ishigaki/items/8da80e4da3e2249a85f8)から

   ``` latex
   %\documentclass[xelatex,ja=standard,a4paper]{bxjsarticle}
   \documentclass[a4paper]{bxjsreport}
   %\documentclass[xelatex,a4paper,precisetext,noautoxspacing]{bxjsbook}
   %
   \usepackage{fontspec}
   \usepackage{zxjatype}
   %\usepackage{xltxtra}
   \setjamainfont{ipam.ttf}
   \setjasansfont{ipag.ttf}
   \setjamonofont{ipag.ttf}
   
   \usepackage{amsmath,amssymb,amsfonts}
   \usepackage{bm}
   \usepackage{siunitx}
   
   \usepackage[colorlinks=true, bookmarks=true,
   bookmarksnumbered=true, bookmarkstype=toc, linkcolor=blue,
   urlcolor=blue, citecolor=blue]{hyperref}
   
   
   \title{平成XX年度修士論文\\XXに関する数値シミュレーション}
   \author{Hoge hoge}
   \date{平成31年2月}
   
   \begin{document}
   
   \maketitle
   
   \include{abstract}
   
   %% 目次
   \tableofcontents
   \listoffigures
   \listoftables
   
   %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
   %%%  本文
   %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
   
   \include{introduction}
   \include{solution}
   \include{result}
   \include{conclusion}
   
   
   
   %% reference
   \begin{thebibliography}{99}
   \bibitem{test1} reference
   %\bibitem{test2} reference
   %\bibitem{test3} reference
   %
   \end{thebibliography}
   
   
   \appendix
   \chapter{付録}
   
   \end{document}
   ```

#### pLaTeX での日本語環境設定

1. Blank Projectを作る

2. 「Menu」> 「Settings」> 「Compiler」から「LaTeX」に設定する

3. 「New File」をクリック，「latexmkrc」のファイル名で以下の内容を入力

   ``` latex
   $latex = 'platex';
   $bibtex = 'pbibtex';
   $dvipdf = 'dvipdfmx %O -o %D %S';
   $makeindex = 'mendex %O -o %D %S';
   $pdf_mode = 3; 
   ```

4. テンプレート

   ```latex
   \documentclass[dvipdfmx,autodetect-engine]{jsarticle}
   
   \title{サンプル文書}
   \author{著者}
   
   \begin{document}
   \maketitle
   
   \begin{abstract}
   日本語を用いた文書を作成します。    
   \end{abstract}
   
   \section{はじめに}
   
   \end{document}
   ```

   

5. おまけ
   「jlreq.cls」を用いる例：[https://v2.overleaf.com/read/xhrhnsnqwmgr](https://v2.overleaf.com/read/xhrhnsnqwmgr)



