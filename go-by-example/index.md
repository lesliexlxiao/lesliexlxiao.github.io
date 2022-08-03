# Go by Example 题目


本文主要是将 Go by Exmaple 中的示例转换成题目描述便于熟悉 Golang 语法。

### Hello World
文件名：01-hello-world.go

题目描述：输出 "hello world" 字符串

### 值
文件名：02-values.go

题目表述：

- 输出两个字符串相加的结果

- 输出两个整型相加的结果

- 输出两个浮点型相除的结果

- 输出 bool 型并的结果

### 变量
文件名：03-variables.go

题目表述：

- 给 a 赋值字符串，输出结果

- 同时给整型 b c 赋值，输出结果

- 声明并初始化字符串变量 f，输出结果


### 常量
文件名：04-contants.go

题目表述：

- 给常量字符串 s 赋值，输出结果


### For 循环
文件名：05-for.go

题目描述：
- 单个循环条件，输出 1 2 3

- 初始/条件/后续 for 循环，输出 1 2 3

- 不带条件的 for 循环将一直重复执行，直到在循环体内使用了 break 或者 return 跳出循环

- continue 使用

### If/Else 分支
文件名：06-if-else.go

题目描述：
- num 值为 9。如果小于 0，输出 "is negative"；如果大于 0，输出 "is positive"; 其他，输出 "equal 0"

### Switch 分支结构
文件名：07-switch.go

题目描述：
- i 值为 2。通过 switch 判断，如果为 1，输出 1；如果为 2，输出 2；如果为 3；输出 3。

- 使用 switch 模拟 If/Else 分支 逻辑。num 值为 9。如果小于 0，输出 "is negative"；如果大于 0，输出 "is positive"; 其他，输出 "equal 0"。

- 使用 switch 判定传递 interface 类型。如果 bool，输出 "I'm a bool"；如果 int，输出 "I'm an int"；其他，输出 "Don't know type + 真正的类型"。

### 数组
文件名：08-arrays.go

题目描述：
- 创建长度为 5 的空数组 a，输出 a 的结果。给第 5 个元素赋值 10，输出结果。

- 初始化长度为 5 的数组 吧，初始值为 1 2 3 4 5。

### 切片
文件名：09-slice.go

题目描述：
- 创建长度为 3 的空切片 s，输出 s。

- 给 s 赋值 a b c 三个值，输出第三个元素的值。

- 输出 s 的长度。

- 给 s 添加两个元素 e f，再次输出 s。

- 创建切片 c，长度为 s 的长度；把 s 的值 copy 到 c 中，输出 c。

- 输出 s[0] 到 s[5]（不包含 5）的元素。

- 输出包含从 s[2]（包含 2）之后的元素。

- 初始化切片 t，初始化值为 "g"，"h"，"i"，输出 t 的值。

### Map
文件名：10-map.go

题目描述：
- 创建一个空 map m，key 为 string 类型，值为 string 类型；赋值两个元素，k1 为 7，k2 为 13；输出 m 的值。

- 输出 m 的长度。

- 删除 k2，输出 m。

- 判断 m 是否包含 k3，如果有输出 "exist k3"；如果不存在，输出 "not exist k3"。

- 初始化 map n。包含两个值 "foo" = 1，"bar" = 2，输出 n。

### Range 遍历
文件名：11-range.go

题目描述：

- 初始化切片 nums，包含 2 3 4 三个元素，计算总和，输出结果。

- 遍历 nums，如果值为 3，输出它的下标。

- 初始化 map n。包含两个值 "a" = "apple"，"b" = "banana"，遍历 n，输出键值对。

- 遍历 map n，只输出 key 的值。

- 遍历字符串 "golang"，输出下标和值。

### 函数
文件名：12-functions.go

题目描述：
- 函数接受两个 int 类型的数据，返回他们的和

- 函数接受三个 int 类型的数据，返回他们的和

### 多返回值
文件名：13-multiple-return-values.go

题目描述：
- 定义一个返回两个 int 类型的函数 vals，返回值为 3，7

- 对上述函数执行多赋值操作，打印相应的值

### 变参函数
文件名：14-variadic-functions.go

题目描述：
- 定义一个函数 sum 接受任意数量的 int 作为参数，计算这些数值的总和

- 传递 1 2 3 给 sum 作为参数

- 传递一个 slice 给 sum 作为参数

### 闭包
文件名：15-closures.go

### 递归
文件名：16-recursion.go

题目描述：
- 递归求解 n 阶层

### 指针
文件名：17-pointers.go

题目描述：
- 定义 zeroval 函数，接受整型变量 ival，并赋值 0

- 定义 zeroptr 函数，接受整型变量指针 ival，并赋值 0

- main 函数定义变量 i，把值赋值给 zeroval 和 zeroptr，看看 i 值的变化

### 字符串和 rune 类型
文件名：18-strings-and-runes.go

### 结构体
文件名：19-structs.go

题目描述：
- 定义 person 结构体包含了 name 和 age 两个字段，name string 类型，age 字符串类型

- 初始化结构体，打印 name 的值

### 方法
文件名：20-methods.go

题目描述：
- 给上述结构体定义一个 output 方法，输出 name 和 age 信息

### 接口
文件名：21-interfaces.go

题目描述：
- 定义 interface animal，定义方法 say()，然后定义两个结构体 cat 和 dog，并实现 interface 中的方法

### Embedding
文件名：22-embedding.go

题目描述：
- 定义 base 结构体，里面有 num int 属性，定义结构体方法 describe，打印 num 的值；定义 container 结构体，嵌入 base 结构体。

### 泛型
文件名：
