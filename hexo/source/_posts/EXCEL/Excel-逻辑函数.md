---
title: EXCEL-逻辑函数
date: 2019-04-30 12:32:45
tags: "Excel"
cover: true
summary: 一些excel中经常用到的函数，希望对你有所帮助，经常更新。有什么错误，希望您及时指出。互相学习。
categories: "Excel"
---
## EXCEL-逻辑函数

# 逻辑函数：

### If
>用途：执行逻辑判断，它可以根据逻辑表达式的真假，返回不同的结果，从而执行数值或公式的条件检测任务。  
  
* 语法：If(Logical_Test，Value_If_True，Value_If_False)	  
 &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;If(条件，满足条件时执行，不满足条件时执行)     

* 参数：Logical_Test计算结果为True或False的任何数值或表达式；Value_If_True是Logical_Test为True时函数的返回值，如果Logical_Test为True并且省略了Value_If_True，则返回True。而且Value_If_True可以是一个表达式；Value_If_False是Logical_Test为False时函数的返回值。如果Logical_Test为False并且省略Value_If_False，则返回False。Value_If_False也可以是一个表达式。

### AND 
> 用途：返回逻辑值：如果所有参数值均为逻辑“真（TRUE）”，则返回逻辑“真（TRUE）”，反之返回逻辑“假（FALSE）”。  
  
* 语法：AND(logical1,logical2,  ...) 　  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;AND(条件1，条件2,….)

* 参数：Logical1,Logical2,Logical3……：表示待测试的条件值或表达式，最多至30个。

### OR　
> 用途：返回逻辑值，仅当所有参数值均为逻辑“假（FALSE）”时返回函数结果逻辑“假（FALSE）”，否则都返回逻辑“真（TRUE）”。　　

* 语法：OR(logical1,logical2,  ...)　  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;OR(条件1，条件2,….)　

* 参数：Logical1,Logical2,Logical3……：表示待测试的条件值或表达式，最多至0个.

### Not   
> 用途：以函数的逻辑值求反

* 语法：Not(logical)　  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Not(条件)　
   
### Iseven
> 用途：测试参数的奇偶性，如果参数为偶数返回True，否则返回False。

* 语法：Iseven(Number)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Iseven(数值)  

* Number待测试的数值。如果参数值不是整数，则自动截去小数部分取整。    
**注意：** 该函数必须加载“分析工具库”方能使用。如果参数Number不是数值，Iseven函数返回错误值#Value!。

### Isodd

> 用途：测试参数的奇偶性，如果参数为奇数返回True，否则返回False。 
 
* 语法：Isodd(Number)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Iseven(数值)   

* 参数：Number待测试的数值。如果参数不是整数，则自动截去小数部分取整。  
**注意：** 该函数必须加载“分析工具库”方能使用。

### Iserror   

> 用途：检查一个值是否为错误   
 
* 语法：iserror(value)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;iserror(运算结果)  

* 参数：value可以是一个表达式，如果结果有错则返回TRUE。

