# 使用Python计算



### Python for Computing <a href="#python-for-computing" id="python-for-computing"></a>

有许多在线资源可用于学习Python。比如官方文档：[https://www.python.org/doc/](https://www.python.org/doc/)

本章重点介绍如何在Jupyter笔记本中使用Python。在Python中进行简单的计算非常简单。但是，一旦你尝试做一些复杂的事情，有一些技巧需要学习。特别是，如何使情节出现在笔记本中，如何制作动画以及其他一些细节。

### Python 2 或 3？ <a href="#python-2-or-3" id="python-2-or-3"></a>

请使用 **Python 3**。这是该语言的现代版本。

这两个版本有何不同？不多。命令 2/3 在 Python 2（整数除法）中返回 0，而 2/3 在 **Python 3**（浮点除法）中返回 .66666666666。print命令有点不同。**Python 3**中有足够的新的，好的东西，你真的应该使用它

<mark style="color:orange;">**DATAHUB平台使用 Python 3**</mark>。

### 在 Python 笔记本中绘图 <a href="#plotting-in-a-python-notebook" id="plotting-in-a-python-notebook"></a>

在你能够策划之前，有三件事。

* 您告诉 Jupyter 您希望绘图以内联方式显示
* 你加载数字Python，所以你可以处理数字数组
* 你加载PyPlot来做你的绘图。

这是通过以下代码完成的：

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
```

使用“as np”或“as plt”，有助于保持命名空间的干净。因此，当你调用像“sin”这样的函数时，你需要说出它来自哪里，就像“np.sin”一样。

现在，要绘制几个数字，只需调用 plot 函数，将数字作为数组：

```python
plt.plot([1,4,9,16,25])
```

![巴新](https://intro.syzygy.ca/img/P\_Poutput\_3\_1.png)

您可以以类似的方式绘制正弦函数的一部分，将数字列表传递给该函数：`sin`

```python
plt.plot(np.sin([0,.1,.2,.3,.4,.5,.6,.7,.8,.9,1.0]))
```

![巴新](https://intro.syzygy.ca/img/P\_Poutput\_5\_1.png)

通常，您希望将 x 和 y 值绘制在一起，可以执行以下操作：

```python
x = [0,.1,.2,.3,.4,.5,.6,.7,.8,.9,1.0,1.1,1.2,1.3,1.4,1.5,1.6];
y = np.sin(x);
plt.plot(x,y)
```

![巴新](https://intro.syzygy.ca/img/P\_Poutput\_7\_1.png)

### 为绘图添加动画效果[#](https://intro.syzygy.ca/python-for-computing/#animating-plots) <a href="#animating-plots" id="animating-plots"></a>

我们可以使用html5作为动画，如[本网页](http://louistiao.me/posts/notebooks/embedding-matplotlib-animations-in-jupyter-notebooks/)中所建议的那样。

这似乎是在Python中做动画的现代方式。

第一步是在Python中初始化一些东西。

* 我们需要 %matplotlib 内联才能在笔记本上正确绘制内容
* 我们需要麻木的数学
* 我们需要 matplotlib 进行绘图
* 我们需要来自matplotlib的动画，以及来自iPython.display的HTML来显示动画。

我们通过以下导入获得所有这些：

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import animation, rc
from IPython.display import HTML
```

我们现在有四个步骤来获取动画情节

* 设置图形框
* 定义初始化函数
* 定义绘制动画每一帧的函数
* 调用动画器函数，该函数创建所有帧并为您保存它们

然后，我们准备调用“HTML”来显示动画。

```python
# First set up the figure, the axis, and the plot element we want to animate
fig, ax = plt.subplots()

ax.set_xlim(( 0, 2))
ax.set_ylim((-2, 2))

line, = ax.plot([], [], lw=2)
# NOTE: THIS WILL DISPLAY JUST AN EMPTY BOX.
```

![巴新](https://intro.syzygy.ca/img/P\_Aoutput\_3\_0.png)

初始化功能：绘制每帧的背景

```python
def init():
    line.set_data([], [])
    return (line,)
```

按顺序调用

```python
def animate(i):
    x = np.linspace(0, 2, 1000)
    y = np.sin(2 * np.pi * (x - 0.01 * i))
    line.set_data(x, y)
    return (line,)
```

blit=True 表示仅重新绘制已更改的部分。

```python
anim = animation.FuncAnimation(fig, animate, init_func=init,
                               frames=100, interval=20, blit=True)

HTML(anim.to_html5_video())
```

每当需要画图时，都可以随意调用它，并使用以下代码：

```python
# equivalent to rcParams['animation.html'] = 'html5'
rc('animation', html='html5')
```

### 数据分析[#](https://intro.syzygy.ca/python-for-computing/#data-analysis) <a href="#data-analysis" id="data-analysis"></a>

#### Python中pandas的简单演示[#](https://intro.syzygy.ca/python-for-computing/#a-simple-demo-with-pandas-in-python) <a href="#a-simple-demo-with-pandas-in-python" id="a-simple-demo-with-pandas-in-python"></a>

本笔记本基于Lamoureux在卡尔加里大学2016年冬季的数学651课程的课程笔记。

这是一个在Python中尝试一些资源的练习。具体来说，我们希望从网络上抓取一些有关股票价格的数据，并显示在pandas中。然后对信息进行一些基本的数据分析。

我们利用这样一个事实，即网络上可以免费访问大量财务数据，并且很多人会发布有关如何使用它的信息。

#### Python中的pandas[#](https://intro.syzygy.ca/python-for-computing/#pandas-in-python) <a href="#pandas-in-python" id="pandas-in-python"></a>

#### 如何从 Web 访问真实数据并应用数据分析工具。[#](https://intro.syzygy.ca/python-for-computing/#how-to-access-real-data-from-the-web-and-apply-data-analysis-tools) <a href="#how-to-access-real-data-from-the-web-and-apply-data-analysis-tools" id="how-to-access-real-data-from-the-web-and-apply-data-analysis-tools"></a>

本文使用Wes McKinney的**Python for Data Analysis**一书作为本节的参考。

使用Python的要点是，很多人都创造了很好的代码来做到这一点。

pandas的名字来自Panel Data，一个用于多维结构化数据集的计量经济学术语，以及Python数据分析。

pandas中出现的数据帧对象起源于 R。但显然，它们在Python中比在R中具有更多的功能。

在本节中，我还将使用PYLAB，因此我们可以使用NUMPY和MATPLOTLIB。

#### 访问数据[#](https://intro.syzygy.ca/python-for-computing/#accessing-financial-data) <a href="#accessing-financial-data" id="accessing-financial-data"></a>

对于免费的石油等商品的历史数据，[http://www.databank.rbs.com](http://www.databank.rbs.com/) 该网站将直接将数据下载到电子表格中，绘制历史数据的图表等。以下是过去15年油价（西德克萨斯中质原油）的示例。看看它有多低...

![图片来自苏格兰皇家银行数据库](https://intro.syzygy.ca/img/RBS\_graph.jpg)

雅虎提供当前的股票和商品价格。这是一个有趣的网站，告诉你如何将大量数据下载到csv文件中。[http://www.financialwisdomforum.org/gummy-stuff/Yahoo-data.htm](http://www.financialwisdomforum.org/gummy-stuff/Yahoo-data.htm)

这是另一个讨论访问各种财务数据源的网站。[http://quant.stackexchange.com/questions/141/what-data-sources-are-available-online](http://quant.stackexchange.com/questions/141/what-data-sources-are-available-online)

#### 从 Web 加载数据[#](https://intro.syzygy.ca/python-for-computing/#loading-data-off-the-web) <a href="#loading-data-off-the-web" id="loading-data-off-the-web"></a>

让我们来看看一些简单的股价——比如苹果和微软。我们可以导入一些基本的网络工具，直接从雅虎获得价格。

```python
# Get some basic tools
%pylab inline
from pandas import Series, DataFrame
import pandas as pd
import pandas.io.data as web
```

```python
# Here are apple and microsoft closing prices since 2001
aapl = web.get_data_yahoo('AAPL','2001-01-01')['Adj Close']
msft = web.get_data_yahoo('MSFT','2001-01-01')['Adj Close']
subplot(2,1,1)
plot(aapl)
subplot(2,1,2)
plot(msft)
```

![png](https://intro.syzygy.ca/img/output\_4\_1.png)

```python
aapl


    Date
    2001-01-02      0.978015
    2001-01-03      1.076639
    2001-01-04      1.121841
    2001-01-05      1.076639
    2001-01-08      1.088967
    2001-01-09      1.130060
    2001-01-10      1.088967
    2001-01-11      1.183481
    2001-01-12      1.130060
    2001-01-16      1.125950
    2001-01-17      1.105404
    2001-01-18      1.228683
    2001-01-19      1.282104
    2001-01-22      1.265667
    2001-01-23      1.347853
    2001-01-24      1.347853
    2001-01-25      1.310869
    2001-01-26      1.286213
    2001-01-29      1.425930
    2001-01-30      1.430039
    2001-01-31      1.421820
    2001-02-01      1.388946
    2001-02-02      1.356072
    2001-02-05      1.327306
    2001-02-06      1.388946
    2001-02-07      1.364290
    2001-02-08      1.364290
    2001-02-09      1.257448
    2001-02-12      1.294432
    2001-02-13      1.257448
                     ...    
    2016-05-04     93.620002
    2016-05-05     93.239998
    2016-05-06     92.720001
    2016-05-09     92.790001
    2016-05-10     93.419998
    2016-05-11     92.510002
    2016-05-12     90.339996
    2016-05-13     90.519997
    2016-05-16     93.879997
    2016-05-17     93.489998
    2016-05-18     94.559998
    2016-05-19     94.199997
    2016-05-20     95.220001
    2016-05-23     96.430000
    2016-05-24     97.900002
    2016-05-25     99.620003
    2016-05-26    100.410004
    2016-05-27    100.349998
    2016-05-31     99.860001
    2016-06-01     98.459999
    2016-06-02     97.720001
    2016-06-03     97.919998
    2016-06-06     98.629997
    2016-06-07     99.029999
    2016-06-08     98.940002
    2016-06-09     99.650002
    2016-06-10     98.830002
    2016-06-13     97.339996
    2016-06-14     97.459999
    2016-06-15     97.139999
    Name: Adj Close, dtype: float64
```

观察股票价格的变化，标准化为百分比

```python
aapl_rets = aapl.pct_change()
msft_rets = msft.pct_change()
subplot(2,1,1)
plot(aapl_rets)
subplot(2,1,2)
plot(msft_rets)
```

![png](https://intro.syzygy.ca/img/output\_6\_1.png)

这两个系列之间的相关性

```python
pd.rolling_corr(aapl_rets, msft_rets, 250).plot()

    /opt/conda/envs/python2/lib/python2.7/site-packages/ipykernel/__main__.py:2: FutureWarning: pd.rolling_corr is deprecated for Series and will be removed in a future version, replace with 
    	Series.rolling(window=250).corr(other=<Series>)
      from ipykernel import kernelapp as app
```

![png](https://intro.syzygy.ca/img/output\_7\_2.png)

#### 变得花哨。[#](https://intro.syzygy.ca/python-for-computing/#getting-fancy) <a href="#getting-fancy" id="getting-fancy"></a>

现在，我们可以使用一些更复杂的统计工具，如最小二乘回归。但是，我必须做一些工作才能让Python识别这些项目。但我没有太努力，我只是遵循了错误消息。

很明显，我需要返回终端窗口才能加载某些软件包。我必须输入的两个命令是

* pip install statsmodels
* pip install patsy

“pip”是一个“python安装程序包”，它将代码包安装到您的计算机（或任何运行python的计算机）上。两个包“statsmodels”和“patsy”是各种各样的统计包。

```python
# We may also try a least square regression, also built in as a panda function
model = pd.ols(y=aapl_rets, x={'MSFT': msft_rets},window=256)

    /opt/conda/envs/python2/lib/python2.7/site-packages/ipykernel/__main__.py:2: FutureWarning: The pandas.stats.ols module is deprecated and will be removed in a future version. We refer to external packages like statsmodels, see some examples here: http://statsmodels.sourceforge.net/stable/regression.html
      from ipykernel import kernelapp as app
model.beta
```

```python
model.beta['MSFT'].plot()
```

![png](https://intro.syzygy.ca/img/output\_11\_1.png)

这两个图表看起来很相似。让我们一起绘制它们

```python
subplot(2,1,1)
pd.rolling_corr(aapl_rets, msft_rets, 250).plot()
title('Rolling correlations')
subplot(2,1,2)
model.beta['MSFT'].plot()
title('Least squaresn model')


    /opt/conda/envs/python2/lib/python2.7/site-packages/ipykernel/__main__.py:3: FutureWarning: pd.rolling_corr is deprecated for Series and will be removed in a future version, replace with 
    	Series.rolling(window=250).corr(other=<Series>)
      app.launch_new_instance()
```

![png](https://intro.syzygy.ca/img/output\_12\_2.png)

#### 更多股票[#](https://intro.syzygy.ca/python-for-computing/#more-stocks) <a href="#more-stocks" id="more-stocks"></a>

网络上有各种整理过的数据。这是SPY交易所 标准普尔500指数。

```python
px = web.get_data_yahoo('SPY')['Adj Close']*10
px

    Date
    2010-01-04     998.08658
    2010-01-05    1000.72861
    2010-01-06    1001.43318
    2010-01-07    1005.66052
    2010-01-08    1009.00712
    2010-01-11    1010.41626
    2010-01-12    1000.99287
    2010-01-13    1009.44749
    2010-01-14    1012.17761
    2010-01-15    1000.81670
    2010-01-19    1013.32249
    2010-01-20    1003.01842
    2010-01-21     983.73128
    2010-01-22     961.80210
    2010-01-25     966.73395
    2010-01-26     962.68278
    2010-01-27     967.26241
    2010-01-28     956.16569
    2010-01-29     945.77354
    2010-02-01     960.48105
    2010-02-02     972.10617
    2010-02-03     967.26241
    2010-02-04     937.40701
    2010-02-05     939.34454
    2010-02-08     932.56318
    2010-02-09     944.27638
    2010-02-10     942.42694
    2010-02-11     952.29063
    2010-02-12     951.49804
    2010-02-16     966.46975
                     ...    
    2016-05-04    2050.09995
    2016-05-05    2049.70001
    2016-05-06    2057.20001
    2016-05-09    2058.89999
    2016-05-10    2084.49997
    2016-05-11    2065.00000
    2016-05-12    2065.59998
    2016-05-13    2047.59995
    2016-05-16    2067.79999
    2016-05-17    2048.50006
    2016-05-18    2049.10004
    2016-05-19    2041.99997
    2016-05-20    2054.90005
    2016-05-23    2052.10007
    2016-05-24    2078.69995
    2016-05-25    2092.79999
    2016-05-26    2093.39996
    2016-05-27    2102.40005
    2016-05-31    2098.39996
    2016-06-01    2102.70004
    2016-06-02    2109.10004
    2016-06-03    2102.79999
    2016-06-06    2113.50006
    2016-06-07    2116.79993
    2016-06-08    2123.69995
    2016-06-09    2120.80002
    2016-06-10    2100.70007
    2016-06-13    2084.49997
    2016-06-14    2080.39993
    2016-06-15    2077.50000
    Name: Adj Close, dtype: float64

plot(px)
```

![png](https://intro.syzygy.ca/img/output\_15\_1.png)

### Python 中的科学计算[#](https://intro.syzygy.ca/python-for-computing/#scientific-computing-in-python) <a href="#scientific-computing-in-python" id="scientific-computing-in-python"></a>

这是在Python中进行一些科学计算的示例。

我们参考了John M. Stewart的“Python for Scientists”一书中的一些想法。具体来说，我们想探索一个常微分方程（ODE）的数值求解器，称为ODEint。该求解器基于[lsoda，这是](http://www.oecd-nea.org/tools/abstract/detail/uscd1227)劳伦斯利弗莫尔实验室的Fortran软件包，是解决这些难题的可靠主力。

我们研究了四种不同的ODE，它们很有趣，并且在数字上具有挑战性。它们是：

* 谐波振荡器（或线性摆锤）
* 非线性钟摆
* 洛伦兹方程，它是混沌行为的模型
* 范德波尔斯方程，这是具有周期性行为的刚性ODE的一个例子。

我们对ODE数值求解器进行一些基本测试，以测试其准确性，并考虑我们对摆锤的渐近分析是否有效。

与前面的示例一样，我们必须从代码开始，告诉 Notebook 以内联方式绘制项目，并在包中加载以进行数值计算 （numpy）、科学计算 （scipy） 和绘图 （matplotlib）。

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint # This is the numerical solver
```

我们从二阶线性方程开始，它具有通常的谐波振荡器解。

\$$ y''（t） + \omega^2 y（t） = 0， \qquad y（0） = 1， y'（0） = 0.\$$

要将其放入数值求解器中，我们需要重新表述为一个 2 维一阶系统：\$$\mathbf{y} = （y，y'）^T， \qquad \mathbf{y}'（t） = （y'， -\omega^2 y）^T.\$$ 这是一个以数字方式解决问题的简单代码片段。

```python
def rhs(Y,t,omega):  # this is the function of the right hand side of the ODE
    y,ydot = Y
    return ydot,-omega*omega*y

t_arr=np.linspace(0,2*np.pi,101)
y_init =[1,0]
omega = 2.0
y_arr=odeint(rhs,y_init,t_arr, args=(omega,))
y,ydot = y_arr[:,0],y_arr[:,1]
plt.ion()
plt.plot(t_arr,y,t_arr,ydot)
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_3\_1.png)

让我们画一个相位肖像，将y和ydot绘制在一起

```python
plt.plot(y,ydot)
plt.title("Solution curve when omega = %4g" % omega)
plt.xlabel("y values")
plt.ylabel("ydot values")
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_4\_1.png)

通过比较精确的解和数值解来测试准确性

```python
t_arr=np.linspace(0,2*np.pi,101)
y_init =[1,0]
omega = 2.0
y_exact = y_init[0]*np.cos(omega*t_arr) + y_init[1]*np.sin(omega*t_arr)/omega
ydot_exact = -omega*y_init[0]*np.sin(omega*t_arr) + y_init[1]*np.cos(omega*t_arr)
y_arr=odeint(rhs,y_init,t_arr, args=(omega,))
y,ydot = y_arr[:,0],y_arr[:,1]
plt.plot(t_arr,y,t_arr,y_exact)
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_6\_1.png)

绘制差异图

```python
plt.plot(t_arr,y-y_exact)
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_7\_1.png)

因此，在上面的测试中，我们看到一个随时间振荡和增长的误差，大小约为2x 10^（-7）。这是单精度精度。

现在，显然ODEint自己计算出了很好的步长。让我们尝试再次运行代码，在 t 变量中使用不同数量的步骤。

```python
numsteps=1000001  # adjust this parameter
y_init =[1,0]
omega = 2.0
t_arr=np.linspace(0,2*np.pi,numsteps)
y_exact = y_init[0]*np.cos(omega*t_arr) + y_init[1]*np.sin(omega*t_arr)/omega
ydot_exact = -omega*y_init[0]*np.sin(omega*t_arr) + y_init[1]*np.cos(omega*t_arr)
y_arr=odeint(rhs,y_init,t_arr, args=(omega,))
y,ydot = y_arr[:,0],y_arr[:,1]
plt.plot(t_arr,y-y_exact)
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_9\_1.png)

误差只减少到大约1.0x10^（-7）。没有太大的改进。

让我们尝试另一个实验，在那里我们走了很长一段时间。假设比上面的例子长100个时间。

```python
numsteps=100001  # adjust this parameter
y_init =[1,0]
omega = 2.0
t_arr=np.linspace(0,2*1000*np.pi,numsteps)
y_exact = y_init[0]*np.cos(omega*t_arr) + y_init[1]*np.sin(omega*t_arr)/omega
ydot_exact = -omega*y_init[0]*np.sin(omega*t_arr) + y_init[1]*np.cos(omega*t_arr)
y_arr=odeint(rhs,y_init,t_arr, args=(omega,))
y,ydot = y_arr[:,0],y_arr[:,1]
plt.plot(t_arr,y-y_exact)
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_11\_1.png)

```python
p1=np.size(t_arr)-1
p0=p1-100
plt.plot(t_arr[p0:p1],y[p0:p1],t_arr[p0:p1],y_exact[p0:p1])
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_13\_1.png)

```python
plt.plot(t_arr[p0:p1],y[p0:p1]-y_exact[p0:p1])
```

![png](https://intro.syzygy.ca/img/P\_Soutput\_14\_1.png)



### 嵌入视频 <a href="#youtube" id="youtube"></a>

只需几行，您就可以将YouTube/BiliBili视频插入Jupyter笔记本中。

```python
from IPython.display import YouTubeVideo
YouTubeVideo('kthi--SH2Nk')   # Counting to 100 in Cree 
```

### d3 和用户界面 <a href="#d3-and-fancy-user-interface" id="d3-and-fancy-user-interface"></a>

我们可以使用一个名为 d3 的资源来制作notebook中非常复杂的用户界面。

在此示例中，将创建一组球，当计算机鼠标追逐球时，这些球会四处移动，如下所示。单击图片以与示例进行交互。

此代码是从此处fork的：[https://github.com/skariel/IPython\_d3\_js\_demo/blob/master/d3\_js\_demo.ipynb](https://github.com/skariel/IPython\_d3\_js\_demo/blob/master/d3\_js\_demo.ipynb)

此示例中有三个单元格。

* 第一个单元格创建一个文件，其中包含一些html代码和javascript来控制球
* 第二个单元格定义了Python函数，用于编辑文件，以调整球的数量等。
* 第三个单元格调用Python funciton f1，它启动html和javascript。

这是第一个单元格。

```python
%%writefile f1.template
<!DOCTYPE html>
<html>
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
    <script type="text/javascript" src="https://mbostock.github.io/d3/talk/20111018/d3/d3.js"></script>
    <script type="text/javascript" src="https://mbostock.github.io/d3/talk/20111018/d3/d3.geom.js"></script>
    <script type="text/javascript" src="https://mbostock.github.io/d3/talk/20111018/d3/d3.layout.js"></script>
    <style type="text/css">

circle {
  stroke: #000;
  stroke-opacity: .5;
}

    </style>
  <body>
    <div id="body">
    <script type="text/javascript">

var w = {width},
    h = {height};

var nodes = d3.range({ball_count}).map(function() { return {radius: Math.random() * {rad_fac} + {rad_min}}; }),
    color = d3.scale.category10();

var force = d3.layout.force()
    .gravity(0.1)
    .charge(function(d, i) { return i ? 0 : -2000; })
    .nodes(nodes)
    .size([w, h]);

var root = nodes[0];
root.radius = 0;
root.fixed = true;

force.start();

var svg = d3.select("#body").append("svg:svg")
    .attr("width", w)
    .attr("height", h);

svg.selectAll("circle")
    .data(nodes.slice(1))
  .enter().append("svg:circle")
    .attr("r", function(d) { return d.radius - 2; })
    .style("fill", function(d, i) { return color(i % {color_count}); });

force.on("tick", function(e) {
  var q = d3.geom.quadtree(nodes),
      i = 0,
      n = nodes.length;

  while (++i < n) {
    q.visit(collide(nodes[i]));
  }

  svg.selectAll("circle")
      .attr("cx", function(d) { return d.x; })
      .attr("cy", function(d) { return d.y; });
});

svg.on("mousemove", function() {
  var p1 = d3.svg.mouse(this);
  root.px = p1[0];
  root.py = p1[1];
  force.resume();
});

function collide(node) {
  var r = node.radius + 16,
      nx1 = node.x - r,
      nx2 = node.x + r,
      ny1 = node.y - r,
      ny2 = node.y + r;
  return function(quad, x1, y1, x2, y2) {
    if (quad.point && (quad.point !== node)) {
      var x = node.x - quad.point.x,
          y = node.y - quad.point.y,
          l = Math.sqrt(x * x + y * y),
          r = node.radius + quad.point.radius;
      if (l < r) {
        l = (l - r) / l * .5;
        node.x -= x *= l;
        node.y -= y *= l;
        quad.point.x += x;
        quad.point.y += y;
      }
    }
    return x1 > nx2
        || x2 < nx1
        || y1 > ny2
        || y2 < ny1;
  };
}

    </script>
  </body>
</html>
```

这是第二个单元格。

```python
from IPython.display import IFrame
import re

def replace_all(txt,d):
    rep = dict((re.escape('{'+k+'}'), str(v)) for k, v in d.items())
    pattern = re.compile("|".join(rep.keys()))
    return pattern.sub(lambda m: rep[re.escape(m.group(0))], txt)    

count=0
def serve_html(s,w,h):
    import os
    global count
    count+=1
    fn= '__tmp'+str(os.getpid())+'_'+str(count)+'.html'
    with open(fn,'w') as f:
        f.write(s)
    return IFrame('files/'+fn,w,h)

def f1(w=500,h=400,ball_count=150,rad_min=2,rad_fac=11,color_count=3):
    d={
       'width'      :w,
       'height'     :h,
       'ball_count' :ball_count,
       'rad_min'    :rad_min,
       'rad_fac'    :rad_fac,
       'color_count':color_count
       }
    with open('f1.template','r') as f:
        s=f.read()
    s= replace_all(s,d)        
    return serve_html(s,w+30,h+30)
```

这是第三个单元格。

```python
f1(ball_count=50, color_count=17, rad_fac=10, rad_min=3, w=600)
```
