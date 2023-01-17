---
title: 一文入门Latex
date: 2023-01-03 18:54:16
tags: Latex
categories: 工具
category_bar: true
top: true
mathjax: true
---





## 什么是Latex？

LaTeX是一种基于TeX的排版系统，用于生成专业和学术文档。它通过使用标记语言来描述文档的结构和格式，使用户能够专注于文档的内容而不是排版。LaTeX可用于生成各种文档类型，如论文，书籍，幻灯片和信件。



# 配置Latex



## 安装Texlive

首先，下载Texlive，从[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)中（如下图）下载镜像即可。

> TeX Live 是一个免费的、开源的、跨平台的 TeX 发行版，提供了许多 TeX 和 LaTeX 工具，包括 pdfTeX、XeTeX、LuaTeX 等 TeX 引擎，以及大量的字体、宏包和工具。它是由 TeX 用户社区发起并维护的，并且在 GNU 通用公共许可证（GPL）下发布。TeX Live 可以在多种操作系统上使用，例如 Linux、macOS 和 Windows。它是一个集成的 TeX 发行版，可以方便地安装和维护。

![清华大学开源镜像站](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031551493.png)



下载完后我们对**iso文件**进行解压，解压后的文件夹是这样的：

![iso文件内部结构](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031551587.png)



接下来运行**install-tl-windows.bat**文件，然后会出现安装界面：

> 为了避免用户权限问题，建议使用管理员模式运行。

![执行TexLive安装器](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031554472.png)

点击Advanced，进行设置安装：

<img src="https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031555509.png" alt="设置TexLive安装选项" style="zoom:67%;" />

这里为了控制一下TeX Live占用的存储空间大小，我们可以选择修改**N. of collections**选项，去掉Texworks（比较老的编辑器，不推荐）以及部分我们日常不会使用的语言包。

![image-20230103155648765](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031556823.png)

设置完成后，点击安装，进入漫长的等待……

![image-20230103155956358](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031559433.png)

安装完毕后，使用一下命令测试是否能够正常使用。

```sh
tex -v
latex -v
xelatex -v
pdflatex -v
```

> 如果报错的话，就将 `安装路径\texlive\2022\bin\win32` 加到path环境变量中。
>



## 配置Latex编辑器

安装好Texlive后，我们还需要一个编辑器来使用Latex，这里我们选择Vscode。安装好Vscode，下载插件 LaTex Workshop

![image-20230103183901503](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031839637.png)



接下来我们创建一个 **tex** 文件来测试下插件是否起作用。

![image-20230103184257554](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301031842705.png)

全部配置好后，我们就可以开始写代码了。




# 使用Latex编写文章



