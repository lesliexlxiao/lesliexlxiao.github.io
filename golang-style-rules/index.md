# Golang 开发规范


本文主要介绍了 golang 语言开发中的一些规范。


## 1. 声明语句的规范化
我们在编写 golang 程序的时候，通常涉及到的内容声明语句包括 package、import、func、var、const、type 等。<font color=#FF0099>**import 声明是必须跟在文件的 package 声明之后的</font>，**而 func、var、const、type 等声明语句的顺序并不重要，但我们最好还是定一下规范，这样<font color=#FF0099>**有助于统一代码风格、提高代码的可读性**</font>。个人的内容声明语句风格如下：


```go
package main

import "fmt"

type Person struct {
    name string
}

const constant string = "constant"

var v string = "var"

func main() {
    p := Person{name: "xlxiao"}
    fmt.Println(p.name)

    fmt.Println(constant)

    fmt.Println(v)
}
```

## 2. go fmt 的使用
单个文件格式化
```shell
$ go fmt hello.go
```

目录代码格式化
```shell
$ go fmt ./directory/
```
- 上述命令只能格式化 directory 目录下的 go 文件，并不能格式化整个项目的 go 文件。


项目格式化，如果项目的 module 名字为 github.com/lesliexlxiao/golang-test，那么格式化语句如下：
```
$ go fmt github.com/lesliexlxiao/golang-test/...
```

## 3. 参考文章
[1] Alan A.A.Donovan, Brian W.Kernighan.Go 语言圣经.p20.

[2] My_Fuzz.Golang 编码规范.https://www.jianshu.com/p/1f0ded986f28.
