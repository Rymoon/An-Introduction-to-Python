绪论
----------


用python解决问题
==================

用python解决问题，需要学习的东西远远超过掌握python的语法。首先，实际问题转化到程序问题，这需要编程以外的知识，调用别人写好的程序包也要学习新的规则。

举个例子，当手里的程序越写越长，如果我想要添加一个新功能，会发生什么？很有可能你的代码莫名奇妙的就崩溃了。这个bug可能在新代码中，也可能隐藏在旧的片段里，只是刚刚被触发。无论如何， 你想要让程序先回到“上次成功运行”的样子，来排查问题。我们可以在增加功能前用注释标出未经测试的部分，以及修改的日期。但是，如果bug藏在旧的代码里，你可能需要找到更早的改动。而若是功能分布在多个脚本文件中，对一个的改动的“回退”可能让依赖它的程序失效，从而不能测试……我们需要一个记录程序更改的自动软件。

一个例子：Git
^^^^^^^^^^^^^^^

git，这个程序可以给文件夹拍“快照”，并给予一个独一无二的标识，你随时可以跳转到任何一个历史版本。上周的程序？没问题。依赖库也要回滚？你可以在快照里查看“历史上”的依赖库。

此外，git还可以创建“分支(branch)”，让你保留一个程序的多个变体，并记录他们的继承关系。git的独特技术让它只占用很小的硬盘空间——这比定期备份旧版本要好的多。配合github，你可以同步你的工作到云端（这一切完全免费），以及一切修改记录。你的合作者的工作，也可以智能地合并(merge)到你的项目(repo)中。

你还可以使用Gitpython来使用python脚本来管理git repo.

这只是一个例子，类似的还有使用sqlite3管理数据库、使用re module处理正则表达式以及使用requests模块做网络爬虫等等。这些辅助功能在python之外，但有益于python的开发、数据处理、可视化，或者干脆被整合为python library.

其次，Python作为一门编程语言是很独特的。“解释型语言”、“面象对象”、“没有函数重载”等等这些细节，罗列起来并不能说明python的独特。你仍然可以像写c++一样写python程序——基本的语法python都具备。但这样是不正确的，python语言的所有特性最终导致了不一样的思考方式和开发步骤。在其他语言中的最佳实践，用在python上可能是不适合的。


一个例子：Duck Type
^^^^^^^^^^^^^^^^^^^^^^^^^^

什么是鸭子类型？我们不事先检查它的类型是不是鸭子。如果它能走，能游，还能呱呱叫。那我们就当它是鸭子。

    Don’t check whether it is-a duck: check whether it quacks-like-a duck, walks-like-a duck, etc, etc, depending on exactly what subset of duck-like behavior you need to play your language-games with. (comp.lang.python, Jul. 26, 2000)

    — Alex Martelli

这听起来没有什么新奇的，似乎只是“动态属性”的另一种描述。而且实现这个功能并不难，在典型的静态语言如c++，你可以通过继承+虚函数、模版、函数重载、void*等等方式实现这种效果，当然它们是实现检查了的，只是编程的人不用手动写if-else的检查，可以直接调用。

可是结合上python的种种特性，我们很快就能发现这导致了编程思想上的不同：Python is not a dynamic c++. （并不是因为python速度慢 (\*￣3￣)╭）.

Python的异常处理语句是这个样子的：

.. code-block:: python
    :linenos: 

    try:
        dangerous_call()
    except OSError:
        log('OSError...')
    else:
        after_call()
    finally:
        always_call()

异常处理顾名思义，处理程序崩溃的状况，输出错误信息，清理现场，或者跳过出错的部分，继续执行。但在Python中，这常常用于控制流(Control-Flow)，就像if-else语句一样。事实上，因为duck-type的原因，“试图访问不存在的属性”这种事情总是会发生的。



""""""""""
EAFP
""""""""""

    摘自图书 *Fluent Python*

**Easier to ask for forgiveness than permission.** This common Python coding style
assumes the existence of valid keys or attributes and catches exceptions if the assumption proves false. This clean and fast style is characterized by the presence of many try and except statements. The technique contrasts with the LBYL style common
to many other languages such as C.

