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

+ 在.pot文件中为每个msgids添加uid行。
+ 计算新msgids和以前保存的旧msgids之间的相似性。(计算时间长)
	
如果想加速计算, 可以使用 pip install python-levenshtein 来使用C编写的 python-levenshtein 第三方包。

默认是 False.

gettext_location
,,,,,,,,,,,,,,,,,,,,

如果为true, 则Sphinx为消息目录中的消息生成位置信息。默认 True.

gettext_auto_build
,,,,,,,,,,,,,,,,,,,,,,

如果为true, 则Sphinx为每个翻译目录文件构建mo文件。

默认是 True.

gettext_additional_targets
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

指定名称以启用gettext提取和转换。可以指定以下名称:

=============== ==============
索引:           索引条款
Literal-block:  文字块和code-block
Doctest-block:  doctest块
Raw:            原始内容
图片:           image/figure uri 和 alt
=============== ==============

例如: gettext_additional_targets = ['literal-block', 'image']
默认是 []

figure_language_filename
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

语言特定数字的文件名格式。默认值为 `{root}.{language}{ext}`
它将从 `.. image:: dirname/filename.png` 扩展为 `dirname/filename.en.png` 可用的格式标记是:

+ {root} - 文件名, 包括任何路径组件, 没有文件扩展名, 例如 dirname/filename
+ {path} - 文件名的目录路径组件, 如果非空, 则带有斜杠, 例如 dirname/
+ {basename} - 没有目录路径或文件扩展名组件的文件名, 例如 filename
+ {ext} - 文件扩展名, 例如 .png
+ {language} - 翻译语言, 例如 en

例如, 将其设置为 `{path}{language}/{basename}{ext}` 将扩展为 `dirname/en/filename.png`

数学选项
-----------------------

================== ==========================================
math_number_all    如果要对所有显示的数学项进行编号, 请将此选项设置为 True 。默认为 False 。
math_eqref_format  用于格式化方程式引用标签的字符串。 {number} 占位符代表等式编号。
                   例: 'Eq.{number}' 被渲染为, 例如, Eq.10.
math_numfig        如果为 True , 则在页面中下显示的数学公式编号。默认为 True 。
================== ==========================================

HTML输出选项
------------------

这些选项会影响HTML以及HTML帮助输出, 以及使用Sphinx的HTMLWriter类的其他构建器。

html主题html_theme
,,,,,,,,,,,,,,,,,,,,,

页面主题模板，默认 alabaster 。 `内置主题信息 <https://www.sphinx.org.cn/usage/theming.html#builtin-themes>`_

html_theme_options
,,,,,,,,,,,,,,,,,,,,,,,,,

所选主题外观的选项字典。

html_theme_path
,,,,,,,,,,,,,,,,,,,,,,

包含自定义主题的路径列表, 可以是子目录, 也可以是zip文件。相对路径被视为相对于配置目录。

html_style
,,,,,,,,,,,,,,,,,,,
用于HTML页面的样式表。该名称的文件必须存在于Sphinx的 static/ 路径中, 或者存在于 html_static_path 中给出的自定义路径之一。
默认值是所选主题给出的样式表。如果您只想添加或覆盖与主题样式表相比的一些内容, 使用CSS @import 导入主题的样式表。

html_title
,,,,,,,,,,,,,,,,,

使用Sphinx内置模板生成的html页面的title。默认 `<project> v<revision> documentation`

html_short_title
在HTML docs 和 HTML Help docs 使用的 html title。
默认使用 html_title 的设置值

html_baseurl
,,,,,,,,,,,,,,,,,,,

指向HTML文档根目录的URL。它用于表示文档的位置, 如 canonical_url 。

html_context
要传递到所有页面的模板引擎上下文的值字典。
单个值也可以使用sphinx-build 的-A命令行选项来设置。

html_logo
,,,,,,,,,,,,,,

文档的徽标,位于侧边栏的顶部，宽度不应超过200像素。默认值:None。

