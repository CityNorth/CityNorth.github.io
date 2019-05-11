---
title: EXCEL-日期函数
date: 2019-04-30 12:32:45
tags: "Excel"
cover: 
summary: EXCEL-日期函数
categories: "Excel"
---
## EXCEL-日期函数

# 日期函数

### Now

> 用途：返回当前日期和时间所对应的序列号。

* 语法：Now()


### Today

> 用途：返回系统当前日期的序列号。

* 语法：Today()


### Weekday

> 用途：返回某日期的星期数。在默认情况下，它的值为1(星期天)到7(星期六)之间的一个整数。

* 语法：Weekday(Serial_Number，Return_Type)

* 参数：Serial_Number是要返回日期数的日期，它有多种输入方式：带引号的文本串(如"2001/02/26")、序列号(如35825表示1998年1月30日)或其他公式或函数的结果(如dateValue("2000/1/30"))。Return_Type为确定返回值类型的数字，数字1或省略则1至7代表星期天到数星期六，数字2则1至7代表星期一到星期天，数字3则0至6代表星期一到星期天。 

### Weeknum

> 用途：返回一个数字，该数字代表一年中的第几周。

* 语法：Weeknum(Serial_Num，Return_Type)

* 参数：Serial_Num代表一周中的日期。应使用date 函数输入日期，或者将日期作为其他公式或函数的结果输入。Return_Type为一数字，确定星期计算从哪一天开始。默认值为 1。

### Date 

> Date  Date(year, month,day)  

> Time time(hour, minute, second)   

### Datedif  

> 用途：计算两个日期的间隔。

* 语法：Datedif DATEDIF(start_date,end_date,unit)  
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;DATEDIF(开始日期，结束日期，Type (yd,md,ym, y,m,d))

* 参数：Start_date 为一个日期，它代表时间段内的第一个日期或起始日期。(起始日期必须在1900年之后)。End_date 为一个日期，它代表时间段内的最后一个日期或结束日期。Unit 为所需信息的返回类型。

* **注：** 
	> "Y" 时间段中的整年数。  
	> "M" 时间段中的整月数。  
	> "D" 时间段中的天数。  
	> "MD" 起始日期与结束日期的同月间隔天数。 忽略日期中的月份和年份。  
	> "YD" 起始日期与结束日期的同年间隔天数。忽略日期中的年份。  
	> "YM" 起始日期与结束日期的同年间隔月数。忽略日期中年份  


### 截取时间中的数值 

>Year
>Month
>Day
>Hour
>Minute
>second