The glossary then defines LBYL:

""""""""
LBYL
""""""""

**Look before you leap.** This coding style explicitly tests for pre-conditions before making calls or lookups. This style contrasts with the EAFP approach and is characterized by the presence of many if statements. In a multi-threaded environment, the LBYL approach can risk introducing a race condition between “the looking” and “the leaping”. For example, the code, if key in mapping: return mapping[key] can fail if another thread removes key from mapping after the test, but before the lookup.

This issue can be solved with locks or by using the EAFP approach.
Given the EAFP style, it makes even more sense to know and use well else blocks in
try/except statements.

总结一下
^^^^^^^^^^^

用Python解决问题，需要使用很多python语法以外的东西来辅助，这还不算那些针对特定任务的第三方程序包。python的好处是，很多东西都作为标准库集成了进来，比如sqlite3（数据库）、re（正则表达式）、doctest（自动测试）、pathlib+shutil（文件系统）等等。

关于Python
============


试试这个！

.. code-block:: python

    import this


Python这们语言的历史很早，前些年因为数据科学而大火起来。Python的语法、无需编译的特性、pip/conda方便的包管理、强大的注释功能，让python的开发快捷，代码易读，运行方便。Python的运行速度相对c++慢一些，但可以通过很多方式调用c语言的函数库。所以，用python调用pytorch等程序包做数值计算，速度是很快的。



Python 2 or Python 3?
^^^^^^^^^^^^^^^^^^^^^^^^

    教材 *A Primer on Scientific Programming with Python, 5th ed*

我建议使用Python 3，但是这本书推荐Python 2：

    To work with this book, I recommend using `Python version 2.7`. For Chaps. 5–9 and Appendices A–E, you need the NumPy and Matplotlib packages, preferably Preface also the IPython and SciTools packages, and for Appendix G, Cython is required. Other packages used in the text are nose and sympy. Section H.1 has more information on how you can get access to Python and the mentioned packages.

以及

    Python version 2 or 3? A common problem among Python programmers is to choose between version 2 or 3, which at the time of this writing means choosing between version 2.7 and 3.5. A common recommendation is to go for Python 3, because this is the version that will be further developed in the future. However, there is a problem that much useful mathematical software in Python has not yet been ported to Python 3. Therefore, Python version 2.7 is the most popular version for doing scientific computing, and that is why also this book applies version 2.7.

书里还提到了Python 3.5，根据 `changelog <https://docs.python.org/3/whatsnew/3.5.html>`_ ，Python 3.5是2015年推出的， 现在python 3.9都出来了。虽然书中解释说“很多数学库没有迁移到python 3”，那大概也说的是2015年的事情了。现在，很多数学库已经停止了对Python 2.7的支持。

这是Numpy（Python的矩阵运算库）停止对python 2支持的声明：

    **Plan for dropping Python 2.7 support**

    The Python core team plans to stop supporting Python 2 in 2020. The NumPy project has supported both Python 2 and Python 3 in parallel since 2010, and has found that supporting Python 2 is an increasing burden on our limited resources; thus, we plan to eventually drop Python 2 support as well. Now that we’re entering the final years of community-supported Python 2, the NumPy project wants to clarify our plans, with the goal of to helping our downstream ecosystem make plans and accomplish the transition with as little disruption as possible.

    Our current plan is as follows.

    Until December 31, 2018, all NumPy releases will fully support both Python2 and Python3.

    Starting on January 1, 2019, any new feature releases will support only Python3.

    The last Python2 supporting release will be designated as a long term support (LTS) release, meaning that we will continue to merge bug fixes and make bug fix releases for a longer period than usual. Specifically, it will be supported by the community until December 31, 2019.

    On January 1, 2020 we will raise a toast to Python2, and community support for the last Python2 supporting release will come to an end. However, it will continue to be available on PyPI indefinitely, and if any commercial vendors wish to extend the LTS support past this point then we are open to letting them use the LTS branch in the official NumPy repository to coordinate that.


我们还是用python 3进行教学吧。我个人习惯用python 3.7。

