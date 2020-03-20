reStructureText语法
====================

内联标记 Inline Markup
-------------------------

==========================  =========================   ===========================
语法                        效果                        说明  
==========================  =========================   ===========================
``*emphasis*``              *emphasis*                  强调，斜体
``**strong**``              **strong**                  加粗
\`interpreted-text\`        `interpreted-text`          使用两个反逗号包裹内容，表征对其解释
\`\`inline literal\`\`      ``inline literal``          当包括内容包含空格时使用两个反逗号来包裹
``ref_  .. _ref: 链接``     ref_   	                    链接：纯文本，外部链接
\`phrase ref\`\_	        `带空格 外链`__             链接：文字间有空格标点，外部链接
``anonymous__``             anonymous                   链接: 匿名链接
``_`inline_link``           inline_link	                交叉引用链接
``|substitution ref|``      ``|substitution ref|``      指示链接(图片，链接等)
``footnote [1]_``	        footnote [1]_               脚注（包括参考文献）
``citation [CIT2002]_``	    ``citation [CIT2002]``      引用
http://docutils.sf.net/     http://docutils.sf.net/     独立链接
==========================  =========================   ===========================

..  _ref: https://docutils.sourceforge.io/docs/user/rst/quickref.html#hyperlink-targets
__  带别名的超链接_

.. [1] 脚注1


反斜杠转义 Escaping with Backslashes
----------------------------------------

使用反斜杠来转义任意rst语法符号为符号本身，包括反斜杠自己

+ 转义内联标记：  ``\*去除斜体*``
+ 转义反斜杠（用两个反斜杠）：  ``\\``

在python中，最简单的方式是在字符串外表示raw strings(加r)

