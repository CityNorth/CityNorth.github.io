---
title: R语言-电影评分预测模型
date: 2019-05-19 21:29:01
img: https://raw.githubusercontent.com/CityNorth/material/master/image/movie-model.jpg
top: true
tags: 
	- "数据分析"
	- "R"
summary: 基于R语言构建的电影评分预测模型
categories: "R"
---


## R语言-电影评分预测模型
 
评分系统是一种常见的推荐系统。

现在使用R语言基于协同过滤算法来构建一个电影评分预测模型及电影推荐模型。


### 一、前提准备  
  
  
1. R语言包：  

 - ggplot2包（绘图），	
 - recommenderlab包，	
 - reshape包（数据处理）  
		    install.packages("recommenderlab")
		    install.packages("reshape")
		    install.packages("ggplot2")
		    library(recommenderlab)
		    library(reshape)
		    library(ggplot2) 
  
2. 获取数据：大家可以在明尼苏达州大学的社会化计算研究中心官网上面下载这些免费数据集，网站链接为http://grouplens.org/datasets/movielens/

	或者：链接：https://pan.baidu.com/s/1o8mlt8Y 密码：bkyu

	数据说明：

	这个数据集包括： 	

	* 来自943个用户的1682个电影的10万个评级（1-5）。 
	* 每个用户已经评价至少20部电影。 
    * 为用户提供简单的人口统计信息（年龄，性别，职业，邮编）

  
以下是数据的简要说明。

----
	
> ml-data.tar.gz - 压缩的tar文件。要重建u数据文件，请执行以下操作：gunzip ml-data.tar.gz tar xvf ml-data.tar mku.sh
> u.data - 完整的u数据集，984个用户对1682项的100000评级。每位用户至少评了20部电影。用户和项目从1开始连续编号。数据是随机排序的。这是一个以制表符分隔的用户ID列表 项目ID | 评级| 时间戳。时间戳是自1970年1月1日UTC以来的unix秒
> u.info - u数据集中的用户，项目和评级数。
> u.item - 有关项目（电影）的信息; 这是一个以标签分隔的电影ID列表 电影片名| 发布日期| 视频发布日期| IMDb URL | 未知| 行动| 冒险| 动画| 儿童| 喜剧| 犯罪| 纪录片| 戏剧| 幻想| 电影黑色| 恐怖| 音乐| 神秘| 浪漫| 科幻| 惊悚片| 战争| 西方| 最后19个字段是流派，1表示电影属于该类型，0表示不是; 电影可以同时使用多种类型。电影ID是u.data数据集中使用的。
> u.genre - 类型列表。
> u.user - 有关用户的人口统计信息; 这是一个以制表符分隔的用户ID列表 年龄| 性别| 职业| 邮政编码用户ID是u.data数据集中使用的ID。
> u.occupation - 职业列表。
> u1.base - 数据集u1.base和u1.test通过u5.base和u5.test u1.test将u数据的80％/ 20％拆分为训练和测试数据。u2.base u1，...，u5中的每一个都有不相交的测试集; 这个如果用于u2.test 5折交叉验证（在那里你用每个训练和测试集重复你的实验u3.base并平均结果）。u3.test这些数据集可以通过mku.sh从u.data生成。u4.base u4.test u5.base u5.test
> ua.base - 数据集ua.base，ua.test，ub.base和ub.test ua.test将u数据分成训练集和ub.base的测试集，每个用户只有10个等级测试集。集合ub.test ua.test和ub.test是不相交的。这些数据集可以通过mku.sh从u.data生成。
> allbut.pl - 生成训练和测试集的脚本，其中除了n个用户评级之外的所有评级都在训练数据中。
> mku.sh - 用于从u.data生成所有u数据集的shell脚本。  

### 二、数据处理

	# 读取数据
	mydata<-read.table("D:\\r语言\\ml-100k\\u.data",header = FALSE,stringsAsFactors = TRUE)
	# stringAsFactor=TRUE 表示表中的所有列都不是因子，是数值型数据

第一列为用户ID，第二列电影ID，第三列是评分，第四列是用户评分的时间。这些在数据介绍中都要介绍。用户的评论时间对我们的分析没有用处，因此我们可以删掉这一列。

    mydata<-mydata[,-4]

现在这份数据集只有三列。

使用ggplot2分析用户对电影的评分结果。

要使用饼图来展现出结果，这样可以很好的展现评分列的分布特点。  

    ggplot(mydata,x=V3,aes(x=factor(1),fill=factor(V3)))+geom_bar(width = 1)+
      coord_polar(theta="y")+ggtitle("评分分布图")+
      labs(x="",y="")+
      guides(fill=guide_legend(title = '评分分数'))

  
