---
title: R语言常包
date: 2019-04-29 13:33:37
top: true
author: 城北
cover: true
img: #
categories: R语言
tags: R
summary: 一些R语言常用到的包，查漏补缺，经常更新。有什么不懂的，欢迎来问
---

## R语言常用包

 
1. 计算总体的均值：mean(x);
2. 计算总体的方差：var(x);
3. 计算总体的标准差：sd(x);
4. 计算总体的中位数：median(x)；
5. 计算总体四分位距：c(quantile(data,probs=c(0.75)))-c(quantile(data,probs=c(0.25)));
6. 计算总体的离散系数：总体标准差/总体7.均值 sd(x)/mean(x)；
8. 计算总体全距：c(max(x)-min(x));
9. 计算总体的(不及格率)：length(x[x<60])/length(x);
10. 求和：sum(x);
11. 从小到大排序：sort(x);
12. 按原数据排序的反方向排序：rev(x);
13. 求向量的置：rank(x);
14. 求积：prod；
15. 在外向量插入元素：append(x,1:3,after=3)
16. 把缺省值na置0：x[is.na(x)]<-0;
17. 把NA过滤掉：u<-x[!is.na(x)];
18. 矩阵的转置：t(x);
19. 求矩阵的对角线：diag(x);
20. 求矩阵的逆矩阵：solve(x);
21. 求矩阵的特征值和特征矩阵：x.eigen<-eigen(x,symmetric=T);
22. 求矩阵(数组)的维数：dim(x);
23. 矩阵的行数：nrow(x);
24. 矩阵的列数：ncol(x);
25. 求矩阵的下三角矩阵：lower.tri(x); x[lower.tri(x)]=0; x[upper.tri(x)]=0;
26. 数组的定义：array;
27. 创建因子:factor(x);
28. 因子的水平：level(x);
29. 数据框的合并：rbind(x1,x2);
30. 求绝对值：abs(x);
31. 开方：sqrt(x);
32. 不大于x的最大整数：floor(x);
33. 不小于x的最大整数：ceilling(x);
34. 去掉小数点之后的数：trunc(x);
35. 保留小数点的位数：round(x,digits=2),digits是保留的位数
36. 编辑数据集：x<-edit(x)等价于fix(x)；
37. 连接字符：paste(x1,x2,x3);
38. 查看某个函数的参数：args( );
39. 查看某个包中包含的所有函数：help(package=” ”)
40. 更改数据框的列名为小写字母：names(x)<-tolower(names(x))
41. 将某进制的数转换为十进制的数：strtoi(“1111”,base=2) base 指的是某进制的数
42. 将十进制的数转换为二进制的数：intToBits(132)
43. 计算区域中心坐标： coordinates()
44. 用来解决向量或者数据框重复值的函数，它会返回一个TRUE和FALSE的向量: duplicated()
45. 根据数据框中的某一列进行排序：sh[order(sh[,1]),]或者arrange(df,.(var1),(.varb))
46. 简单随机抽样：sample(x,n,replace=T,prob=NULL)x是样本，n是抽取个数，replace代表是否是有放回抽样，prob是抽取各个样本的概率。
47. 分层抽样：strata(data,stratanames=NULL,size,method=c(“srswor”,”srswr”,”poission”,”systematic”),pik,description=FALSE)data为数据集，stratanames中放置进行分层所依据的变量名称，size设置各层中将要抽出的观测样本数，method用于选择其中的抽样方法（无放回、有放回、泊松、系统抽样），pik用于设置各层的抽样概率，description选择是否输出含有各层基本信息的结果。
48. 整群抽样：cluster(data,clustername,size,method=c(“srswor”,”srswr”,”poisson”,”systematic”),pik,description=FALSE)
49. 给出数据的属性列表：attributes()
50. 查看数据的内部结构：str()
51. 查看变量的详细情况：describe()（Hmisc包）
52. 查看更加详细的数据情况：basicStats()（fBasics包）
53. 查看数据的缺失值分布状况：md.pattern()（mice包）
54. 显示数据的行列数：nrow();ncol();
55. 点图：dotchart()
56. 处理缺失值的函数：mice()(mice包)
57. 寻找噪声数据：outlier()(outliers包)
58. 卡方检验：chisq.test(x)
59. 求两列数据的协方差：cov(x)
60. 数据的标准化：scale()
61. 判断是否存在完整观测样本：complete.cases()
62. 对向量进行赋值：assign(“w”,c(1,2))
63. 返回向量的范围：range(x)
64. 求向量的连乘积：prod(x)
65. 向向量中添加元素：append(y,10:5,after=5)
66. 矩阵之间的乘法：A%*%B
67. 取得矩阵的对角元素：diag()
68. 求矩阵的特征值和特征向量：eigen()
69. 绘制函数图像：curve()
70. 改变缺省调色板：palette()