如果给定, 则必须是图像文件的名称(相对于 configuration directory 的路径)。

若图片文件不存在于 _static目录，将被复制到输出HTML的 _static 目录中。

html_favicon
,,,,,,,,,,,,,,,,

文档的favicon，现代浏览器使用它作为标签, 窗口和书签的图标。它应该是一个Windows风格的图标文件(.ico), 大小为16x16或32x32像素。默认值: None 。

如果给定, 则必须是图像文件的名称(相对于 configuration directory 的路径)。

若图片文件不存在于 _static目录，将被复制到输出HTML的 _static 目录中。

html_css_files
,,,,,,,,,,,,,,,,,,

CSS文件列表。该条目必须是filename字符串或包含filename 字符串和attributes字典的元组。 
filename 必须相对于 html_static_path , 或者是一个完整的URI, 如 http://example.org/style.css 。
attributes 用于 <link> 标签的属性。默认为空列表。

::

	html_css_files = ['custom.css'
                  'https://example.com/css/custom.css',
                  ('print.css', {'media': 'print'})]

html_js_files
,,,,,,,,,,,,,,,,,

JavaScript filename 列表。该条目必须是 filename 字符串或包含 filename 字符串和 attributes 字典的元组。 
filename 必须相对于 html_static_path , 或者是一个完整的URI, 如 http://example.org/script.js 。 
attributes 用于 <script> 标签的属性。默认为空列表。

::

    html_js_files = ['script.js',
                 'https://example.com/scripts/custom.js',
                 ('custom.js', {'async': 'async'})]

html_static_path
,,,,,,,,,,,,,,,,,,,,,

包含自定义静态文件(例如样式表css或脚本文件js)的路径列表。

相对路径被视为相对于配置目录。它们被复制到主题的静态文件之后的输出的 \_static 目录中, 
因此名为 default.css 的文件将覆盖主题的 default.css 。

由于这些文件不是要构建的, 因此它们会自动从源文件中排除。

html_extra_path
,,,,,,,,,,,,,,,,,,

包含与文档无直接关系的额外文件的路径列表, 例如 robots.txt 或 .htaccess 。

相对路径被视为相对于配置目录。它们被复制到输出目录。它们将覆盖任何同名的现有文件。

由于这些文件不是要构建的, 因此它们会自动从源文件中排除。

html_last_updated_fmt
,,,,,,,,,,,,,,,,,,,,,,,,,,

如果这不是None, 则使用给定的 strftime() 格式在每个页面底部插入 ‘Last updated on:’ 时间戳。空字符串相当于 '％b％d, ％Y' (或依赖于语言环境的等价物)。

html_use_smartypants
,,,,,,,,,,,,,,,,,,,,,,,,,,

如果为true, 则引号和短划线将转换为印刷正确的实体。默认值: True 。

html_add_permalinks
,,,,,,,,,,,,,,,,,,,,,,,,,,

Sphinx will add “permalinks” for each heading and description environment as paragraph signs that become visible when the mouse hovers over them.

This value determines the text for the permalink; it defaults to "¶". Set it to None or the empty string to disable permalinks.

html_sidebars
,,,,,,,,,,,,,,,,,,

自定义侧边栏模板必须是将文档名称映射到模板名称的字典。

键可以包含glob样式的模式, 所有匹配的文档都将获得指定的侧边栏。(当多个glob样式模式与任何文档匹配时会发出警告)

值是列表,它指定要包括的侧边栏模板的完整列表。如果要包含所有或部分默认侧边栏, 则必须将它们放入此列表中。
默认侧边栏(适用于与任何模式不匹配的文档)由主题本身定义。
内置主题默认使用这些模板: ['localtoc.html', 'relations.html' , 'sourcelink.html' , 'searchbox.html']

可呈现的内置侧边栏模板是:

