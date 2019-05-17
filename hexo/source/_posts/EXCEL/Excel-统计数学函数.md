
	---
title: EXCEL-统计数学函数
date: 2019-05-1 03:20:05
tags: "Excel"
summary: EXCEL-统计数学函数
categories: "Excel"
---
## EXCEL-统计数学函数

# 统计数学函数：

### Sum
> 用途：返回某一单元格区域中所有数字之和。 
 
* 语法：Sum(Number1，Number2，...)   
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Sum(数据区域)

* 参数：Number1，Number2，...为1到30个需要求和的数值(包括逻辑值及文本表达式)、区域或引用。
注意：参数表中的数字、逻辑值及数字的文本表达式可以参与计算，其中逻辑值被转换为1、文本被转换为数字。如果参数为数组或引用，只有其中的数字将被计算，数组或引用中的空白单元格、逻辑值、文本或错误值将被忽略。

### Sumif

> 用途：根据指定条件对若干单元格、区域或引用求和。


* 语法：Sumif(Range，Criteria，Sum_Range)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Sumif(条件范围，条件，求和范围)

* 参数：Range为用于条件判断的单元格区域，Criteria是由数字、逻辑表达式等组成的判定条件，Sum_Range为需要求和的单元格、区域或引用。


### Sumifs
> Sumif(求和范围，条件范围1，条件1，条件范围2，条件2。。。)


### Average

> 用途：计算所有参数的算术平均值。

* 语法：	Average(Number1，Number2，...)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Average(数据区域)

* 参数：Number1、Number2、...是要计算平均值的1～30个参数。

### Count
> 用途：返回数字参数的个数。它可以统计数组或单元格区域中含有数字的单元格个数。

* 语法：	Count(Value1，Value2，...)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Count(数值数据区域)

* 参数：Value1，Value2，...是包含或引用各种类型数据的参数(1～30个)，其中只有数字类型的数据才能被统计。

### Counta

> 用途：返回参数组中非空值的数目。利用函数counta可以计算数组或单元格区域中数据项的个数。

* 语法：Counta(Value1，Value2，...)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Counta(字符数据区域)



### Countblank

> 用途：计算某个单元格区域中空白单元格的数目。

* 语法：Countblank(Range)   
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Countblank(区域)

* 参数：Range为需要计算其中空白单元格数目的区域。

### Countif

> 用途：计算区域中满足给定条件的单元格的个数。  

* 语法：Countif(Range，Criteria)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Countif(区域，条件)
* 参数：Range为需要计算其中满足条件的单元格数目的单元格区域。Criteria为确定哪些单元格将被计算在内的条件，其形式可以为数字、表达式或文本。

### Countifs

> 用途：计算区域中满足给定条件的单元格的个数。   

* Countifs(区域1，条件1, 区域2，条件2)

### Max

> 用途：返回数据集中的最大数值。

* 语法：Max(Number1，Number2，...)   
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Max(数据区域)
* 参数：Number1，Number2，...是需要找出最大数值的1至30个数值。

### Min

> 用途：返回给定参数表中的最小值。

* 语法：Min(Number1，Number2，...)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Min(数据区域)

* 参数：Number1，Number2，...是要从中找出最小值的1到30个数字参数。

### Sumproduct

> 用途：在给定的几组数组中，将数组间对应的元素相乘，并返回乘积之和。 

* 语法：Sumproduct(Array1，Array2，Array3，...)   
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Sumproduct(数组3，数组2，数组3，...)

* 参数：Array1，Array2，Array3，...为2至30个数组，其相应元素需要进行相乘并求和。

### Sumsq

> 用途：返回所有参数的平方和。

* 语法：Sumsq(Number1，Number2，...)

* 参数：Number1，Number2，...为1到30个需要求平方和的参数，它可以是数值、区域、引用或数组。


### INT
> 用途：将任意实数向下取整为最接近的整数。

* 语法：INT(Number)

* 参数：Number为需要处理的任意一个实数。

### MOD

> 用途：返回两数相除的余数，其结果的正负号与除数相同。

* 语法：Mod(Number，Divisor)

* 参数：Number为被除数，Divisor为除数(Divisor不能为零)。

### Trunc
> 用途：将数字的小数部分截去，返回整数。

* 语法：Trunc(Number，Num_Digits)

* 参数：Number是需要截去小数部分的数字，Num_Digits则指定保留小数的精度(几位小数)。

* **注意：** Trunc函数可以按需要截取数字的小数部分，而int函数则将数字向下舍入到最接近的整数。Int和Trunc函数在处理负数时有所不同：Trunc(-4.3)返回-4，而INT(-4.3)返回-5。

### Product

> 用途：将所有数字形式给出的参数相乘，然后返回乘积值。

* 语法：Product(Number1，Number2，...)

* 参数：Number1，Number2，...为1到30个需要相乘的数字参数。

### Round

> 用途：按指定位数四舍五入某个数字。

* 语法：Round(Number，Num_Digits)

* 参数：Number是需要四舍五入的数字；Num_Digits为指定的位数，Number按此位数进行处理。

* **注意：** 如果Num_Digits大于0，则四舍五入到指定的小数位；如果Num_Digits等于0，则四舍五入到最接近的整数；如果Num_Digits小于0，则在小数点左侧按指定位数四舍五入。

### Rounddown

> 用途：按绝对值减小的方向舍入某一数字。

* 语法：Rounddown(Number，Num_Digits)

* 参数：Number是需要向下舍入的任意实数，Num_Digits指定计算的小数位数。

* **注意：** Rounddown函数和Round函数的用途相似，不同之处是Rounddown函数总是向下舍入数字。

### Roundup

> 用途：按绝对值增大的方向舍入一个数字。

* 语法：Roundup(Number，Num_Digits)

* 参数：Number为需要舍入的任意实数，Num_Digits指定舍入的数字位数。

* **注意：** 如果Num_Digits为0或省略，则将数字向上舍入到最接近的整数。如果Num_Digits小于0，则将数字向上舍入到小数点左边的相应位数。

### ABS

> 用途：返回某一参数的绝对值。

* 语法：ABS(Number)

* 参数：Number是需要计算其绝对值的一个实数。

### Sqrt

> 用途：返回某一正数的算术平方根。

* 语法：Sqrt(Number)

* 参数：Number为需要求平方根的一个正数。


### Power  

> 用途：对数值求几次幂

* 语法：Power(数值，几次幂)
