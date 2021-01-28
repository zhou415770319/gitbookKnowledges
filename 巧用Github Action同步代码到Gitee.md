# 巧用Github Action同步代码到Gitee

### 1. 背景

在开源贡献的代码托管的过程中，我们有时候有需要将Github的代码同步到其他远端仓库的需求。具体的，对于我们目前参与的项目来说核心诉求是：**以Github社区作为主仓，并且定期自动同步到Gitee作为镜像仓库**。

### 2. 调研

- 结论1: 由于会被Github屏蔽，Gitee的自动同步功能暂时无法支持。
  这个问题在Gitee的官方反馈中，[建议github导入的项目能设置定时同步](https://gitee.com/oschina/git-osc/issues/IKH12)提及过，官方的明确答复是不支持。最近又再次和官方渠道求证，由于会被Github屏蔽的关系，这个功能不会被支持。本着有轮子用轮子，没轮子造轮子的原则，我们只能选择**自己实现**。
- 结论2: 靠手动同步存在时效问题，可能会造成部分commit的丢失。
  Gitee本身是提供了手动同步功能的，也算比较好用，但是想想看，如果一个组织下面，发展到有几百上千个项目后，这种机制显然无法解决问题了。因此，我们需要**某种计算资源去自动的完成同步**。
- 结论3: 目前我们开源的好几个项目（例如Mindspore, OpenGauss, Kunpeng）都有类似的需求。
  作为一个合格的程序员，为了守住DRY(don’t repeat yourself，不造重复的轮子)的原则，所以，我们需要实现一个**工具**，同步简单的配置就可以完成多个项目的同步。

最终结论：我们需要**自己实现**一个**工具**，通过**某种计算资源自动的**去完成**周期同步**功能。



### 3. 选型

其实调研结论有了后，我们面对的选型就那么几种：

- 使用crontab调用脚本周期性同步。这个计算资源得我们自己维护，太重了。排除！
- 使用Travis、OpenLab等CI资源。这些也可以支持，但是和Github的集成性比较差。
- Github Action。无缝的和Github集成，处于对新生技术的新鲜感，还是想试一把的，就选他了！关于Github Action的详细内容可以直接在官网看到：https://github.com/features/actions

PS：严格来讲，Github Action其实是第二种选择的子集，其实就是单纯的想体验一把，并且把我们的业务需求实现了。

### 4. 实现

#### 4.1 GITHUB ACTION的实现

Github Action提供了[2种方式](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/about-actions#types-of-actions)去实现Action：

- Docker container. 这种方式相当于在Github提供的计算资源起个container，在container里面把功能实现。具体的原理大致如下：
  ![image](https://user-images.githubusercontent.com/1736354/72601545-9482fa00-3950-11ea-849a-6788b7a7df2f.png)
- JavaScript. 这种方式相当于在Github提供的计算资源上，直接用JS脚本去实现功能。

作为以后端开发为主的我们，没太多纠结就选择了第一种类型。关于怎么构建一个Github的Action可以参考Github的官方文档[Building actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/building-actions)。官方文档真的写的非常详细了，并且也通了了hello-world级别的入门教程。

#### 4.1 同步的核心代码实现

而最终的关键实现就是，我们需要定义这个容器运行的脚本，原理很简单：
![image](https://user-images.githubusercontent.com/1736354/72602279-fa23b600-3951-11ea-986e-d48446465a40.png)
大致就是以上4步：

1. 通过Github API读取Repo列表。
2. 下载或者更新Github repo的代码
3. 设置远端分支
4. 将最新同步的commit、branch、tag推送到Gitee。

关心细节的同学，具体可以参考代码：https://github.com/Yikun/gitee-mirror-action/blob/master/entrypoint.sh

### 5. 怎么用呢？

举了个简单的例子，我们想将Github/kunpengcompute同步到Gitee/kunpengcompute上面，需要做的非常简单，只需要2步：

1. 将Gitee的私钥和Token，上传到项目的setting的Secrets中。
   ![image](https://user-images.githubusercontent.com/1736354/72600755-33a6f200-394f-11ea-832d-331c222a0b4e.png)

可以参考[官方指引](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets#creating-encrypted-secrets)

1. 新建一个Github workflow，在这个workflow里面使用Gitee Mirror Action。

   ```
   name: Gitee repos mirror periodic job
   on:
   # 如果需要PR触发把push前的#去掉
   # push:
     schedule:
       # 每天北京时间9点跑
       - cron:  '0 1 * * *'
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
       - name: Mirror the Github organization repos to Gitee.
         uses: Yikun/gitee-mirror-action@v0.01
         with:
           # 必选，需要同步的Github用户（源）
           src: github/Yikun
           # 必选，需要同步到的Gitee的用户（目的）
           dst: gitee/yikunkero
           # 必选，Gitee公钥对应的私钥，https://gitee.com/profile/sshkeys
           dst_key: ${{ secrets.GITEE_PRIVATE_KEY }}
           # 必选，Gitee对应的用于创建仓库的token，https://gitee.com/profile/personal_access_tokens
           dst_token:  ${{ secrets.GITEE_TOKEN }}
           # 如果是组织，指定组织即可，默认为用户user
           # account_type: org
           # 还有黑、白名单，静态名单机制，可以用于更新某些指定库
           # static_list: repo_name
           # black_list: 'repo_name,repo_name2'
           # white_list: 'repo_name,repo_name2'
   ```

可以参考[鲲鹏库的实现](https://github.com/kunpengcompute/Kunpeng/blob/master/.github/workflows/gitee-repos-mirror.yml)。

![image](https://user-images.githubusercontent.com/1736354/72601756-fa6f8180-3950-11ea-9be2-c6c37210fc3b.png)

上图，大概是每个阶段的原理和最终的效果。现在，这个使用Gitee Mirror Action的workflow已经运行起来了，可以在[链接](https://github.com/kunpengcompute/Kunpeng/actions)看到。

### 6. 最后

好啦，这篇硬核软文就写到这里，有同步需求的同学，放心使用。更多用法，可以参考Hub-mirror-action的主页Readme。

**Github Action 官方链接**：https://github.com/marketplace/actions/hub-mirror-action
**代码仓库**：https://github.com/Yikun/hub-mirror-action

有任何问题或者疑问，希望可以和大家一起改进这个Action，有问题可以直接提Issue或者PR，不用客气。