+ localtoc.html - 当前文档的细粒度目录
+ globaltoc.html – 折叠整个文档集的粗粒度目录
+ relations.html – 两个指向上一个和下一个文档的链接
+ sourcelink.html – 指向当前文档源的链接(如果在 html_show_sourcelink 中启用)
+ searchbox.html – the “quick search” box

::

    html_sidebars = {
   '**': ['globaltoc.html', 'sourcelink.html', 'searchbox.html'],
   'using/windows': ['windowssidebar.html', 'searchbox.html'],}
   
这将呈现自定义模板 windowssidebar.html 和给定文档侧边栏内的快速搜索框, 并呈现所有其他页面的默认侧边栏(除了本地TOC被全局TOC替换)。

|  如果所选主题不具有侧边栏, 则此值仅无效, 例如内置 scrolls 和 haiku 。

html_additional_pages
,,,,,,,,,,,,,,,,,,,,,,,,,

为HTML页面指定其他模板，为文档名称映射到模板名称的字典。

::

  html_additional_pages = {
    'download': 'customdownload.html',}
	
这将把模板 customdownload.html 渲染为页面 download.html 。

html_domain_indices
,,,,,,,,,,,,,,,,,,,,,,,

如果为true, 则除了常规索引外, 还会生成特定于域的索引。对于例如Python域, 这是全局模块索引。默认为 True 。

此值可以是bool或应生成的索引名称列表。要查找特定索引的索引名称, 请查看HTML文件名。
例如, Python模块索引的名称为 'py-modindex' 。

html_use_index
,,,,,,,,,,,,,,,,,,

默认为True,为HTML文档添加索引。

html_split_index
,,,,,,,,,,,,,,,,,,,,

默认False，如果为true, 则索引生成两次:一次作为包含所有条目的单个页面, 一次作为每个起始字母的一个页面。

html_copy_source
,,,,,,,,,,,,,,,,,,,,,,

默认为true, reST源包含在HTML构建中 \_sources/name

html_show_sourcelink
,,,,,,,,,,,,,,,,,,,,,,,,,,,,

默认为true(并且 html_copy_source 也为 true ), 则指向reST源的链接将添加到侧栏。

html_sourcelink_suffix
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

附加到源链接的后缀(参见html_show_sourcelink), 除非它们已经有这个后缀。默认是 '.txt' 。

html_use_opensearch
,,,,,,,,,,,,,,,,,,,,,,,,,,,
If nonempty, an OpenSearch description file will be output, and all pages will contain a <link> tag referring to it. 
Since OpenSearch doesn’t support relative URLs for its search page location, 
the value of this option must be the base URL from which these documents are served (without trailing slash), e.g. "https://docs.python.org". The default is ''.

html_file_suffix
,,,,,,,,,,,,,,,,,,,,,

生成的HTML文件后缀，默认为 ".html"

html_link_suffix
,,,,,,,,,,,,,,,,,,,,,

生成HTML文件链接的后缀。默认值为 html_file_suffix 设置值;它可以设置不同(例如, 支持不同的Web服务器设置)。

html_show_copyright
,,,,,,,,,,,,,,,,,,,,,,,,,

在HTML Footer显示 “(C) Copyright …”, 默认True

html_show_sphinx
,,,,,,,,,,,,,,,,,,,,

在HTML Footer显示 “Created using Sphinx” ,"Built with Sphinx"，默认True

html_output_encoding
,,,,,,,,,,,,,,,,,,,,,,,,,

HTML输出文件的编码。默认为 'utf-8' 

html_compact_lists
,,,,,,,,,,,,,,,,,,,,,,,,,

默认为True, 如列表中包含单个段落和/或子列表的所有项目等等…(递归定义)，将不会对其任何项目使用 <p> 元素。
这是标准的docutils行为。

html_secnumber_suffix
,,,,,,,,,,,,,,,,,,,,,,,,,,,,

章节编号的后缀(最后一个，与章节标题相连的部分)，默认是". ", 比如 "2.1.1. 章节标题"，可设置为" "(空格)。

