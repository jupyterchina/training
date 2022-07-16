# 准备

{% hint style="info" %}
**在**在学校账户认证体系允许接入的情况下，我们将开启使用学校账户直接登录。目前，只能通过注册用户的形式进行认证。

请在[Broken link](broken-reference "mention")页面获取。
{% endhint %}

#### 平台访问地址

[https://datahub.swufe8.org ](https://datahub.swufe8.org)

#### 浏览器

您可以己喜欢的任何网络浏览器。但是，一些经验表明：

* Firefox更擅长渲染数学公式，但剪切/复制/粘贴在终端中不起作用。
* Chrome/Edge更擅长在终端中剪切/复制/粘贴，例如，在使用GIT时很重要。
* Safari 运行正常，包括在 iPad 和 iPhone 上。
* Internet Explorer不建议使用，原因太多。

### 关于Jupyter Notebook、终端 <a href="#notebooks-terminals-and-unix" id="notebooks-terminals-and-unix"></a>

登录后，Jupyter平台服务将启动一个**服务器**，即您正在访问的计算服务。（如果它没有自动启动，请单击“启动服务器”按钮。服务器运行后，您将看到帐户中存在的文件和文件夹列表。这称为 Hub，是一个视图，类似于 Mac 上的 Finder 或 Windows 计算机上的文件资源管理器。

在此Hub中，您可以单击文件和文件夹以打开它们，您可以选择它们并执行重命名，复制或删除它们等操作。某些文件将具有后缀 .ipynb，代表“iPython Notebook”。

Jupyter Notebook是包含Markdown文本、Latex数学公式和程序代码的文件。

大多数情况下，您可以在datahub中创建和使用notebook，每个notebook都有一个单元格集合，可以创建，编辑和运行这些单元格。

因此，你可以把所有工作都交给datahub中的notebook包括要使用的文本，数学和代码片段。

{% hint style="info" %}
在Jupyter Hub的后台是一台完成所有工作的Linux机器。
{% endhint %}

### 移动文件[#](https://intro.syzygy.ca/getting-started/#moving-files-around) <a href="#moving-files-around" id="moving-files-around"></a>

在某些时候，您将需要重新组织Jupyter Hub中的文件和文件夹。

* 如果你熟悉linux的命令行Bash,可以打开一个新的终端，并使用or命令移动文件。`mv 、cp`
* 你也可以使用命名系统来移动文件。

&#x20;       通过单击文件名左侧的方形框，在 Hub 中选择一个文件。然后，您可以选择“重命名”该文件。单击重命名按钮，然后输入以下选项之一：

* `newname`– 为文件指定新名称
* `../oldname`– 将文件向上和移出当前文件夹，移动到上一个文件夹中
* `foldername/oldname`– 将文件移动到这个文件夹中。此文件夹应已存在（因为之前使用“新建文件夹”命令创建了它）。

这些重命名方法还可用于移动文件夹及其内容。

要在目录树中的多个分支之间移动，您需要知道文件的完整路径名以及它们的位置。这意味着您需要找出根树结构的名称。执行此操作的一种快速方法是在notebook中使用 magic 命令。`%cd`

打开notebook，单击空单元格，然后键入 %cd，按 shift-return 键。它将返回当前目录。通常类似于 或 `/home/username/home/usernumber`

可以使用此功能将文件移动到任何文件夹中。只需将文件重命名为类似（最好已经存在，以便您将某些内容移动到其中）。`/home/username/folderA/filenamefolderA`

请参阅Shell 技巧部分，了解有关移动文件的更多提示。
