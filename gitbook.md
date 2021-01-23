[打造完美写作系统：Gitbook+Github Pages+Github Actions](https://blog.csdn.net/qq_40889820/article/details/110013310)

## 1.安装nodejs

现在安装 Node.js 都会默认安装 npm（node 包管理工具），所以我们不用单独安装 npm，打开命令行，执行以下命令安装 GitBook：

```shell
npm install -g gitbook-cli
1
```

安装完之后，就会多了一个 **gitbook** 命令（如果没有，请确认上面的命令是否加了 `-g`）。

上面我推荐的是 GitBook + Typora + Git，所以你还需要安装 Typora（一个很棒的支持 macOS、Windows、Linux 的 Markdown 编辑工具）和 Git 版本管理工具。戳下面：

> - Typora 下载地址：https://typora.io/
> - Git 下载地址：https://git-scm.com/downloads

Typora 的安装很简单，难点在于需要翻墙才能下载（当然你也可以找我要）。Git 的安装也很简单，但要用好它需要不少时间，这里就不展开了（再讲下去怕你要跑啦~）。

### 怎么使用

想象一下，现在你准备构建一本书籍，你在硬盘上新建了一个叫 mybook 的文件夹，按照以前的做法，你会新建一个 Word 文档，写上标题，然后开始巴滋巴滋地笔耕。但是现在有了 GitBook，你首先要做的是在 mybook 文件夹下执行以下命令：

```shell
gitbook init
1
```

执行完后，你会看到多了两个文件 —— README.md 和 SUMMARY.md，它们的作用如下：

> - README.md —— 书籍的介绍写在这个文件里
> - SUMMARY.md —— 书籍的目录结构在这里配置

这时候，我们启动恭候多时的 Typora 来编辑这两个文件了：

![这里写图片描述](https://img-blog.csdn.net/2018071818281621?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2x1Y2t5ZGFyY3k=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70#pic_center)

编辑 SUMMARY.md 文件，内容修改为：

```markdown
# 目录

* [前言](README.md)
* [第一章](Chapter1/README.md)
  * [第1节：衣](Chapter1/衣.md)
  * [第2节：食](Chapter1/食.md)
  * [第3节：住](Chapter1/住.md)
  * [第4节：行](Chapter1/行.md)
* [第二章](Chapter2/README.md)
* [第三章](Chapter3/README.md)
* [第四章](Chapter4/README.md)

123456789101112
```

然后我们回到命令行，在 mybook 文件夹中再次执行 `gitbook init` 命令。GitBook 会查找 SUMMARY.md 文件中描述的目录和文件，如果没有则会将其创建。

Typora 是所见即所得（实时渲染）的 Markdown 编辑器，这时候它是这样的：

![这里写图片描述](https://img-blog.csdn.net/20180718185415241?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2x1Y2t5ZGFyY3k=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70#pic_center)

接着我们执行 `gitbook serve` 来预览这本书籍，执行命令后会对 Markdown 格式的文档进行转换，默认转换为 html 格式，最后提示 “Serving book on http://localhost:4000”。嗯，打开浏览器看一下吧：
![这里写图片描述](https://img-blog.csdn.net/20180718185251753?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2x1Y2t5ZGFyY3k=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70#pic_center)

当你写得差不多，你可以执行 `gitbook build` 命令构建书籍，默认将生成的静态网站输出到 _book 目录。实际上，这一步也包含在 `gitbook serve` 里面，因为它们是 HTML，所以 GitBook 通过 Node.js 给你提供服务了。

当然，build 命令可以指定路径：

```shell
gitbook build [书籍路径] [输出路径]
1
```

serve 命令也可以指定端口：

```shell
gitbook serve --port 2333
1
```

你还可以生成 PDF 格式的电子书：

```shell
gitbook pdf ./ ./mybook.pdf
1
```

生成 epub 格式的电子书：

```shell
gitbook epub ./ ./mybook.epub
1
```

生成 mobi 格式的电子书：

```shell
gitbook mobi ./ ./mybook.mobi
1
```

如果生成不了，你可能还需要安装一些工具，比如 ebook-convert。或者在 Typora 中安装 Pandoc 进行导出。

除此之外，别忘了还可以用 Git 做版本管理呀！在 mybook 目录下执行 `git init` 初始化仓库，执行 `git remote add` 添加远程仓库（你得先在远端建好）。接着就可以愉快地 commit，push，pull … 啦！

不是程序员的小伙伴可能不太喜欢用命令行，那其实版本管理这部分可以下载安装 Git 或 GitHub 这些客户端程序，在图形界面上操作也是可以完成工作的。





