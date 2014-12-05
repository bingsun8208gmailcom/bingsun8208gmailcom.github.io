---
layout: post
title: Python异常处理
categories: [IT, Python]
tags: [Python]
fullview: true
---

一个典型的Python错误处理语句：

	#!/usr/bin/python

	import traceback
	try:
	    1/0
	except Exception as e:
	    print e

#一：try语句

##1 使用try和except语句来捕获异常

	try:
	    block
	except [exception,[data…]]:
	    block

	try:
	    block
	except [exception,[data...]]:
	    block
	else:
	    block

该种异常处理语法的规则是：

·   执行try下的语句，如果引发异常，则执行过程会跳到第一个except语句。

·   如果第一个except中定义的异常与引发的异常匹配，则执行该except中的语句。

·   如果引发的异常不匹配第一个except，则会搜索第二个except，允许编写的except数量没有限制。

·   如果所有的except都不匹配，则异常会传递到下一个调用本代码的最高层try代码中。

·   如果没有发生异常，则执行else块代码。

例:

	try:
	    f = open(“file.txt”,”r”)
	except IOError, e:
	    print e

捕获到的IOError错误的详细原因会被放置在对象e中,然后运行该异常的except代码块

捕获所有的异常

	try:
	    a=b
	    b=c
	except Exception,ex:
	    print Exception,":",ex

使用except子句需要注意的事情，就是多个except子句截获异常时，如果各个异常类之间具有继承关系，则子类应该写在前面，否则父类将会直接截获子类异常。放在后面的子类异常也就不会执行到了。

##2 使用try跟finally:

语法如下:

	try:
	    block
	finally:
	    block

该语句的执行规则是：

·   执行try下的代码。

·   如果发生异常，在该异常传递到下一级try时，执行finally中的代码。

·   如果没有发生异常，则执行finally中的代码。

第二种try语法在无论有没有发生异常都要执行代码的情况下是很有用的。例如我们在python中打开一个文件进行读写操作，我在操作过程中不管是否出现异常，最终都是要把该文件关闭的。

这两种形式相互冲突，使用了一种就不允许使用另一种，而功能又各异

#二：用raise语句手工引发一个异常

	raise [exception[,data]]

在Python中，要想引发异常，最简单的形式就是输入关键字raise，后跟要引发的异常的名称。异常名称标识出具体的类：Python异常是那些类的对象。执行raise语句时，Python会创建指定的异常类的一个对象。raise语句还可指定对异常对象进行初始化的参数。为此，请在异常类的名称后添加一个逗号以及指定的参数（或者由参数构成的一个元组）。

例:

	try:
	    raise MyError #自己抛出一个异常
	except MyError:
	    print 'a error'

	raise ValueError,’invalid argument’

捕捉到的内容为:

	type = VauleError
	message = invalid argument

#三：采用traceback(跟踪)模块查看异常

发生异常时，Python能“记住”引发的异常以及程序的当前状态。Python还维护着traceback（跟踪）对象，其中含有异常发生时与函数调用堆栈有关的信息。记住，异常可能在一系列嵌套较深的函数调用中引发。程序调用每个函数时，Python会在“函数调用堆栈”的起始处插入函数名。一旦异常被引发，Python会搜索一个相应的异常处理程序。如果当前函数中没有异常处理程序，当前函数会终止执行，Python会搜索当前函数的调用函数，并以此类推，直到发现匹配的异常处理程序，或者Python抵达主程序为止。这一查找合适的异常处理程序的过程就称为“堆栈辗转开解”（Stack Unwinding）。解释器一方面维护着与放置堆栈中的函数有关的信息，另一方面也维护着与已从堆栈中“辗转开解”的函数有关的信息。

格式:

	try:
	    block
	except:
	    traceback.print_exc()

