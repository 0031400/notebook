# standalone 单独编译局部图片
如果我们一个文章里面有很多图片是用 latex 写的话，而且这些图片还要经过自己的反复调试，每次都要编译整个文章，效率是非常慢的，所以我们可以使用 standalone ，在单独的文件编辑图片，然后引入到主文章中。  
主文件要引入 `\usepackage{standalone}` ，并且使用 `\includestandalone{relative/path/file}` 引入。文件名不用后缀，并且 windows 系统也可以使用正斜线。  
子文件需要这样声明 `\documentclass{standalone}` ，仍然需要 `\begin{document}` 开头的文章主体。
# tikz 绘制 DFA
模拟电路经常使用 DFA 图片，使用 tikz 挺方便的。  
需要引入 `\usepackage{tikz}` ，并且需要引入 `\usetikzlibrary{positioning,arrows.meta,automata}` ，在 `\begin{tikzpicture}` 里面写内容。  
`\node (p00) [state,initial] at (0,0) {(0,0)};` 是指画一个节点。 `at (0,0)` 表示这个节点的位置是在 (0,0) ， `(p00)` 表示它的变量代号是 p00 ，`{(0,0)}` 表示节点里面渲染出来的内容， 中括号里面的 `state` 会渲染出圆形。 `initial` 会渲染出初始状态，也就是一个箭头指向这个节点。要用分号结尾。  
`\node (p5) [state,right=of p4,accepting] {p5};` 这里的 `right=of p4` 表示在 p4 节点的右边。 `accepting` 表示是接受状态，有两个圆圈。位置关系使用这四个词语 `left right above below`  
`\draw [->] (p0) edge node [above] {0,1} (p1);` 表示从 p0 到 p1 画一条直线。直线上面写着 `0,1` 并且是在上面显示，也可使用左边，下面或者右边。  
`\draw [->] (p6) edge [loop above] node [above] {0,1} ();` 表示 p6 节点的上面有个指向自己的箭头，并且文字标注是在箭头的上面。
`\draw [->] (p1) to[bend left] node [above] {0} (p2);` 是指 p1 到 p2 之间有个弯箭头，并且是从左边弯的。
# 循环
```
\foreach \y in {0,1}{
			\node (p\y3) [state,accepting,right=of p\y2] {p\y3};
		}
```
上面的变量是 \y ，范围是 0,1
# 自定义命令
```
\newcommand{\includeimage}[1]{
	\begin{figure}[H]
		\centering
		\includestandalone{./#1/#1}
	\end{figure}
}
```
上面表示命令名字是 includeimage ，有一个参数。
```
\foreach \x [evaluate=\x as \xx using int(\x+1)] in {0,1,2}{
			\foreach \y in {0,1}{
					\draw [->] (p\y\x) edge node [above] {0} (p\y\xx);
				}
		}
```
上面是使用了 \x+1 的写法
# 浮点丢失问题
`! LaTeX Error: Float(s) lost.` 如果使用了 figure 环境可能会造成这种问题。解决方法是
```
\usepackage{float}
\begin{figure}[H]
	......
\end{figure}
