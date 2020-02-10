reStructureText语法
====================

内联标记 Inline Markup
-------------------------

==========================  =========================   ===========================
语法                                      效果                    说明  
==========================  =========================   ===========================
``*emphasis*``                   *emphasis*                  强调，斜体
``**strong**``                    **strong**                   加粗
**interpreted text**          **interpreted text**           用于解释的文本
``inline literal``            ``inline literal``            行内文本
reference_               	reference	                   链接：纯文本
`phrase reference`_	        phrase reference                链接：文字间有空格标点
anonymous__	                 anonymous	                        链接
``_`inline_link``               inline_link	              交叉引用链接
|substitution reference|     |substitution reference|       指示链接(图片，链接等)
footnote reference [1]_	     footnote reference [1]_	     脚注 
citation [CIT2002]_	         citation [CIT2002]       	         引用
http://docutils.sf.net/      http://docutils.sf.net/        独立链接
==========================  =========================   ===========================


反斜杠转义 Escaping with Backslashes
----------------------------------------

使用反斜杠来转义任意rst语法符号为符号本身，包括反斜杠自己

+ 转义内联标记：  ``\*去除斜体*``
+ 转义反斜杠（用两个反斜杠）：  ``\\``

在python中，最简单的方式是在字符串外表示raw strings(加r)
==============================  ==============================
py字符串                              显示结果
==============================  ==============================
r"""\*去除斜体*  "\\""""          r"""\*去除斜体*  "\\""""
 """\\*去除斜体*  "\\\\\\""""     """\*去除斜体*  "\\""""
 """\*去除斜体*  "\\""""          """\*去除斜体*  "\\""""
==============================  ==============================

章节标记 Section Structure
-----------------------------

任意可打印的7个bit的ASCII码字符都可以作为章节标识符，它们是

``! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~``

不过有些可能会看起来比较奇怪，因此推荐使用其中的

``= - ` : . ' " ~ ^ _ * + #``

+ 在reStructureText中未明确各个章节标识符层级的顺序，**它按照标识符在书写文本中的顺序来指定标识符指示的标题层级**。
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
无序列表 Bullet Lists
-------------------------
有序列表 Enumerated Lists
---------------------------
定义列表Definition Lists
--------------------------
Field Lists
--------------------
参数列表Option Lists
---------------------
文字块 Literal Blocks
--------------------------
行块 Line Blocks
---------------------
块引用 Block Quotes
---------------------------
文档测试块 Doctest Blocks
-------------------------------

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









Transitions

脚注 Footnotes
------------------------
引用Citations
------------------------------

超链接Hyperlink Targets
-----------------------------
External Hyperlink Targets
Internal Hyperlink Targets
Indirect Hyperlink Targets
Implicit Hyperlink Targets

扩展指令 Directives
---------------------------
Directives are a general-purpose extension mechanism, a way of adding support for new constructs without adding new syntax. For a description of all standard directives, see reStructuredText Directives.
https://docutils.sourceforge.io/docs/ref/rst/directives.html

Substitution References and Definitions
------------------------------------------
Comments
-----------------
非上述语法，则都作为Comments处理。