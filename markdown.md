---
title: MarkDown
date: 2016-08-28 01:55:56
tags: markdown
---

> Markdown 语法的目标是：成为一种适用于网络的书写语言。

Markdown 不是想要取代 HTML，甚至也没有要和它相近，它的语法种类很少，只对应 HTML 标记的一小部分。Markdown 的构想不是要使得 HTML 文档更容易书写。在我看来， HTML 已经很容易写了。Markdown 的理念是，能让文档更容易读、写和随意改。**HTML 是一种发布的格式，Markdown 是一种书写的格式。**就这样，Markdown 的格式语法只涵盖纯文本可以涵盖的范围。

<!-- more -->

# 区块元素

---

### 段落和换行

> 一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行（空行的定义是显示上看起来像是空的，便会被视为空行。比方说，若某一行只包含空格和制表符，则该行也会被视为空行）。普通段落不该用空格或制表符来缩进。

### 标题

> 利用 = （最高阶标题）和 - （第二阶标题），例如：

```
This is an H1
=============

This is an H2
-------------
```

> 在行首插入 1 到 6 个 # ，对应到标题 1 到 6 阶，例如：

```
# 这是 H1

## 这是 H2

###### 这是 H6
```

### 区块引用 Blockquotes

> 在每行的最前面加上 > ：

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```
	
> Markdown 也允许你偷懒只在整个段落的第一行最前面加上 > ：

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisseid sem consectetuer libero luctus adipiscing.
```

> 区块引用可以嵌套（例如：引用内的引用），只要根据层次加上不同数量的 > ：

```
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```

### 列表

Markdown 支持有序列表和无序列表。

> 无序列表使用星号、加号或是减号作为列表标记：

```
*   Red
*   Green
*   Blue
```

等同于：

```
+   Red
+   Green
+   Blue
```

也等同于：

```
-   Red
-   Green
-   Blue
```

> 有序列表则使用数字接着一个英文句点：

```
1.  Bird
2.  McHale
3.  Parish
```

**很重要的一点是，你在列表标记上使用的数字并不会影响输出的 HTML 结果**，上面的列表所产生的 HTML 标记为：

```
<ol>
    <li>Bird</li>
    <li>McHale</li>
    <li>Parish</li>
</ol>
```

如果你的列表标记写成：

```
1.  Bird
1.  McHale
1.  Parish
```

或甚至是：

```
3. Bird
1. McHale
8. Parish
```

你都会得到完全相同的 HTML 输出。重点在于，你可以让 Markdown 文件的列表数字和输出的结果相同，或是你懒一点，你可以完全不用在意数字的正确性。

如果要在列表项目内放进引用，那 > 就需要缩进：

```
*   A list item with a blockquote:

	> This is a blockquote
    > inside a list item.
```
    	
如果要放代码区块的话，该区块就需要缩进两次，也就是 8 个空格或是 2 个制表符：

```
*   一列表项包含一个列表区块：

        <代码写在这>
```

### 代码区块

> 要在 Markdown 中建立代码区块很简单，只要简单地缩进 4 个空格或是 1 个制表符就可以，例如，下面的输入：

```
这是一个普通段落：

	这是一个代码区块。
```
    	
> 这个每行一阶的缩进（4 个空格或是 1 个制表符），都会被移除，例如：

```
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
```
	    
一个代码区块会一直持续到没有缩进的那一行（或是文件结尾）。

### 分隔线

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

```
* * *

***

*****

- - -

---------------------------------------
```

# 区段元素

-----------

> Markdown 支持两种形式的链接语法： 行内式和参考式两种形式。

> 不管是哪一种，链接文字都是用 [方括号] 来标记。

行内式的链接,只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如：

```
This is [an example](http://example.com/ "Title") 
inline link.

[This link](http://example.net/) has no title 
attribute.
```

参考式的链接是在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：

```
This is [an example][id] reference-style link.
```
	
接着，在文件的任意处，你可以把这个标记的链接内容定义出来：

```
[id]: http://example.com/  "Optional Title Here"	
```

链接内容定义的形式为：

* 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
* 接着一个冒号
* 接着一个以上的空格或制表符
* 接着链接的网址
* 选择性地接着 title 内容，可以用单引号、双引号或是括弧包着
