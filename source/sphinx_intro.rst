==============
sphinx介绍
==============

基本介绍
----------------

Sphinx 是一种文档工具，它可以令人轻松的撰写出清晰且优美的文档, 由 Georg Brandl 在BSD 许可证下开发。

它最初是为Python文档创建的，它具有出色的工具，可用于各种语言的软件项目文档。

+ 输出格式: HTML（包括Windows HTML帮助），LaTeX（适用于可打印的PDF版本），ePub，Texinfo，手册页，纯文本
+ 广泛的交叉引用: 语义标记和功能，类，引用，词汇表术语和类似信息的自动链接
+ 分层结构: 轻松定义文档树，自动链接到平级，上级和下级
+ 自动索引: 一般索引以及特定于语言的模块索引
+ 代码处理: 使用 `Pygments <https://pygments.org/>`_ 荧光笔自动突出显示
+ 扩展: 自动测试代码片段，包含Python模块（API文档）中的文档字符串等
+ 贡献的扩展: 用户在第二个存储库中贡献了50多个扩展;其中大多数可以从PyPI安装

Sphinx使用reStructuredText作为其标记语言，其许多优点来自reStructuredText及其解析
和翻译套件 `Docutils <https://docutils.sourceforge.io/>`_ 的强大功能和直接性。

安装
-------------------

Sphinx是用 Python 编写的，支持Python 3.5+。

Linux
,,,,,,,,,,

Debian/Ubuntu
..................

使用 apt-get 安装 python3-sphinx:

::

	$ apt-get install python3-sphinx
	
RHEL, CentOS
.....................

使用 yum 安装 python-sphinx :
::

   $ yum install python-sphinx

PyPI
,,,,,,,,,

::

	pip install -U sphinx
	
源码安装
,,,,,,,,,,,

::

   git clone https://github.com/sphinx-doc/sphinx
   $ cd sphinx
   $ pip install .

与其他标记语言互相转换
------------------------

+ Gerard Flanagan编写了一个脚本，将纯HTML转换为reST;它可以在 `Python包索引 <https://pypi.org/project/html2rest/>`_ 找到。
+ 为了将旧的Python文档转换为Sphinx，编写了一个转换器，可以在 `Python SVN存储库 <https://svn.python.org/projects/doctools/converter/>`_ 中找到。
  它包含将Python-doc样式的LaTeX标记转换为Sphinx reST的通用代码。
+ Marcin Wojdyr编写了一个脚本，将Docbook转换为使用Sphinx标记的reST; 它位于 `GitHub <https://github.com/wojdyr/db2rst>`_ 。
+ Christophe de Vienne编写了一个工具，用于将Open/LibreOffice文档转换为Sphinx: `odt2sphinx <https://pypi.org/project/odt2sphinx/>`_ 。
+ 要转换不同的标记语言文本，`Pandoc <https://pandoc.org/>`_ 是一个非常有用的工具。

快速开始
---------------

为了简化入门过程，Sphinx提供了一个工具 sphinx-quickstart，
它将生成一个文档源目录并用一些默认值填充它。

::

   # 如果网速堪忧，增加 -i https://pypi.douban.com/simple
   pip install sphinx sphinx-autobuild sphinx_rtd_theme

::

   # 从命令行进入你的初始化目录，如果要托管到github，则为本地仓目录
   sphinx-quickstart

::

   # 初始化过程中的配置项
   Separate source and  directories (y/n) [n]:y  # 是否分离build和source目录
   Project name: sphinx_handbook  # 项目名
   Author name(s): firewang  # 作者
   Project version []:  # 默认没有版本，按Enter跳过
   Project release []:  # 默认没有发布版本，按Enter跳过   
   Project language [en]: zh_CN  # 默认英文，指定为中文

::

   # Sphinx中的插件配置
   > autodoc: automatically insert docstrings from modules (y/n) [n]:
   > doctest: automatically test code snippets in doctest blocks (y/n) [n]:
   > intersphinx: link between Sphinx documentation of different projects (y/n) [n]:
   > todo: write "todo" entries that can be shown or hidden on build (y/n) [n]:
   > coverage: checks for documentation coverage (y/n) [n]:
   > imgmath: include math, rendered as PNG or SVG images (y/n) [n]:
   > mathjax: include math, rendered in the browser by MathJax (y/n) [n]:
   > ifconfig: conditional inclusion of content based on config values (y/n) [n]:
   > viewcode: include links to the source code of documented Python objects (y/n) [n]:
   > githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]:
   #autodoc:从模块中自动插入代码
   #doctest:在文档中自动测试代码段
   #intersphinx:在不同的项目文档中的链接
   #todo:写入“todo”条目，可以在构建文档中显示或隐藏
   #coverage:检查文档覆盖率
   #imgmath:提供PNG或SVG图像(包含数学)
   #mathjax:提供浏览器插件MathJax(包含数学)
   #ifconfig:根据配置值的内容纳入条件
   #viewcode:包含指向Python对象源代码的链接
   #githubpages:创建.nojekyll文件以在GitHub页面上发布文档


::

   # 初始化完成以后，在目录下就会生成以下内容
   ├── build
   ├── make.bat
   ├── Makefile
   └── source
       ├── conf.py
       ├── index.rst
       ├── _static
       └── _templates
       
   # build 为编译后生成的文档
   # source 为文档目录，其中index.rst 为索引目录，conf.py 是配置文件

之后新增、修改文件后更新编译文档，有两种方式

+ **使用 sphinx-build 程序启动构建**

::
	
	$ sphinx-build -b html sourcedir builddir

其中 sourcedir 是 source directory ，builddir 是您要在其中放置构建文档的目录。 -b 选项选择一个构建器。


+ **通过make**

sphinx-quickstart 脚本创建了一个 Makefile 和一个 make.bat，它让你的生活更加轻松。

::

   make html
   # make pdf
   # make epub