---
title: Selenium的使用
date: 2019-06-10 15:38:26
tags: 
	- "爬虫"
	- "Python"
summary: Selenium的使用
cover: 
img: https://raw.githubusercontent.com/CityNorth/material/master/image/Selenium.png
categories: "爬虫"	
---


## Selenium的使用

### 一、什么是Selenium


selenium 是一套完整的web应用程序测试系统，包含了测试的录制（selenium IDE）,编写及运行（Selenium Remote Control）和测试的并行处理（Selenium Grid）。Selenium的核心Selenium Core基于JsUnit，完全由JavaScript编写，因此可以用于任何支持JavaScript的浏览器上。

selenium可以模拟真实浏览器，自动化测试工具，支持多种浏览器，爬虫中主要用来解决JavaScript渲染问题。

### 二、selenium基本使用

#### 声明浏览器对象

selenium支持很多的浏览器，但是如果想要声明并调用浏览器则需要：
	
	from selenium import webdriver
	
	browser = webdriver.Chrome()
	browser = webdriver.Firefox()

这里只写了两个例子，当然了其他的支持的浏览器都可以通过这种方式调用

#### 访问页面

	from selenium import webdriver
	
	browser = webdriver.Chrome()
	
	browser.get("http://www.baidu.com") 
	print(browser.page_source)
	browser.close() 

上述代码运行后，会自动打开Chrome浏览器，并登陆百度打印百度首页的源代码，然后关闭浏览器

#### 查找元素

**单个元素查找**

	from selenium import webdriver
	
	browser = webdriver.Chrome()
	
	browser.get("http://www.taobao.com")
	input_first = browser.find_element_by_id("q")
	input_second = browser.find_element_by_css_selector("#q")
	input_third = browser.find_element_by_xpath('//*\[@id="q"\]') 
	print(input_first) 
	print(input_second) 
	print(input_third)
	browser.close()

这里我们通过三种不同的方式去获取响应的元素，第一种是通过id的方式，第二个中是CSS选择器，第三种是xpath选择器，结果都是相同的。  
结果如下：


这里列举一下常用的查找元素方法：
		
	find_element_by_name  
	find_element_by_id  
	find_element_by_xpath  
	find_element_by_link_text  
	find_element_by_partial_link_text  
	find_element_by_tag_name  
	find_element_by_class_name  
	find_element_by_css_selector	


下面这种方式是比较通用的一种方式：这里需要记住By模块所以需要导入  
	
	from selenium.webdriver.common.by import By
	
	from selenium import webdriver from selenium.webdriver.common.by import By
	
	browser = webdriver.Chrome()
	
	browser.get("http://www.taobao.com")
	input_first = browser.find_element(By.ID,"q") print(input_first)
	browser.close()

当然这种方法和上述的方式是通用的，browser.find_element(By.ID,"q")这里By.ID中的ID可以替换为其他几个

**多个元素查找**

其实多个元素和单个元素的区别，举个例子：find\_elements,单个元素是find\_element,其他使用上没什么区别，通过其中的一个例子演示：

	from selenium import webdriver
	
	browser = webdriver.Chrome()
	browser.get("http://www.taobao.com")
	lis = browser.find_elements_by_css_selector('.service-bd li') 
	print(lis)
	browser.close()

这样获得就是一个列表


当然上面的方式也是可以通过导入from selenium.webdriver.common.by import By 这种方式实现

lis = browser.find\_elements(By.CSS\_SELECTOR,'.service-bd li')

同样的在单个元素中查找的方法在多个元素查找中同样存在：  

	find_elements_by_name  
	find_elements_by_id  
	find_elements_by_xpath  
	find_elements_by_link_text  
	find_elements_by_partial_link_text  
	find_elements_by_tag_name  
	find_elements_by_class_name  
	find_elements_by_css_selector

#### 元素交互操作

