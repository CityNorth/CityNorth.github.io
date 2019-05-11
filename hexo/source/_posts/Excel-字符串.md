---
title: EXCEL-字符串
date: 2019-04-30 12:32:45
tags: "Excel"
cover: 
categories: "Excel"
summary: EXCEL-字符串
---
## EXCEL-字符串

# 字符串

### Text

> 用途：将数值转换为按指定数字格式表示的文本。

* 语法：Text(Value，Format_Text)

* 参数：Value是数值、计算结果是数值的公式、或对数值单元格的引用；Format_Text是所要选用的文本型数字格式，即“单元格格式”对话框“数字”选项卡的“分类”列表框中显示的格式，它不能包含星号“*”。
注意：使用“单元格格式”对话框的“数字”选项卡设置单元格格式，只会改变单元格的格式而不会影响其中的数值。使用函数Text可以将数值转换为带格式的文本，而其结果将不再作为数字参与计算。

### Search或Searchb

> 用途：返回从start_Num开始首次找到特定字符或文本串的位置编号。其中search以字符数为单位，Searchb以字节数为单位。

* 语法：Search(Find_Text，Within_Text，Start_Num)，Searchb(Find_Text，Within_Text，Start_Num)

* 参数：Find_Text是要查找的文本，可以使用通配符，包括问号“?”和星号“*”。其中问号可匹配任意的单个字符，星号可匹配任意的连续字符。如果要查找实际的问号或星号，应当在该字符前键入波浪线“~”。Within_Text是要在其中查找Find_Text的文本。Start_Num是Within_Text中开始查找的字符的编号。如果忽略Start_Num，则假定其为1。

### Find

> 用途：Find用于查找其他文本串(Within_Text)内的文本串(Find_Text)，并从within_Text的首字符开始返回find_Text的起始位置编号。此函数适用于双字节字符，它区分大小写但不允许使用通配符。

* 语法：Find(Find_Text，Within_Text，Start_Num)

* 参数：Find_Text是待查找的目标文本；Within_Text是包含待查找文本的源文本；Start_Num指定从其开始进行查找的字符，即within_Text中编号为1的字符。如果忽略start_Num，则假设其为1。

### Concatenate

> 用途：将若干文字串合并到一个文字串中，其功能与"&"运算符相同。

* 语法：Concatenate(Text1，Text2，...)

* 参数：Text1，Text2，...为1到30个将要合并成单个文本的文本项，这些文本项可以是文字串、数字或对单个单元格的引用。

### Left或Leftb

> 用途：根据指定的字符数返回文本串中的第一个或前几个字符。此函数用于双字节字符。

* 语法：Left(Text，Num_Chars)或leftb(Text，Num_Bytes)

* 参数：Text是包含要提取字符的文本串；Num_Chars指定函数要提取的字符数，它必须大于或等于0。Num_Bytes按字节数指定由leftb提取的字符数。

### Right或Rightb

> 用途：Right根据所指定的字符数返回文本串中最后一个或多个字符。Rightb根据所指定的字节数返回文本串中最后一个或多个字符。

* 语法：Right(Text，Num_Chars)，Rightb(Text，Num_Bytes)

* 参数：Text是包含要提取字符的文本串；Num_Chars指定希望right提取的字符数，它必须大于或等于0。如果num_Chars大于文本长度，则right返回所有文本。如果忽略num_Chars，则假定其为1。Num_Bytes指定欲提取字符的字节数。

### Len或Lenb

> 用途：Len返回文本串的字符数。Lenb返回文本串中所有字符的字节数。

* 语法：Len(Text)或Lenb(Text)

* 参数：Text待要查找其长度的文本。

* **注意：** 此函数用于双字节字符，且空格也将作为字符进行统计。

### Lower

> 用途：将一个文字串中的所有大写字母转换为小写字母。

* 语法：Lower(Text)

* 参数：Text是包含待转换字母的文字串。

* **注意：** Lower函数不改变文字串中非字母的字符。Lower与proper和upper函数非常相似。

### Upper

> 用途：将文本转换成大写形式。

* 语法：Upper(Text)

* 参数：Text为需要转换成大写形式的文本，它可以是引用或文字串。

### Mid或Midb

> 用途：Mid返回文本串中从指定位置开始的特定数目的字符，该数目由用户指定。Midb返回文本串中从指定位置开始的特定数目的字节，该数目由用户指定。Midb函数可以用于双字节字符。

* 语法：Mid(Text，Start_Num，Num_Chars)或midb(Text，Start_Num，Num_Bytes)

* 参数：Text是包含要提取字符的文本串。Start_Num是文本中要提取的第一个字符的位置，文本中第一个字符的start_Num为1，以此类推；Num_Chars指定希望mid从文本中返回字符的个数；Num_Bytes指定希望midb从文本中按字节返回字符的个数。

### trim

> 用途：去除字符串中的空格

* 语法：trim(Text)

