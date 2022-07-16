# 常见问题

您可能会不时遇到服务的问题。以下提示可以帮助您在不进一步干预的情况下重新开始，但如果没有，请联系 alone@swufe.edu.cn

### 安装新的package <a href="#restarting-your-server" id="restarting-your-server"></a>

!pip install packagename --user

### 重新启动服务器 <a href="#restarting-your-server" id="restarting-your-server"></a>

重新启动服务器可以解决许多问题。如果您看到以下任何消息，请尝试重新启动服务器。

* `500 internal server error, permissi9n failure checking authorization, I may need a new token`

若要重新启动服务器，请单击笔记本右上角的“控制面板”按钮。这应该显示一个带有红色“停止我的服务器”按钮的页面。单击按钮几秒钟后，红色按钮应变为绿色并显示“我的服务器”，再次单击它，您的服务器应该再次开始启动。重新启动服务器可能需要大约 30 秒的时间。

### 损坏的配置文件[#](https://intro.syzygy.ca/troubleshooting/#broken-configuration-files) <a href="#broken-configuration-files" id="broken-configuration-files"></a>

Jupyter（以及Python和Julia ...）将配置文件存储在您的主目录中，并且这些配置文件可能会不时损坏。最简单的解决方法是简单地删除配置文件并恢复为默认配置。在大多数情况下，文件存储在隐藏目录中（例如.local），诀窍只是知道它们在哪里，这里有一些常见的

* `~/.jupyter`- Jupyter Notebook 配置文件
* `~/.local`- 本地安装的 python 包 （`pip install --user XXXX`)
* `~/R`- R 包和配置文件。

小心

这些文件一旦删除就无法恢复

如果您已确定其中一个或多个位置中的文件对您造成了问题，则可以使用 UNIX rm 命令删除它们。从笔记本内部，您可以执行例如

```shell
!rm ~/.jupyter/jupyter_notebook_config.py
```

或从终端

```shell
rm ~/.jupyter/jupyter_notebook_config.py
```

对笔记本配置的更改仅在重新启动服务器后生效（见上文）。

### 存储不足[#](https://intro.syzygy.ca/troubleshooting/#out-of-storage) <a href="#out-of-storage" id="out-of-storage"></a>

用户当前默认存储分配为 1GB。如果您发现要从存储中收到消息或无法保存文件，则可能已达到配额。要从中恢复，请通过电子邮件 alone@swufe.edu.cn，其中包含您的用户名和您正在使用的服务器的名称。