关于数值计算
===============

以下列出了一些常用的数值库，并不全面，跟本人背景有关。

=============  =============
基本数学        math
矩阵计算        numpy
基本科学计算    scipy
图像处理        opencv
有限元          finics
分布式计算      bluefog
深度学习        pytorch
深度学习        tensorflow2
机器学习        scikit-learn
xxxxxx          xxxxxxxx
科学计算合集    scitool3
数据管理        pandas
绘图            matplotlib
=============  =============

.. note::

    `scitool3 <https://pypi.org/project/scitools3/#:~:text=SciTools%20is%20a%20Python%20package%20containing%20lots%20of,The%20SciTools%20package%20contains%20a%20lot%20of%20modules%3A>`_ 是一组工具，不是一个工具。它收集了常用的数值计算库，并加入了方便脚本。具体内容可以看这本教材“Python Scripting for Computational Science”, by H. P. Langtangen, 3rd edition, 2nd printing, Springer, 2009*


Python的一大好处就是程序包的获取有统一的平台，你很容易找到文档、示例，以及使用者社区（国内别用Baidu搜！）。具体到本书，用的最多的是 *scitool3* . 这本教材的内容其实相当丰富，在附录里讲了PDE/ODE Solver，还有嵌入C++ library的方法。这都是非常使用的主题。

数值计算也不是非Python不可。排除手撸C++的大佬，Matlab大概才是（物理类）数值计算的主体，大量的仿真都是基于matlab（语言）。学统计的同学可能更熟悉R。更早一点可学计算语言是Fortran，现在很多学校都不再教授了。和C++相比，更简单易用而且适合并发场景的有Golang。以及Julia，年轻但专为科学计算设计。Julia的社区在PDE/ODE以及神经网络方面的讨论和实现很活跃。搞最优化的大佬Stephen Byod就很推荐Julia语言。

事实上，即使是在python大红大紫的深度学习领域，很多知名程序库也在使用自己的语言（或子语言）。比如Pytorch提供了torchscript，它允许通过装饰器，来让PyTorch代码片段作为torchscript编译（这个说法并不太准确），从而获得更高的性能。


教学内容安排（草稿）
====================




第一课（试讲）
========================

本课预览
^^^^^^^^^^^

========  =============================================
环境        - *环境* conda/pip
            - *编辑器* ipython, jupyter notebook, vscode, idle
基本操作    - *基本* import,os,print
            - *控制流* if-else, range + for-lop
            - *容器* list, dict
            - *保存* shelve, json
数值        - *矩阵* numpy
            - *绘图* matplotlib
            - *保存* numpy.save,numpy.load
文档        - *文档* markdown, markdown+latex
========  =============================================


环境搭建
^^^^^^^^^^^

安装Conda `<https://docs.conda.io/projects/conda/en/latest/user-guide/install/>`_

创建python环境，起个名字。

用conda装一个ipython。

在控制台打开ipython，写点什么。

安装vscode，安装Python插件，写点什么。试试debug+breakpoint.

基本操作
^^^^^^^^^^^

写个Hello World，具体来说就是:
.. code-block:: python 

    print("Hello World")

尝试一下控制流，用list打印一个杨辉三角。善用string的split, join， 以及 list的生成器表达式。

把参数存在dict里，尝试用shelve和json保存和加载dict和list.

把整个过程包在函数里，并写成注释（docstring）。

写 ``if __name__=="__main__"`` .

试着从同文件夹下的另一个脚本里，调用这些函数，用import。


数值
^^^^^^^^^^

安装 Numpy

矩阵计算，解个2x2的方程组，numpy.linalg.solve 。

安装 scipy

这次用scipy解方程组，scipy.linalg.solve。

画个函数图像, matplotlib.pyplot.plot。

保存你的结果。

文档
^^^^^

文字描述你的解方程程序，用markdown排个版。

把latex公式写在你的文档里。

Jupyter Notebook
^^^^^^^^^^^^^^^^^^^^^

打开jupyter notebook，把数值和文档两节的内容，装在一个ipynb里。