==============================  ==============================
py字符串                        显示结果
==============================  ==============================
r"""\*去除斜体*  "\\""""        r"""\*去除斜体*  "\\""""
"""\\*去除斜体*  "\\\\\\""""    """\*去除斜体*  "\\""""
"""\*去除斜体*  "\\""""         """\*去除斜体*  "\\""""
==============================  ==============================


章节标记 Section Structure
-----------------------------

任意可打印的7个bit的ASCII码字符都可以作为章节标识符，它们是

``! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~``

不过有些可能会看起来比较奇怪，因此推荐使用其中的

``= - ` : . ' " ~ ^ _ * + #``

+ 在reStructureText中未明确各个章节标识符层级的顺序，**它按照标识符在书写文本中的顺序来指定标识符指示的标题层级** 。
+ 在标题上下，使用两行标识符；和只在标题下使用一行标识符。效果是一样的。
+ 标题标识符的数量至少要和标题文本等长
+ 建议定义如下标题标识符层级（从高到低）为  ``= - , . *``

可以使用如下标准定义各级标题
::

  一级标题
  ==========
  二级标题
  ----------
  三级标题
  ,,,,,,,,,
  四级标题
  ............
  五级标题
  *************


段落 Paragraphs
-----------------

段落一般隶属于某个章节中，是一块左对齐并且没有其他元素体标记的块。
在.rst文件中，段落和其他内容的分割是靠 **空行** 来完成

    如果段落相较于其他的段落有 **缩进**（这段缩进了4个空格），reStructuredText会解析为 **引用段落** ，样式上有些不同。


无序列表 Bullet Lists
-------------------------

reStructuredText中 `无序列表 <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#bullet-lists>`_ 的语法和Markdown中的是一样的。
一般使用 ``"+ ","- ","* "`` 来作为无序列表的指示符，利用缩进来指示列表之间的嵌套关系。

 + 列表的起始项和终止项前后是需要空行的
 + 同层级之间的列表项之间空行可加可不加，不同层级之间的列表项必须加空行
 + 层级中内容有多段，则第二段（后续段落内容）无需指示列表标识符，只需保持同样缩进（即左对齐）。
 + 指示标识符可以混用，但是不推荐，推荐同样层级使用同样符号，一般层级顺序就按照 ``"+ ","- ","* "``

**示例如下:**

::

  + 一级列表第一项
  + 一级列表第二项
  
    - 二级列表，换层级加空行
    
      二级列表的第二段内容，加空行，缩进对齐
    
    + 依然是二级列表，指示标识符可以混用，但不推荐
    
      * 第三级

**效果如下:**


+ 一级列表第一项
+ 一级列表第二项

  - 二级列表，换层级加空行
  
    二级列表的第二段内容，加空行，缩进对齐
  
  + 依然是二级列表，指示标识符可以混用，但不推荐
  
    * 第三级


有序列表 Enumerated Lists
---------------------------

`枚举列表 <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#enumerated-lists>`_ 即顺序列表(ordered-list)，可以使用不同的枚举序号来表示列表。

**枚举指示符有：**

+ 阿拉伯数字: 1, 2, 3, ... (无上限)。
+ 大写字母: A-Z。
+ 小写字母: a-z。
+ 大写罗马数字: I, II, III, IV, ..., MMMMCMXCIX (4999)。
+ 小写罗马数字: i, ii, iii, iv, ..., mmmmcmxcix (4999)。

并且可以使用 "#" 来自动自增。

**支持添加的前缀和后缀：**

+ . 后缀: "1.", "A.", "a.", "I.", "i."。
+ () 包起来: "(1)", "(A)", "(a)", "(I)", "(i)"。
+ ) 后缀: "1)", "A)", "a)", "I)", "i)"。

当正常的文本中包含可被识别为列表的内容时（ ``A. 1. (b) I`` 等），为了避免被识别，可以采取如下措施：

1. 将一行内容，折断为多行书写，这样会被识别为 **段落** 内容，而不会解析为列表；
2. 使用反斜杠 "\\" 在段首进行转义。

**示例如下:**

::

  A. Einstein was a really
  smart dude. （跨行避免）

  A. Einstein was a really smart dude.（未避免）

  \A. Einstein was a really smart dude.（使用\转义）


**效果如下:**

A. Einstein was a really
smart dude.

A. Einstein was a really smart dude.

\A. Einstein was a really smart dude.



有序列表也支持嵌套，规则和无序列表一致

::

  1. Item 1 initial text.
  
     a) Item 1a.
     b) Item 1b.
  
  #. a) Item 2a.使用#号自增
     b) Item 2b.

**效果如下:**

1. Item 1 initial text.

   a) Item 1a.
   b) Item 1b.

#. a) Item 2a.使用#号自增
   b) Item 2b.


定义列表Definition Lists
--------------------------

`定义列表 <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#definition-lists>`_ 可以理解为解释列表，即名词解释(definition_list, classifier, definition)。

条目占一行，解释文本要有缩进；多层可根据缩进实现。

各个条目由三部分组成，条目名称(term)，条目属性(classifier)，条目定义(definition)， 条目名称和条目属性在同一行，使用空格、冒号、空格（" : "）连接，其中条目属性可以为空，也可以有多个
条目定义需要换行缩进。

**示例如下:**

::
 
  term 1
    Definition 1.

  term 2
      Definition 2, paragraph 1.
  
      Definition 2, paragraph 2.
  
  term 3 : classifier
      Definition 3.
  
  term 4 : classifier one : classifier two
      Definition 4.

**效果如下:**

term 1
    Definition 1.

term 2
    Definition 2, paragraph 1.

    Definition 2, paragraph 2.

term 3 : classifier
    Definition 3.

term 4 : classifier one : classifier two
    Definition 4.


字段列表 Field Lists
--------------------

`字段列表 <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#field-lists>`_ 用于指令解释，或者数据库字段（记录）解释的场景。

它在形式上有点像两列的表格，因此在 field body中的功能是和在表格中一样的（即支持嵌套，跨行等等）。

**示例如下：**

::

  :Date: 2020-02-02
  :Version: 1
  :Authors: - fire
            - firewang
            - firewang
  :Indentation: Since the field marker may be quite long, the second
     and subsequent lines of the field body do not have to line up with first line.
     解释可能很长，第二行不用和第一行对齐，但是后续行必须和第二行对齐。
  :Parameter i: field name可以是phrase，即可以带空格，但是不能带":"


**效果如下：**

:Date: 2020-02-02
:Version: 1
:Authors: - fire
          - firewang
          - firewang
:Indentation: Since the field marker may be quite long, the second
   and subsequent lines of the field body do not have to line up with first line.
   解释可能很长，第二行不用和第一行对齐，但是后续行必须和第二行对齐。
:Parameter i: field name可以是phrase，即可以带空格，但是不能带":"


参数(选项)列表 Option Lists
-----------------------------------

选项列表是一个左列为参数，右列为参数说明的两列列表（无表头），用于command-line参数解释。

支持三种参数书写形式:

+ 由一个短横（Short dash）连接的 POSIX 式。
+ 由两个短横（Short dash）连接的 长POSIX 式。
+ DOS/VMS参数形式，即由 `/` 起始的参数形式。

**示例如下：**

::

  -a            command-line option "a"
  -b file       options can have arguments
                and long descriptions
  --long        options can be long also
  --input=file  long options can also have
                arguments
  /V            DOS/VMS-style options too

**效果如下：**

-a            command-line option "a"
-b file       options can have arguments
              and long descriptions
--long        options can be long also
--input=file  long options can also have
              arguments
/V            DOS/VMS-style options too


文字块 Literal Blocks
--------------------------

`文字块 <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#literal-blocks>`_ 就是一段文字信息，指示符为连续两个冒号 ``::`` ，支持文字块的嵌套。

文字块支持三种形式的语法(完全等价)

1. 起始新行，后接空行，块内容需缩进

**示例如下：**

::

  ::
  
    缩进后填写块内容

**效果如下：**

::

  缩进后填写块内容
  
2. 部分简化，前文带一个冒号，加一个空格后，双冒号接在前文后面，不另起行，同时会显示单个冒号，块内容同样缩进

**示例如下：**


::

  这里是前面内容，下面引用: ::
  
    缩进后填写块内容

**效果如下：**

这里是前面内容，下面引用: ::
  
  缩进后填写块内容


3. 完全简化，双冒号接在前文后面，不另起行，同时会显示单个冒号，块内容同样缩进

**示例如下：**


::

  这里是前面内容，下面引用::
  
  > 在（部分/完全）简化形势下支持单行引用形式的嵌套
  > 再来一个单行引用

**效果如下：**

这里是前面内容，下面引用::
  
> 在简化形势下支持单行引用形式的嵌套
> 再来一个单行引用


行块 Line Blocks
---------------------

::

  | 行块使用 | 指示符，
  | 一般用于描述地址，歌
    词，诗歌，简单列表等。

**效果如下：**

| 行块使用 "\|" 指示符，
| 一般用于描述地址，歌词，诗歌，简单列表等。


块引用 Block Quotes
---------------------------

块引用是 **通过缩进来实现** 的，引用块要在前面的段落基础上缩进。

通常引用结尾会加上出处(attribution)，出处的文字块开头是两个或者三个连续短横（"--","---"）后面加上出处信息。

块引用可以使用空的注释 .. 分隔上下的块引用。

注意在新的块和出处都要添加一个空行。

**示例如下：**

::

  实际效果：
   
      “真的猛士，敢于直面惨淡的人生，敢于正视淋漓的鲜血。”
   
      --- 鲁迅
   
  ..
   
      “人生的意志和劳动将创造奇迹般的奇迹。”
   
      -- 涅克拉索
  

实际效果：
 
    “真的猛士，敢于直面惨淡的人生，敢于正视淋漓的鲜血。”
 
    --- 鲁迅
 
..
 
    “人生的意志和劳动将创造奇迹般的奇迹。”
 
    -- 涅克拉索


文档测试块 Doctest Blocks
-------------------------------

文档测试块是交互式的Python会话，以 ``>>>`` 开始，一个空行结束，是一种特殊的文字块，**内容不需要缩进** 。

可直接复制到python的 docstrings中，用于为doctest模块提供测试环境。

当文字块语法和文档测试块语法同时出现时，文字块语法优先级更高。

>>> print('this is a Doctest block')
this is a Doctest block


表格 Tables
--------------------
reStructureText提供两种表格：网格表格（Grid Tables）， 简单表格（Simple Tables）。

表格前后都需要空行


网格表格
,,,,,,,,,,
+ "-" 分隔行(短破折号，减号)
+ "=" 分隔表头和表体行
+ "|" 分隔列
+ "+" 表示行和列相交的节点

**网格表格注意点**：

+ 网格表格编辑复杂，可以使用Emacs来编辑生成
+ 行和列都支持并格
+ 如果文本内包含"|" ，并且恰好与表格内分隔对齐了，那么会产生错误。解决方案_ : 方式一是加空格避免对齐，方式二是为该行增加一行
+ 可以不包含表头。
+ 列需要和"="左对齐，不然可能会导致出错
+ 如果碰到第一列为空，需要使用 "\\" 来转义, 不然会被视为是上一行的延续。

.. _解决方案: https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#tables


**示例：**

::

    +------------------------+------------+----------+----------+
    | Header row, column 1   | Header 2   | Header 3 | Header 4 |
    | (header rows optional) |            |          |          |
    +========================+============+==========+==========+
    | body row 1, column 1   | column 2   | column 3 | column 4 |
    +------------------------+------------+----------+----------+
    | body row 2             | Cells may span columns.          |
    +------------------------+------------+---------------------+
    | body row 3             | Cells may  | - Table cells       |
    +------------------------+ span rows. | - contain           |
    | body row 4             |            | - body elements.    |
    +------------------------+------------+---------------------+

**结果：**

+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
| (header rows optional) |            |          |          |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | Cells may span columns.          |
+------------------------+------------+---------------------+
| body row 3             | Cells may  | - Table cells       |
+------------------------+ span rows. | - contain           |
| body row 4             |            | - body elements.    |
+------------------------+------------+---------------------+


简单表格
,,,,,,,,,,,

简单表格使用 "=" 和 "_" 来进行绘制，其中"=" 放置于表格的最外两行（首行和末行）,如果有表头，则表头也用该符号进行分隔，"_"用于跨列合并（column span）。

简单表格需要各列首字母与该列指示的"="对齐(表头可不对齐，为了保持统一，尽量保持左对齐)，每列的"="需要覆盖该列字符的长度


包含表头的简单表格
......................

**语法如下：**

:: 
  
  =====  =====  =======
  A      B      A and B
  =====  =====  =======
  False  False  False
  True   False  False
  False  True   False
  True   True   True
  =====  =====  =======

**效果如下：**

=====  =====  =======
  A      B    A and B
=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======

无表头的简单表格
.....................

**语法如下：**

:: 
  
  =====  =====  =======
  False  False  False
  True   False  False
  False  True   False
  True   True   True
  =====  =====  =======

**效果如下：**

=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======

跨列合并
..............

"_"用于跨列合并，**仅支持在表头使用**，"_"长度需要从起始列的第一个指示符"="到终止列的最后一个指示符"="

**语法如下：**

::
  
  =====  =====  ======
  合并两列      单独列
  ------------  ------
    A      B    A or B
  =====  =====  ======
  False  False  False
  True   False  True
  False  True   True
  True   True   True
  =====  =====  ======


**效果如下:**

=====  =====  ======
合并两列      单独列
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======


单个表格中可以多行
.....................

+ 简单表格的单个格子中可以包含多行的内容（比如列表），但是不支持行合并；
+ 增加空行可以进行换行，否则会自动将文本连接在一起。
+ 首列不能为空，为空时使用 \\ 进行占位。

**语法如下：**

::

  =====  ===================================
  col 1  col 2
  =====  ===================================
  1      Second column of row 1.
  2      Second column of row 2.
         Second line of paragraph.
  3      - Second column of row 3.
  
         - Second item in bullet
           list (row 3, column 2).
  \      Row 4; column 1 will be empty.
  =====  ===================================

**效果如下：**

=====  ===================================
col 1  col 2
=====  ===================================
1      Second column of row 1.
2      Second column of row 2.
       Second line of paragraph.
3      - Second column of row 3.

       - Second item in bullet
         list (row 3, column 2).
\      Row 4; column 1 will be empty.
=====  ===================================



Transitions
------------------

转换分隔用于段与段之间的分隔，相当于html中的<hr>，就是跨屏的一个横线。

使用4个及以上的标点符号(推荐使用短横 "-")就可以生成，同样需要前后空行，另外，**不能连续出现** ，不能在文档结尾使用。

**示例如下:**

::

  前后需要空行

  ,,,,,,,,
  
  使用标点符号
  
  .............
  
  不能连续出现
  
  ---------------

  不能在结尾使用


**效果如下：**

前后需要空行

,,,,,,,,

使用标点符号

.............

不能连续出现

---------------

不能在结尾使用


脚注 Footnotes
------------------------

`脚注 <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#footnotes>`_ 有三种形式，
手工序号(标记序号123之类)、自动序号(填入 \# 号会自动填充序号)、自动符号(填入 \* 会自动生成符号) 

手工序号可以和 \# 结合使用，会自动延续手工的序号。

#表示的方法可以在后面加上一个名称，这个名称就会生成一个链接。

1. 手工标序(标记序号123之类)

**示例如下:**

::

  Footnote references, like [5]_.
  Note that footnotes may get [3]_
  rearranged, e.g., to the bottom of
  the "page".
  
  .. [5] A numerical footnote. Note
     there's no colon after the ].
  .. [3] 脚注3

**效果如下：**

Footnote references, like [5]_.
Note that footnotes may get [3]_
rearranged, e.g., to the bottom of
the "page".

.. [5] A numerical footnote. Note
   there's no colon after the ``]``.
.. [3] 脚注3

2. 自动序号(填入 \# 号会自动填充序号)

**示例如下:**

::

  自动排序脚注, like using [#]_ and [#]_.
  .. [#] This is the first one.
  .. [#] This is the second one.

**效果如下：**

自动排序脚注, like using [#]_ and [#]_.

.. [#] This is the first one.
.. [#] This is the second one.

可以添加别名，即可同时实现自动排序，又带有自定义名称，**这个功能相当于实现了文献引用功能** ；

**示例如下:**

::

  They may be assigned 'autonumber
  labels' - for instance,
  [#fourth]_ and [#third]_.
  
  .. [#third] a.k.a. third_
  
  .. [#fourth] a.k.a. fourth_

**效果如下：**

They may be assigned 'autonumber
labels' - for instance,
[#fourth]_ and [#third]_.

.. [#third] a.k.a. third_
.. [#fourth] a.k.a. fourth_


3. 自动符号(填入 \* 会自动生成符号)。

自动填符号功能上和自动填序号是一样的，只是换了一种辨识符号。

**示例如下:**

::

  自动脚注符号, like this: [*]_ ,[*]_ , [*]_ and [*]_.
  
  .. [*] This is the first one.
  .. [*] This is the second one.
  .. [*] This is the third one.
  .. [*] This is the fourth one.

**效果如下：**

自动脚注符号, like this: [*]_ ,[*]_ , [*]_ and [*]_.

.. [*] This is the first one.
.. [*] This is the second one.
.. [*] This is the third one.
.. [*] This is the fourth one.


引用Citations
------------------------------

引用和脚注是一样的，只不过引用只能用文本而不能用数字。

**示例如下:**

::

  引用参考的内容通常放在页面结尾处，比如 [One]_，Two_
 
  .. [One] 参考引用一
  .. [Two] 参考引用二

**效果如下：**

引用参考的内容通常放在页面结尾处，比如 [One]_，[Two]_
 
.. [One] 参考引用一
.. [Two] 参考引用二


超链接Hyperlink Targets
-----------------------------

`超链接Hyperlink <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#hyperlink-targets>`_ 有三种：

.. _带别名的超链接:


+ 带别名的超链接 ，语法为 ``.. _hyperlink-name: link-address`` ；由 ``..``，空格，短下划线"_"，别名，冒号，空格和链接地址构成。
  在原文引用处书写语法为 ``hyperlink-name_`` （特别注意原文中"_"在别名后，而在指示链接出，"_"在别名前）。
+ 匿名anonymous的超链接，即不带别名的超链接，语法为 ``.. __: link-address`` ； 由 ``..``，空格，两个短下划线"__"，冒号，空格和链接地址构成。
+ 匿名的超链接，另一种语法形式，语法为 ``__ link-address``  。

外部链接 External Hyperlink Targets
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

外部链接有两种方式，需要引用的话，使用上述带别名的超链接的语法形式，即

**示例如下:**

::

  这是我的 reStructureText_ 实践笔记。
  
  .. _reStructureText: https://sphinx-practise.readthedocs.io/zh_CN/latest/index.html


**效果如下：**

这是我的 reStructureText_ 实践笔记。
  
.. _reStructureText: https://sphinx-practise.readthedocs.io/zh_CN/latest/index.html

另一种是直接在名称后附加地址, 语法为 \`别名 <链接>\`_

**示例如下:**

::

  这是我的 `reStructureText <https://sphinx-practise.readthedocs.io/zh_CN/latest/index.html>`_ 实践笔记。

**效果如下：**

这是我的 `reStructureText <https://sphinx-practise.readthedocs.io/zh_CN/latest/index.html>`_ 实践笔记。

锚点链接 Internal Hyperlink Targets
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

内部超链接，即锚点。


锚点的语法即外部超链接中 带别名的超链接_ 去除外部链接，其他语法一致。


间接链接 Indirect Hyperlink Targets
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

间接超链接是基于匿名链接的基础上的，就是将匿名链接地址换成了外部引用名。

**示例如下:**
::

  Python_ is `my favourite
  programming language`__.
  
  .. _Python: http://www.python.org/
  
  __ Python_

**效果如下：**

Python_ is `my favourite
programming language`__.

.. _Python: http://www.python.org/

__ Python_

其中 python\_ 就是一个正常的外部链接，而后面那句话是一个匿名链接，
对这个匿名链接使用间接链接方式链接到 Python这个外部链接的链接地址上去。


Implicit Hyperlink Targets
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
隐式超链接

小节标题、脚注和引用参考会自动生成超链接地址，使用小节标题、脚注或引用参考名称作为超链接名称就可以生成隐式链接。

本质上它们的写法都是和 `外部链接 External Hyperlink Targets`_ 相一致的, 只是做了一些微小改动，以做出区别。

例如链接到 `超链接Hyperlink Targets`_ 这个章节目录去
::

  `超链接Hyperlink Targets`_


扩展指令 Directives
--------------------

指令（Directives）是reStructureText的扩展机制。
可以在不增加新语法的情况下，增加新的结构性支持(a way of adding support for new constructs)。

指令由三部分组成

::

	.. directive-type:: directive-block

其中指令类型（directive-type）指明指令的类型，指令内容体又由三部分组成

+ 指令作用对象Directive arguments：指明该指令针对哪个对象作用
+ 指令选项参数Directive options：该指令的可选参数（可选），是一个参数列表
+ 指令内容说明Directive content：说明文档（可选）

比如插入一个图片

::

	.. figure:: 图片名.png  # 这里是指令作用对象
	   :scale: 50     # 这里是指令参数
 	   :width: 100

	   这是一个图片   # 这里是说明

已在 `reference reStructuredText parser <https://docutils.sourceforge.io/docs/ref/rst/directives.html>`_ 中实现的指令。

警告信息Admonitions
,,,,,,,,,,,,,,,,,,,,

特定的警告信息
...............

格式为

::

   .. admonition:: admonition-title(可空)
      :class: class-name(可选)
	  :name: name(可选)
      admonition-content说明信息

admonition-title和admonition-content显示效果是一体的，
但是admonition-title(可空)会在html中单独存在一个title标签中。
	  
支持如下特定警告信息

+ attention
+ caution
+ danger
+ error
+ hint
+ important
+ note
+ tip
+ warning

**示例如下：**

::

   .. attention:: This is a attention admonition.
      second attention paragraph.
      
   .. caution:: This is a caution admonition.
      second caution paragraph.
   
   .. danger:: This is a danger admonition.
      second danger paragraph.
   
   .. error:: This is a error admonition.
      second error paragraph.
   
   .. hint:: This is a hint admonition.
      second hint paragraph.
   
   .. important:: This is a important admonition.
      second important paragraph.   
      
   .. note:: This is a note admonition.
      This is the second line of the first paragraph.
   
      - The note contains all indented body elements
        following.
      - It includes this bullet list.
   
   .. tip:: This is a tip admonition.
      second tip paragraph.
   
   .. warning:: This is a warning admonition.
      second warning paragraph.
   


**效果如下：**

.. attention:: This is a attention admonition.
   second attention paragraph.

.. caution:: This is a caution admonition.
   second caution paragraph.

.. danger:: This is a danger admonition.
   second danger paragraph.

.. error:: This is a error admonition.
   second error paragraph.

.. hint:: This is a hint admonition.
   second hint paragraph.

.. important:: This is a important admonition.
   second important paragraph.   
   
.. note:: This is a note admonition.
   This is the second line of the first paragraph.

   - The note contains all indented body elements
     following.
   - It includes this bullet list.

.. tip:: This is a tip admonition.
   second tip paragraph.

.. warning:: This is a warning admonition.
   second warning paragraph.

通用警告信息Generic Admonition
...............................

通用警告信息即不指定为特定的警告类别，使用admonition指代警告。
与特定警告不同的是，特定警告的admonition-title在通用警告中为admonition-name，
这是我们自定义的警告名，用于和特定警告（danger,hint,important等）提供同等标识。

**示例如下：**

::

   .. admonition:: And, by the way...
   
      You can make up your own admonition too.

**结果如下：**
	  
.. admonition:: And, by the way...

   You can make up your own admonition too.

   
图片Images
,,,,,,,,,,,

使用image

::

   .. image:: picture.jpeg
      :class: class-name
	  :name: name 
      :height: 100 px(长度)
      :width: 200 px (长度或者百分比)
      :scale: 50 % (百分比，百分号可省略)
      :alt: alternate text
      :align: right
	  :target: https://www.baidu.com

align可选top,middle,bottom,left,center,right

target使得图片可点击跳转。

scale表示等比例伸缩（放大或者缩小）

.. important:: scale需要和width或者height（或者2者）一起使用。

使用figure

::

   .. figure:: picture.png
      :figwidth: 200 px (长度或者百分比)
      :scale: 50 %
	  :align: center
	  :figclass: figure-class
      :alt: map to buried treasure
   
       +---------------------------+
       |        figure             |
       |                           |
       |<------ figwidth --------->|
       |                           |
       |  +---------------------+  |
       |  |     image           |  |
       |  |                     |  |
       |  |<--- width --------->|  |
       |  +---------------------+  |
       |                           |
       |The figure's caption should|
       |wrap at this width.        |
       +---------------------------+

figure相当于一个画布（类似于html中的一个div或者一个canvas），
它对处于其内的内容进行样式统一管理。相比image可以包含除图片外的更多内容。

figure支持image的所有指令选项参数，除了align在figure中指示整个画布的对齐方式。
且它只能选择为left,center,right。

.. important:: 和image一致，要使得scale（这里是对整个画布作用）起作用需要和figwidth一起使用  

页面元素Body Elements
,,,,,,,,,,,,,,,,,,,,,,

表格Tables
,,,,,,,,,,,

文档Documents
,,,,,,,,,,,,,,

References
,,,,,,,,,,,,

HTML-Specific
,,,,,,,,,,,,,,

Substitution Definitions
,,,,,,,,,,,,,,,,,,,,,,,,,,

其他
,,,,,,


通用指令选项参数
,,,,,,,,,,,,,,,,,

============ =====================================
\:class\:    得到
\:name\:     为指令设置名称(可用于简化别名链接)
============ =====================================

::
  
   .. image:: build.png
      :name: my pic
   与下列方式等价
   .. _my pic
   
   .. image:: build.png
   


Substitution References and Definitions
----------------------------------------

Comments
---------
非上述语法，则都作为Comments处理。