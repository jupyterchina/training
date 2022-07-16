# 文件管理

教学过程中使用JupyterHub时，我们需要便捷地将学习材料/教学资料/教学jupyter notebook分发到学生的空间中。

**学生应该能够**：

* 轻松获取**最新版本**的教学资料，即便学生已经有了一份拷贝，也能够及时更新到教师的最新版本。
* 学生所做的任何修改和作业都不会因为教师更新资料而被覆盖。
* 不必处理手动合并冲突或其他复杂操作。

**教师应该能够**：

* 使用现代协作版本控制工具来创作和存储教学资料。我们推荐使用 Git，同时我们也提供了Github Enterprise版本（校内和校外）。

在平台内，我们引入nbgitpuller这个工具，实现上述目标。 本教程将介绍如何使用Git和Github，通过nbgitpuller形成一个学生可以点击的连接，而学生通过点击这个链接就能够直接从教师的git存储库中获取最新版本的教学材料。

### 使用 Git 和 GitHub

Git 是一种快速、通用、高度可缩放的免费开源 VCS（版本控制系统）。 它的主要作者是 Linux 的创建者 Linus Torvalds。Git 用于与他人共享代码和其他计算机文件，并且能进行协作。代码和文件会被git管理，并归置到”存储库“中。在处理大型项目时，Git作为版本控制工具，非常强大：项目中需要跟踪许多不同文件中的更改，这些文件可能由许多不同的人编写，Git能追踪和还原这些复杂的更改，推进项目进展。

Github可以存储您的代码和其他计算机文件，无论是”私有“还是”公开“。通过上传（同步）到github，能把本地电脑的”存储库“同步到Github的”存储库“，并设置访问权限，便于进行共享和协作。

我们为SWUFE所有师生开设了Github的企业版，目前可以直接访问https://github.com, 并通过申请页面获取企业版权限。 本报告的原文存储库也是在github上，可以在此处查看：https://github.com/swufe-fic/jupyter

通常要获取一个存储库的副本，只需打开一个新的Jupyter notebook并输入以下命令：

```
!git clone https://github.com/SWUFE-FIC/OSPDA.git
```

这将在你的目录中创建一个名为“OSPDA”的新文件夹，其中包含该文件夹中的所有代码。现在就可以直接在平台上打开这些文件并运行代码。

随着你在Git和Github上获得更多的经验，你可能想克隆其他人的存储库并使用他们的代码。为管理好你的数据空间，可以创建一个新文件夹，并将新内容直接克隆到该新文件夹中。

用于执行此操作的一系列 Notebook 命令将如下所示：

```
%mkdir MyNewDirectory 
%cd MyNewDirectory
!git clone https://github.com/THE-USER-NAME/THE-REPOSITORY-NAME.git
```

当查看某个存储库时，右侧有一个按钮，上面写着“克隆或下载”。单击“克隆或下载”并请求“使用HTTPS克隆”，将获得存储库的 https 地址，将其粘贴到上面的 git clone 命令中。&#x20;

也可以在终端窗口中执行此操作（通过在Jupyter服务器的首页中打开“新建终端”） 有关克隆Github存储库的一些详细信息，请参阅：https://help.github.com/articles/cloning-a-repository/

{% hint style="warning" %}
重要提示：如果您要从Github上的私有存储库进行克隆，则需要使用终端进行克隆，因为服务器会要求您提供用户名和密码（以确保您确实可以访问该私有存储库）。
{% endhint %}



### 使用nbgitpuller

#### 1. 生成可供学生点击同步的链接

&#x20;   a. [使用浏览器插件](https://github.com/yuvipanda/nbgitpuller-link-generator-webextension/releases/download/v1.0/nbgitpuller\_link\_generator-1.0.zip) 在github仓库的页面地址，直接生成URL （[安装浏览器插件的方法](https://jingyan.baidu.com/article/e5c39bf56286ae39d6603374.html)）

<img src="../../.gitbook/assets/image (2).png" alt="" data-size="original">

![](<../../.gitbook/assets/image (3).png>)

&#x20;  b. 使用[链接生成器 ](https://jupyterhub.github.io/nbgitpuller/link)

#### 2. 学生或协作者点击链接进行同步

* 以某种方式将链接发送给学生 ，或者把它放在教学大纲页面上
* 当使用者单击该链接时，系统将要求他们登录到https://datahub.swufe8.org（如果尚未登录）。
* 当 git 存储库被获取并执行所需的任何自动合并时，将看到一个进度条。
* 当进度走完时，即可打开你指定的文件或文件夹

<img src="https://tljh.jupyter.org/en/latest/_images/pull-progress.png" alt="正在拉取 git 存储库的进度条" data-size="original">
