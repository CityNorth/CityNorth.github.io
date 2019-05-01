---
title: hexo入门
date: 2019-04-28 21:40:30
tags: "hexo"
cover: true
summary: 梳理搭建流程，细数自己踩过的坑，如果能帮到你，最好不过了。
categories: "其他"
---

## 说在前面
* 其实早在之前刚接触HTML的时候，我就一直想搭建一个属于自己的博客，但由于种种原因一直没有去学习这方面的知识，最近一周和一个朋友讲到，所以就坚定下来搭好这个博客。从开始到搭建完成的过程中踩过很多坑，因为在这之前对Github一点了解较少，靠着搜素框，看着各个大佬的教程，不断的跳进一个又一个坑，但最后还是搭建好了。
### 那么为什么要搭建自己的博客？ [为什么你要写博客？—陈素封](https://zhuanlan.zhihu.com/p/19743861?columnSlug=cnfeat)
1. 重新认识自己
2. 提供持续学习的动力
3. 积累更多知识
4. 提高将事情将清楚的能力
5. 分享带来的连锁反应
6. 找到志同道合的人
7. 记录成长
8. 培养持续做一件事情的能力
9. 讨论反思
10. 搜寻到你意想不到东西
11. 一个人在做一件属于自己的事
### 以上11件肯定可以实现一半以上     fighting!
## 1. 开始搭建
	
* 参考：[我是如何利用Github Pages搭建起我的博客，细数一路的坑](https://www.cnblogs.com/jackyroc/p/7681938.html)

* 参考：[傻瓜都可以利用github pages建博客](http://cyzus.github.io/2015/06/21/github-build-blog/)  



----------
1. 前期工作
	* 了解github，注册号github账号。
	* 在自己的账号下面创建一个 **XX**.github.io **XX**为你的名字。
	* 建完仓库后，在当前页面右边选择Settings，进入设置页面，在这里生成你的github pages。随便选择一个模板（后面会改）。
	* 预览页面 在浏览器中输入  **XX**.github.io，这样就进入了你的博客页面。


2. 下载安装一些使用到的软件  


下载安装github   


- [https://windows.github.com/](https://desktop.github.com/)  
- [https://www.git-scm.com/downloads](https://www.git-scm.com/downloads)

>个人习惯这两个搭配上一起用，更好管理。

下载安装node  
  
- [https://nodejs.org/en/download/](https://nodejs.org/en/download/)   


下载安装Hexo 

- 在你要安装Hexo的目录下 （新建文件夹）右键 Git Bash

    	npm install hexo-cli -g   
		hexo init #初始化网站 
		npm install 
		hexo g #生成或 hexo generate  
		hexo s #启动本地服务器 或者 hexo server,这一步之后就可以通过http://localhost:4000  查看了

## 2. 安装主题
 
1. 先清空之前的缓存  
	`hexo clean`  
2. 拷贝一份主题到本地  
    `git clone https://github.com/blinkfox/hexo-theme-matery.git`  
3. 切换主题  
	修改 Hexo 根目录下的 _config.yml 的 theme 的值：theme: hexo-theme-matery  
4. 更新主题  
    `hexo g`  
	`hexo s`
>此时刷新http://localhost:4000/页面就能看到新的主题了

## 3. 部署到github 
1. 编辑更目录下_config.yml文件
 
    	deploy:
    		type: git
    		repo: git@github.com:XX/XX.github.io.git  #这里的网址填你自己的
    		branch: master
 	> 此处有大坑，每个：必须有一个空格，所有编辑_config.yml文件内 冒号后必须有空格。

 	保存后安装一个扩展：  

 	`npm install hexo-deployer-git --save` 

2. 使用SSH Keys的设置  
 
    	ssh-keygen -t rsa -C "邮件地址@youremail.com" #生成新的key文件,邮箱地址填你的Github地址   
    	#Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车就好>   
    	#接下来会让你输入密码  
3. 添加SSH Key到Github

	进入github首页-->头像（Settings）--> 添加SSH Key-->New SSH Key
	
	找到 系统当前用户目录下(开启查看隐藏文件)
	.ssh id_rsa.pub文件以文本方式打开。打开之后全部复制到key中
	Title 随便写个标记
	完成后就可以测试一下是否成功  

		ssh -T git@github.com
		#看到successfully就便是成功了
4. 上传到github

    `hexo d`  
	这时再刷新 XX.github.io 就可以看到你的博客了
## 4. 多台电脑更新博客
1. 原理  
	>利用git分支实现  
	hexo生成的静态博客文件默认放在master分支上。
	hexo的源文件（部署环境文件）可以都放在hexo分支上（可以新创建一个hexo分支），换新电脑时，直接git clone hexo分支（git@github.com:XX/XX.github.io.git）即可。  

2. 实现流程  
	1. 对username.github.io仓库新建hexo分支，并克隆   
		>在Github的username.github.io仓库上新建一个xxx分支，并切换到该分支，并在该仓库->Settings->Branches->Default branch中将默认分支设为hexo，save保存；然后将该仓库克隆到本地，进入该XX.github.io文件目录  
	
	2. 完成上面步骤后，在当前目录使用Git Bash执行git branch命令查看当前所在分支，应为新建的分支hexo：  
	
		 	 $git branch   
		 	 *hexo  
	3. 将本地博客的部署文件拷贝进xx.github.io文件目录

	进入xx.github.io文件目录下，将该目录下的全部文件提交hexo分支，提交之前需注意：
	
		>将themes目录以内中的主题的.git目录删除（如果有），因为一个git仓库中不能包含另一个git仓库，提交主题文件夹会失败。  

3. 提交hexo分支

		使用GitHub Desktop 
		点击 commit to hexo  
		点击 pull origin 
		这样就将博客的hexo部署环境提交到GitHub个人仓库的hexo分支

	现在可以在GitHub上的username.github.io仓库看到两个分支的差异了。  
		
	> master分支和hexo分支各自保存着一个版本，master分支用于保存博客静态资源，提供博客页面供人访问；hexo分支用于备份博客部署文件，供自己维护更新，两者在一个GitHub仓库内互不冲突，完美！

4. 在新电脑上编辑博客
	>* 将新电脑的生成的ssh key添加到GitHub账户上  
	>* 在新电脑上克隆username.github.io仓库的hexo分支到本地，此时本地git仓库处于hexo分支
	>* 切换到username.github.io目录，执行npm install(由于仓库有一个.gitignore文件，里面默认是忽略掉  node_modules文件夹的，也就是说仓库的hexo分支并没有存储该目录[也不需要]，所以需要install下)  
	>`nmp install`

	注意： 每次换电脑进行博客更新时，不管上次在其他电脑有没有更新，最好先  
   	`git pull`

我一般就是使用 GitHub Desktop 来维护博客部署文件，Git Bash 来更新博客。
这样就基本完成了，当然还有一些坑没填，后期会慢慢写到。