html_search_language
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

全文检索使用的语言，默认为en

支持这些语言:

+ da – 丹麦语
+ nl – 荷兰语
+ en – 英语
+ fi – 芬兰语
+ fr – 法语
+ de – 德语
+ hu – 匈牙利语
+ it – 意大利语
+ ja – 日语
+ no – 挪威语
+ pt – 葡萄牙语
+ ro – 罗马尼亚语
+ ru – 俄语
+ es – 西班牙语
+ sv – 瑞典语
+ tr – 土耳其语
+ zh – 中文

每种语言(日语除外)都提供自己的词干算法。 Sphinx默认使用Python实现。您可以使用C实现来加速构建索引文件。
`PorterStemmer <https://pypi.org/project/PorterStemmer/>`_ (en)，
`PyStemmer <https://pypi.org/project/PyStemmer/>`_ (所有语言)


html_search_options
,,,,,,,,,,,,,,,,,,,,,,,

带有搜索语言支持选项的字典, 默认为空。这些选项的含义取决于所选语言。

英语支持没有选择。

日本的支持有这些选择:

Type: type 是点模块路径字符串, 用于指定应该从哪实现 sphinx.search.ja.BaseSplitter。
如果未指定或指定None, 将使用 'sphinx.search.ja.DefaultSplitter' 。

可以从以下模块中进行选择:

+ ‘sphinx.search.ja.DefaultSplitter’: TinySegmenter algorithm. 这是默认分割器。
+ ‘sphinx.search.ja.MecabSplitter’: MeCab绑定。要使用这个拆分器, 需要 ‘mecab’ python绑定或动态链接库( ‘libmecab.so’ 用于linux, ‘libmecab.dll’ 用于windows)。
+ ‘sphinx.search.ja.JanomeSplitter’: Janome绑定。要使用这个分离器, 需要 Janome 。

1.6 版后已移除: 'mecab', 'janome' and 'default' 已弃用. 为了保持兼容性, 'mecab', 'janome' and 'default' 也可以接受。

其他选项值取决于您选择的拆分器值。

'mecab' 的选项:
+ dic_enc: MeCab算法的编码。
+ dict: 用于MeCab算法的字典。
+ lib: 用于在未安装Python绑定的情况下通过ctypes查找MeCab库的库名。

::

    html_search_options = {
    'type': 'mecab',
    'dic_enc': 'utf-8',
    'dict': '/path/to/mecab.dic',
    'lib': '/path/to/libmecab.so',}
	
'janome' 的选项:

+ user_dic : Janome的用户词典文件路径。
+ user_dic_enc : user_dic选项指定的用户词典文件的编码。默认为 `utf8` 


中文的支持有这些选择:
dict – 如果想使用自定义词典, jieba 字典路径。

html_search_scorer
,,,,,,,,,,,,,,,,,,,,,,,,,

实现搜索结果记分器的JavaScript文件的名称(相对于配置目录)。如果为空, 则使用默认值。

html_scaled_image_link
,,,,,,,,,,,,,,,,,,,,,,,,

