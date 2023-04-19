此文转载自：https://blog.csdn.net/qq_40889820/article/details/110013310#commentBox



### 文章目录

- [前言](https://blog.csdn.net/qq_40442753/article/details/110157897#_1)
- [Getting Started](https://blog.csdn.net/qq_40442753/article/details/110157897#Getting_Started_25)
- [Gitbook](https://blog.csdn.net/qq_40442753/article/details/110157897#Gitbook_28)
- - [安装](https://blog.csdn.net/qq_40442753/article/details/110157897#_29)
  - - [环境需求](https://blog.csdn.net/qq_40442753/article/details/110157897#_30)
    - [利用npm安装gitbook](https://blog.csdn.net/qq_40442753/article/details/110157897#npmgitbook_37)
  - [创建](https://blog.csdn.net/qq_40442753/article/details/110157897#_55)
  - [输出](https://blog.csdn.net/qq_40442753/article/details/110157897#_91)
  - - [website](https://blog.csdn.net/qq_40442753/article/details/110157897#website_93)
    - [ebook](https://blog.csdn.net/qq_40442753/article/details/110157897#ebook_163)
  - [配置](https://blog.csdn.net/qq_40442753/article/details/110157897#_190)
  - [插件](https://blog.csdn.net/qq_40442753/article/details/110157897#_210)
  - [其他](https://blog.csdn.net/qq_40442753/article/details/110157897#_484)
  - - [自动生成SUMMARY.md文件](https://blog.csdn.net/qq_40442753/article/details/110157897#SUMMARYmd_486)
    - [可参考的book.json文件](https://blog.csdn.net/qq_40442753/article/details/110157897#bookjson_561)
  - [小结](https://blog.csdn.net/qq_40442753/article/details/110157897#_623)
- [Github Pages](https://blog.csdn.net/qq_40442753/article/details/110157897#Github_Pages_629)
- - [概述](https://blog.csdn.net/qq_40442753/article/details/110157897#_631)
  - [开通](https://blog.csdn.net/qq_40442753/article/details/110157897#_637)
  - - [新建github仓库](https://blog.csdn.net/qq_40442753/article/details/110157897#github_639)
    - [设置Github Pages](https://blog.csdn.net/qq_40442753/article/details/110157897#Github_Pages_667)
    - [新建gh-pages分支](https://blog.csdn.net/qq_40442753/article/details/110157897#ghpages_681)
  - [小结](https://blog.csdn.net/qq_40442753/article/details/110157897#_739)
- [Travis CI](https://blog.csdn.net/qq_40442753/article/details/110157897#Travis_CI_747)
- - [概述](https://blog.csdn.net/qq_40442753/article/details/110157897#_749)
  - [开始使用](https://blog.csdn.net/qq_40442753/article/details/110157897#_757)
  - [编写.travis.yml](https://blog.csdn.net/qq_40442753/article/details/110157897#travisyml_786)
  - [测试](https://blog.csdn.net/qq_40442753/article/details/110157897#_844)
  - [小结](https://blog.csdn.net/qq_40442753/article/details/110157897#_893)
- [Github Actions](https://blog.csdn.net/qq_40442753/article/details/110157897#Github_Actions_911)
- - [概述](https://blog.csdn.net/qq_40442753/article/details/110157897#_913)
  - [快速开始](https://blog.csdn.net/qq_40442753/article/details/110157897#_940)
  - [编写.github/workflow/*.yml](https://blog.csdn.net/qq_40442753/article/details/110157897#githubworkflowyml_990)
  - [测试](https://blog.csdn.net/qq_40442753/article/details/110157897#_1046)
  - [小结](https://blog.csdn.net/qq_40442753/article/details/110157897#_1068)
- [后记](https://blog.csdn.net/qq_40442753/article/details/110157897#_1081)

# 前言

本文最终实现的是：**利用Github Actions自动导出Gitbook并将其部署到Github Pages**。

效果展示：https://wangzhebufangqi.github.io/Leetcode/

项目github地址：https://github.com/wangzhebufangqi/auto-export-gitbook
(如果觉得有趣，不妨点个star!😄后续更新第一时间会放在这个仓库)

最开始的灵感来源为使用 travis + gitbook + github pages 优雅地发布自己的书[1](https://blog.csdn.net/qq_40442753/article/details/110157897#fn1)，后来在学习的过程中发现Github Actions和Github结合的更加密切，因此将Travis CI替换成了Github Actions，并在原文的基础上进行了一系列优化。

本文涉及到的主要工具、技术有：

- markdown
- gitbook
- git/github
- github pages
- travis ci
- github actions

默认你会以下的技能：

- 使用过github，掌握了一定的命令
- fq

# Getting Started



如果你想快速使用👉[使用方法](https://github.com/wangzhebufangqi/auto-export-gitbook/blob/main/README.md#使用方法)
(最终使用时本地无需安装gitbook，本地只需要配置好git环境)

# Gitbook



## 安装



### 环境需求

NodeJS(4.0及以上版本)Windows, Linux, Unix, 或 Mac OS X其中，NodeJS可在其官网(https://nodejs.org/zh-cn/)下载安装。安装好后可查看版本号：![image-20201118151905747](https://img-blog.csdnimg.cn/img_convert/9907d861b0f0ce8d381b3cb9ac6f051e.png)

### 利用npm安装gitbook

安装好NodeJS后，可利用它的包管理器(npm)安装gitbook：`npm install gitbook-cli -g 12`npm的包安装分为本地安装(local)、全局安装(global)两种
本地安装:
npm install xxx 安装到命令行所在目录的node_module目录。
全局安装:
npm install xxx -g 安装到 \AppData\Roaming\npm\node_modules目录gitbook-cli是一个实用程序，可在同一系统上安装和使用多个版本的gitbook。 它将自动安装所需版本的gitbook。安装好后可查看版本号：![image-20201118151758803](https://img-blog.csdnimg.cn/img_convert/9168272e3744d54bdd4b34cb2b789da0.png)

## 创建

gitbook能创建模板书：`gitbook init[./directory] 12`最后一个参数为创建的目录，可省略，默认为当前目录下。![image-20201118154028943](https://img-blog.csdnimg.cn/img_convert/ebcfe1b255cf4151d8043f4c89a6f43a.png)命令执行完后会生成两个文件：`README.md`和`SUMMARY.md`README.md文件用来介绍该书籍，SUMMARY.md文件为该书籍的目录。对SUMMARY.md文件进行如下编辑：`# Summary * [Introduction](README.md)* [Easy](easy/README.md)    * [1.Two Sum](easy/1.Two Sum.md)    * [7.Reverse Integer](easy/7.Reverse Integer.md)* [Medium](medium/README.md)    * [2.Add Two Numbers](medium/2.Add Two Numbers.md)    * [3.Longest Substring Without Repeating Characters](medium/3.Longest Substring Without Repeating Characters.md)123456789`再次执行命令`gitbook init`，如果目录里的文件不存在，将会自动创建：![image-20201118155520614](https://img-blog.csdnimg.cn/img_convert/372b049390e6fa1fe32be4e85595d55a.png)然后我们对其中的md文件编写相应的内容即可。

## 输出



### website

执行命令可进行预览：`gitbook serve ./{book_name}  12`最后一个参数指定输出静态网站内容的目录，可省略，默认会在当前目录下新建一个子目录`_book`：![image-20201118160610682](https://img-blog.csdnimg.cn/img_convert/b1a6745b20908015372b8e29c7c061a4.png)若只执行`gitbook build`，会生成_book目录，但不能预览。_book目录中包含以下文件：`│  index.html│  search_index.json│├─easy│      1.Two Sum.html│      1.Two Sum.md│      7.Reverse Integer.html│      7.Reverse Integer.md│      index.html│      README.md│├─gitbook│  │  gitbook.js│  │  style.css│  │  theme.js│  ││  ├─fonts│  │  └─fontawesome|  |		..(略)│  ├─gitbook-plugin-fontsettings|  |		..│  ├─gitbook-plugin-highlight│  │		..│  ├─gitbook-plugin-livereload│  │		..│  ├─gitbook-plugin-lunr│  │		..│  ├─gitbook-plugin-search│  │		..│  ├─gitbook-plugin-sharing│  │		..│  └─images│          apple-touch-icon-precomposed-152.png│          favicon.ico└─medium        2.Add Two Numbers.html        2.Add Two Numbers.md        3.Longest Substring Without Repeating Characters.html        3.Longest Substring Without Repeating Characters.md        index.html        README.md1234567891011121314151617181920212223242526272829303132333435363738394041`可以看到原md文件都对应生成了一个html文件(README.md生成了index.html)，新生成的gitbook文件夹包含了一些主题、样式、字体、插件、图像等。同时也可以看到，默认加载了7个插件。关于插件的内容，后文会详细介绍。在网址`localhost:4000`即可预览书籍，即本机的4000端口。按`CTRL+C键`可退出，退出后，浏览器页面点击目录不再跳转。![image-20201118160828465](https://img-blog.csdnimg.cn/img_convert/866fbc82847a9e0f29f18b8974ad61f7.png)这时候如果想将书籍提供给他人阅读，岂不是只需要将这个静态网站打包，再上传到服务器上即可？没错！就是这样。

### ebook

gitbook创建的书籍还可以导出为电子书，比如pdf、epub和mobi格式。`gitbook pdf ./ ./mybook.pdf gitbook epub ./ ./mybook.epub gitbook mobi ./ ./mybook.mobi12345`其中，最后一个参数表示输出文件的文件名，可省略，默认输出为当前目录下的book文件。
再前面一个参数表示gitbook所在的目录。

直接运行上述命令可能会报错，导出电子书之前，需先安装一款本地电子书管理工具：[Calibre](https://calibre-ebook.com/)

**安装后记得将其安装根目录添加到环境变量PATH中**

然后就可以成功的导出为电子书了。

转成的pdf格式如下：



![image-20201118165358050](https://img-blog.csdnimg.cn/img_convert/3ca73f4239ee318a689ed3173d2d2218.png)

可惜的是有个小问题，导出的pdf无论是左侧书签还是TOC目录，在跳转上存在着一些问题。但是导出的epub和mobi都非常棒。

## 配置

所有的配置都以**JSON格式**存储在名为 `book.json` 的文件中。主要有以下字段：

| 字段          | 示例                                                         | 说明                                                         |
| :------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| gitbook       | { “gitbook”: “>=2.0.0” }                                     | 探测用来生成书本的GitBook的版本。格式是一个 [SEMVER](http://semver.org/) 条件。 |
| title         | {“title”: “Summary”}                                         | 书名，默认从README中提取                                     |
| authon        | {“author”: “tom”}                                            | 作者名                                                       |
| description   | { “description”: “This is my first book!” }                  | 定义了书本的描述，默认是从 **README**(第一段)中提取的。      |
| isbn          | { “isbn”: “978-7-115-32010-0” }                              | 定义了书本的ISBN                                             |
| language      | { “language”: “fr” }                                         | 定义了书本的语言，默认值是 `en`                              |
| direction     | { “direction”: “rtl” }                                       | 用来重新设置语言的文字方向的。rtl：从右至左。ltr：从左至右   |
| styles        | {“styles”: { “website”: “styles/website.css”, “pdf”: “styles/pdf.css” } } | 自定义书本的css                                              |
| plugins       | { “plugins”: [“myplugins”] }                                 | 插件列表                                                     |
| pluginsConfig | { “pluginsConfig”: { “myplugins”: { “message”: “Hello World” } } } | 插件配置                                                     |
| structure     | { “structure”: {“readme”: “INTRO.md” } }                     | 指定README，SUMMARY等文件的路径                              |
| variables     | { “variables”: { “myTest”: “Hello World” } }                 | 定义在 [模板](https://chrisniael.gitbooks.io/gitbook-documentation/content/format/templating.html) 中使用的变量值 |
| links         | “links” : { “sidebar” : { “Home” : “https://wangzhebufangqi.github.io” } } | 在左侧导航栏添加链接信息                                     |

## 插件

插件是扩展 GitBook 功能(电子书和网站)最好的方式。**查找插件**

在nmp官网(https://www.npmjs.com/ )上搜索关键词`gitbook-plugin`或`gitbook`即可

**添加插件**

添加至`book.json`文件后，再执行命令`gitbook install`将插件下载至本地即可

```json
{



	"plugins": ["myPlugin", "anotherPlugin"]



}1234
```

**删除插件**

如果不想使用自带的插件，在插件名称前面加`-`：

```json
{



	"plugins":[ "-search"]



}1234
```

如果不是自带的，将其从插件列表中去掉即可。

**插件推荐**：

**折叠目录**👉[Expandable-chapters-small](https://github.com/chrisjake/gitbook-plugin-expandable-chapters-small)

```json
{    



    "plugins": ["expandable-chapters-small"] 



}1234
```

**提供非官方的github按钮(star, fork, sponsor, and follow )**👉[github-buttons](https://github.com/azu/gitbook-plugin-github-buttons)

```json
{



  "plugins": [



    "github-buttons"



  ],



  "pluginsConfig": {



    "github-buttons": {



      "buttons": [{



        "user": "azu",



        "repo": "JavaScript-Plugin-Architecture",



        "type": "star",



        "size": "large"



      }, {



        "user": "azu",



        "type": "follow",



        "width": "230",



        "count": false



      }]



    }



  }



}123456789101112131415161718192021
```

| Option  | Description                                                  | 备注               |
| :------ | :----------------------------------------------------------- | :----------------- |
| `user`  | GitHub username that owns the repo/Username to sponsor       | 必须，用户名       |
| `repo`  | GitHub repository to pull the forks and watchers counts      | 必须，仓库名       |
| `type`  | Type of button to show: `watch`, `fork`, `sponsor`, or `follow` | 必须，4种类型之一  |
| `count` | Show the optional watchers or forks count: *none* by default or `true` | 可选，是否显示计数 |
| `size`  | Optional flag for using a larger button: *none* by default or `large` | 可选，按钮大小     |

**Google Analysis**👉[ga](https://github.com/GitbookIO/plugin-ga)

```json
{



    "plugins": ["ga"],



    "pluginsConfig": {



        "ga": {



            "token": "UA-XXXX-Y"



        }



    }



}123456789
```

在Google Analysis官网(https://analytics.google.com/)(需fq)开通服务获取Token

**百度多渠道统计**👉[baidu-tongji-with-multiple-channel](https://github.com/snowdreams1006/gitbook-plugin-baidu-tongji-with-multiple-channel)

单渠道：

```json
{



    "plugins": [



        "baidu-tongji-with-multiple-channel"



    ],



    "pluginsConfig": {



        "baidu-tongji-with-multiple-channel": {



            "token": "73be72a36cee8ef8daa9843c7861cecc"



        }



    }



}1234567891011
```

推荐！百度统计官网：https://tongji.baidu.com/

**Disqus评论插件**👉[disqus](https://github.com/GitbookIO/plugin-disqus)

```json
{



    "plugins": ["disqus"],



    "pluginsConfig": {



        "disqus": {



            "shortName": "XXXXXXX"



        }



    }



}123456789
```

登录disqus官网(https://disqus.com/)(需fq)，申请一个shortName。

**页面顶部编辑本页**👉[editlink](https://github.com/zhaoda/gitbook-plugin-editlink)

```json
{



  "plugins": ["editlink"],



  "pluginsConfig": {



    "editlink": {



      "base": "https://github.com/zhaoda/webpack-handbook/edit/master/content",



      "label": "Edit This Page",



      "multilingual": false



    }



  }



}1234567891011
```

**复制代码按钮**👉[copy-code-button](https://github.com/WebEngage/gitbook-plugin-copy-code-button)

```json
{



    "plugins": ["copy-code-button"]



}1234
```

**锚点导航-ex**👉[anchor-navigation-ex](https://github.com/zq99299/gitbook-plugin-anchor-navigation-ex)

```json
{



  "plugins": [



       "anchor-navigation-ex"



  ]



}123456
```

- 给页面H1-H6标题增加锚点效果
- 浮动导航模式
- 页面内顶部导航模式
- 导航标题前的层级图标是否显示，自定义H1-H3的层级图标
- plugins[“theme-default”],页面标题层级与官方默认主题的`showLevel`层级关联
- plugins[“theme-default”],插件样式支持官网默认主题的三种样式：White、Sepia、Night
- 在页面中增加`<extoc></extoc>`标签，会在此处生成TOC目录
- 在页面中增加`<!-- ex_nonav -->`标签，不会在该页面生成悬浮导航
- config.printLog=true,打印当前的处理进度，排错很有用
- config.multipleH1=false,去掉丑陋的多余的1. 序号(如过您的书籍遵循一个MD文件只有一个H1标签的话)
- config.showGoTop=true,显示返回顶部按钮 V1.0.11+
- config.float.floatIcon 可以配置浮动导航的悬浮图标样式 V1.0.12+
- 在页面中增加`<!-- ex_nolevel -->`不会在该页面生成层级序号 V1.0.12+

**定制页脚👉**[page-footer-ex](https://github.com/zq99299/gitbook-plugin-page-footer-ex)

```json
{



    "plugins": [



        "page-footer-ex"



    ],



    "pluginsConfig": {



        "page-footer-ex": {



            "copyright": "[mrcode](https://github.com/zq99299)",



            "markdown": true,



            "update_label": "<i>updated</i>",



            "update_format": "YYYY-MM-DD HH:mm:ss"



        }



    }



}1234567891011121314
```

**基于Prism的代码高亮**👉[prism](https://github.com/gaearon/gitbook-plugin-prism)

使用prism时，要移除默认的代码高亮插件highlight

```json
{



  "plugins": ["prism", "-highlight"]



}1234
```

选择CSS样式：([https://github.com/PrismJS/prism](https://github.com/PrismJS/))

```json
"pluginsConfig": {



  "prism": {



    "css": [



      "prismjs/themes/prism-solarizedlight.css"



    ]



  }



}12345678
```

通过别名化现有前缀来支持非标准语法前缀：

```json
"pluginsConfig": {



  "prism": {



    "lang": {



      "flow": "typescript"



    }



  }



}12345678
```

忽视某些语言：

```json
"pluginsConfig": {



  "prism": {



    "ignore": [



      "mermaid",



      "eval-js"



    ]



  }



}123456789
```

**中文搜索**👉[search-pro](https://www.npmjs.com/package/gitbook-plugin-search-pro)

```json
{



    "plugins": [



      "-lunr", "-search", "search-pro"



    ]



}123456
```

**捐赠打赏**👉[donate](https://github.com/willin/gitbook-plugin-donate)

```json
{



    "plugins": ["donate"],



    "pluginsConfig": {



        "donate": {



          "wechat": "例：/images/qr.png",



          "alipay": "http://blog.willin.wang/static/images/qr.png",



          "title": "默认空",



          "button": "默认值：Donate",



          "alipayText": "默认值：支付宝捐赠",



          "wechatText": "默认值：微信捐赠"



        }



    }



}1234567891011121314
```

**左侧拖拽栏**👉[splitter](https://github.com/yoshidax/gitbook-plugin-splitter)

```json
{



    "plugins": ["splitter"]



}1234
```

**…**

更多插件推荐可参考gitbook常用的插件[2](https://blog.csdn.net/qq_40442753/article/details/110157897#fn2)

## 其他



### 自动生成SUMMARY.md文件

前面提到，修改SUMMARY.md文件后，再执行`gitbook init`命令可以创建不存在的文件。那么是否存在一种方法，使得新创建md文件后，无需去手动修改SUMMARY.md呢？(若是不去修改SUMMARY.md文件呢？创建的md文件就不会被导出为html文件，加入不了静态网站或电子书)

实际上，存在两种方法可以自动生成SUMMARY.md文件，一种是[gitbook-plugin-summary](https://github.com/julianxhokaxhiu/gitbook-plugin-summary)，另一种是[Gitbook Summary](https://github.com/imfly/gitbook-summary)。

第一种是一个插件，笔者尝试了几次没有取得好的效果，这里就不采用它了。

第二种是先将其作为一个npm包，进行全局安装，然后运行脚本，效果挺好。

下面对第二种方法进行简单的介绍：

**安装**

```bash
npm install -g gitbook-summary
12
```

下载到路径：C:\Users\LENOVO\AppData\Roaming\npm\node_modules\gitbook-summary

**使用**

进入到项目根目录，执行`book sm`命令，即可生成SUMMARY.md文件。后面可带参数：



![image-20201118202054326](https://img-blog.csdnimg.cn/img_convert/77abd41a5beeac7bef34e34412fd0f8e.png)

```bash
PS F:\gitbookTest> book sm --help



Usage: summary|sm [options]



 



Generate a `SUMMARY.md` from a folder



 



Options:



  -r, --root [string]           root folder, default is `.`



  -t, --title [string]          book title, default is `Your Book Title`.



  -c, --catalog [list]          catalog folders included book files, default is `all`.



  -i, --ignores [list]          ignore folders that be excluded, default is `[]`.



  -u, --unchanged [list]        unchanged catalog like `request.js`, default is `[]`.



  -o, --outputfile [string]     output file, defaut is `./SUMMARY.md`



  -s, --sortedBy [string]       sorted by sortedBy, for example: `num-`, defaut is sorted by characters



  -d, --disableTitleFormatting  don't convert filename/folder name to start case (for example: `JavaScript` to `Java Script`), default is `false`



  -h, --help                    output usage information



12345678910111213141516
```

为了简便，可以将参数写入到`book.json`文件中，比如：

```javascript
{



    "title": "json-config-name",



    "outputfile": "test.md",



    "catalog": "all",  // or [chapter1，chapter2, ...]



    "ignores": [],  //Default: '.*', '_book'...



    "unchanged": [], // for example: ['myApp'] -> `myApp` not `My App`



    "sortedBy": "-",



    "disableTitleFormatting": true // default: false



}12345678910
```

然后只需在命令行执行`book sm`即可。

采用这种方式自动生成的SUMMARY.md文件：

```markdown
# Summary



 



- [Easy](easy/README.md)



  * [1.Two Sum](easy/1.Two Sum.md)



  * [7.Reverse Integer](easy/7.Reverse Integer.md)



- [Medium](medium/README.md)



  * [2.Add Two Numbers](medium/2.Add Two Numbers.md)



  * [3.Longest Substring Without Repeating Characters](medium/3.Longest Substring Without Repeating Characters.md)12345678
```

### 可参考的book.json文件

基础版：`{	"title": "Summary",	"plugins" : [		"expandable-chapters",		"github-buttons",		"editlink",		"copy-code-button",		"page-footer-ex",		"anchor-navigation-ex",		"expandable-chapters-small",		"prism", 		"-highlight",		"-lunr", 		"-search", 		"search-pro",		"donate",		"splitter"	],	"pluginsConfig": {		"editlink": {			"base": "https://github.com/wangzhebufangqi/ActionTest/tree/main",			"label": "Edit This Page"		},			"github-buttons": {			"buttons": [{				"user": "wangzhebufangqi",				"repo": "ActionTest",				"type": "star",				"size": "small"			}]		},			"page-footer-ex": {            "copyright": "By [wangzhebufangqi](https://github.com/wangzhebufangqi)，使用[知识共享 署名-相同方式共享 4.0协议](https://creativecommons.org/licenses/by-sa/4.0/)发布",            "markdown": true,            "update_label": "<i>updated</i>",            "update_format": "YYYY-MM-DD HH:mm:ss"		},			"prism": {			"css": ["prismjs/themes/prism-solarizedlight.css"],			"lang": {"flow": "typescript"}		},			"donate": {			"wechat": "https://gitee.com/wangzhebufangqi/PictureBed/raw/master/20201122131942.png",			"alipay": "https://gitee.com/wangzhebufangqi/PictureBed/raw/master/20201122131820.png",			"title": "",			"button": "Donate",			"alipayText": "支付宝捐赠",			"wechatText": "微信捐赠"		}			},	"ignores" : ["_book", "node_modules"]}	123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354`使用的插件无需在第三方网站上进行注册。只需要修改对应的github用户名与图片链接即可。

## 小结

gitbook是一个基于Node.js的命令行工具，可使用Github/Git来制作精美的电子书。这部分介绍了gitbook的本地预览，后文会介绍将其部署到Github Pages上。

更多gitbook相关可参考Gitbook文档(中文版)[3](https://blog.csdn.net/qq_40442753/article/details/110157897#fn3)

# Github Pages



## 概述



> [Github Pages](http://pages.github.com/) 是面向用户、组织和项目开放的公共静态页面搭建托管服务，站点可以被免费托管在 Github 上，你可以选择使用 Github Pages 默认提供的域名 [github.io](https://jekyllcn.com/docs/github-pages/) 或者自定义域名来发布站点。

每个github账号有且只有一个主页站点(<username>.github.io)，无限多的项目站点(<username>.github.io/repo)。

## 开通



### 新建github仓库

如未开通主页站点，先新建名为`<username>.github.io`(如：wangzhebufangqi.github.io)的仓库，再在其中添加文件`index.html`即可访问主页站点，可能需要等10分钟左右。❗**其实不开通主页站点也能开通项目站点。**

利用主页站点配合jekyll、hexo等静态博客生成系统可以搭建博客。可以参考笔者的博客搭建[4](https://blog.csdn.net/qq_40442753/article/details/110157897#fn4)。闲话休提，下面的主角是项目站点。

新建空仓库`gitbookTest`，不必勾选添加README.md文件



![image-20201119191310496](https://img-blog.csdnimg.cn/img_convert/6a083341e2bb09a3db039bfea438946f.png)

按前文所提到的，只需要将`_book`中的文件上传到该仓库，再开通Github Pages就能访问站点了。试一试：

```bash
cd _book



git init



git add .		#添加_book目录下的所有文件



git commit -m "first commit"



git branch -M main



git remote add origin https://github.com/wangzhebufangqi/gitbookTest.git  #注意修改用户名



git push -u origin main12345678
```

push完成后仓库目录为：



![image-20201119212710757](https://img-blog.csdnimg.cn/img_convert/fe2fdb28e92f22e283edebfc77651eb6.png)

### 设置Github Pages

进入仓库，`Settings -> Options -> Github Pages`选择好分支与目录，点击Save。![image-20201119213533949](https://img-blog.csdnimg.cn/img_convert/6c1228ff996518b537475abf1cc0040e.png)

访问项目站点([wangzhebufangqi.github.io/gitbookTest](https://wangzhebufangqi.github.io/gitbookTest))：(下图效果未新增插件，有时更新站点需要较长时间)



![image-20201119213825955](https://img-blog.csdnimg.cn/img_convert/a162a1707d5e5769ba1d87d279f72086.png)

到这一步，已经成功的将gitbook生成的书籍部署到了Github Pages上。但是又有问题来了，每次新增或删除文件时，都要执行gitbook build，进入到_book目录，再手动push，能不能更简单、智能一些呢？

### 新建gh-pages分支

Github支持一个名为Travis CI的服务，后面会提到，可以简单看成能执行线上脚本的工具。这就需要将根目录也push进仓库。同时也可以发现，Github Pages可以选择分支，这就提供了一种思路：将项目根目录下所有源文件push进仓库的main分支利用Travis CI服务生成_book将_book中的所有文件push进同一个仓库的gh-pages分支Github Pages依赖的分支设置为gh-pages(默认完成)如此这般。下面在不利用Travis CI的情况下测试一遍：**删除并新建github仓库**进远程仓库，`Settings -> Options ->Danger Zone -> Delete this repository`删除远程仓库比较麻烦，为了方便这里将其直接删除再重新新建(本地git记录也要删掉)。**将根目录下所有文件push进main分支(gitbook编译前)**`git initgit add .		#添加根目录下的所有文件git commit -m "first commit"git branch -M maingit remote add origin https://github.com/wangzhebufangqi/gitbookTest.git  #注意修改用户名git push -u origin main1234567`**gitbook编译**`gitbook build1`在项目根目录下重新生成_book文件夹**将_book目录下所有文件push至gh-pages分支**`cd _bookgit initgit remote add origin https://github.com/wangzhebufangqi/gitbookTest.gitgit add .git commit -m "second commit"git branch -M maingit push --force --quiet "https://github.com/wangzhebufangqi/gitbookTest.git" main:gh-pages #将_book中的main分支强制提交到远程仓库的gh-pages分支，不提示多余消息12345678`可以看到创建分支成功![image-20201119225049542](https://img-blog.csdnimg.cn/img_convert/07f085691f5c09d03b1aed8b93a8c83c.png)**设置Github Pages依赖分支**会默认设置好为gh-pages的根目录![image-20201119225222220](https://img-blog.csdnimg.cn/img_convert/74bd34a91e2211bdb83c6830001583a1.png)

## 小结

至此，整个流程的大概思路就清楚了：在main分支进行写作，gitbook静态网站资源保存至gh-pages分支。

其实生成的gitbook导出至[gitbook.com](https://gitbook.com/)可能会更方便。但是现在登录该网站需要fq，而且对免费用户的书籍也有数量限制。因此就选择导出至Github Pages，数量无限制，而且又能DIY，最后实现也很方便，何乐而不为呢？

下一步是利用Travis CI服务，利用main分支的源文件，自动进行gitbook build，并把生成的静态网站push到gh-pages分支，使得Github Pages生效。

# Travis CI



## 概述

**Travis CI**是在软件开发领域中的一个在线的，分布式的持续集成服务，用来构建及测试在GitHub托管的代码。Travis CI 提供的是持续集成服务(Continuous Integration，简称 CI)。它绑定 Github 上面的项目，只要有新的代码，就会自动抓取。然后，提供一个运行环境，执行测试，完成构建，还能部署到服务器。持续集成指的是只要代码有变更，就自动运行构建和测试，反馈运行结果。确保符合预期以后，再将新代码"集成"到主干。

## 开始使用



Travis CI的官方网站有两个，https://travis-ci.org/为免费版，https://travis-ci.com/为收费版(有免费次数)。但是.org在2020/12/31后会更改为一个只读的网站，目前正在进行.org向.com的迁移，所以这里选择.com。

> **Q. When will the migration from travis-ci.org to travis-ci.com be completed?** [#](https://docs.travis-ci.com/user/migrate/open-source-repository-migration#q-when-will-the-migration-from-travis-ciorg-to-travis-cicom-be-completed)
>
> A. In an effort to ensure that all of our users - whether you build open-source, public or private repositories - receive regular feature updates, security patches and UX/UI enhancements, we are announcing that travis-ci.org will be officially closed down completely no later than December 31st, 2020, allowing us to focus all our efforts on bringing new features and fixes to travis-ci.com and all of our awesome users like yourself on the travis-ci.com domain.
>
> **Q. What will happen to travis-ci.org after December 31st, 2020?** [#](https://docs.travis-ci.com/user/migrate/open-source-repository-migration#q-what-will-happen-to-travis-ciorg-after-december-31st-2020)
>
> A. Travis-ci.org will be switched to a read-only platform, allowing you to see your jobs build history from all repositories previously connected to travis-ci.org.

进入网址https://travis-ci.com/

**登录Travis CI**

SIGN IN WITH GITHUB，登入之后点击`ACTIVATE ALL REPOSITORIES USING GITHUB APPS`



![image-20201120160731510](https://img-blog.csdnimg.cn/img_convert/9c6e47a80e1beb16ede673700d95ab39.png)

**批准安装Travis CI**



![image-20201120215456470](https://img-blog.csdnimg.cn/img_convert/da3315c22ac8b0f9ee0b40e12116ae0f.png)

**激活Travis Ci服务**



![img](https://img-blog.csdnimg.cn/img_convert/85201e35bd275bf39fc1f68988fc8a8f.png)


点击 https://travis-ci.com/网站上方的 `Dashboard`会显示Active respositories。

## 编写.travis.yml

Travis 要求项目的根目录下面，必须有一个`.travis.yml`文件。这是配置文件，指定了 Travis 的行为。该文件必须保存在 Github 仓库里面，一旦代码仓库有新的 Commit，Travis 就会去找这个文件，执行里面的命令。该文件采用的格式为YAML。示例：`language: pythonsudo: requiredbefore_install: sudo pip install fooscript: py.test12345`上面代码中，设置了四个字段：运行环境是 python，需要sudo权限，在安装依赖之前需要安装foo模块，然后执行脚本py.test。下面根据此次任务编写所需的.travis.yml文件：`language: node_js   #运行环境为nodejsnode_js:            #设置版本号  - "10"cache: npm notifications:      #通知  email:    recipients:      - 1823636309@qq.com   #设置通知邮件    on_success: change    on_failure: always install:                             #install阶段 安装依赖  - npm install -g gitbook-cli       #安装gitbook   - gitbook install                  #安装插件  - npm install -g gitbook-summary   #使自动生成SUMMARY.md的一个工具 script:                              #script阶段 运行脚本  - book sm                          #利用安装的工具gitbook-summary自动生成SUMMARY.md文件  - gitbook build                    #gitbook编译，生成静态网站站点_book   after_script:                        #script阶段之后执行  - cd _book                         #进入_book目录  - git init                           - git remote add origin https://${REF}    #设置要托管到的仓库名  - git add .                               #添加_book目录下的所有文件  - git commit -m "Updated By Travis-CI With Build $TRAVIS_BUILD_NUMBER For Github Pages"   - git branch -M main  - git push --force --quiet "https://${TOKEN}@${REF}" main:gh-pages  #强制推送到gh-pages分支 branches:  only:    - main env:  global:    - REF=github.com/wangzhebufangqi/gitbookTest.git # 设置 github 地址123456789101112131415161718192021222324252627282930313233343536373839`

## 测试

**创建github个人访问令牌**为了使Travis CI有权限往github仓库提交代码，还需要在github上创建个人访问令牌(**Personal access tokens**)`Settings -> Developer Settings -> Personal access tokens`点击`Generate new token`，勾选`repo` ，再点击`Generate Token`生成个人访问令牌。![image-20201120152054343](https://img-blog.csdnimg.cn/img_convert/a1973ae76ca322962378aa13e44ba15f.png)生成的个人访问令牌详细信息**只会出现一次**，妥善保存。**令牌填入Travis CI**回到Travis CI，选择仓库gitbookTest，`More options -> Settings -> Environment Variables`![image-20201120153029436](https://img-blog.csdnimg.cn/img_convert/ff34f92430043a7feeead392b12bf375.png)将复制好的个人访问令牌填入环境变量，将其命名为`TOKEN`，前面的脚本用的就是这个值。![image-20201120153319292](https://img-blog.csdnimg.cn/img_convert/509dc6ba4bbaf42a1dd36db22fde9c9f.png)**将项目托管至github**这里为了更直观的看到效果，可以删除远程仓库重新新建，并将本地.git文件、gitbook编译生成的_book文件夹删除，然后将上文提到的.travis.yml文件添加至项目根目录，最后进行push：`git initgit add .		#添加根目录下的所有文件git commit -m "first commit"git branch -M maingit remote add origin https://github.com/wangzhebufangqi/gitbookTest.git  #注意修改用户名git push -u origin main1234567`push成功后，Travis CI检测到有.travis.yml文件，收到任务(`Job Received`)，然后进行排队(`Queued`)，再是开启虚拟机(`Booting virtual machine`)，开始执行脚本，在`Job log`栏可以查看进度/日志，`View config`可以查看配置信息(.travis.yml)。![image-20201121001230700](https://img-blog.csdnimg.cn/img_convert/9b949fa21be329efeeefa833e7b67bb4.png)![image-20201121001619000](https://img-blog.csdnimg.cn/img_convert/60b1808e06d760b173cfa8a203737bb5.png)最后不出意外的话如下图，如失败请检查上述步骤是否有错漏之处(成功或失败会发邮件通知)：![image-20201121001724476](https://img-blog.csdnimg.cn/img_convert/62fe1aca14a82fceeceb708c82472770.png)检查github可发现，gh-pages分支被创建并且更新了相关文件，项目站点也可以被访问。

## 小结



到这部分，已经成功结合了gitbook+Github Pages+Travis CI，完成了最初的设想。但Travis CI到2021年可能会需要付费，因此下一部分考虑用Github Action替换Travis CI。
更多信息，如加密Token，.travis.yml完整的生命周期等，可参考持续集成服务Travis CI教程[5](https://blog.csdn.net/qq_40442753/article/details/110157897#fn5)

**小插曲：**

笔者一开始不知道竟然有两个官网，在.org网站上遭遇了很长的排队时长，一个多小时才开始执行脚本。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/f1bb691476013a5587ed11650d211a1d.gif)


后来发现正值.org网站向.com网站迁移完成之际，难怪如此。

关于Travis CI以后是否还面向免费用户，官网上有个相关的Q&A：

> **Q. Will Travis CI be getting rid of free users?** [#](https://docs.travis-ci.com/user/migrate/open-source-repository-migration#q-will-travis-ci-be-getting-rid-of-free-users)
>
> A. Travis CI will continue to offer a free tier for public or open-source repositories on travis-ci.com and will not be affected by the migration.

现在免费用户有10000初始积分(Credit)，build会消耗积分，关于后续积分补充可能需要申请或氪金。

# Github Actions



## 概述



[GitHub Actions](https://github.com/features/actions) 是 GitHub 的持续集成服务，于2018年10月推出。

> 持续集成由很多操作组成，比如抓取代码、运行测试、登录远程服务器，发布到第三方服务等等。GitHub 把这些操作就称为 actions。
>
> 很多操作在不同项目里面是类似的，完全可以共享。GitHub 注意到了这一点，想出了一个很妙的点子，允许开发者把每个操作写成独立的脚本文件，存放到代码仓库，使得其他开发者可以引用。
>
> 如果你需要某个 action，不必自己写复杂的脚本，直接引用他人写好的 action 即可，整个持续集成过程，就变成了一个 actions 的组合。这就是 GitHub Actions 最特别的地方。

github官方的actions放在https://github.com/actions，可以进行引用，比如：

```yml
name: learn-github-actions				#文件名



on: [push]								#push触发



jobs:



  check-bats-version:



    runs-on: ubuntu-latest				#运行环境设置为支持的最新版ubuntu



    steps:



      - uses: actions/checkout@v2		#https://github.com/actions/checkout/tree/v2



      - uses: actions/setup-node@v1		#https://github.com/actions/setup-node/tree/v1



      - run: npm install -g bats



      - run: bats -v1234567891011
```

更多细节可参考Github Actions官方文档[6](https://blog.csdn.net/qq_40442753/article/details/110157897#fn6)

## 快速开始

GitHub Actions 的配置文件叫做 workflow 文件，存放在代码仓库的`.github/workflows`目录。github新建远程空仓库`ActionTest`，本地新建文件夹`ActionTest`，新建文件README.md，新建目录`.github/workflows`，在该目录下新建文件`test.yml`，文件内容参见上一节。![image-20201121162130104](https://img-blog.csdnimg.cn/img_convert/d13662af0171a4d1502d06f96582b594.png)`git initgit add .git commit -m "first commit"git branch -M maingit remote add origin https://github.com/wangzhebufangqi/ActionTest.gitgit push -u origin main1234567`进行push后，Github Actions检测到文件`.github/workflows/test.yml`，开始执行脚本![image-20201121163428531](https://img-blog.csdnimg.cn/img_convert/ecc17a32db388744cca992e11e9660b3.png)点击进去查看工作日志![image-20201121163710068](https://img-blog.csdnimg.cn/img_convert/970d71492aba1ccb4e0ad4df33532513.png)一些版本信息如下：比如设置的ubuntu为18.04.5的LTS版本、用到了两个github官方的actions：checkout和setup-node`Current runner version:'2.274.2'Operating System  Ubuntu  18.04.5  LTSVirtual Environment  Environment: ubuntu-18.04  Version: 20201115.1  Included Software: https://github.com/actions/virtual-environments/blob/ubuntu18/20201115.1/images/linux/Ubuntu1804-README.mdPrepare workflow directoryPrepare all required actionsGetting action download infoDownload action repository 'actions/checkout@v2'Download action repository 'actions/setup-node@v1'123456789101112131415`![image-20201121164057650](https://img-blog.csdnimg.cn/img_convert/dcfc12c28f3ad800c6e799442c1dddff.png)可以尝试更多命令，此处不赘述。熟悉之后开始编写这次所需要的.yml文件。

## 编写.github/workflow/*.yml



.yml文件缩进很重要，[YAML、YML在线编辑(校验)器](https://www.bejson.com/validators/yaml_editor/)可以检验yml格式是否正确。

主要命令已经在.travis.yml写过了，这里将其转换为Github Actions所需的格式：

```yml
name: auto-generate-gitbook
on:                                 #在main分支上进行push时触发  
  push:
    branches:
    - main
jobs:
  main-to-gh-pages:
    runs-on: ubuntu-latest
    steps:
    - name: checkout main
      uses: actions/checkout@v2
      with:
        ref: main
    - name: install nodejs
      uses: actions/setup-node@v1
    - name: configue gitbook
      run: |
        npm install -g gitbook-cli          
        gitbook install
        npm install -g gitbook-summary
    - name: generate _book folder
      run: |
        book sm
        gitbook build
        cp SUMMARY.md _book
    - name: push _book to branch gh-pages 
      env:
        TOKEN: ${{ secrets.TOKEN }}
        REF: github.com/${{github.repository}}
        MYEMAIL: 415770319@qq.com                  # ！！记得修改为自己github设置的邮箱
        MYNAME: ${{github.repository_owner}}
      run: |
        cd _book
        git config --global user.email "${MYEMAIL}"
        git config --global user.name "${MYNAME}"
        git init
        git remote add origin https://${REF}
        git add . 
        git commit -m "Updated By Github Actions With Build ${{github.run_number}} of ${{github.workflow}} For Github Pages"
        git branch -M main
        git push --force --quiet "https://${TOKEN}@${REF}" main:gh-pages
```

## 测试

**新建Person Access Token**在个人设置里生成一个新的个人令牌，权限仅选择`repo`即可。进入仓库，点击`Settiings -> Secrets -> New repository`，将其命名为`TOKEN`。![image-20201121172401974](https://img-blog.csdnimg.cn/img_convert/df2ca0f7e0d6a7b73f381037fee208d3.png)**将项目托管至github**添加一些测试的md文件，在前文push的基础上再进行push：`git add .git commit -m "update"git push1234`



![image-20201122002152059](https://img-blog.csdnimg.cn/img_convert/aa72912d327bd3df89dcaf9055d2efce.png)


项目站点： https://wangzhebufangqi.github.io/ActionTest/
测试成功。



## 小结

至此，成功的用Github Actions替代了Travis CI。Github Actions比起Travis CI，Github Actions毫无疑问和Github结合的更好，用户可以使用他人分享在GitHub Marketplace的workflows，非常方便。而且对开源仓库是免费的。一些错误：一个`step`中不能同时含有键`uses`和`run`![image-20201121221429203](https://img-blog.csdnimg.cn/img_convert/c886758f43745d61aff4f956d53c400b.png)设置email和name![image-20201121221631485](https://img-blog.csdnimg.cn/img_convert/e5a8d9c80ae168e978b7669b5bd97386.png)

# 后记

笔者最开始是因为实在太喜欢gitbook样式的书籍了，就想着自己DIY一下，于是在学习的过程中学到了很多。后面会慢慢改进的。![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/2a15dd26c73d3b54d404cd3f4f1de6aa.png)



1. 

2. 

   [使用 travis + gitbook + github pages 优雅地发布自己的书](https://segmentfault.com/a/1190000018002602) [↩︎](https://blog.csdn.net/qq_40442753/article/details/110157897#fnref1)

3. [gitbook常用的插件](https://segmentfault.com/a/1190000019806829) [↩︎](https://blog.csdn.net/qq_40442753/article/details/110157897#fnref2)

4. [Gitbook文档(中文版)](https://chrisniael.gitbooks.io/gitbook-documentation/content/index.html) [↩︎](https://blog.csdn.net/qq_40442753/article/details/110157897#fnref3)

5. [搭建我的个人博客](https://wangzhebufangqi.github.io/2020/11/15/搭建我的个人博客/) [↩︎](https://blog.csdn.net/qq_40442753/article/details/110157897#fnref4)

6. [持续集成服务 Travis CI 教程](http://www.ruanyifeng.com/blog/2017/12/travis_ci_tutorial.html) [↩︎](https://blog.csdn.net/qq_40442753/article/details/110157897#fnref5)

7. [Github Actions官方文档](https://docs.github.com/en/free-pro-team@latest/actions/learn-github-actions/introduction-to-github-actions) [↩︎](https://blog.csdn.net/qq_40442753/article/details/110157897#fnref6)





2.1.0版本需求开发