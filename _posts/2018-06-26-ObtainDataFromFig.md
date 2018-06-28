---
title: Figファイルからデータ取得
description: MATLABのFigファイルからデータを取得する手法をメモ
categories:
 - Tips
tags: MATLAB, Code
---

> Figファイル：MATLABのFigureオブジェクトをそのまま保存できるファイルフォーマットとして「*.fig」がある．MATLABでのみ再度開くことができるというデメリット以外に，画像の再編成や微修正(カスタマイズ)できる利点がとても使いやすい．

保存されたFigファイルを開く方法を[公式](https://jp.mathworks.com/help/matlab/ref/openfig.html)に詳しく説明されたが，保存されたデータを取得（または修正）しようとした際のやり方はまだない．よって，これを豆知識として書いてみる．

> MEMO：MATLABが2014bで一部のメソッドを変えた(追加？)したので，新しいバージョンでの操作のみを記録する．

![MATLABfigFormat](/My-Blog/figs/MATLABfigFormat.png)

図(via [MATLAB official](https://jp.mathworks.com/help/matlab/learn_matlab/understanding-handle-graphics-objects.html))に示しているように，Figureオブジェクトに３通りの階層構造になる．これはグラフィックスプロット関数の種類によって異なる．今回は，一番多く使われる「plot」関数の場合を例(右手の構造)とする．

「plot」関数では，データを保持するオブジェクトはトップにある「Figure」オブジェクトから数えて，第三層の「Data Objects」である．それに，Dataは軸により「XData」と「YData」として保存されている．したがって，データ取得のコードは以下となる．

``` matlab
% Figure -> Axes -> Data Objects(line) -> X or Y Data
% 	h.    Children.       Children.        X(Y)Data
h = open('example.fig');
data_x = h.Children.Children.XData;
data_y = h.Children.Children.YData;
```