默认为True，图像本身会链接到原始图像(如果它没有target选项或缩放相关选项: `scale` , `width` , `height`

html_math_renderer
,,,,,,,,,,,,,,,,,,,,,,,,

HTML输出的math_renderer扩展名。默认为 ``mathjax`` 。

singlehtml_sidebars
,,,,,,,,,,,,,,,,,,,,,

单个HTML页面输出选项，自定义侧边栏模板必须是将文档名称映射到模板名称的字典。它只允许一个名为 "index" 的键。
所有其他键都被忽略。默认情况下，与 html_sidebars 相同。

htmlhelp_basename
,,,,,,,,,,,,,,,,,,,,,

HTML帮助构建器的输出文件基名。默认是 ``pydoc``

htmlhelp_file_suffix
,,,,,,,,,,,,,,,,,,,,,,,,,,,

HTML帮助文档文件名后缀，默认 ``.html``

htmlhelp_link_suffix
,,,,,,,,,,,,,,,,,,,,,,,,,

HTML帮助文档链接后缀，默认 `.html`

EPUB输出配置项
----------------

`EPUB输出配置项 <https://www.sphinx.org.cn/usage/configuration.html#options-for-epub-output>`_

LaTeX输出配置项
-------------------

`LaTeX输出配置项 <https://www.sphinx.org.cn/usage/configuration.html#options-for-latex-output>`_

文本输出选项
------------------

text_newlines
,,,,,,,,,,,,,,,,,,

确定在文本输出中使用哪个行尾字符。

+ 'unix': 使用Unix风格的行结尾(``\n``)
+ 'windows': 使用Windows风格的行结尾(``\r\n``)
+ 'native': 使用构建文档的平台的行结束样式

默认值: 'unix' 。

text_sectionchars
,,,,,,,,,,,,,,,,,,,,,,,

一个7个字符的字符串, 应该用于下划线部分。第一个字符用于第一级标题, 第二个字符用于第二级标题, 依此类推。

默认为 ``*=-~"+```

text_add_secnumbers
,,,,,,,,,,,,,,,,,,,,,,,,,,

一个布尔值, 用于决定文本输出中是否包含节号。默认为 True 。

text_secnumber_suffix
,,,,,,,,,,,,,,,,,,,,,,,,,,,

章节编号的后缀(最后一个，与章节标题相连的部分)，默认是 ". " ,比如 ``2.1.1. 章节标题`` ,可设置为 " "(空格)。


HTML主题
---------------

Sphinx支持通过 themes 更改其HTML输出的外观。

主题是HTML模板, 样式表和其他静态文件的集合。此外, 它还有一个配置文件, 用于指定要继承的主题, 要使用的突出显示样式以及用于自定义主题外观的选项。

也可以自己 `制作主题 <https://www.sphinx.org.cn/theming.html>`_

使用（配置）主题
,,,,,,,,,,,,,,,,,,,,,

使用内置主题
................

设置 ``conf.py`` 中 ``html_theme`` 的值即可

::

   html_theme = 'classic'

修改主题的一些配置选项，修改 ``html_theme_options`` 配置项，
对于使用的主题适用于哪些修改，视具体主题而定。

::

   html_theme_options = {
    "rightsidebar": "true",
    "relbarbgcolor": "black"}

使用自定义主题
......................

自定义主题可以是静态文件形式或Python包。 
对于静态表单, 支持目录(包含 theme.conf 和其他所需文件)或具有相同内容的zip文件。
有配置值 html_theme_path，路径为相对conf.py所在目录的**相对路径** ,

例如, 如果文件中有一个主题 blue.zip, 则可以将其放在包含 conf.py 的目录中并使用此配置

::

   html_theme = "blue"
   html_theme_path = ["."]

python包主题
....................

使用 pip 安装主题包之后，和上一小节一样的流程配置即可。

::

   pip install sphinxjp.themes.dotted

内置主题
,,,,,,,,,,,,,,,,,,

.. figure:: ./_static/buildinthemes/alabaster.png
   :alt: alabaster
   
   alabaster

.. figure:: ./_static/buildinthemes/agogo.png
   :alt: agogo
   
   agogo
   
.. figure:: ./_static/buildinthemes/bizstyle.png
   :alt: bizstyle
   
   bizstyle
   
.. figure:: ./_static/buildinthemes/classic.png
   :alt: classic
   
   classic
   
.. figure:: ./_static/buildinthemes/haiku.png
   :alt: haiku
   
   haiku
   
.. figure:: ./_static/buildinthemes/nature.png
   :alt: nature
   
   nature
   
.. figure:: ./_static/buildinthemes/pyramid.png
   :alt: pyramid
   
   pyramid
   
.. figure:: ./_static/buildinthemes/sphinxdoc.png
   :alt: sphinxdoc
   
   sphinxdoc
   
.. figure:: ./_static/buildinthemes/scrolls.png
   :alt: scrolls
   
   scrolls
   
.. figure:: ./_static/buildinthemes/traditional.png
   :alt: traditional
   
   traditional

basic
...........

基本上没有样式的布局, 用作其他主题的基础, 也可用作自定义主题的基础

+ nosidebar (true or false): 不包括侧边栏. 默认为 False .
+ sidebarwidth (int或str): 侧边栏的宽度(以像素为单位). 这可以是 int, 它被解释为像素或有效的CSS维度字符串, 例如 ‘70em’ 或 ‘50％’. 默认为230像素.
+ body_min_width (int或str):文档正文的最小宽度. 这可以是int, 它被解释为像素或有效的CSS维度字符串, 例如’70em’或’50％’. 如果您不想要宽度限制, 请使用0. 默认值可能取决于主题(通常为450px).
+ body_max_width (int或str):文档正文的最大宽度. 这可以是int, 它被解释为像素或有效的CSS维度字符串, 例如’70em’或’50％’. 如果您不想要宽度限制, 请使用 none . 默认值可能取决于主题(通常为800px).

alabaster
...............

来自@kennethreitz的修改后的 Kr Sphinx主题(Requests项目中使用), 它本身最初基于@mitsuhiko用于Flask及相关项目的主题。
`配置信息 <https://alabaster.readthedocs.io/en/latest/installation.html>`_

classic
................

经典主题

+ rightsidebar (true or false):将侧边栏放在右侧。默认为 False
+ stickysidebar (true or false):使侧边栏固定。默认为False
+ collapsiblesidebar (true or false):添加一个实验性 JavaScript代码段, 通过侧面的按钮使侧边栏可折叠。默认为False
+ externalrefs (true或false):显示外部链接与内部链接不同。默认为 False

还有各种颜色和字体选项可以更改颜色方案, 而无需编写自定义样式表:

+ footerbgcolor (CSS颜色):页脚行的背景颜色.
+ footertextcolor (CSS颜色):页脚行的文本颜色.
+ sidebarbgcolor (CSS颜色):侧边栏的背景颜色.
+ sidebarbtncolor （CSS颜色:侧边栏折叠按钮的背景颜色（当 collapsiblesidebar 为 True 时使用）。
+ sidebartextcolor (CSS颜色):侧边栏的文本颜色.
+ sidebarlinkcolor (CSS颜色):侧边栏的链接颜色.
+ relbarbgcolor (CSS颜色):关系栏的背景颜色.
+ relbartextcolor (CSS颜色): 关系栏的文本颜色.
+ relbarlinkcolor (CSS颜色):关系栏的链接颜色.
+ bgcolor (CSS颜色):身体背景颜色.
+ textcolor (CSS颜色):正文文本颜色.
+ linkcolor (CSS颜色):正文链接颜色.
+ visitedlinkcolor (CSS颜色):访问过的链接的正文颜色.
+ headbgcolor (CSS颜色):标题的背景颜色.
+ headtextcolor (CSS颜色):标题的文本颜色.
+ headlinkcolor (CSS颜色):标题的链接颜色.
+ codebgcolor (CSS颜色):代码块的背景颜色.
+ codetextcolor (CSS颜色): 代码块的默认文本颜色，如果没有通过突出显示样式设置不同.
+ bodyfont (CSS字体系列):普通文本的字体.
+ headfont (CSS字体系列):标题的字体.

sphinxdoc
..........

可配置nosidebar, sidebarwidth

scrolls
........

一个更轻量级的主题, 基于 `Jinja <http://jinja.pocoo.org/>`_ 文档。有以下颜色选项:

+ headerbordercolor
+ subheadlinecolor
+ linkcolor
+ visitedlinkcolor
+ admonitioncolor

agogo
.......

+ bodyfont (CSS字体系列):普通文本的字体.
+ headerfont (CSS字体系列):标题字体.
+ pagewidth (CSS长度):页面内容的宽度, 默认为70em.
+ documentwidth (CSS长度):文档的宽度(没有侧边栏), 默认为50em.
+ sidebarwidth (CSS长度):侧边栏的宽度, 默认为20em.
+ bgcolor (CSS color): 背景颜色.
+ headerbg (“background” 的CSS值):标题区域的背景, 默认为浅灰色渐变.
+ footerbg (“background” 的CSS值):页脚区域的背景, 默认为浅灰色渐变.
+ linkcolor (CSS颜色):正文链接颜色.
+ headercolor1, headercolor2 (CSS颜色):<h1>和<h2>标题的颜色.
+ headerlinkcolor (CSS颜色):标题中后向引用链接的颜色.
+ textalign (CSS text-align 值):正文的文本对齐方式, 默认为 justify.

nature
........

一个绿色的主题。可配置nosidebar, sidebarwidth

pyramid
........

由Blaise Laflamme设计的金字塔网络框架项目的主题。

可配置nosidebar, sidebarwidth

haiku
.......

没有侧栏的主题

+ full_logo (true 或 false, 默认为 False):如果True, 标题只会显示 html_logo. 用于大型徽标。 如果为False, 则徽标(如果存在)将浮动右侧显示, 文档标题将放在标题中.
+ textcolor, headingcolor, linkcolor, visitedlinkcolor, hoverlinkcolor (CSS颜色):各种身体元素的颜色.

traditional
............

一个类似于旧Python文档的主题。可配置nosidebar, sidebarwidth

epub
.....

epub构建器的主题。 这个主题试图保留视觉空间, 这是电子书阅读器上的稀疏资源。

+ relbar1 (true 或 false, 默认为 True): 如果为true, 则将 relbar1 块插入epub输出中
+ footer (true 或 false, 默认为 True):如果为true, 则在脚本输出中插入 footer 块

bizstyle
.........
一个简单的蓝色主题。 可配置nosidebar, sidebarwidth, rightsidebar

   
第三方主题
,,,,,,,,,,,,,,,,,,,   

有许多第三方主题可用。其中一些是一般用途, 而另一些则是针对单个项目的。

可在 `PyPI <https://pypi.org/search/?q=&o=&c=Framework+%3A%3A+Sphinx+%3A%3A+Theme>`_ , 
`GitHub <https://github.com/search?utf8=%E2%9C%93&q=sphinx+theme&type=>`_ 
和 `sphinx-themes.org <https://sphinx-themes.org/>`_ 上可以找到更多第三方主题。

sphinx_rtd_theme
.........................

`Read the Docs Sphinx Theme <https://pypi.org/project/sphinx_rtd_theme/>`_. 

这是一个针对readthedocs.org制作的适合移动设备的sphinx主题. 


Markdown支持
-----------------

为了支持基于Markdown的文档，Sphinx使用 `recommonmark <https://recommonmark.readthedocs.io/en/latest/index.html>`_ 。

recommonmark是一个Docutils桥接器，是用于解析 `CommonMark <https://commonmark.org/>`_ Markdown风格的Python包。

1. 安装Markdown解析器 recommonmark

::

	pip install --upgrade recommonmark

2. 将 recommonmark 添加到扩展名列表

::

    extensions = ['recommonmark']
	
3. 调整source_suffix变量。

下面的示例配置Sphinx将所有扩展名为 .md 和 .txt 的文件解析为 Markdown

::

	source_suffix = {
    '.rst': 'restructuredtext',
    '.txt': 'markdown',
    '.md': 'markdown',}

4. 进一步配置 recommonmark 以允许标准 CommonMark 不支持的自定义语法

详阅 `recommonmark documentation <https://recommonmark.readthedocs.io/en/latest/auto_structify.html>`_
	
HTML模板
---------

sphinx扩展ext
--------------

内置扩展
,,,,,,,,,

外部扩展
,,,,,,,,,

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