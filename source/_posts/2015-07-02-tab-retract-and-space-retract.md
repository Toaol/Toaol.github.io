---
layout: post
title: Tab 缩进和空格缩进
date: 2015-07-02 22:15:29 +0800
comments: true
categories: 乱七八糟
---

写代码的途中为了代码的美观以及提高代码的可读性，常常需要使用缩进。举一个例子：

```C++
        std::string         fileName_;
        std::fstream        input_;
        int                 line_;
        int                 column_;
        TokenLocation       loc_;
        char                currentChar_;
        bool                errorFlag_;
        State               state_;
        Token               token_;
        Dictionary          dictionary_;
        std::string         buffer_;
```
在写代码的过程中使用了 `Tab` 
键来对齐代码，然而，如果就这样保存了，那么在某些时候可能会出现一些奇怪的效果。
<!--more-->

在我设置 `"tab_size": 2` 的 Sublime Text 编辑器中打开代码，效果如下：

```C++
        std::string     fileName_;
        std::fstream    input_;
        int         line_;
        int         column_;
        TokenLocation   loc_;
        char        currentChar_;
        bool        errorFlag_;
        State       state_;
        Token       token_;
        Dictionary      dictionary_;
        std::string     buffer_;

```
如果在默认 tab 为 8 个空格的记事本中打开，显示同样会很奇怪。

出现这样的效果是因为代码在保存的时候保存的是 `\t` 而非空格。
```C++
std::string         fileName_;
```
 保存的格式就是 

 ```C++
 std::string\t\t\tfileName_;
 ```
 那么在不同的环境打开的时候，环境就会根据自己的设置来显示它，就造成了上面的情况。

上面的情况只是让代码变得不好看，实际上，还有可能出现更严重的问题。比如 Python 语言。

 Python 的缩进是有意义的，那么，一旦在代码中同时使用了空格缩进与 Tab 缩进，代码就会有问题。

 ```python
 if a == 1:
    print('Hello, ')
    print('world')
 ```
如果这段代码上一句使用了 Tab 缩进而下一句使用了空格缩进，那么保存的格式就应该是

 ```python
 if a == 1:\n\tprint('Hello, ')\n    print('world')
 ```
 在执行这个程序的时候会报错，可是从肉眼看上去这段程序并没有错误。


 所以说，为了让程序在各处看起来都一样，应该坚持使用空格缩进。不过不停地按空格是很难受的，正确的做法是在写的时候用 Tab，而在保存的时候保存为空格。

在 Visual Studio 里面，按照 `Tools --> Options --> Text Editor --> C /C++-->Tabs`，选中 `Insert spaces` 就好。

在 Sublime Text 里面，在个人设置中添加一行

```python
"translate_tabs_to_spaces": true
```

其它的代码编辑器应该都提供了类似功能，写代码的时候都应该加上。