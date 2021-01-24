## 如何将一个项目同时提交到GitHub和Gitee(码云)两个仓库

众所周知，`GitHub` 是全球最大的同性交友网站[Doge]，里面不缺乏大神写的优秀的开源项目，可是 `GitHub` 有一个致命的弊端，就是国内访问速度太慢了。为了解决这个问题，一个优秀的国产代码托管平台 `Gitee`（码云）应用而生，但是 `Gitee` 并没有 `GitHub` 那么有知名度。那么我们想我的代码既能放到最知名的`GitHub`上，同时也要兼容访问和下载速度，那怎么办呢？

答案就是同时将代码提交到 `GitHub` 和 `Gitee` 上，那该如何去做呢？接下来我将一步步从头新建一个项目，然后同时提交到 `GitHub` 和 `Gitee` 两个仓库。

首先，你的先注册 `GitHub` 和 `Gitee` 这两个网站，注册好以后还需将你的 `SSH keys` 同时添加到这两个网站，这两步请自行完成！

一切准备工作就绪以后我们就可以开始了。

##### 1. 在 `GitHub` 上新建一个空仓库

![在这里插入图片描述](https://www.pianshen.com/images/467/06f491236375a14b35c0ab551a3e749b.png)

##### 2. 在 `Gitee` 上新建一个关联 `GitHub` 的空仓库

![在这里插入图片描述](https://www.pianshen.com/images/991/64d08b3bbb36cf3fefc1a602d07e14d7.png)

##### 3. 将`GitHub` 的空仓库克隆到本地

![在这里插入图片描述](https://www.pianshen.com/images/91/d2edc8c68361a86594daf92efe714b5b.png)

##### 4. 修改 `Git` 的配置文件

![在这里插入图片描述](https://www.pianshen.com/images/460/1fd970df8f826a4c912d209714a04d0c.png)

##### 5. 将项目同时提交到 `GitHub` 和 `Gitee` 两个仓库

![在这里插入图片描述](https://www.pianshen.com/images/379/e8d3900d6e2aa239fe69df652295c9ab.png)

##### 5. 验证 `GitHub` 和 `Gitee` 两个仓库

![在这里插入图片描述](https://www.pianshen.com/images/237/722e6814cd224dad542fc7b912388efd.png)

![在这里插入图片描述](https://www.pianshen.com/images/983/95b4b1525fc19c253f5af49676ec526f.png)

最后再提一嘴，通过 `git` 的配置我们还可以同时提交多个仓库，除了 `GitHub` 和 `Gitee` 之外，还有 `GitLab`、`Bitbucket` 或是你自己搭建的 `Git` 服务器。不过这里建议你提交远程仓库最多不要超过两个，私有仓库没必要，公共的有这两个就够用了，毕竟多提交一个仓库就多一分耗时嘛。

版权声明：本文为博主原创文章，遵循[ CC 4.0 BY-SA ](https://creativecommons.org/licenses/by-sa/4.0/)版权协议，转载请附上原文出处链接和本声明。本文链接：https://blog.csdn.net/yilovexing/article/details/107226141