==============
sphinx配置
==============

配置文件 /source/conf.py 在构建时作为Python代码执行
(使用 execfile() , 并且当前目录设置为其包含目录)。

项目信息
---------------

=========== ================================================================================================================
project     记录的项目名称。
author      该文件的作者姓名。 默认值为 unknown
copyright   2020, Author Name 风格的版权声明
version     主要项目版本, 用作 `|version|` 的替代品。 例如, 对于Python文档, 这可能类似于 2.6 。
release     完整的项目版本, 用作 `|release|` 的替代品, 例如在HTML模板中。 例如, 对于Python文档, 这可能类似于 2.6.0rc1 。

            如果你不需要在 version 和 release 之间提供分隔, 只需将它们设置为相同的值即可。
=========== ================================================================================================================

一般配置项
--------------

extensions
,,,,,,,,,,,,,,,,,,

可以是Sphinx(名为 sphinx.ext.*)或自定义的扩展。

请注意, 如果扩展名位于另一个目录中, 则可以在conf文件中扩展 sys.path(**使用绝对路径**)。 

如果扩展路径是相对于 configuration directory , 使用 os.path.abspath()

::

   import sys, os
   sys.path.append(os.path.abspath('sphinxext'))
   extensions = ['extname']

这样, 你可以从子目录 sphinxext 加载一个名为 extname 的扩展名。

source_suffix
,,,,,,,,,,,,,,,,,,,,

源文件的文件扩展名。 Sphinx将具有此后缀的文件视为源。

::

   source_suffix = {
       '.rst': 'restructuredtext',
       '.txt': 'restructuredtext',
       '.md': 'markdown',
   }

可以使用源解析器扩展添加新文件类型。
   
source_encoding
,,,,,,,,,,,,,,,,,,

所有reST源文件的编码。推荐的编码和默认值是 'utf-8-sig' 。
   
source_parsers
,,,,,,,,,,,,,,,,,

如果给出, 则不同源的解析器类字典就足够了。键是后缀, 值可以是类或字符串, 给出解析器类的完全限定名称。 
解析器类可以是 docutils.parsers.Parser 或 sphinx.parsers.Parser 。 
不在字典中的后缀的文件将使用默认的reStructuredText解析器进行解析。   

::

   source_parsers = {'.md': 'recommonmark.parser.CommonMarkParser'}

master_doc
,,,,,,,,,,,,,,,,

主目录文件名，默认为index

exclude_patterns
,,,,,,,,,,,,,,,,,,,,,

查找源文件时应排除的glob样式模式列表。 它们与源目录相对于源目录进行匹配, 在所有平台上使用斜杠作为目录分隔符。

示例模式:

::

   'library/xml.rst' – 忽略 library/xml.rst 文件(替换条目 unused_docs)
   'library/xml' – 忽略 library/xml 目录
   'library/xml*' – 忽略以 library/xml 开头的所有文件和目录
   '**/.svn' – 忽略所有 .svn 目录

templates_path
,,,,,,,,,,,,,,,,,

包含额外模板的路径列表(覆盖内置/主题特定模板的模板)。相对路径被视为相对于配置目录。

由于这些文件不是要构建的, 因此它们会自动添加到 exclude_patterns 中.
  
rst_epilog
,,,,,,,,,,,

一串reStructuredText, 它将包含在每个读取的源文件的末尾。

::

   rst_epilog = """
   .. |psf| replace:: Python Software Foundation
   """

rst_prolog
,,,,,,,,,,,,,,,,

一串reStructuredText, 它将包含在每个读取的源文件的开头。 

::

   rst_prolog = """
   .. |psf| replace:: Python Software Foundation
   """

primary_domain
,,,,,,,,,,,,,,,,,

default_role
,,,,,,,,,,,,,

keep_warnings
,,,,,,,,,,,,,,,,,,

suppress_warnings
,,,,,,,,,,,,,,,,,,,,,,

用于禁止任意警告消息的警告类型列表。

