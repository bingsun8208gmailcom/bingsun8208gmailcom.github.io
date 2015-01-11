---
layout: post
title: Objective-C 语法简介
categories: [IT, Objective-C]
tags: [Objective-C]
fullview: true
---

# 概述

Objective-C，通常写作ObjC和较少用的Objective C或Obj-C，是扩充C的面向对象编程语言。它主要使用于Mac OS X和GNUstep这两个使用OpenStep标准的系统，而在NeXTSTEP和OpenStep中它更是基本语言。

# 简明概述

* 开始学习前，假设你已经具备了一些C语言的基础知识，包括变量类型、函数、返回值、以及指针的相关概念。
* Objective-C，是 C 的衍生体，继承了所有 C 语言的特性。是有一些例外，但是它们不是继承于 C 的语言特性本身。
* nil：在 C/C++ 你或许曾使用过 NULL，而在 Objective-C 中则是 nil。不同之处是你可以传递消息给 nil（例如 [nil message];），这是完全合法的，然而你却不能对 NULL 如法炮制，由于nil是一个Objective-C类对象的引用类型（即id类型），而NULL在C语言中通常被定义为(void*)0，因而并不是一个Objective-C类对象的引用。
* BOOL：C没有正式的布尔类型，而在 Objective-C 中也不是「真的」有。它是包含在 Foundation classes（基本类别库）中（即 import NSObject.h；nil 也是包括在这个标头档内）。BOOL 在 Objective-C 中有两种型态：YES 或 NO，而不是 TRUE 或 FALSE。
* \#import vs \#include：就如同你在 hello world 范例中看到的，我们使用了 \#import。\#import 由 gcc 编译器支援。我并不建议使用 \#include，\#import 基本上跟 .h 档头尾的 \#ifndef \#define \#endif 相同。许多程式员们都同意，使用这些东西这是十分愚蠢的。无论如何，使用 \#import 就对了。


#Hello World

## hello.m
	
	#import <Foundation/Foundation.h>

	int main( int argc, const char *argv[] ) {
		NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		NSLog( @"hello world" );
		[pool drain];
		return 0;
	}

## 输出
	
	hello world

* 在Objective-C中使用 \#import 代替 \#include 
* Objective-C的代码文件使用.m后缀
* NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init]; 代表程序将在缓存池里预留内存空间， [pool drain]; 表示释放内存空间。
* NSLog具有自动换行功能，因此不需要\n

# 类

## 示例

### Fraction.h

	#import <Foundation/Foundation.h>
	@interface Fraction : NSObject {
		int numerator;
		int denominator;
	}

	- (void) print;
	- (void) setNumberator : (int) n;
	- (void) setDenominator : (int) d;
	- (int) numerator;
	- (int) denominator;

	@end

### Fraction.m

	#import "Fraction.h"

	@implementation Fraction 

	- (void) print {
		NSLog(@"%i/%i", numerator, denominator);
	}

	- (void) setNumberator : (int) n {
		numerator = n;
	}
	- (void) setDenominator : (int) d {
		denominator = d;
	}
	- (int) numerator {
		return numerator;
	}
	- (int) denominator {
		return denominator;
	}

	@end

* NSObject是Objective-C中所有类的基类，它位于类继承链的最顶端，等同于C#中的Object。
* 夹在 @interface Fraction : NSObject { ... } 中的被称为实例变量(instance variables)。
* 没有设定存取权限（protected, private, public)时，默认权限为 protected 。
* instance methods 以 - 开头（等同于C#的成员函数），class level methods 以 + 开头（等同于C#的static静态函数）。
* 类(@interface)以 @end 作为结束符。
* 在.m文件中，使用@implementation修饰符来实现.h文件中定义的类。

## 合成存储器方法

前例中，Fraction类中numerator,denominator分别手工设置了getter和setter，

	#import <Foundation/Foundation.h>
	@interface Fraction : NSObject {
		int numerator;
		int denominator;
	}

	- (void) print;
	- (void) setNumberator : (int) n;
	- (void) setDenominator : (int) d;
	- (int) numerator;
	- (int) denominator;

	@end

考虑改进方法，

	// Fraction.h
	#import <Foundation/Foundation.h>
	@interface Fraction : NSObject {
		int numerator;
		int denominator;
	}

	@property int numerator, denominator;
	- (void) print;

	@end

	// Fraction.m

	@implementation Fraction
	
	@synthesize numerator, denominator;

	- (void) print {
		NSLog(@"%i/%i", numerator, denominator);
	}

	@end

其中@property int numerator, denominator;是为类Fraction定义两个实例变量numerator, denominator；
@synthesize则是告诉编译器要为numerator, denominator自动生成getter，setter方法。