# gitBook使用

教程网 http://c.biancheng.net/
11
#### gitbook 服务开启

```gitbook serve ```

当你写得差不多，你可以执行 `gitbook build` 命令构建书籍，默认将生成的静态网站输出到 _book 目录。实际上，这一步也包含在 `gitbook serve` 里面，因为它们是 HTML，所以 GitBook 通过 Node.js 给你提供服务了。

当然，build 命令可以指定路径：

```shell
gitbook build [书籍路径] [输出路径]
1
```



## 写笔记

在这里给大家介绍一些typora比较常用的功能

### 各级标题

在typora中使用crtl + 1~6可以创建1-6级标题，1级最大，6级最小。同时typora的大纲会显示所有标题，

### 表格

可以在段落--->表格中插入表格，或者按快捷键crtl+T，mac（command+option+t）

### 代码块

这个功能用的很频繁，可以在段落--->代码块中插入，也可以使用快捷键(```+空格)

### 专注模式和打字机模式

打字机模式就是让当前输入行保持在屏幕中间，专注模式就是输入行正常颜色，其他行变灰，可以在视图中打开

### 源代码模式

源代码模式就是展示Markdown的文件本来的样子，如图

这个模式会展示出Markdown文件的标识符

### 插入图片

这个不多说，在格式--->图像里，快捷键crtl+shift+i

### 插入链接

用两个尖括号括起来就行，如下：

<[www.baidu.com](https://links.jianshu.com/go?to=http%3A%2F%2Fwww.baidu.com)>

### 更换主题

直接点主题就好，typora内置了6个主题，值得一提的是typora的主题是css格式，所以会css的小伙伴可以自己写主题，或者调整已有的主题

### 内容目录

就是你们在本文上面看到的那个目录，简单点说就是把大纲放到了文章里，在段落--->内容目录里可以找到（有标题时才能用）

### 常见的格式

就比如加粗，斜体，下划线什么的。在格式里有

https://zhou415770319.github.io/gitbookKnowledges/
