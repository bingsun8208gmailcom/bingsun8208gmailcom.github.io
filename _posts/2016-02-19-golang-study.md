---
layout: post
title: Go语言入门
categories: [IT]
tags: [golang]
fullview: true
---

# GO语言介绍

Go语言是谷歌2009发布的第二款开源编程语言。
Go语言专门针对多处理器系统应用程序的编程进行了优化，使用Go编译的程序可以媲美C或C++代码的速度，而且更加安全、支持并行进程。

# 安装

Go语言官网为[www.golang.org](http://www.golang.org)，不过由于网络原因（你懂的），我们无法正常访问，不过好在国内有众多Go语言爱好者，因此可以在墙内下载[www.golangtc.com](http://www.golangtc.com)。
根据不同平台，下载对应版本。安装完成后，配置GOROOT和GOPATH，注意，GOROOT为Go语言安装路径。如：

    windows:      c:\go
    linux:        /usr/local/go

GOPATH为Go源码所在路径。注意GOROOT和GOPATH的路径一定不能相同。

# Hello World

    package main
    
    import "fmt"
    
    func main() {
        fmt.Println("Hello World")
    }

每个Go源文件开头都有一个package声明语句，指明源文件所在的包。同时，我们也可以根据具体的需要 来选择导入(import语句)特定功能的包。在这个例子中，我们通过导入fmt包来使用我们熟悉的printf函数。 不过在Go语言中，Printf函数的是大写字母开头，并且以fmt包名作为前缀：fmt.Printf。

关键字func用于定义函数。在所有初始化完成后，程序从main包中的main函数开始执行。

常量字符串可以包含Unicode字符，采用UTF-8编码。实际上，所有的Go语言源文件都采用UTF-8编码。

代码注释的方式和C++类似：

          /* ... */
          // ...
稍后，我们还有很多的关于打印的话题。

# 编译
打开终端，定位到源码所在目录，运行以下命令

    go build helloworld.go
    go run helloworld.go
    helloworld

结果为：

    Hello World