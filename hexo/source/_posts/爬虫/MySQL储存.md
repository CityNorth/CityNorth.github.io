---
title: MySQL储存
date: 2019-06-04 15:38:26
tags: 
	- "爬虫"
	- "Python"
summary: 用Python进行MySQL储存
cover: 
img: https://raw.githubusercontent.com/CityNorth/material/master/image/MYSQLchucun.png
categories: "爬虫"	
---


## 爬虫MYSQL储存

### 一、连接并创建数据库

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306)
	cursor = db.cursor()
	cursor.execute('SELECT VERSION()')
	data = cursor.fetchone()
	print('Database version:', data)
	cursor.execute("CREATE DATABASE spiders DEFAULT CHARACTER SET utf8")
	db.close()

执行结果：

	Database version: ('8.0.15',)

结果是创建一个名为spiders的数据库

### 二、创建数据表

注意：这次连接数据库时需要指定创建数据表所在的数据库，也就是db参数的值
	
	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	sql = 'CREATE TABLE IF NOT EXISTS students (id VARCHAR(255) NOT NULL, name VARCHAR(255) NOT NULL, age INT NOT NULL, PRIMARY KEY (id))'
	cursor.execute(sql)
	db.close()

### 三、插入一条数据

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	id = '20120001'
	user = 'Bob'
	age = 20
	
	sql = 'INSERT INTO students(id, name, age) values(%s, %s, %s)'
	try:
	    cursor.execute(sql, (id, user, age))
	    db.commit()
	except:
	    db.rollback()
	db.close()

**通用写法：**

推荐使用：这样一来，若是写入更多值的话直接给data字典增加数据就行了，就不用其他sql语句了

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	table = 'students'
	
	data = {
	    'id': '20120002',
	    'name': 'Bob11',
	    'age': 200
	}
	
	keys = ', '.join(data.keys())
	values = ', '.join(['%s'] * len(data))
	
	sql = 'INSERT INTO {table} ({keys}) VALUES ({values})'.format(table=table, keys=keys, values=values)
	try:
	    if cursor.execute(sql, tuple(data.values())):
	        print('Successful')
	        db.commit()
	except:
	    print('Failed')
	    db.rollback()
	db.close()

### 四、更新数据

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	sql = 'UPDATE students SET age = %s WHERE name = %s'
	try:
	   cursor.execute(sql, (25, 'Bob'))
	   db.commit()
	except:
	   db.rollback()
	db.close()

**通用写法：**

根据主键进行判断，若主键存在则更新，若不存在则插入，推荐使用

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	table = 'students'
	
	data = {
	    'id': '20120001',
	    'name': 'Bob',
	    'age': 21
	}
	
	keys = ', '.join(data.keys())
	values = ', '.join(['%s'] * len(data))
	
	sql = 'INSERT INTO {table}({keys}) VALUES ({values}) ON DUPLICATE KEY UPDATE'.format(table=table, keys=keys,
	                                                                                     values=values)
	update = ','.join([" {key} = %s".format(key=key) for key in data])
	sql += update
	try:
	    if cursor.execute(sql, tuple(data.values()) * 2):
	        print('Successful')
	        db.commit()
	except:
	    print('Failed')
	    db.rollback()
	db.close()

### 五、查询数据

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	sql = 'SELECT * FROM students WHERE age >= 20'
	try:
	    cursor.execute(sql)
	    print('Count:', cursor.rowcount)
	    row = cursor.fetchone()
	    while row:
	        print('Row:', row)
	        row = cursor.fetchone()
	except:
	    print('Error')

### 六、删除数据

	import pymysql
	
	db = pymysql.connect(host='localhost', user='root', password='123456', port=3306, db='spiders')
	cursor = db.cursor()
	
	table = 'students'
	condition = 'age > 20'
	
	sql = 'DELETE FROM  {table} WHERE {condition}'.format(table=table, condition=condition)
	try:
	    cursor.execute(sql)
	    db.commit()
	except:
	    db.rollback()
	
	db.close()


### 后记

在一般的生成环境中，通常是先在MYSQL中先建好表，再将数据一条一条的插入进去，下面为一些语句解释。
		
	import pymysql
	
	# 打开数据库连接        “地址      用户名    密码       数据库        编码”
	db = pymysql.connect("localhost", "root", "123456", "spiders", charset='utf8' )
	
	# 使用cursor()方法获取操作游标 
	cursor = db.cursor()
	
	# 使用execute方法执行SQL语句
	cursor.execute("SELECT VERSION()")
	
	# 使用 fetchone() 方法获取一条数据
	data = cursor.fetchone()
	
	print("Database version : %s " % data) 
	
	# 关闭数据库连接
	db.close()

[菜鸟教程](https://www.runoob.com/python3/python3-mysql.html)
