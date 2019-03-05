---
layout: post
title: Markdown CheatSheet!
---

source: from [Github Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

#### 1.1 Escape character
反斜线\转义输入Markdown标记符号的原义字符，原理等同shell的#。

#### 1.2 Font size
#号加文字代表不同字号的字体，二者之间必须有一个空格符。#号越多字号越小，单独一个#号为最高级标题H1，一共六级标题。
# H1
## H2
### H3
#### H4
##### H5
###### H6


创建华丽分割线，使用---（三横线上方不要有文字）。
效果如下

---

#### 1.3 Font emphasis
Italics, 斜体。使用* *或_ _包裹文字；  
Bold，加粗。使用\*\* \*\*或\_\_ \_\_包裹文字；  
Strikethrough，删除线。使用~~ ~~包裹文字。

#### 1.4 New line
Enter两次才能实现一次换行。

#### 1.5 Lists
##### 1.5.1 列表展示
   1. order 1  
   2. order 2  
   '*' unodered sub-list  
   '-' unodered sub-list  
   '+' unodered sub-list
   
上述点号均为空格符，编辑实际效果如下
1. order 1
2. order 2  
* unodered sub-list
- unodered sub-list
+ unodered sub-list

##### 1.5.2 段落对齐
在一句话的开头按三次空格符space，句子结束三次space实现。如下以点号。示意实际键入的space。

...paragraph 1..

...paragraph 2..

...paragraph 3..

...paragraph 4..



按上述展示，实际操作后的效果如下，即每段开头自动对齐，这在对齐开头非常有用。  
**以句末两次space代替Enter更常用，文字排版更美观！**

   paragraph 1  
   paragraph 2  
   paragraph 3  
   paragraph 4  

#### 1.6 Blockquotes
通过在引用的文字前加>号，引用别人的文字，可用于Email回复，或者论述的引用。
> sentence 1 这句话以>开头  
> 这句话没有内容，但为保持引用块的衔接性，此行仍以>开头，否则引用块会在中间断开！
> last quoted sentence! 这句话以>开头

#### 1.7 Tables
* 冒号用来对齐列。
* 用至少3个连字符（-）分隔header cell。
* 用管道符（|）分隔每一列。

> Colons can be used to align columns.
> ```
> | Tables         | Are           | Cool  | 
> | ---------------| :-----------: | -----:|
> | col 3 is       | right-aligned | $1600 |
> | col 2 is       | centered      |   $12 |
> | zebra sstripes | are neat      |    $1 |
> ```
> End of the blockquotes!

成品咔咔~~

| Tables         | Are           | Cool  | 
| ---------------| :-----------: | -----:|
| col 3 is       | right-aligned | $1600 |
| col 2 is       | centered      |   $12 |
| zebra sstripes | are neat      |    $1 |


#### 1.8 Code and Syntax Highlighting
> Inline \`code\` has \`back-ticks around\` it

Inline `code` has `back-ticks around` it.

> Blocks of code are fenced by lines with three back-ticks \```.  
> \```python  
> s = "Python syntax highlighting"  
> print s  
> \```
```python
s = "Python syntax highlighting"
print s
```
Note: 通过代码块内指定语言标识符实现语法着色。

#### 1.9 Task List
\- \[ \]添加tick框,\- \[x\]添加checked框。
> \- \[ \] Task 1 To do  
> \- \[x\] Task 2 Done
- [ ] Task 1 To do
- [x] Task 2 Done

#### 1.10 Inner link
##### 1.10.1 Bookmark
HTML的<a>标签最重要的属性是href，其指示的链接目标可以是外部站点，也可以是页内锚点。构建页内锚点可以实现类似书签跳转的功能，最典型的应用就是点击TOC中的目录书签跳转到指定章节阅读。
> STEP 1 定义锚点ID: `<a href="#auchor_id">bookmark_text</a>`,如`<a href="#end">Go to the End!</a>>`  
> STEP 2 定义一个ID为auchor_id的对象，这里以\<p\>为例，`<p id="auchor_id">auchor_text</p>`，如`<p id="end">The end! </p>`

成品粗来了!

<a href="#end">Go to the end</a>
<p id="end">The end! </p>  
定义书签`Go to the end!`后，点击该书签将跳转到文末id为#end的锚点

##### 1.10.2 Footnote
> STEP 1 在需要脚注的单词后添加footnote，`terminology[^Footnote]`  
> STEP 2 在文末术语区域添加脚注（注解），`[^Footnote]: explanatory notes`  

#### 1.11 Links/Images/Youtube Videos
`[Github Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)`  
[Github Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)  


`![_config.yml](https://github.com/MingCHEN4/MingCHEN4.github.io/blob/master/images/IMG_2889.jpg)`  
![_config.yml](https://github.com/MingCHEN4/MingCHEN4.github.io/blob/master/images/IMG_2889.jpg)  


`[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://www.youtube.com/watch?v=gjsVyvMZr2o&index=9&list=LL1Zf7z3vBNhFRJ5QE_evpJg&t=431s)`  
[![地中海烤鱼](https://s.ytimg.com/yts/img/favicon_48-vflVjB_Qk.png)](https://www.youtube.com/watch?v=gjsVyvMZr2o&index=9&list=LL1Zf7z3vBNhFRJ5QE_evpJg&t=431s)


Note: Videos can't be added directly but you can add an image with a link to the video like the example shown above.

#### 1.12 Related useful tools
To render *LaTeX* mathematical expressions using [**MathJax**](https://www.mathjax.org/).  
Online Markdown editor [**DILLINGER**](https://dillinger.io/) with preview function.