![](https://img-blog.csdn.net/20171203151748893?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjQyOTU1NQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  

由图可知，评分为一分，两分的特别少，用户给出三分，四分的比较多，占了三分之二多。当一个新电影的评分低于3.5分时，差不多就失去了一半的用户。使用reshape包对数据进行处理，生成一个v1*v2，v3值的填充矩阵。  

    mydata<-cast(mydata,V1~V2,value="V3") #生成一个以v1为行，v2为列的矩阵，使用v3进行填充
    mydata<-mydata[,-1] #第一列数字为序列，剔除

  
这个时候，mydata有两个属性值cast\_df 和data.frame。cast\_df就类似Excel中的透视表；我们要将mydata属性改为数据框，其中cast\_df是不能直接转换为matrix的，因此需要去掉这个类属性，只保留data.frame。  

    mydata<-as.data.frame(mydata)
	dim(mydata)  
	#输出行列数  [1]  943 1682
	
接下来，我们仍要对数据进行处理，使之转换成recommenderlab包可以处理的realRatingMatrix属性。在下面，我们首先将mydata转化为一个矩阵，然后使用as()函数，进行强制类型转换，达到了我们要的结果。我们还需要给我每列数据命名，否则后面建模会出现报错

    mydata<-as.matrix(mydata)
    mydata<-as(mydata,"realRatingMatrix")  
    #生成一个 943*1682 realRatingMatrix类型的矩阵，包括了100000条记录 
    colnames(mydata)<-paste0("movie",1:1682,sep="")
	#利用paste0给电影编号起名

### 三、建立模型  

在recommenderlab包里面，针对realRatingMatrix数据类型，总共提供了6种模型，分别是：基于项目协同过滤（IBCF）， 主成分分析（PCA）， 基于流行度推荐（POPULAR）,随机推荐（RANDOM）,奇异值分解（SVD），基于用户协同过滤算法（UBCF）。  
  
* 协同过滤主要有两个步骤：  

 * ①依据目标用户的已知电影评分找到与目标用户观影风格相似的用户群。  
  
 * ②计算该用户群对其他电影的评分，并作为目标用户的预测评分。  
  
  
这份数据是943位用户对1682部电影的一个评分，但每个人不可能将这些电影全都看完，而且不可能对所有看过的电影进行评分，因此我们我们刚刚生成的评分矩阵是一个非常稀疏，而且含有许多缺失值的矩阵。但这些并不影响协同过滤的工作效果。所以我们选择了协同过滤来建立我们的模型。
	
##### 建立模型

    mydata.model <- Recommender( mydata[1:943], method = "UBCF")

###### 预测1

    mydata.predict <- predict(mydata.model,mydata[100:110], type="ratings")    
    as(mydata.predict,"matrix")[1:4,1000:1005]

---
	    movie1000 movie1001 movie1002 movie1003 movie1004 movie1005
	100  3.067797  3.043630  3.067797  3.067797  3.067797  3.067797
	101  2.895522  2.895522  2.895522  2.895522  2.895522  2.895522
	102  2.615741  2.615741  2.615741  2.615741  2.615741  2.535489
	103  3.620690  3.620690  3.620690  3.620690  3.620690  3.620690

- 用户100~103 对电影 1000~1005 预测评分。

---

###### 预测2

    mydata.predict1<-predict(mydata.model,mydata[10:15],n=5)
	as(mydata.predict1,"list")   

---

	$`10`
	[1] "movie313" "movie300" "movie222" "movie311" "movie405"
	
	$`11`
	[1] "movie285" "movie315" "movie302" "movie313" "movie269"
	
	$`12`
	[1] "movie313" "movie100" "movie288" "movie268" "movie316"
	
	$`13`
	[1] "movie134" "movie513" "movie169" "movie660" "movie408"
	
	$`14`
	[1] "movie300" "movie258" "movie272" "movie887" "movie286"
	
	$`15`
	[1] "movie183" "movie100" "movie172" "movie98"  "movie197"


修改一下参数，给用户推荐电影。预测2为给用户10~15 推荐5部电影

### 四、协同过滤 

1. 什么是协同过滤

	协同过滤是利用集体智慧的一个典型方法。要理解什么是协同过滤 (Collaborative Filtering, 简称 CF)，首先想一个简单的问题，如果你现在想看个电影，但你不知道具体看哪部，你会怎么做？大部分的人会问问周围的朋友，看看最近有什么好看的电影推荐，而我们一般更倾向于从口味比较类似的朋友那里得到推荐。这就是协同过滤的核心思想。

	换句话说，就是借鉴和你相关人群的观点来进行推荐，很好理解。

2. 协同过滤的实现

	收集数据——找到相似用户和物品——进行推荐

- 收集数据

	这里的数据指的都是用户的历史行为数据，比如用户的购买历史，关注，收藏行为，或者发表了某些评论，给某个物品打了多少分等等，这些都可以用来作为数据供推荐算法使用，服务于推荐算法。需要特别指出的在于，不同的数据准确性不同，粒度也不同，在使用时需要考虑到噪音所带来的影响。

- 找到相似用户和物品
	这一步也很简单，其实就是计算用户间以及物品间的相似度。以下是几种计算相似度的方法：
	> 欧式距离
	> 皮尔逊相关系数
	> Cosine 相似度
	> Tanimoto 系数

- 进行推荐

	在知道了如何计算相似度后，就可以进行推荐了
	
	在协同过滤中，有两种主流方法：基于用户的协同过滤，和基于物品的协同过滤。

	- 基于用户的 CF 的基本思想相当简单，基于用户对物品的偏好找到相邻邻居用户，然后将邻居用户喜欢的推荐给当前用户。计算上，就是将一个用户对所有物品的偏好作为一个向量来计算用户之间的相似度，找到 K 邻居后，根据邻居的相似度权重以及他们对物品的偏好，预测当前用户没有偏好的未涉及物品，计算得到一个排序的物品列表作为推荐。

	- 基于物品的 CF 的原理和基于用户的 CF 类似，只是在计算邻居时采用物品本身，而不是从用户的角度，即基于用户对物品的偏好找到相似的物品，然后根据用户的历史偏好，推荐相似的物品给他。从计算的角度看，就是将所有用户对某个物品的偏好作为一个向量来计算物品之间的相似度，得到物品的相似物品后，根据用户历史的偏好预测当前用户还没有表示偏好的物品，计算得到一个排序的物品列表作为推荐。

3. 总结

	> 以上两个方法都能很好的给出推荐，并可以达到不错的效果。但是他们之间还是有不同之处的，而且适用性也有区别。下面进行一下对比
	
	* 计算复杂度 
	
		Item CF 和 User CF 是基于协同过滤推荐的两个最基本的算法，User CF 是很早以前就提出来了，Item CF 是从 Amazon 的论文和专利发表之后（2001 年左右）开始流行，大家都觉得 Item CF 从性能和复杂度上比 User CF 更优，其中的一个主要原因就是对于一个在线网站，用户的数量往往大大超过物品的数量，同时物品的数据相对稳定，因此计算物品的相似度不但计算量较小，同时也不必频繁更新。但我们往往忽略了这种情况只适应于提供商品的电子商务网站，对于新闻，博客或者微内容的推荐系统，情况往往是相反的，物品的数量是海量的，同时也是更新频繁的，所以单从复杂度的角度，这两个算法在不同的系统中各有优势，推荐引擎的设计者需要根据自己应用的特点选择更加合适的算法。

	* 适用场景 
	
		在非社交网络的网站中，内容内在的联系是很重要的推荐原则，它比基于相似用户的推荐原则更加有效。比如在购书网站上，当你看一本书的时候，推荐引擎会给你推荐相关的书籍，这个推荐的重要性远远超过了网站首页对该用户的综合推荐。可以看到，在这种情况下，Item CF 的推荐成为了引导用户浏览的重要手段。同时 Item CF 便于为推荐做出解释，在一个非社交网络的网站中，给某个用户推荐一本书，同时给出的解释是某某和你有相似兴趣的人也看了这本书，这很难让用户信服，因为用户可能根本不认识那个人；但如果解释说是因为这本书和你以前看的某本书相似，用户可能就觉得合理而采纳了此推荐。
	
		相反的，在现今很流行的社交网络站点中，User CF 是一个更不错的选择，User CF 加上社会网络信息，可以增加用户对推荐解释的信服程度。



### 五、引伸

> 试着将基于用户协同过滤算法（UBCF），换成基于项目协同过滤（IBCF）,建模用时更长


##### 建立模型

    mydata.model <- Recommender( mydata[1:943], method = "IBCF")

###### 预测1

    mydata.predict <- predict(mydata.model,mydata[100:110], type="ratings")    
    as(mydata.predict,"matrix")[1:4,1000:1005]

---
	    movie1000 movie1001 movie1002 movie1003 movie1004 movie1005
	100        NA         2         3  4.000000        NA        NA
	101         2        NA        NA  2.500000         4        NA
	102         2        NA         3  2.666667         3         3
	103        NA        NA        NA  2.000000        NA        NA

- 用户100~103 对电影 1000~1005 预测评分。

---

###### 预测2

    mydata.predict1<-predict(mydata.model,mydata[10:15],n=5)
	as(mydata.predict1,"list")   

---

		$`10`
	[1] "movie75"  "movie327" "movie339" "movie360" "movie379"
	
	$`11`
	[1] "movie18"  "movie68"  "movie113" "movie292" "movie316"
	
	$`12`
	[1] "movie37"  "movie360" "movie537" "movie723" "movie766"
	
	$`13`
	[1] "movie16"  "movie30"  "movie46"  "movie104" "movie112"
	
	$`14`
	[1] "movie37"  "movie41"  "movie74"  "movie115" "movie256"
	
	$`15`
	[1] "movie43"  "movie51"  "movie52"  "movie107" "movie114"


修改一下参数，给用户推荐电影。预测2为给用户10~15 推荐5部电影



### 参考资料

*   [深入推荐引擎相关算法 - 协同过滤](https://www.ibm.com/developerworks/cn/web/1103_zhaoct_recommstudy2/index.html)
    
*   [推荐系统：基于用户和模型的协同过滤电影推荐](https://www.cnblogs.com/luban/p/8950350.html)
       








