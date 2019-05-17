---
title: EXCEL-查找引用
date: 2019-04-30 12:32:45
tags: "Excel"
author: 城北
cover: 
summary: EXCEL-查找引用
categories: "Excel"
---
## EXCEL-查找引用

# 查找引用

### VLOOKUP

> 用途：在表格或数值数组的首列查找指定的数值，并由此返回表格或数组当前行中指定列处的数值。

* 语法：VLOOKUP(lookup_value，table_array，col_index_num，range_lookup)   
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;VLOOKUP(找谁，在哪里找，第几列，怎么找) 

* 参数：Lookup_value为需要在数据表第一列中查找的数值，Table_array 为需要在其中查找数据区域。Col_index_num 为table_array 中待返回的匹配值的列序号。Range_lookup为一逻辑值，指明函数VLOOKUP 返回时是精确匹配还是近似匹配。如果Range_lookup为 1或省略，则返回近似匹配值（模糊匹配），
如果找不到精确匹配值，则返回小于lookup_value 的最大数值；
如果range_value 为0， 函数VLOOKUP 将返回精确匹配值。

* **注意：** 1. 查找值一定要在第一列。  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;2. 模糊匹配时第一列一定要升序排列。

### Match

> 用途：返回在指定方式下与指定数值匹配的数组中元素的相应位置。如果需要找出匹配元素的位置而不是匹配

* 元素本身，则应该使用match函数。

* 语法：Match(Lookup_Value，Lookup_Array，Match_Type)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Match(找谁，在哪里找，怎么找)

* 参数：Lookup_Value为需要在数据表中查找的数值，它可以是数值(或数字、文本或逻辑值)、对数字、文本或逻辑值的单元格引用。Lookup_Array是可能包含所要查找的数值的连续单元格区域，Lookup_Array可以是数组或数组引用；Match_Type为数字-1、0或1，它说明Excel如何在Lookup_Array中查找Lookup_Value。如果Match_Type为1，函数Match查找小于或等于Lookup_Value的最大数值。如果Match_Type为0，函数Match查找等于Lookup_Value的第一个数值。如果Match_Type为-1，函数Match查找大于或等于Lookup_Value的最小数值。

### INDEX（） 

> 用途：返回列表或数组中的元素值，此元素由行序号和列序号的索引值进行确定。　　

* 使用格式：INDEX(array,row_num,column_num)
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;INDEX(范围，范围里的行号, 范围里的列号)

* 参数说明：Array代表单元格区域或数组常量；Row_num表示指定的行序号（如果省略row_num，则必须有  column_num）；Column_num表示指定的列序号（如果省略column_num，则必须有 row_num）


### Offset 
> 用途：选取区域数据

* 使用格式： Offset(相对位置， 下移几行，右移几列， 高，宽)	


### Indirect

> 为对单元格的引用， 

* 使用格式：INDIRECT(ref_text,[a1])
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Indirect(字符串)

### Column   

> 返回单元格的列号

* Column([单元格])


### Row 

> 返回单元格的行号

* Row （[单元格]）