Latex所有命令都以`\`开头，其后接上**命令名**，后面可跟上`{}`表示**命令的参数**

```
\命令名{参数}
```



## 声明文章类型

当 latex 处理源文件时，首先需要声明所要创建的文档类型，文档类型可由如下命令来指定。

```latex
\documentclass[选项]{文章类型}
```

**常用的文章类型**：

- **article** 文章格式的文档类，广泛用于科技论文、报告、说明文档等。
- **report** 长篇报告格式的文档类，具有章节结构，用于综述、长篇论文、简单的书籍等。
- **book** 书籍文档类，包含章节结构和前言、正文、后记等结构。
- **proc** 基于 article 文档类的一个简单的学术文档模板。
- **slides** 幻灯格式的文档类，使用无衬线字体。
- **minimal** 一个极其精简的文档类，只设定了纸张大小和基本字号，用作代码测试的最小工作示例。
- **ctexart**  支持中英文混排的文字





**常用选项**：

- **10pt, 11pt, 12pt …** 指定文档的基本字号。默认为 10pt。
- **a4paper, letterpaper, …** 指定纸张大小，默认为美式信纸 letterpaper（大约相当于 21*.*6 cm *×* 28*.*0 cm）。
- **twoside, oneside** 指定单面/双面排版。双面排版时，奇偶页的页眉页脚、页边距不同。article和 report 默认为 oneside，book 默认为 twoside。
- **onecolumn, twocolumn** 指定单栏/双栏排版。默认为 onecolumn。
- **openright, openany** 指定新的一章 \chapter 是在奇数页（右侧）开始，还是直接紧跟着上一页开始。report 默认为 openany，book 默认为 openright。对 article 无效。
- **landscape** 指定横向排版。默认为纵向。
- **titlepage, notitlepage** 指定标题命令 \maketitle 是否生成单独的标题页。article 默认为notitlepage，report 和 book 默认为 titlepage。
- **fleqn** 令行间公式左对齐。默认为居中对齐。
- **leqno** 将公式编号放在左边。默认为右边。
- **draft, final** 指定草稿/终稿模式。草稿模式下，断行不良（溢出）的地方会在行尾添加一个黑色方块；插图、超链接等功能也会受这一组选项影响。默认为 final。





## 内容的书写环境

Latex中书写内容的环境，类似于编程语言中的作用域，任何介于同一个**begin**和**end**之间的内容都属于同一环境，位于同一环境的内容将会共享相同的文字格式。

```latex
\begin{环境类型}
内容
\end{环境类型}
```



### 正文区

我们所有的内容，都会书写在名为 **document** 的环境中

```latex
\begin{document}
内容
\end{document}
```



`\textbf{内容}`：**bold font**，加粗

`\textit{内容}`：italic，斜体

`\underline{内容}`：下划线

`\paragraph{段落名}` 开启一个段落。

> 除此之外，添加新段落，还可以输入两个**换行符**；单独的一个换行符只会生成一个空格。

`\subparagraph{段落名}` 开启一个子段落。





### 前言区

所有位于`\begin{document}`前的内容被称为前言（Preamble），类似HTML的`head`，可以在这里指定页面格式、尺寸、需要导入的宏包等，如：

```latex
\title{文章的标题}
\author{作者的名字}
\date{文档的修改日期}  % 可以设置自动生成当天的日期 `\date{\today}`
\usepackage{graphicx} % 导入宏包graphicx 
```

设置完前言的内容后，我们还需要在标题的**正文区**添加一个`\maketitle`命令：在当前位置生成文档的标题，标题内容就是在前言中设定的信息。

```latex
\documentclass{ctexart}

\title{文章的标题}
\author{作者的名字}
\date{文档的修改日期}  %可以设置自动生成当天的日期 \date{\today}

% 导入宏包graphicx
\usepackage{graphicx}

