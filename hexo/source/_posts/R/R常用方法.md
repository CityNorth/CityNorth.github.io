
## R语言使用中的一些奇技淫巧


### 1 读取excel内存溢出 

		#下载包
		install.packages("openxlsx")
		#读取openxlsx包
		library(openxlsx)
		file<-read.xlsx("Z:\\-2019\\周报\\2019.6.24\\6.21库存.xlsx",1)

### 字段筛选
	data<-file[c(2:7,15,25,26,29)]

### 将文本变为同名字符串

	test<-c(1,2,3,4,5)
	nameTest<-substitute(test)


#多条件字段内容删选  选出产品分类中：赠品、产品目录、其他 另存新表

	tichu<-data[which((start_data$产品分类=="赠品")|(start_data$产品分类=="产品目录")|(start_data$产品分类=="其他")),]

	#查看饰品中是否有较多库存  >= 30 有就也剔除
	#使用该方法是因为 >=30  的时候符合该条件的情况为0  就会导出删选出错  所以使用以下方法
	shipin<-which((kucun$产品分类=="饰品")&(as.integer(kucun$可销库存)>=30))
	if(length(shipin)>0){
	  kucun<-kucun[-shipin,]
	}



### 使用数据透视表方法  用sql实现  

	library(sqldf)
	result<-(sqldf('select "产品名称","产品分类", count("产品名称"),sum(可销库存),sum("7天销量"),sum("30天销量"),sum("昨日销量") from CC group by "产品名称"'))

#excel中时间处理

excel 中起始时间为  1900-01-01   Excel把1900年当做闰年，计算了2月29日  所以r转化差两天  origin="1899-12-30"

r语言 中起始时间为 1970-01-01 origin = "1970-01-01"

https://support.microsoft.com/en-us/help/214326/excel-incorrectly-assumes-that-the-year-1900-is-a-leap-year

#  将上新时间修复  异常的置空  
	Online_Time$上新时间<-as.Date(as.integer(Online_Time$上新时间),origin="1899-12-30")
	as.Date(Online_Time[,1],origin = "1970-01-01")

# 两个数据表连接 

	library("dplyr")
	process<-left_join(result,Online_Time,by="款号")[1:8]

#将数据分sheet写出

	#构造数据list
	list_data <- list("原数据" = data, "剔除" = tichu )
	#定义一个储存路径
	path="Z:\\-2019\\周报\\2019.6.24\\库存清洗_20190621.xlsx"
	#写出
	write.xlsx(list_data, file = path)

#数字以逗号分隔 先替换在转换 gsub(",","", tianmao$支付金额)
  
  tianmao$支付金额<-as.numeric(gsub(",","", tianmao$支付金额))

# 计算商品名称中包含预售的支付金额  求和  
	yuhsou<-sum(tianmao[grep(pattern="预售",tianmao$商品名称),"支付金额"])
	
	调整输出小数位数  options(digits=4)


# 超级好用的字符串处理包
	library(stringr)
	#取出商品名中的款号  例：PT616
	kuanhao<-str_extract_all(tianmao[1:20,"商品名称"],"[A-Z]+[0-9]+")[]
