# standalone 单独编译局部图片
如果我们一个文章里面有很多图片是用 latex 写的话，而且这些图片还要经过自己的反复调试，每次都要编译整个文章，效率是非常慢的，所以我们可以使用 standalone ，在单独的文件编辑图片，然后引入到主文章中。  
主文件要引入 `\usepackage{standalone}` ，并且使用 `\includestandalone{relative/path/file}` 引入。文件名不用后缀，并且 windows 系统也可以使用正斜线。  
子文件需要这样声明 `\documentclass{standalone}` ，仍然需要 `\begin{document}` 开头的文章主体。
