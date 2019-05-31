---
title: R语言字符串处理
date: 2019-05-18 20:05:54
img: https://raw.githubusercontent.com/CityNorth/material/master/image/zifuchuanchuli.png
tags: "R"
summary: 字符串处理
categories: "R"

---


# R语言中的字符串处理函数

### 内容概览

  尽管R是一门以数值向量和矩阵为核心的统计语言，但字符串有时候也会在数据分析中占到相当大的份量。


*   获取字符串长度：nchar()能够获取字符串的长度，它也支持字符串向量操作。注意它和length()的结果是有区别的。
    
*   字符串粘合：paste()负责将若干个字符串相连结，返回成单独的字符串。其优点在于，就算有的处理对象不是字符型也能自动转为字符型。
    
*   字符串分割：strsplit()负责将字符串按照某种分割形式将其进行划分，它正是paste()的逆操作。
    
*   字符串截取：substr()能对给定的字符串对象取出子集，其参数是子集所处的起始和终止位置。
    
*   字符串替代：gsub()负责搜索字符串的特定表达式，并用新的内容加以替代。sub()函数是类似的，但只替代第一个发现结果。
    
*   字符串匹配：grep()负责搜索给定字符串对象中特定表达式 ，并返回其位置索引。grepl()函数与之类似，但其后面的"l"则意味着返回的将是逻辑值。
    
*   字符(串)的格式化(定制)输出：R中将字符或字符串按照一定的格式和要求输出。
    
        字符串分割函数：strsplit()
        字符串连接函数：paste()及paste0()
        计算字符串长度：nchar()及length()
        字符串截取函数：substr()及substring()
        字符串替换函数：chartr()、sub()及gsub()
        字符串匹配函数：grep()及grepl()
        大小写转换函数：toupper()、tolower()及casefold()
        字符(串)的格式化(定制)输出函数：sprintf()、sink()、cat()、print()、strtrim()、strwrap()
    

字符串函数参数详解及示例
------------

* * *

#### 1\. 字符串分割函数：strsplit()

  strsplit()是一个拆分函数，该函数可以使用正则表达式进行匹配拆分。

    其命令形式为：**strsplit(x, split, fixed= F, perl= F, useBytes= F)**

  在R里面，strsplit一般用来进行字符串分割操作，我们先来看下strsplit函数有哪些选项：**x、split、fixed、perl** 这四个选项是我们会经常用到的。

*   参数x为字符串格式向量，函数依次对向量的每个元素进行拆分
    
*   参数split为拆分位置的字串向量，即在哪个字串处开始拆分；该参数默认是正则表达式匹配；若设置fixed= T则表示是用普通文本匹配或者正则表达式的精确匹配。用普通文本来匹配的运算速度要快些。
    
*   参数perl的设置和perl的版本有关，表示可以使用perl语言里面的正则表达式。如果正则表达式过长，则可以考虑使用perl的正则来提高运算速度。
    
*   参数useBytes表示是否逐字节进行匹配，默认为FALSE，表示是按字符匹配而不是按字节进行匹配。
    
*   **Example1**
    
    > strsplit()函数用于字符串分割，其中split是分割参数。所得结果以默认以list形式展示。
    > 首先x和split是两个必须的选项

        > x = "character vector, each element of which is to be split. Other inputs, including a factor, will give an error."
        > x
        [1] "character vector, each element of which is to be split. Other inputs, including a factor, will give an error."
        > strsplit(x,split = "\\s+")
        [[1]]
         [1] "character" "vector,"   "each"      "element"   "of"        "which"     "is"        "to"        "be"        "split."    "Other"    
        [12] "inputs,"   "including" "a"         "factor,"   "will"      "give"      "an"        "error."   
        
        > strsplit(x,split = " ")
        [[1]]
         [1] "character" "vector,"   "each"      "element"   "of"        "which"     "is"        "to"        "be"        "split."    "Other"    
        [12] "inputs,"   "including" "a"         "factor,"   "will"      "give"      "an"        "error."   
        
        > strsplit(x,split = "")
        [[1]]
          [1] "c" "h" "a" "r" "a" "c" "t" "e" "r" " " "v" "e" "c" "t" "o" "r" "," " " "e" "a" "c" "h" " " "e" "l" "e" "m" "e" "n" "t" " " "o" "f" " " "w"
         [36] "h" "i" "c" "h" " " "i" "s" " " "t" "o" " " "b" "e" " " "s" "p" "l" "i" "t" "." " " "O" "t" "h" "e" "r" " " "i" "n" "p" "u" "t" "s" "," " "
         [71] "i" "n" "c" "l" "u" "d" "i" "n" "g" " " "a" " " "f" "a" "c" "t" "o" "r" "," " " "w" "i" "l" "l" " " "g" "i" "v" "e" " " "a" "n" " " "e" "r"
        [106] "r" "o" "r" "."
        
        