Sphinx支持以下警告类型:

+ app.add_node
+ app.add_directive
+ app.add_role
+ app.add_generic_role
+ app.add_source_parser
+ download.not_readable
+ image.not_readable
+ ref.term
+ ref.ref
+ ref.numref
+ ref.keyword
+ ref.option
+ ref.citation
+ ref.footnote
+ ref.doc
+ ref.python
+ misc.highlighting_failure
+ toc.secnum
+ epub.unknown_project_files

needs_sphinx
,,,,,,,,,,,,,

指定用来构建的sphinx版本，如果设置为 major.minor 版本字符串, 如 '1.1' , 
Sphinx会将其与版本进行比较, 如果它太旧则拒绝构建。 默认是没有要求的。

needs_extensions
,,,,,,,,,,,,,,,,,,,,,,,

指定扩展的版本 , 例如: needs_extensions = {'sphinxcontrib.something':'1.5'} 。
版本字符串应采用 major.minor 形式。不必为所有扩展指定要求, 仅适用于您要检查的扩展。

manpages_url
,,,,,,,,,,,,,,,,,

交叉引用的URL manpage 指令。
如果将其定义为 https://manpages.debian.org/{path} , 则 :manpage:`man(1)` 角色将链接到 <https://manpages.debian.org/man(1)> 。

可用的模式是:

+ page - 手册页 (man)
+ section - 手册部分 (1)
+ path - 原始的手册页和指定的部分(man(1))

numfig
,,,,,,,,,,,

如果为true, 则数字, 表格和代码块如果有标题则会自动编号。 numref 角色已启用。

numfig_format
,,,,,,,,,,,,,,,,,,

一个字典将 'figure' , 'table' , 'code-block' 和 'section' 映射到用于图号格式的字符串。作为一个特殊字符, ％s 将被替换为图号。
默认是使用 'Fig. %s' 为 'figure' , 'Table ％s' 为 'table' , 'Listing ％s' 为 'code-block' 和 'Section' 为 'section'

numfig_secnum_depth
,,,,,,,,,,,,,,,,,,,,,,,,,,,

+ 如果设置为 0 , 则数字, 表格和代码块从 1 开始连续编号。
+ 如果 1 (默认)数字将是 x.1 , x.2 , … 与 x 的节号(顶级切片;没有 x 如果没有部分)。只有当通过 toctree 指令的 :numbered: 选项激活了段号时, 这才自然适用。
+ 2 表示数字将是 xy1 , xy2 , …如果位于子区域(但仍然是 x.1 , x.2 , … 如果直接位于一个部分和 1 , 2 , … 如果不在任何顶级部分。)

smartquotes
,,,,,,,,,,,,,,,,,,

smartquotes_action
,,,,,,,,,,,,,,,,,,,,,,,,

smartquotes_excludes
,,,,,,,,,,,,,,,,,,,,,,,,

tls_verify
,,,,,,,,,,,,,,,,,,,,

如果为true, Sphinx将验证服务器认证。默认为 True 。

tls_cacerts
,,,,,,,,,,,,,,,,,
CA的证书文件的路径或包含证书的目录的路径。这也允许字典映射主机名到证书文件的路径。证书用于验证服务器认证。

highlight_language
,,,,,,,,,,,,,,,,,,,,,,,,,

用于突出显示源代码的默认语言。默认语言为 'python3' 。
`代码高亮 <https://www.sphinx.org.cn/usage/restructuredtext/directives.html#code-examples>`_

highlight_options
,,,,,,,,,,,,,,,,,,,,,,,

`Pygments documentation <http://pygments.org/docs/lexers/>`_

pygments_style
,,,,,,,,,,,,,,,,,,

用于Pygments突出显示源代码的样式名称。如果未设置, 则为HTML输出选择主题的默认样式或 'sphinx' 。

add_function_parentheses
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
一个布尔值, 决定是否将括号附加到函数和方法角色文本(例如 :func:`input` 的内容)以表示该名称是可调用的。默认为 True 。

