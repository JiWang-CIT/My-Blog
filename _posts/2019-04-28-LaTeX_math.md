---
title: LaTeX数学公式总结
description: $\LaTeX$公式写作技巧总结
date: 2019-04-28 20:42:34
categories:
 - Tutorial
tags: LaTeX
---

## 基础数学公式表达

$\LaTeX$中的数学公式表达可以分为行内公式和行间公式，说白了，就是公式是否单独另起一行。行内公式的书写比较单一，一般来说就是将书写内容用`$`(美刀)符号夹住。例如：$\mathrm{$y=ax$} \rightarrow y=ax$。

而行间公式的书写稍显复杂，这方面markdown做得更简洁，`$$`前后夹住表达内容，就代表了单独一行书写公式。而latex需要使用一个代码块：

```latex
\documentclass{article}
\usepackage{amsmath} % 加载数学表达用宏宝
\begin{document}

% 插入行间公式，如果不需要公式序号，则使用equation*
\begin{equation}
E = mc^2
\end{equation}

\end{document}
```

上文经过编译后的结果如下
$$
E=mc^2 \tag{1}
$$
公式中的英文字体和文章中的字体有些略微区别，比如斜体的字符间距，默写情况就不是很符合读写习惯，所以如果公式中有需要插入英文单词的时候，推荐使用`\textit{}`来插入单词。
$$
\begin{eqnarray}
\$\textrm{different}\$ &\longrightarrow different \\
\textrm{\textit{different}} &\longrightarrow \textit{different}
\end{eqnarray}
$$

### 数学符号的字体选择

这里插一段题外话，关于数学公式的字体选择，latex的标准字体是Computer Modern字体，而一般论文会使用Times系统的字体，比如比较有名的Times New Roman等。这里备注两种常用的字体，需要的时候可以和数学宏宝一同预先载入。

``` latex
\usepackage{newtxtext,newtxmath} % 正文和数学公式都使用Times系字体
\usepackage{newpxtext,newpxmath} % 正文和数学公式都使用Palatino系字体
\usepackage{mathpazo}		 % 正文和数学公式都使用Palatino系字体，设计略微不同
```

### 基础数学表达

#### 上下标

$$
\begin{align*}
\textrm{2^{3}} & \longrightarrow & 2^{3} \\
\textrm{2_{a}} & \longrightarrow & 2_{a} \\
\textrm{2^{\circ}} & \longrightarrow & 2^{\circ} \\
\textrm{\underset{0\leq j}{\arg\min}} & \longrightarrow & \underset{0\leq j}{\arg\min}
\end{align*}
$$

另外可以用宏(Macro)来增加一些常用数学表达式的便捷性

```latex
\newcommand{\combination}[2]{_{#1} \mathrm{C}_{#2}} % 预定义
\combination{n}{k} = \frac{n!}{k! (n-k)!} % 正文中
```

$$_n \mathrm{C}_{k} = \frac{n!}{k! (n-k)!}$$



#### 多行公式的对齐

align：用`&`分割各个对齐单元，使用`\\`换行。 它的每行是一个公式，都会独立编号。

split：它用于将一个公式拆分成多行，但是它整体还只是一个公式。

```latex
\begin{align}
 f(x) & = (x+a)(x+b) \\
      & = x^2 + (a+b)x + ab
\end{align}
\begin{split}
 f(x) & = (x+a)(x+b) \\
      & = x^2 + (a+b)x + ab
\end{split}
```

$$
\begin{align}
 f(x) & = (x+a)(x+b) \tag{2}\\
      & = x^2 + (a+b)x + ab	\tag{3}
\end{align}
$$

$$
	\begin{align*}
 	f(x) & = (x+a)(x+b) \\
      	 & = x^2 + (a+b)x + ab	\tag{4}
	\end{align*}
$$

#### 空格

```latex
a \! b \, c \: d \; e \quad f \qquad g \hspace{1cm}
```

$$
a \! b \, c \: d \; e \quad f \qquad g \hspace{1cm}
$$

#### 求和，乘积，积分

```latex
\sum_{i=1}^{n} \qquad 
\int_{0}^{\pi} \qquad
\prod_\epsilon \qquad
\sum_{\substack{0<i<n \\ 0<j<n}} A_{ij}
```

$$
\sum_{i=1}^{n} \qquad 
\int_{0}^{\pi} \qquad
\prod_\epsilon \qquad
\sum_{\substack{0<i<n \\ 0<j<n}} A_{ij}
$$

#### 分数

```latex
\frac{x^{2n}}{k+1} \qquad
x^{\frac{2}{k+1}}  \qquad
x^{1/2}
```

$$
\frac{x^{2n}}{k+1} \qquad
x^{\frac{2}{k+1}}  \qquad
x^{1/2}
$$

#### 向量

```latex
\vec{a} \qquad
\overrightarrow{AB}
```

$$
\vec{a} \qquad
\overrightarrow{AB}
$$

#### 开根号

```latex
\sqrt{x} \qquad
\sqrt[3]{2} \qquad
\surd[x^2+y^2]
```

$$
\sqrt{x} \qquad
\sqrt[3]{2} \qquad
\surd[x^2+y^2]
$$