> 在上面的例子中我们可以看到，我们对split选项设置了三个不同的参数，第一个是`\\s+`，第二个是一个空格，第三个一个空字符。
> 第一个参数`\\s+`和第二个参数空格达到了相同的效果，都是把x字符串按照空白进行分割。那个这里为什么是`\\s+`呢？相信对正则表达式有一点了解的同学一定会知道`\s+`是什么意思。`\s+`是表示匹配一个或一个以上的空白字符，包括空格、制表符和换行符等。这里的第一个`\` 是用来转义第二个`\` 符号的。
> 那么第三个参数里面，我们设置 `split=""` 又是什么意思呢？当设置为空字符的时候，`strsplit` 函数会把字符串按照字符一个个进行分割。
    
*   **Example2**
    
    > strsplit默认支持正则表达式
    > 在上面的例子中我们也可以看到strsplit默认是支持正则表达式的。
    > 那么如果我要不支持正则表达式强行按照固定字符匹配怎么办呢？除了我们用更加高级的正则表达式达到这一目的我们还可以通过设定fixed参数来达到目的：
        
        > x = "asdas\\sasdasd"
        > x
        [1] "asdas\\sasdasd"
        > strsplit(x,split = "\\s")
        [[1]]
        [1] "asdas\\sasdasd"
        
        > strsplit(x,split = "\\s",fixed = T)
        [[1]]
        [1] "asdas"  "asdasd"
        
        > strsplit(x,split = "\s")
        Error: '\s' is an unrecognized escape in character string starting ""\s"
        
    > 比如这里的 x 字符串，它带有两个`\`，我要以`\\s`来进行分割。如果我直接设定`split='\\s'`参数时，`strsplit`函数无法正确的分割字符串，但是当我加了`fixed=T`参数后，`strsplit`函数可以正确分割这些字符串。
    > 在strsplit函数中，是默认支持正则表达式的，我们可以通过设置perl来支持使用perl兼容的正则表达式。也可以通过fixed来设置不支持正则表达式，而且fixed选项拥有比perl更高的优先级。
    
*   **Example3**
    
    > fixed为TRUE表示精确匹配，否则表示可以使用正则表达式另外需要说明一点的是：直接使用split函数得到的结果是一个列表，如果希望得到一个向量，可以使用 unlist() 函数。
        # 由于split是正则表达式，所以在切割包含.的字符串的时候万分小心
        unlist(strsplit("a.b.c", "."))
        ## [1] "" "" "" "" ""
        ## following are right answers
        unlist(strsplit("a.b.c", "[.]"))
        ## [1] "a" "b" "c"
        unlist(strsplit("a.b.c", ".", fixed = TRUE))
        unlist(strsplit("a.b.c","\\."))
        ## 编写逆写字符串
        ## a useful function: rev() for strings
        strReverse <- function(x)
                sapply(lapply(strsplit(x, NULL), rev), paste, collapse = "")
        strReverse(c("abc", "Statistics"))
        
        ## 得到R核心团队成员的名First Name
        ## get the first names of the members of R-core
        a <- readLines(file.path(R.home("doc"),"AUTHORS"))[-(1:8)]
        a <- a[(0:2)-length(a)]
        (a <- sub(" .*","", a))
        # and reverse them
        strReverse(a)
        # 注意：最后一个空字符串将会被忽略
        strsplit(paste(c("", "a", ""), collapse="#"), split="#")[[1]]
        # [1] ""  "a"
        
        # split=NULL逐个切割字符串
        strsplit("abcde",NULL)
    

* * *

#### 2. 字符串连接函数：paste() 及 paste0()

  主要参数： **paste(..., sep = " ", collapse = NULL)**

       **paste0(..., collapse = NULL)**

  paste()函数用于字符串连接，其中 sep 负责两组字符串间的连接； collapse 负责一组字符串内部的连接，常常在一些作图的标题中看到paste的使用。

*   **Example1**
    
    > paste()函数可以将多个字符型向量连接成一个向量。如果要将一个不同类型的向量连接起来，这个向量首先会被转换成字符型向量。
        
        > x <- c("a","b", "c", "d", "e")
        > y <- c("A", "B", "C", "D","E")
        > paste(x, y)
        [1] "a A" "b B" "c C" "d D" "e E"
    
*   **Example2**
    
    > 在默认情况下，向量的值之间使用空格进行分隔的。 若想使用其他分隔符，可以使用sep参数进行设置，例如：
        
        > paste(x, y, sep = "-")
        [1] "a-A" "b-B" "c-C" "d-D" "e-E"
        > paste(x, y, sep = "")
        [1] "aA" "bB" "cC" "dD" "eE"
        
        > paste(letters[1:6],1:6,sep="-")
        [1] "a-1" "b-2" "c-3" "d-4" "e-5" "f-6"
    
*   **Example3**
    
    > 若将返回的所有向量都连成一个字符串，那么则需要collapse参数来指定这些值之间的连接符。例如：
        
        > paste(x, y, sep = "-", collapse = "#")
        [1] "a-A#b-B#c-C#d-D#e-E"
        
        > paste(letters[1:6],1:6,sep="-",collapse=";")
        [1] "a-1;b-2;c-3;d-4;e-5;f-6"
        
        > nth <- paste0(1:12, c("st", "nd", "rd", rep("th", 9)))
        > paste(month.abb, "is the", nth, "month of the year.", sep = "_*_")
        [1] "Jan_*_is the_*_1st_*_month of the year."  "Feb_*_is the_*_2nd_*_month of the year."
        [3] "Mar_*_is the_*_3rd_*_month of the year."  "Apr_*_is the_*_4th_*_month of the year."
        [5] "May_*_is the_*_5th_*_month of the year."  "Jun_*_is the_*_6th_*_month of the year."
        [7] "Jul_*_is the_*_7th_*_month of the year."  "Aug_*_is the_*_8th_*_month of the year."
        [9] "Sep_*_is the_*_9th_*_month of the year."  "Oct_*_is the_*_10th_*_month of the year."
        [11] "Nov_*_is the_*_11th_*_month of the year." "Dec_*_is the_*_12th_*_month of the year."
    
*   **Example4**
    
    > paste()在不指定分割符的情况下，默认分割符是空格；paste0()在不指定分割符的情况下，默认分割符是空。
        
        # 默认以空格隔开
        paste("Hello","world")
        [1] "Hello world"
        
        # 没有空格
        paste0("Hello","world")
        [1] "Helloworld"
        
        # 指定分割符
        paste("abc", "efg", "hijk", sep = "-")
        [1] "abc-efg-hijk"
        
        # 分别对向量的每一个元素进行连接
        paste0("A", 1:6, sep = "")
        [1] "A1" "A2" "A3" "A4" "A5" "A6"
        
        # collapse参数：每一个元素操作之后，再把向量的每一个元素进行连接
        paste0("A", 1:6, sep = "",collapse = "-")
        [1] "A1-A2-A3-A4-A5-A6"
    

* * *

#### 3\. 计算字符串长度：nchar()及length()

  nchar()返回字符串的长度，取字符数量的函数。length与nchar不同，length是取向量的长度（nchar用于计算 x 中的字符数量，length函数返回 x 的集合长度）。

  用法：**nchar(x, type = "chars", allowNA = FALSE, keepNA = FALSE)**

  **nzchar(x)**用于判断一个变量的长度是否为0。

  需要注意的是，对于缺失值NA，nzchar()的结果为TRUE，而函数nchar()的返回结果为2。所以在对字符串进行测量之前，最好先使用is.na()函数判断一下是否是NA值。

*   **Example**
    
        x <- c("asfef", "qwerty", "yuiop[", "b", "stuff.blah.yech")
        > nchar(x)
        # 5  6  6  1 15
        
        #现R语言设定为NA长度为2
        > nchar(NA) 
        ## [1] 2
        > nzchar(NA)
        [1] TRUE
        > x <- ''
        > nzchar(x)
        [1] FALSE
        > nchar("你好",type="chars")   #默认情况
        ## [1] 2
        > nchar("你好",type="bytes")   #每个中文字符占2个bytes
        ## [1] 4
        > nchar("你好",type="width")
        ## [1] 4
        
        > m<-"who wins 123"
        > nchar(m)
        [1] 12
        > length(m)
        [1] 1
        
        # nchar表示字符串中的字符的个数
        > nchar("abcd")
        [1] 4
        
        # length表示向量中元素的个数
        > length("abcd")
        [1] 1
        > length(c("hello", "world"))
        [1] 2
        > length("")  #虽然字符为空，但是它仍然是一个元素。
        [1] 1
    

* * *

#### 4\. 字符串截取函数：substr()；substring()

  substr()函数和substring()函数是截取字符串最常用的函数，两个函数功能方面是一样的，只是其中参数设置不同。

  substr()函数：必须设置参数start和stop，如果缺少将出错。

  substring()函数：可以只设置first参数，last参数若不设置，则默认为1000000L，通常是指字符串的最大长度。

  `substr(x, start, stop)`

  `substring(text, first, last = 1000000L)`

  `substr(x, start, stop) <- value`

  `substring(text, first, last = 1000000L) <- value`

*   **Example1**
    
    > substr能够提取或替换一个字符向量中的子串或替换子字符串

        > substr('abcdef',2,4)
        [1] "bcd"
        > substr("abcdef", 2, 4)   #两种表达方式等价
        [1] "bcd"
        > x <- "abcdef"
        > substr(x, 1, 1) <- "ccc"
        > x
        [1] "cbcdef"
        > x <- "abcdef"
        > substr(x, 1, 1) <- ""
        > x
        [1] "abcdef"
        > x <- "abcdef"
        > substr(x, 1, 1) <- " "
        > x
        [1] " bcdef"
        > #如果start大于字符串长度，则返回""
        > x <- c("asfef", "qwerty", "yuiop[", "b", "stuff.blah.yech")
        > substr(x, 2, 5)
        [1] "sfef" "wert" "uiop" ""     "tuff"
        
        > m<-"who wins 123"
        > substr(m,1,8)
        [1] "who wins"
        > substr(m,1,3)<-"Tom"
        > m
        [1] "Tom wins 123"
    
*   **Example2**
    
    > substring函数则可以对字符串向量进行提取或替换
        
        > substring('abcdef', 1, 6)
        [1] "abcdef"
        
        > substring('abcdef', 1:6, 6)
        [1] "abcdef" "bcdef"  "cdef"  
        [4] "def"    "ef"     "f"  
        
        ### 切割字符串另类方法，但速度不如strsplit
        >substring('abcdef',1：6，1：6)
        [1] "a" "b" "c" "d" "e" "f"
        
        ### 替换字符串向量中的部分元素
        > x <- c("asfef", "qwerty", "yuiop[", "b", "stuff.blah.yech")
        ### 由于x长度为5，赋值向量会循环补齐，相当于 c("..", "+++", "..", "+++", "..")
        ### substring(x, 2) <- c("..", "+++", "..", "+++", "..")
        > substring(x, 2) <- c("..", "+++")
        > x
        [1] "a..ef"           "q+++ty"         
        [3] "y..op["          "b"              
        [5] "s..ff.blah.yech"
    
*   **Example3**
    
    > 两者的一些区别：substr返回的字串个数等于第一个参数的长度，而substring返回字串个数等于三个参数中最长向量长度，短向量循环使用。
        
        > substr("abcdef", 1:6, 1:6) 
        [1] "a"
        
        #注意还有一个substring函数，效果就不一样了：
        > substring("abcdef",1:6,1:6) 
        [1] "a" "b" "c" "d" "e" "f"
        
        #等价于：substr("123456789", 2, 4)
        > substr("123456789", c(2, 3), c(4, 5, 6))  
        [1] "234"
        
        #最长的向量长度为3，其它向量都循环补齐
        > substring("123456789", c(2, 3), c(4,5,6)) 
        [1] "234"   "345"   "23456"
    

* * *

#### 5\. 字符串替换函数：chartr()、sub()及gsub()

  chartr()函数：将原有字符串中特定字符替换成所需要的字符。其中参数old 表示原有字符串中内容；new 表示替换后的字符内容。

  **chartr (old,new,x)**，chartr-将对象中旧的字符用新的字符替代。

  这种功能和shell里面的rename有点类似，但old的字符数不能大于new，new字符数大于old的字符也将会被忽略，相当于重命名的意思。不同于rename的是chartr不能随意的替换字符串，用起来也有一定的局限性。

*   **Example1**
    
        > m<-"who wins 123"
        > chartr("w","W",m)
        [1] "Who Wins 123"
        
        > chartr(old="a", new="c", x="a123")
        [1] "c123"
        
        > chartr(old="a", new="A", x="data")
        [1] "dAtA"
    
*   **Example2**
    
    > gsub() 替换匹配到的全部；sub() 替换匹配到的第一个。

    > sub() 函数可以用来替换字符串。需要注意的是我们需要设置一个变量来接受这个替换操作后的字符，sub()函数不会对原变量进行操作。
        
    > ######正则表达式解释######
    >  /^\d+$/ 是正则表达式
    >  ^和$用来匹配位置:^表示行首,$表示行尾
    >  \d表示数字,即0-9
    >  +表示重复1次以上
    >  综合起来,/^\d+$/ 这个正则表达式就是匹配一整行1个以上的数字
    >  /^\d+$/ 就相当于 $_=~/^\d+$/ 
    >  就是对默认变量$_进行匹配,匹配成功就返回'真',否则就返回'假'
    >  !/^\d+$/ 就是对~/^\d+$/返回的布尔值取反
    > ######正则表达式解释######

        > str <- "Now is the time      "
        > sub(" +$", " 12:00", str)  ## spaces only
        [1] "Now is the time 12:00"
        ##几种错误写法##
        > sub(" +s", " 12:00", str)
        [1] "Now is the time      "
        > sub(" ", " 12:00", str)
        [1] "Now 12:00is the time      "
        > sub("     ", " 12:00", str)
        [1] "Now is the time 12:00 "
        
        # 将b替换为B
        > gsub(pattern = "b", replacement = "B", x = "baby")
        [1] "BaBy"
        > gsub(pattern = "b", replacement = "B", x = c("abcb", "boy", "baby"))
        [1] "aBcB" "Boy"  "BaBy"
        # 只替换第一个b
        > sub(pattern = "b", replacement = "B", x = "baby")
        [1] "Baby"
        > sub(pattern = "b", replacement = "B", x = c("abcb", "baby"))
        [1] "aBcb" "Baby"
    

* * *

#### 6\. 字符串匹配函数：grep()及grepl()

  其表达式为：

  **grep(pattern, x, ignore.case = FALSE, perl = FALSE, value = FALSE,fixed = FALSE, useBytes = FALSE, invert = FALSE)**

  **grepl(pattern, x, ignore.case = FALSE, perl = FALSE,fixed = FALSE, useBytes = FALSE)**

  可以理解为搜索字符向量中匹配参数pattern的模型，fixed的逻辑值决定将pattern视为正则表达式或一个文本字符串，若fixed=TURE，则视pattern为文本字符串（精确匹配）；fixed=FALSE，则视之为正则表达式，正则表达式则相当于一种条件，函数返回匹配值的下标；perl=TURE，使用perl风格的正则表达式；value则决定返回的类型是匹配值的下标还是匹配的值。

*   **Example1**
    
        > x = "Hello World"
        > grep(pattern = "Hello",x = x)
        [1] 1
        > grep(pattern = "l",x = x)
        [1] 1
        > grepl(pattern = "l",x = x)
        [1] TRUE
    
*   **Example2**
    
    > grep和grepl的区别在于grep返回的是匹配正确的字符串在 x 向量中的元素下标。而grepl返回的则是逻辑变量TRUE和ALSE。
    > 如果我们想要返回匹配正确字符的值要怎么办呢？我们可以通过设置grep中的value=T来达到目的。如：
        
        > x = c("Hello","Bye","Hi")
        > grep(pattern = "l",x = x,value = T)
        [1] "Hello"
        > grep(pattern = "H",x = x,value = T)
        [1] "Hello" "Hi"   
        > grep(pattern = "H",x = x,value = F)
        [1] 1 3
    
*   **Example3**
    
    > 在grep和grepl中，fixed和perl两个参数的用法跟strsplit中的用法是一致的。
    > 正则表达式中，“[a-z]”就表示匹配a～z，所以[a-f]表示匹配正则表达式前面6个

        > grep("[a-f]",letters)      
        [1] 1 2 3 4 5 6 
    
*   **Example4**
    
    > 使用fixed=T,因为我们匹配的类型是精确匹配，so

        >grep("[a-f]",letters,fixed=T)      
        integer(0)    #精确匹配中，[a-f]代表的是字符，所以就不能匹配到
    
*   **Example5**
    
    > 匹配的 fixed 默认为F，这也提示我们应尽量的去使用正则表达式去匹配
     
        > txt <- c("arm","foot","lefroo", "bafoobar")
        > grep("foo",txt)
        [1] 2 4
    
*   **Example6**
    
    > ignore.case 决定匹配是否对大小写敏感，为了达到精确匹配，默认为对大小写敏感；你完全可以设置不敏感，比如一些开头字母大写的问题。例如：
        
        > grep("Foo",txt)
        integer(0)
        
        > grep("Foo",txt,ignore.case=TRUE)
        [1] 2 4
        
        > grep("Foo",txt,ignore.case=T,value=T)
        [1] "foot"     "bafoobar"
    
*   **Example7**
    
    > invert 参数非常实用，它决定返回的的是匹配值还是非匹配值，往往我们要的结果就是非匹配值，例如在众多的邮件中根据内容不含”xxx”进行保留。
        
        > grep("Foo",txt,ignore.case=T,invert=T,value=T)
        [1] "arm"    "lefroo"
    
*   **Example8**
    
    > grepl函数与grep函数不同的地方在于返回的形式是否为布尔值（是 true 或 false 中的一个），grepl返回TURE或者FALSE，而grep函数返回匹配值下标或者匹配值本身，使用什么函数要看我们的需要。
        
        > grepl("Foo",txt,ignore.case=T)
        [1] FALSE  TURE FALSE  TURE
    

* * *

#### 7\. 大小写替换函数：toupper()、tolower()、casefold()

  toupper()函数：将字符串统一转换为大写。

  tolower()函数：将字符串统一转换为小写。

  casefold()函数：根据参数转换大小写。

  `tolower(x)`

  `toupper(x)`

  `casefold(x, upper = FALSE)`

  `chartr(old, new, x)`

*   **Example**
    
    > 这两个函数就不用多介绍了，按字面意思就是把对象转换成大写或小写，应用于全部的对象，例如：
        
        >toupper("abc")
        [1]"ABC"
        >tolower("ABC")
        [1]"abc"
        >x<-c("My","First","Trip")
        >tolower(x)
        [1] "my" "first" "trip"
        
        > casefold('ABDATA', upper = FALSE)
        [1] "abdata"
        > casefold('baorui', upper = FALSE)
        [1] "baorui"
        > casefold('baorui', upper = TRUE)
        [1] "BAORUI"
        
        # 这里这只提供全部应用的大小写转换，部分转换可以参照函数chartr()。
        chartr(old, new, x)
    

* * *

#### 8\. 字符(串)的格式化(定制)输出

*   **字符格式化输出**
    
        使用%s替代字符变量
        a <- "string"
        sprintf("This is where a %s goes.", a)
        # "This is where a string goes."
        
        # 使用%d替代整数
        x <- 8
        sprintf("Regular:%d", x)
        # "Regular:8"
        # Can print to take some number of characters, leading with spaces.
        sprintf("Leading spaces:%4d", x)
        # "Leading spaces:   8"
        # Can also lead with zeros instead.
        sprintf("Leading zeros:%04d", x)
        #"Leading zeros:0008:"
        
        #使用%f替代浮点数
        # %m.nf m为输出字符宽度，即最小包含的字符量。如果字符串没有达到m长度，那么可以通过补0或者空格，n表示小数的精度
        sprintf("%f", pi)         # "3.141593"
        sprintf("%.3f", pi)       # "3.142"
        sprintf("%1.0f", pi)      # "3"
        sprintf("%5.1f", pi)      # "  3.1"
        sprintf("%05.1f", pi)     # "003.1"
        sprintf("%+f", pi)        # "+3.141593"
        sprintf("% f", pi)        # " 3.141593"
        sprintf("%-10f", pi)      # "3.141593  "   (left justified)
        sprintf("%e", pi)         #"3.141593e+00"
        sprintf("%E", pi)         # "3.141593E+00"
        sprintf("%g", pi)         # "3.14159"
        sprintf("%g",   1e6 * pi) # "3.14159e+06"  (exponential)
        sprintf("%.9g", 1e6 * pi) # "3141592.65"   ("fixed")
        sprintf("%G", 1e-6 * pi)  # "3.14159E-06"
        
        x <- "string"
        sprintf("Substitute in multiple strings: %s %s", x, "string2")
        # "Substitute in multiple strings: string string2"
        
        # To print a percent sign, use "%%"
        sprintf("A single percent sign here %%")
        # "A single percent sign here %"
        #写入文件，重定向sink()
        #sink()重定向文件写入
        
        # Start writing to an output file
        sink('analysis-output.txt')
        
        set.seed(12345)
        x <-rnorm(10,10,1)
        y <-rnorm(10,11,1)
        # Do some stuff here
        cat (sprintf("x has %d elements:\n", length(x)))
        print(x)
        cat ("y =", y, "\n")
        
        cat("=============================\n")
        cat("T-test between x and y\n")
        cat("=============================\n")
        t.test(x,y)
        
        # Stop writing to the file
        sink()
               
        # Append to the file
        sink('analysis-output.txt', append=TRUE)
        cat("Some more stuff here...\n")
        sink()
    
*   **字符串的定制输出**
    
      这个内容有点类似于字符串的连接。这里用到了strtrim()，用于将字符串修剪到特定的显示宽度，其命令形式如下：strtrim(x, width)该函数返回的字符串向量的长度等于参数x的长度。
    
        strtrim(c("abcde", "abcde", "abcde"), c(1, 5, 10))
        ## [1] "a"     "abcde" "abcde"
        strtrim(c(1, 123, 12345), 4)  #短向量循环
        ## [1] "1"    "123"  "1234"
    
      strtrim()会根据width参数提供的数字来修剪字符串，若width提供的数字大于字符串的字符数的话，则该字符串会保持原样，不会增加空格之类的东西。
    
      strwrap()会把字符串当成一个段落来处理（不管段落中是否有换行），按照段落的格式进行缩进和分行，返回结果就是一行行的字符串，其命令形式如下：strwrap(x, width, indent= 0, exdent= 0, prefix= “”, simplify= T, initial= prefix)函数返回结果中的每一行的字符串中的字符数目等于参数width。
    
        string <- "Each character string in the input is first split into\n paragraphs (or lines containing whitespace only). The paragraphs are then formatted by breaking lines at word boundaries."
        string
        ## [1] "Each character string in the input is first split into\n paragraphs (or lines containing whitespace only). The paragraphs are then formatted by breaking lines at word boundaries."
        cat(string)
        ## Each character string in the input is first split into
        ##  paragraphs (or lines containing whitespace only). The paragraphs are then formatted by breaking lines at word boundaries.
        strwrap(string)  #直接将换行符忽略了
        ## [1] "Each character string in the input is first split into paragraphs"
        ## [2] "(or lines containing whitespace only). The paragraphs are then"   
        ## [3] "formatted by breaking lines at word boundaries."
        strwrap(string, width = 40, indent = 4)  #首行缩进
        ## [1] "    Each character string in the input"
        ## [2] "is first split into paragraphs (or"    
        ## [3] "lines containing whitespace only). The"
        ## [4] "paragraphs are then formatted by"      
        ## [5] "breaking lines at word boundaries."
        strwrap(string, width = 40, exdent = 4)  #除了首行的其余行缩进
        ## [1] "Each character string in the input is" 
        ## [2] "    first split into paragraphs (or"   
        ## [3] "    lines containing whitespace only)."
        ## [4] "    The paragraphs are then formatted" 
        ## [5] "    by breaking lines at word"         
        ## [6] "    boundaries."
        strwrap(string, width = 40, simplify = F)  # 返回结果是个列表，而不再是个字符串向量
        ## [[1]]
        ## [1] "Each character string in the input is"
        ## [2] "first split into paragraphs (or lines"
        ## [3] "containing whitespace only). The"     
        ## [4] "paragraphs are then formatted by"     
        ## [5] "breaking lines at word boundaries."
        strwrap(string, width = 40, prefix = "******")
        ## [1] "******Each character string in the"    
        ## [2] "******input is first split into"       
        ## [3] "******paragraphs (or lines containing" 
        ## [4] "******whitespace only). The paragraphs"
        ## [5] "******are then formatted by breaking"  
        ## [6] "******lines at word boundaries."
    

### 参考资料

*   [R中的普通文本处理-汇总](http://rstudio-pubs-static.s3.amazonaws.com/13823_dbf87ac4114b44f8a4b4fbd2ea5ea162.html)
    
*   [R中的正则表达式及字符处理函数总结](http://yphuang.github.io/blog/2016/02/29/R-Regular-Expressions-And-String-Functions/)
       
*   [字符串处理函数](http://www.bkjia.com/ASPjc/965932.html)