\begin{document}
\maketitle
\end{document}
```





## 使用列表

无序列表：`\begin{itemize}...\end{itemize}`

列表中的每一个元素都需要以`\item`开头

```latex
\begin{itemize}
\item 列表项1
\item 列表项2
\item 列表项3
\end{itemize}
```



有序列表：`\begin{enumerate}...\end{enumerate}`

与无序列表相同，列表中的每一个元素都需要以`\item`开头



## 使用表格

使用`tabular`环境：（其参数含义为：三个c表示表格存在三列，`c`表示居中，可以替换为`l`左对齐，`r`右对齐

```latex
\begin{tabular}{c c c}
单元格1 & 单元格2 & 单元格3 \\
单元格4 & 单元格5 & 单元格6 \\
\end{tabular}
```

表格中每一列的数据需要使用`&`分隔开，每一行的数据需要使用`\\`分割。



==为表格添加边框==：

此时的表格是完全无边框的，我们可以在参数中使用`{|c|c|c|}`来添加竖直方向的边框，在内容中使用`\hline`添加水平方向的边框（你甚至可以添加两次`\hline`来实现双横线的效果）。



==为每一列指定单独宽度==：

若未指定宽度，其宽度是统一且自动设置的，若你需要为单独的一列指定宽度，按照如下格式：

```latex
\begin{tabular}{p{2cm}|c|c} 
```

将`c`替换为`p{宽度}`(paragraph)



==为表格取标题==：

与图片类似，使用`caption{标题名}`来指定表格的标题，具体使用可参看**图片**的格式书写。





## 添加图片

若要添加图片，需要现在前言区引用**graphicx**包

```latex
\usepackage{graphicx}
```

然后在正文区使用`\includegraphics{图片名}`：在当前位置添加一张图片（图片名可省略后缀，如**.png**)

若图片尺寸不符，可以选择参数进行调整：textwidth为当前文档宽度，0.5表示0.5倍。

```latex
\includegraphics[width=0.5\textwidth]{}
```



**给图片添加标题：**
先将图片嵌套在一个**figure**环境中，然后使用**caption**来指定图片的标题：（这里还使用了**centering**使图片居中）

```latex
\begin{figure}
\centering
\includegraphics[width=0.5\textwidth]{图片名}
\caption{图片标题}
\end{figure}
```





## 章节

开启新章节：

```latex
\section{章节的名字}
章节下的内容
```

子章节：

```latex
\section{章节1}
Hello World
\subsection{子章节1.1}
Hello Word
\subsubsection{子章节1.1.1}
Hell Word
```



> 如果使用到的文档类型是`\docunmentclass[UTF-8]{ctexbook}`，我们还可以加入比`section`更大的`chapter`，通常用来表示书籍中的第几章。比`chapter`还要大的有`part`，通常用来表示书籍中的第几部。
















# 使用Latex排版数学公式

[Latex数学公式在线编辑器](https://latex.codecogs.com/eqneditor/editor.php)

## 行内和行间公式

Latex中的数学公式有两种排版方式：

其一是与文字混排，称为**行内公式**；行内公式由一对 `$` 符号包裹：$a^2 + b^2 = c^2$.

```latex
$a^2 + b^2 = c^2$.
```



其二是单独列为一行排版，称为**行间公式**；行间公式居中独占一行，两边各使用`$$`将内容括住，还可以用 `\tag` 命令对行间公式的编号：



$$a^2 + b^2 = c^2 \tag{1}$$

```latex
$$a^2 + b^2 = c^2 \tag{1}$$
```

> 除了使用`$$`，使用`\begin{equation}...\end{equation}`也能实现行间公式，或简写为`\[ ... \]`
>



## 公式中的常用字符

### 字符转义

 **# $ % & ~ _ ^ \ { }** 有特殊意义，需要表示这些字符时，需要转义：

| Latex命令        | 输出符号 | Latex命令 | 输出符号 |
| ---------------- | -------- | --------- | -------- |
| `\#`             | #        | `\$`      | $        |
| `\%`             | %        | `\{`      | {        |
| `\}`             | }        | `\sim`    | ~        |
| `\_{}`           | _        | `\^{}`    | ^        |
| `\textbackslash` | \        | `\&`      | &        |





### 公式中的空格

数学模式中输入的空格被忽略。数学符号的间距默认由符号的性质（关系符号、运算符等）决定。需要人为引入间距时，使用 `\quad` 和 `\qquad` 等命令。

```latex
1\quad+\quad2\quad=\quad3
```

$$1\quad+\quad2\quad=\quad3$$



### 加减乘除模

**拉丁字母**、**阿拉伯数字**和 `+`、`-`、`*`、`/`、`=` 运算符均可以直接输入获得，其他常用运算符有：

| 符号   | latex      | 效果      |
| ------ | ---------- | --------- |
| 乘号   | `(\times)` | $\times$  |
| 除号   | `(\div)`   | $\div$    |
| 点乘   | `(\cdot)`  | $\cdot$   |
| 加减号 | `(\pm)`    | $(\pm)$   |
| 加减号 | `(\mp)`    | $(\mp)$   |
| 取模   | `\bmod`    | $\bmod$   |
| 约等于 | `\approx`  | $\approx$ |
| 恒等于 | `\equiv`   | $\equiv$  |
| 不等号 | `\neq`     | $\neq$    |