add_module_names
,,,,,,,,,,,,,,,,,,,,,
A boolean that decides whether module names are prepended to all object names 
(for object types where a “module” of some kind is defined), e.g. for py:function directives. Default is True.

show_authors
,,,,,,,,,,,,,,,,,,,
一个布尔值, 决定 codeauthor 和 sectionauthor 指令在构建的文件中产生任何输出。

modindex_common_prefix
,,,,,,,,,,,,,,,,,,,,,,,,,
为了对Python模块索引进行排序而忽略的前缀列表(例如, 如果将其设置为 ['foo.'] , 那么 foo.bar 将显示在 B 下, 而不是 F )。
如果您记录包含单个包的项目, 这可能很方便。仅适用于当前的HTML构建器。默认是 [] 。

trim_footnote_reference_space
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
在脚注引用之前修剪空格, 这是reST解析器识别脚注所必需的, 但在输出中看起来不太好。

trim_doctest_flags
,,,,,,,,,,,,,,,,,,,,,,,,,,
如果为true, 则删除doctest标志(在行的末尾看起来像 doctest:FLAG, ... 的注释)和 <BLANKLINE> 标记, 
以显示交互式Python会话的所有代码块(即doctests) 。
默认为 True 。有关包含doctests的更多可能性, 请参阅扩展名 doctest 。

国际化选项
----------------

影响Sphinx的 母语支持 

language
文档编写语言的代码。Sphinx自动生成的任何文本都将使用该语言。

目前Sphinx支持的语言是:

+ bn – 孟加拉语
+ ca – 加泰罗尼亚语
+ cs – 捷克语
+ da – 丹麦语
+ de – 德语
+ en – 英语
+ es – 西班牙语
+ et – 爱沙尼亚语
+ eu – 巴斯克语
+ fa – 伊朗语
+ fi – 芬兰语
+ fr – 法语
+ he – 希伯来语
+ hr – 克罗地亚语
+ hu – 匈牙利语
+ id – 印度尼西亚语
+ it – 意大利语
+ ja – 日语
+ ko – 朝鲜语
+ lt – 立陶宛语
+ lv – 拉脱维亚语
+ mk – 马其顿语
+ nb_NO – 挪威博克马尔语
+ ne – 尼泊尔语
+ nl – 荷兰语
+ pl – 波兰语
+ pt_BR – 巴西葡萄牙语
+ pt_PT – 欧洲葡萄牙语
+ ru – 俄语
+ si – 僧伽罗语
+ sk – 斯洛伐克语
+ sl – 斯洛文尼亚语
+ sv – 瑞典语
+ tr – 土耳其语
+ uk_UA – 乌克兰语
+ vi – 越南语
+ zh_CN – 简体中文
+ zh_TW – 繁体中文

locale_dirs
,,,,,,,,,,,,,,,,,

相对于源目录, 在其中搜索其他消息目录(请参阅 language )的目录。此路径上的目录由标准 gettext 模块搜索。

内部消息是从 sphinx 的文本域中获取的;因此, 如果将目录 。/locale 添加到此设置, 则消息目录(使用 msgfmt 编译为 .po 格式)必须位于 ./locale/language/LC_MESSAGES/sphinx.mo 。
单个文档的文本域取决于 gettext_compact 。

默认是 ['locales'].

gettext_compact
,,,,,,,,,,,,,,,,,,,,,,,,
如果为true, 则文档的文本域是其docname, 如果它是顶级项目文件, 则为其基本目录。

默认情况下, 文档 markup/code.rst 最终出现在 markup 文本域中。将此选项设置为 False , 它是 标记/代码 。

gettext_uuid
,,,,,,,,,,,,,,,,,

如果为true, 则Sphinx会在消息目录中生成用于版本跟踪的uuid信息。它用于:

在.pot文件中为每个msgids添加uid行。

