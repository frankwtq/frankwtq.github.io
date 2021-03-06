---
layout: post
title: Linux基础学习笔记2 Shell
category : 学习笔记
tags: [Linux]
stickie: true
---


#Linux基础学习笔记2 Shelll

这是Linux基础学习笔记的第二部分，主要介绍Shell。上一部分为[Linux基础学习笔记1](https://frankwtq.github.io/%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/2017/04/16/Linux%E5%9F%BA%E7%A1%80%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B01.html)
## 参考资料
* 主要为视频资料：[慕课网](http://www.imooc.com/course/list?c=linux)
* 辅助书籍：**Linux从入门到精通**（刘忆智 清华大学出版社）
  
## Shell概述  
* shell是一个命令行解释器，他为用户提供一个Linux内核发送请求以便运行程序的界面系统及程序，用户可以用Shell来启动、挂起、停止甚至是编写一些程序。
* Shell还是一个功能相当强大的编程语言，易编写，易调试，灵活性强。Shell是解释执行的脚本语言，在Shell中可以直接调用Linux系统命令
* Shell的两种主要语法类型有Bourne和C，彼此不兼容。Bourne包括：sh、ksh、Bash、psh、zsh；C主要包括：csh、tcsh。我们常使用的是Bash
* /etc/shells文件中记录了能使用的shell  

## 脚本执行方式
### echo输出命令 
  
	echo [选项] [输出内容]
		-e	支持反斜杠控制的字符转换
	\a	输出警告音
	\b	退格键，就是向左删除键
	\n	换行符
	\r	回车键
	\t	制表符，就是Tab键
	\v	垂直制表符
	\0nnn	按照八进制ASCII码表输出字符
	\xhh	按照十六进制ASCII码表输出字符
  
### 第一个脚本
  
	vim hello.sh
	#!/bin/Bash
	#The first program
	
	echo -e "\e[1;34m 天上掉下个林妹妹! \e[0m"
  
### 脚本执行
* 赋予执行权限，直接运行  
  
<pre>
chomd 755 hello.sh
./hello.sh
</pre>
* 通过Bash调用执行
	
<pre>
bash hello.sh
</pre>  
## Bash的基本功能  
### 命令别名与快捷键
查看与设定别名
  
	alias
		查看系统中所有的命令别名
	alias 别名= ‘原命令’
		设定命令别名  
  
别名永久生效与删除别名  
  
	vi ~/.bashrc
		写入环境变量配置文件
	source .bashrc
		重新载入环境变量配置文件，使其立马生效
	unalias 别名
		删除别名  
  
### 历史命令
  
	history [选项] [历史命令保存文件]
		-c	清空历史命令
		-w	把缓存中的历史命令写入历史命令保存文件~/.bash_history
		历史命令默认会保存1000条，可以在环境变量配置文件/etc/profile中进行修改
历史命令的调用  
  
* 使用上、下箭头调用以前的历史命令
* 使用"!n"重复执行第n条历史命令
* 使用"!!"重复执行上一条命令
* 使用"!字串"重复执行最后一条以该字串开头的命令
 
### 输出重定向
标准输入输出(stdin stdout stderr)  
  

|  设备  |设备文件名|文件描述符|类型|
|:---:|:---:|:----:|:-------:|
|键盘|/dev/stdin|0|标准输入|
|显示器|/dev/stdout|1|标准输出|
|显示器|/dev/stderr|2|标准错误输出|
  
---

输出重定向
  
	命令 > 文件
	命令 >> 文件
	错误命令 2> 文件
	错误命令 2>> 文件  

* ```>``` 表示以覆盖的方式
* ```>>``` 表示以追加的方式
* ```>```和```>>```表示命令运行正确时输出
* ```2>```和```2>>```表示命令运行错误时输出  
  
---

	命令 > 文件 2>&1
	命令 >> 文件 2>&1
		# 重要，以追加的方式，把正确输出和错误输出都保存到同一个文件中
	命令 &> 文件
	命令 &>> 文件
		# 重要，以追加的方式，把正确输出和错误输出都保存到同一个文件中
	命令 >> 文件1 2>> 文件2
		# 重要，把正确的输出追加到文件1中，把错误的输出追加到文件2中
  
输出重定向  
	
	wc [选项] [文件名]
		-c	统计字节数
		-w	统计单词数
		-l	统计行数
	命令 < 文件把文件作为命令的输入
		例如：wc < abc.log
	命令 << 标识符
		标识符把标识符之间内容作为命令的输入
		例如：wc << abc在后面输入任意字符串，当再次遇到abc时会停止输入并显示统计的结果	
  
### 多命令顺序执行
  
	命令1 : 命令2
		# 多个命令顺序执行，命令之间没有任何逻辑联系
	命令1 && 命令2
		# 逻辑与
		# 当命令1正确执行，则命令2才会执行
		# 当命令1执行不正确，则命令2不会执行
	命令1 || 命令2
		# 逻辑或
		# 当命令1执行不正确，命令2才会执行
		# 当命令1正确执行，命令2不会执行
  
例子：
	
	pwd；touch abc;ls;data
	ls anaconda-ks.cfg && echo yes  	#运行成功显示yes
	ls anaconda-ks.cfg || echo no  	#运行失败显示no
	命令 && echo yes || echo no	#运行成功显示yes，运行失败显示no

管道符
	
	命令1 | 命令2
		命令1的正确输入作为命令2的操作对象
		例如：
			ll –a /etc/ | more
			netstat –an | grep ESTABLISHED | wc -l  
 
  
### Shell中特殊符号
通配符
	
	?	匹配一个任意字符
	*	匹配0个或者任意多个任意字符
	[]	匹配中括号中任意一个字符如：[abc]代表一定匹配一个字符，可以是a，可以是b也可以是c
	[-]	匹配中括号中任意一个字符，-代表一个范围如：[a-z]
	[*]	逻辑非，表示匹配不是中括号内的一个字符。例如[^0-9]代表匹配一个不是数字的字符
  
Bash中其他特殊符号 
  
	''	单引号，单引号中的所有的特殊符号，如$和`(反引号)都没有特殊含义
	""	双引号，双引号中的特殊符号都没有特殊含义，但是$、`和\是例外，拥有调用变量的值、引用命令和转义符的特殊含义
	``	反引号，反引号括起来的内容是系统命令，在Bash中会先执行它。和$()作用一样，不过推荐使用$(),因为反引号非常容易看错
	$()	引用系统命令
	#	在Shell脚本中，#开头的行代表注释
	$	用于调用变量的值，如需要调用变量name的值时，用$name的方式得到
	\	转义符，跟在\之后的特殊符号将失去特殊含义
  
例如：
	
	aa=123;echo $aa
		输出：123
	echo ‘$aa’
		输出：$aa
	echo “$aa”
		输出：123
	aa=`ls`	#反引号 
	echo “$aa”
		输出：执行ls的结果
	aa=$(ls)	#作用同反引号
