# Shell命令

### Shell技巧 <a href="#unix-tricks" id="unix-tricks"></a>

在后台，Jupyter Hub在Linux上运行，你可以访问bash shell，从命令行完成所有的Unix魔术。只需从Jupyter服务器的首页打开一个新的“终端”即可。

以下是我学到的一些避免终端命令的技巧。

### Jupyter Notebook中的Shell和Magic。 <a href="#unix-and-magic-in-a-notebook" id="unix-and-magic-in-a-notebook"></a>

在运行Jupyter Notebook时，您可以直接访问许多Linux命令，而无需使用所谓的“魔术”命令打开终端窗口。这些命令始终以百分号 % 开头。

以下是一些您可能会发现有用的熟悉的Linux命令：

* `%ls`– 列出当前目录中的所有文件
* `%cd`– 查看当前目录的名称
* `%cd dirname`- 更改目录（输入所需目录的名称）
* `%cp oldfile newfile`– 将旧文件复制到新文件
* `%rm filename`– 删除（删除）名为“文件名”的文件

值得庆幸的是，您可以使用这些神奇的命令在目录树中移动。例如，您可能希望将文件从 Directory1 复制到 Directory2 中。您可以使用如下命令：

* `%cp /home/myusername/Directory1/filename /home/myusername/Directory2/filename`

其中“myusername”是Jupyter服务器调用您的帐户的任何内容。使用 （不带参数）后跟 的 路径（包括用户名）。`%cd%pwd`

高级用法

在python 3内核中，您还可以通过在行首放置感叹号“！”来运行任意unix命令，例如

```
!cp /home/myusername/Directory1/filename /home/myusername/Directory2/filename
```

只要有可能，最好选择“%”，但是！也可用。

### NotebooK中的更多Magic <a href="#more-magic-in-a-notebook" id="more-magic-in-a-notebook"></a>

魔术命令比上面列出的Linux命令要丰富得多。[在 ipython 文档中](http://ipython.readthedocs.io/en/stable/interactive/magics.html)提供了对可能性的良好参考

使用双百分号%%，您向Jupyter发出信号，表明整个单元格将被相应地解释。例如，像这样的单元格：

```python
%%latex
\[ \int_0^1 f(x) \,dx = F(1) - F(0) \]
```



要查看 Jupyter 笔记本中所有已定义的魔术命令，请键入（magic）命令

* `%lsmagic`

Magics可以帮助调试，处理文件，定义宏等等。