计算新msgids和以前保存的旧msgids之间的相似性。这种计算需要很长时间。

如果你想加速计算, 你可以使用 pip install python-levenshtein 来使用C编写的 python-levenshtein 第三方包。

默认是 False.

gettext_location
,,,,,,,,,,,,,,,,,,,,
如果为true, 则Sphinx为消息目录中的消息生成位置信息。

默认是 True.

gettext_auto_build
,,,,,,,,,,,,,,,,,,,,,,
如果为true, 则Sphinx为每个翻译目录文件构建mo文件。

默认是 True.

gettext_additional_targets
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
指定名称以启用gettext提取和转换。您可以指定以下名称:

索引
索引条款

Literal-block
文字块: :: 和 code-block.

Doctest-block
doctest块

Raw
原始内容

图片
image/figure uri 和 alt

例如: gettext_additional_targets = ['literal-block', 'image'] .

默认是 [].


figure_language_filename
语言特定数字的文件名格式。默认值为 {root}.{language}{ext} 。它将从 .. image:: dirname/filename.png 扩展为 dirname/filename.en.png 。可用的格式标记是:

{root} - 文件名, 包括任何路径组件, 没有文件扩展名, 例如 dirname/filename

{path} - 文件名的目录路径组件, 如果非空, 则带有斜杠, 例如: dirname/

{basename} - 没有目录路径或文件扩展名组件的文件名, 例如 filename

{ext} - 文件扩展名, 例如 .png

{language} - 翻译语言, 例如 en

例如, 将其设置为 {path}{language}/{basename}{ext} 将扩展为 dirname/en/filename.png。

1.4 新版功能.

在 1.5 版更改: 添加了 {path} 和 {basename} 标记。


配置文件示例
-----------------

