第一节 Hello Python !
-----------------------

.. toctree::

    /notebook/section_1
    /notebook/markdown_example

预览
==========

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
==============

安装Conda `<https://docs.conda.io/projects/conda/en/latest/user-guide/install/>`_

用conda创建python环境，起个名字，然后装一个ipython。

.. code-block:: sh

    conda -n myenv python=3.7
    conda activate myenv
    conda install ipython 


在控制台打开ipython，写点什么。

.. image:: /_static/assets/section_1/images/ipython_sh.png

安装vscode，安装Python插件，写点什么。试试debug+breakpoint.

.. image:: /_static/assets/section_1/images/python_ext.png

基本操作
=================

写个Hello World，具体来说就是:

.. code-block:: python 

    print("Hello World")

写程序，打印一个杨辉三角（程序略）。

.. hint::

    尝试if-else和for-loop，使用list存储数据。善用string类的split, join函数， 以及使用list的生成器表达式来简化代码。

把参数存在dict里，尝试用shelve和json保存和加载dict和list.

.. code-block::

    import shelve
    sh = shelve.open('a.shelf',writeback=True)
    sh['title'] = "An Introduction to Python"
    sh.close()

    sh2 = shelve.open('a.shelf')
    print(sh2['title'])


.. code-block::

    import json
    s = json.dumps({'title':'An Introduction to Python'})
    print(s)
    d = json.loads(s)
    print(type(d))
    print(d)



把整个过程包在函数里，并写成注释（docstring）。

把实际的函数调用放在 ``if __name__=="__main__"``里，这样我们就能从其他文件调用这个函数，而不触发执行：

.. code-block:: python

    # util.py
    def f():
        pass

    if __name__=='__main__':
        f() # call function f

试着从同文件夹下的另一个脚本里，调用这些函数，用import。

.. code-block:: python

    # main.py
    from util import f

    f()


数值
===========

用conda安装 numpy, matplotlib。在ipython里完成以下任务：

- 矩阵计算：解一个2x2线性方程组，numpy.linalg.solve 。

- 绘制函数图像 :math:`y=x(x-1)` ： matplotlib.pyplot.plot。


文档
=======

安装vscode的markdown插件。

文字描述你的解方程程序，用markdown排个版。

用latex把公式写在你的markdwon文档里，作为程序注释。

.. math::

    \begin{pmatrix}
    1&0\\
    1&1
    \end{pmatrix}
    \begin{pmatrix}
    x_1\\
    x_2
    \end{pmatrix}=
    \begin{pmatrix}
    1\\
    2
    \end{pmatrix}

.. code-block:: markdown

    # 解线性方程组

    > 使用 numpy.linalg.solve

    公式如下：

    $$
    \begin{pmatrix}
    1&0\\
    1&1
    \end{pmatrix}
    \begin{pmatrix}
    x_1\\
    x_2
    \end{pmatrix}=
    \begin{pmatrix}
    1\\
    2
    \end{pmatrix}
    $$

渲染效果：

.. image:: /_static/assets/section_1/images/md_lineq.png

Jupyter Notebook
====================

打开jupyter notebook，把数值和文档两节的内容，装在一个ipynb里。