### 省略号

`\ldots`点位于基线上，`\cdots`点设置为居中，`\vdots`使其垂直，`\ddots`对角线排列

$$ x_{1},x_{2},\ldots,x_{5}  \quad x_{1} + x_{2} + \cdots + x_{n} $$





### 上下标 

`_`表示下标、`^`表示上标。

```latex
$$f(x)= a_{ij}^{2} + b^3_{2}=x^{t+1} $$
```


$$f(x)= a_{ij}^{2} + b^3_{2}=x^{t+1} $$

>**当上下标内容不止一个字符时，需用大括号括起来**(在其他符号中也适用）。

除此之外还有一些常用的标签：

| 标签              | latex                | 效果                   |
| ----------------- | -------------------- | ---------------------- |
| `\overset{}{}`    | \overset{5}{1}       | $\overset{5}{1}$       |
| `\underset{}{}`   | \underset{2}{3}      | $\underset{2}{3}$      |
| `\overline`       | \overline{x+y}       | $\overline{x+y}$       |
| ` \underline`     | \underline{a+b}      | $\underline{a+b}$      |
| `\vec`            | \vec{123}            | $\vec{123}$            |
| `\overrightarrow` | \overrightarrow{123} | $\overrightarrow{123}$ |
| `\overleftarrow`  | \overleftarrow{123}  | $\overleftarrow{123}$  |
| `\hat`            | \hat{x}              | $\hat{x}$              |
| `\bar`            | \bar{y}              | $\bar{y}$              |





### 绝对值、根号、分式

| 符号                                          | latex         | 效果          |
| --------------------------------------------- | ------------- | ------------- |
| 绝对值`|内容|`                                | `S_2`         | $|S_2|$       |
| 根号 `\sqrt`表示平方根，`\sqrt[n]`表示n次方根 | `\sqrt{x}`    | $\sqrt{x}$    |
| 分式 `\frac`                                  | `\frac{x}{m}` | $\frac{x}{m}$ |





### 高数

| 符号         | latex                          | 效果                          |
| ------------ | ------------------------------ | ----------------------------- |
| 积分`\int`   | `\int_{1}^{5}x\mathrm{d}x`     | $\int_{1}^{5}x\mathrm{d}x$    |
| 极限`\lim`   | ` \lim_{x \to \infty}x^2_{22}` | $\lim_{x \to \infty}x^2_{22}$ |
| 求和`\sum`   | `\sum_{n=1}^{20} n^{2}`        | $\sum_{n=1}^{20} n^{2}$       |
| 乘积`\prod`  | `\prod_{j=1}^{3} y_{j}`        | $\prod_{j=1}^{3} y_{j}$       |
| 求导`'`      | `f(x)'`                        | $f(x)'$                       |
| 无穷`\inify` | `\infty`                       | $\infty$                      |





### 矩阵

矩阵有`matrix`、`bmatrix`、`vmatrix`、`pmatrix`，其区别为在于外面的括号不同，`&`用于分隔列，`\`用于分隔行。
格式如：


$$
\begin{bmatrix} 
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{bmatrix}
$$

$$
\begin{matrix} 
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{matrix}
$$

$$
\begin{vmatrix} 
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{vmatrix}
$$

$$
\begin{pmatrix} 
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{pmatrix}
$$





## 参照表

### 二元运算符

<img src="https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301061008703.png" alt="在这里插入图片描述" style="zoom:80%;" />



### 二元关系符

所有的二元关系符都可以加 `\not` 前缀得到相反意义的关系符，例如 `\not=` 就得到不等号（同 \ne）。

<img src="https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301061008782.png" alt="在这里插入图片描述" style="zoom:80%;" />





### 希腊字母

**希腊字母**无法直接通过键盘输入获得，在LaTeX中通过反斜杠`\`加上其`字母读音`实现，详见下表:

<img src="https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301161122352.png" alt="image-20230116112222260" style="zoom:80%;" />





