# Golang 空结构体妙用


本文主要介绍了 golang 语言中的空结构体及其使用场景。

## 1. 空结构体
空结构体的宽度是 0，占用了 0 字节的内存空间。

由于空结构体占用0字节，那么空结构体也不需要填充字节。所以空结构体组成的组合数据类型也不会占用内存空间。

示例：
	```go
	package main

	import (
	    "fmt"
	    "unsafe"
	)

	type S struct {
	    A struct{}
	    B struct{}
	}

	func main() {
	    var s struct{}
	    fmt.Println(unsafe.Sizeof(s))

	    var s1 S
	    fmt.Println(unsafe.Sizeof(s1))
	}
	```

## 2. chan struct{}
首先看下 go by example Ticker 代码示例：
```go
package main

import (
    "fmt"
    "time"
)

func main() {

    ticker := time.NewTicker(500 * time.Millisecond)
    done := make(chan bool)

    go func() {
        for {
            select {
            case <-done:
                return
            case t := <-ticker.C:
                fmt.Println("Tick at", t)
            }
        }
    }()

    time.Sleep(1600 * time.Millisecond)
    ticker.Stop()
    done <- true
    fmt.Println("Ticker stopped")
}
```

这里使用了 done := make(chan bool)，这并不是最优解，因为 bool 类型还是有大小的。这里可以使用 make(chan struct{}) 来控制定时器任务的结束。

使用空结构体 channel := make(chan struct{}) 好处：
- 省内存，尤其在事件通信的时候。
- struct 零值就是本身，读取 close 的 channel 返回零值。

优化后代码：
```go
package main

import (
    "fmt"
    "time"
)

func main() {

    ticker := time.NewTicker(500 * time.Millisecond)
    done := make(chan struct{})

    go func() {
        for {
            select {
            case <-done:
                return
            case t := <-ticker.C:
                fmt.Println("Tick at", t)
            }
        }
    }()

    time.Sleep(1600 * time.Millisecond)
    ticker.Stop()
    done <- struct{}{}
    fmt.Println("Ticker stopped")
}
```

## 3. 参考文献
[1] https://blog.csdn.net/inthat/article/details/106917358.

[2] https://gobyexample-cn.github.io/tickers