对于获取的元素调用交互方法

	from selenium import webdriver import time
	
	browser = webdriver.Chrome()
	browser.get("http://www.taobao.com")
	input_str = browser.find_element_by_id('q')
	input_str.send_keys("ipad")
	time.sleep(1)
	input_str.clear() #清除文本框内容
	input_str.send_keys("MakBook pro") #输入文本 
	button = browser.find_element_by_class_name('btn-search')
	button.click() # 模拟点击

运行的结果可以看出程序会自动打开Chrome浏览器并打开淘宝输入ipad,然后删除，重新输入MakBook pro，并点击搜索


#### 执行JavaScript

这是一个非常有用的方法，这里就可以直接调用js方法来实现一些操作，  
下面的例子是通过登录知乎然后通过js翻到页面底部，并弹框提示

	from selenium import webdriver
	browser = webdriver.Chrome()
	browser.get("http://www.zhihu.com/explore")
	browser.execute_script('window.scrollTo(0, document.body.scrollHeight)')
	browser.execute_script('alert("To Bottom")')

**获取元素属性**  

get_attribute('class')
	
	from selenium import webdriver
	
	browser = webdriver.Chrome()
	url = 'https://www.zhihu.com/explore' 
	browser.get(url)
	logo = browser.find_element_by_id('zh-top-link-logo') 
	print(logo) 
	print(logo.get_attribute('class'))

**获取文本值**  
.text
	
	from selenium import webdriver
	
	browser = webdriver.Chrome()
	url = 'https://www.zhihu.com/explore' 
	browser.get(url)
	input = browser.find_element_by_class_name('zu-top-add-question')
	print(input.text)

**获取ID，位置，标签名**  
id  
location  
tag_name  
size

	from selenium import webdriver
	
	browser = webdriver.Chrome()
	url = 'https://www.zhihu.com/explore' browser.get(url)
	input = browser.find_element_by_class_name('zu-top-add-question') 
	print(input.id) 
	print(input.location) 
	print(input.tag_name) 
	print(input.size)


#### 浏览器的前进和后退

back()  后退

forward()  前进

	import time from selenium import webdriver
	
	browser = webdriver.Chrome()
	browser.get('https://www.baidu.com/')
	browser.get('https://www.taobao.com/')
	browser.get('https://www.hao123.com/')
	browser.back() #后退
	time.sleep(1)
	browser.forward()# 前进
	browser.close()

#### cookie操作

	get_cookies()  
	delete_all_cookes()  
	add_cookie()
	
	from selenium import webdriver
	
	browser = webdriver.Chrome()
	browser.get('https://www.zhihu.com/explore') 
	print(browser.get_cookies())
	browser.add_cookie({'name': 'name', 'domain': 'www.zhihu.com', 'value': 'zhaofan'}) 
	print(browser.get_cookies())
	browser.delete_all_cookies() print(browser.get_cookies())

#### 选项卡管理

	import time
	from selenium import webdriver
	
	browser = webdriver.Chrome()
	browser.get('https://www.baidu.com')
	browser.execute_script('window.open()')#打开新窗口
	print(browser.window_handles)#输出窗口信息
	browser.switch_to.window(browser.window_handles[1])#切换窗口
	browser.get('https://www.taobao.com')#在当前窗口打开新页面
	time.sleep(1)
	browser.switch_to.window(browser.window_handles[0])#切换窗口

	browser.close()#多标签页下  关闭当前标签页  只有一个标签则关闭并退出浏览器
	browser.quit()#退出浏览器

#### 异常处理

这里的异常比较复杂，官网的参考地址：  
[http://selenium-python.readthedocs.io/api.html#module-selenium.common.exceptions](http://selenium-python.readthedocs.io/api.html#module-selenium.common.exceptions)  
这里只进行简单的演示，查找一个不存在的元素
	
	from selenium import webdriver 
	from selenium.common.exceptions 
	import TimeoutException, NoSuchElementException
	
	browser = webdriver.Chrome() try:
	    browser.get('https://www.baidu.com') 
	except TimeoutException: 
	print('Time Out') 
	try:
	    browser.find_element_by_id('hello') 
	except NoSuchElementException: 
		print('No Element') 
	finally:
	    browser.close()