::

   # -*- coding: utf-8 -*-
   # test documentation build configuration file, created by
   # sphinx-quickstart on Sun Jun 26 00:00:43 2016.
   #
   # This file is execfile()d with the current directory set to its
   # containing dir.
   #
   # Note that not all possible configuration values are present in this
   # autogenerated file.
   #
   # All configuration values have a default; values that are commented out
   # serve to show the default.
   
   # If extensions (or modules to document with autodoc) are in another directory,
   # add these directories to sys.path here. If the directory is relative to the
   # documentation root, use os.path.abspath to make it absolute, like shown here.
   #
   # import os
   # import sys
   # sys.path.insert(0, os.path.abspath('.'))
   
   # -- General configuration ------------------------------------------------
   
   # If your documentation needs a minimal Sphinx version, state it here.
   #
   # needs_sphinx = '1.0'
   
   # Add any Sphinx extension module names here, as strings. They can be
   # extensions coming with Sphinx (named 'sphinx.ext.*') or your custom
   # ones.
   extensions = []
   
   # Add any paths that contain templates here, relative to this directory.
   templates_path = ['_templates']
   
   # The suffix(es) of source filenames.
   # You can specify multiple suffix as a list of string:
   #
   # source_suffix = ['.rst', '.md']
   source_suffix = '.rst'
   
   # The encoding of source files.
   #
   # source_encoding = 'utf-8-sig'
   
   # The master toctree document.
   master_doc = 'index'
   
   # General information about the project.
   project = u'test'
   copyright = u'2016, test'
   author = u'test'
   
   # The version info for the project you're documenting, acts as replacement for
   # |version| and |release|, also used in various other places throughout the
   # built documents.
   #
   # The short X.Y version.
   version = u'test'
   # The full version, including alpha/beta/rc tags.
   release = u'test'
   
   # The language for content autogenerated by Sphinx. Refer to documentation
   # for a list of supported languages.
   #
   # This is also used if you do content translation via gettext catalogs.
   # Usually you set "language" from the command line for these cases.
   language = None
   
   # There are two options for replacing |today|: either, you set today to some
   # non-false value, then it is used:
   #
   # today = ''
   #
   # Else, today_fmt is used as the format for a strftime call.
   #
   # today_fmt = '%B %d, %Y'
   
   # List of patterns, relative to source directory, that match files and
   # directories to ignore when looking for source files.
   # These patterns also affect html_static_path and html_extra_path
   exclude_patterns = ['_build', 'Thumbs.db', '.DS_Store']
   
   # The reST default role (used for this markup: `text`) to use for all
   # documents.
   #
   # default_role = None
   
   # If true, '()' will be appended to :func: etc. cross-reference text.
   #
   # add_function_parentheses = True
   
   # If true, the current module name will be prepended to all description
   # unit titles (such as .. function::).
   #
   # add_module_names = True
   
   # If true, sectionauthor and moduleauthor directives will be shown in the
   # output. They are ignored by default.
   #
   # show_authors = False
   
   # The name of the Pygments (syntax highlighting) style to use.
   pygments_style = 'sphinx'
   
   # A list of ignored prefixes for module index sorting.
   # modindex_common_prefix = []
   
   # If true, keep warnings as "system message" paragraphs in the built documents.
   # keep_warnings = False
   
   # If true, `todo` and `todoList` produce output, else they produce nothing.
   todo_include_todos = False
   
   
   # -- Options for HTML output ----------------------------------------------
   
   # The theme to use for HTML and HTML Help pages.  See the documentation for
   # a list of builtin themes.
   #
   html_theme = 'alabaster'
   
   # Theme options are theme-specific and customize the look and feel of a theme
   # further.  For a list of options available for each theme, see the
   # documentation.
   #
   # html_theme_options = {}
   
   # Add any paths that contain custom themes here, relative to this directory.
   # html_theme_path = []
   
   # The name for this set of Sphinx documents.
   # "<project> v<release> documentation" by default.
   #
   # html_title = u'test vtest'
   
   # A shorter title for the navigation bar.  Default is the same as html_title.
   #
   # html_short_title = None
   
   # The name of an image file (relative to this directory) to place at the top
   # of the sidebar.
   #
   # html_logo = None
   
   # The name of an image file (relative to this directory) to use as a favicon of
   # the docs.  This file should be a Windows icon file (.ico) being 16x16 or 32x32
   # pixels large.
   #
   # html_favicon = None
   
   # Add any paths that contain custom static files (such as style sheets) here,
   # relative to this directory. They are copied after the builtin static files,
   # so a file named "default.css" will overwrite the builtin "default.css".
   html_static_path = ['_static']
   
   # Add any extra paths that contain custom files (such as robots.txt or
   # .htaccess) here, relative to this directory. These files are copied
   # directly to the root of the documentation.
   #
   # html_extra_path = []
   
   # If not None, a 'Last updated on:' timestamp is inserted at every page
   # bottom, using the given strftime format.
   # The empty string is equivalent to '%b %d, %Y'.
   #
   # html_last_updated_fmt = None
   
   # Custom sidebar templates, maps document names to template names.
   #
   # html_sidebars = {}
   
   # Additional templates that should be rendered to pages, maps page names to
   # template names.
   #
   # html_additional_pages = {}
   
   # If false, no module index is generated.
   #
   # html_domain_indices = True
   
   # If false, no index is generated.
   #
   # html_use_index = True
   
   # If true, the index is split into individual pages for each letter.
   #
   # html_split_index = False
   
   # If true, links to the reST sources are added to the pages.
   #
   # html_show_sourcelink = True
   
   # If true, "Created using Sphinx" is shown in the HTML footer. Default is True.
   #
   # html_show_sphinx = True
   
   # If true, "(C) Copyright ..." is shown in the HTML footer. Default is True.
   #
   # html_show_copyright = True
   
   # If true, an OpenSearch description file will be output, and all pages will
   # contain a <link> tag referring to it.  The value of this option must be the
   # base URL from which the finished HTML is served.
   #
   # html_use_opensearch = ''
   
   # This is the file name suffix for HTML files (e.g. ".xhtml").
   # html_file_suffix = None
   
   # Language to be used for generating the HTML full-text search index.
   # Sphinx supports the following languages:
   #   'da', 'de', 'en', 'es', 'fi', 'fr', 'hu', 'it', 'ja'
   #   'nl', 'no', 'pt', 'ro', 'ru', 'sv', 'tr', 'zh'
   #
   # html_search_language = 'en'
   
   # A dictionary with options for the search language support, empty by default.
   # 'ja' uses this config value.
   # 'zh' user can custom change `jieba` dictionary path.
   #
   # html_search_options = {'type': 'default'}
   
   # The name of a javascript file (relative to the configuration directory) that
   # implements a search results scorer. If empty, the default will be used.
   #
   # html_search_scorer = 'scorer.js'
   
   # Output file base name for HTML help builder.
   htmlhelp_basename = 'testdoc'
   
   # -- Options for LaTeX output ---------------------------------------------
   
   latex_elements = {
       # The paper size ('letterpaper' or 'a4paper').
       #
       # 'papersize': 'letterpaper',
   
       # The font size ('10pt', '11pt' or '12pt').
       #
       # 'pointsize': '10pt',
   
       # Additional stuff for the LaTeX preamble.
       #
       # 'preamble': '',
   
       # Latex figure (float) alignment
       #
       # 'figure_align': 'htbp',
   }
   
   # Grouping the document tree into LaTeX files. List of tuples
   # (source start file, target name, title,
   #  author, documentclass [howto, manual, or own class]).
   latex_documents = [
       (master_doc, 'test.tex', u'test Documentation',
        u'test', 'manual'),
   ]
   
   # The name of an image file (relative to this directory) to place at the top of
   # the title page.
   #
   # latex_logo = None
   
   # If true, show page references after internal links.
   #
   # latex_show_pagerefs = False
   
   # If true, show URL addresses after external links.
   #
   # latex_show_urls = False
   
   # Documents to append as an appendix to all manuals.
   #
   # latex_appendices = []
   
   # If false, no module index is generated.
   #
   # latex_domain_indices = True
   
   
   # -- Options for manual page output ---------------------------------------
   
   # One entry per manual page. List of tuples
   # (source start file, name, description, authors, manual section).
   man_pages = [
       (master_doc, 'test', u'test Documentation',
        [author], 1)
   ]
   
   # If true, show URL addresses after external links.
   #
   # man_show_urls = False
   
   
   # -- Options for Texinfo output -------------------------------------------
   
   # Grouping the document tree into Texinfo files. List of tuples
   # (source start file, target name, title, author,
   #  dir menu entry, description, category)
   texinfo_documents = [
       (master_doc, 'test', u'test Documentation',
        author, 'test', 'One line description of project.',
        'Miscellaneous'),
   ]
   
   # Documents to append as an appendix to all manuals.
   #
   # texinfo_appendices = []
   
   # If false, no module index is generated.
   #
   # texinfo_domain_indices = True
   
   # How to display URL addresses: 'footnote', 'no', or 'inline'.
   #
   # texinfo_show_urls = 'footnote'
   
   # If true, do not generate a @detailmenu in the "Top" node's menu.
   #
   # texinfo_no_detailmenu = False
   
   # -- A random example -----------------------------------------------------
   
   import sys, os
   sys.path.insert(0, os.path.abspath('.'))
   exclude_patterns = ['zzz']
   
   numfig = True
   #language = 'ja'
   
   extensions.append('sphinx.ext.todo')
   extensions.append('sphinx.ext.autodoc')
   #extensions.append('sphinx.ext.autosummary')
   extensions.append('sphinx.ext.intersphinx')
   extensions.append('sphinx.ext.mathjax')
   extensions.append('sphinx.ext.viewcode')
   extensions.append('sphinx.ext.graphviz')
   
   
   autosummary_generate = True
   html_theme = 'default'
   #source_suffix = ['.rst', '.txt']