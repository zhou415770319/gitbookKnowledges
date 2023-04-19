## 1.github，gitee创建仓库

#### 1.1.github 创建新仓库

![创建新仓库](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/创建仓库.png)

创建完成

![](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/创建完成.png)

#### 1.2gitee导入github创建的仓库

![f2e449194fc239b936f8b2f9fd6c6563](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/f2e449194fc239b936f8b2f9fd6c6563.png)

gitee和github同时下载上传代码Git配置

参照[Git配置多个SSH-Key](Git配置多个SSH-Key.md)

#### 1.3gitbook项目构建

参照[gitbook](gitbook.md)

```
gitbook init
gitbook serve
```



13.1gitbook.json参照

```
{
    "title": "zhoufei-studynotes",
    "author": "zhoufei",
    "description": "学习笔记",
    "language": "zh-hans",
    "gitbook": "3.2.3",
    "styles": {
        "website": "./styles/website.css",
        "ebook": "styles/ebook.css",
        "pdf": "styles/pdf.css",
        "mobi": "styles/mobi.css",
        "epub": "styles/epub.css"
    },
    "structure": {
        "readme": "README.md"
    },
    "links": {
        "sidebar": {
            "我的博客": "http://www.feiyum.cn/index/"
        }
    },
    "plugins": [
        "-sharing",
        "splitter",
        "expandable-chapters-small",
        "anchors",

        "github",
        "github-buttons",
        "donate",
        "sharing-plus",
        "anchor-navigation-ex",
        "favicon",
        "summary",
    	"expandable-chapters-small",
    	"editlink",
        "copy-code-button",
        "prism", 
        "-highlight",
        "simple-mind-map"
    ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/zhou415770319"
        },
        "github-buttons": {
            "buttons": [{
                "user": "zhou415770319",
                "repo": "studynotes",
                "type": "star",
                "size": "small",
                "count": true
                }
            ]
        },
        "donate": {
            "alipay": "../../img/alipay.JPG",
            "title": "",
            "button": "赞赏",
            "alipayText": " "
        },
        "sharing": {
            "douban": false,
            "facebook": false,
            "google": false,
            "hatenaBookmark": false,
            "instapaper": false,
            "line": false,
            "linkedin": false,
            "messenger": false,
            "pocket": false,
            "qq": false,
            "qzone": false,
            "stumbleupon": false,
            "twitter": false,
            "viber": false,
            "vk": false,
            "weibo": false,
            "whatsapp": false,
            "all": [
                "google", "facebook", "weibo", "twitter",
                "qq", "qzone", "linkedin", "pocket"
            ]
        },
        "anchor-navigation-ex": {
            "showLevel": false
        },
        "favicon":{
            "shortcut": "./source/images/favicon.jpg",
            "bookmark": "./source/images/favicon.jpg",
            "appleTouch": "./source/images/apple-touch-icon.jpg",
            "appleTouchMore": {
                "120x120": "./source/images/apple-touch-icon.jpg",
                "180x180": "./source/images/apple-touch-icon.jpg"
            }
        },
    	"editlink": {
          "base": "https://github.com/zhaoda/webpack-handbook/edit/master/content",
          "label": "Edit This Page",
          "multilingual": false
        },
        "simple-mind-map": {
            "type": "markdown",
            "preset": "colorful",
            "linkShape": "diagonal",
            "autoFit": true
        }
    }
}

```



配置完插件需要install

```
gitbook install
```



gitbook build

打包生成静态文件默认在_book文件夹

#### 1.3.2_book文件夹配置git提交忽略

mac电脑不显示.gitignore文件，打开终端输入下面的命令

```
defaults write com.apple.finder AppleShowAllFiles -bool true
```

修改.gitignore

```
_book/*
node_modules
.DS_Store
dist
dist-ssr
*.local
.vscode
```



#### 1.3开通gitee go流水线

可以参照

https://blog.csdn.net/qq_40409260/article/details/129599022

不会配，采用github的Actions



#### 1.4github仓库配置

main分支 dev分支代码合并到main分支后触发Actions部署代码把_book中生成的页面提交到gh-pages实现自动更新页面

github创建dev分支 本地笔记修改后先提交dev分支，完成笔记后需要提交到页面上时提交合并请求merge到main分支

github创建gh-pages分支 githubPages设置展示的分支

可以先把gh-pages里面的代码删除

![githubPages设置](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/githubPages设置.png)



#### 1.5开通githubActions

新建Actions

![新建Actions](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/新建Actions.png)

编辑yml文件

![编辑yml文件](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/编辑yml文件.png)

```
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



#### 1.6新建Person Access Token

github账户-头像-`Settiings -> Secrets -> New repository`

![新建Person Access Token](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/新建Person Access Token.png)



#### 1.7新建secret![b88c5887d8c91254023ece6c12f2a6f4](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/新建secret.png)

#### 1.8仓库添加secret

![仓库添加secret](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/仓库添加secret.png)



如果actions出现报错，先新建TOKEN

![no such device](/Users/zhoufei/Desktop/zf-code/gitHub/gitbook/gitbookKnowledges/images/no such device.png)



**安装** gitbook-summary

```bash
npm install -g gitbook-summary
12
```

下载到路径：C:\Users\LENOVO\AppData\Roaming\npm\node_modules\gitbook-summary

**使用**

进入到项目根目录，执行`book sm`命令，即可生成SUMMARY.md文件。后面可带参数：



3.问题记录

# 用鼠标点击mind map后，整个图形会一直跟着鼠标走，怎么处理？

plugins里面删除splitter



2.常用命令

切换node

```
1.切换node(出现Permission denied)
sudo n
node版本查看
node -v
node源查看
nrm ls

```

