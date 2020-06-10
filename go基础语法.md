#### 1. 变量/常量

#### 1.变量

```go
var name1 name2 type=value1 value2
name1 name2 := value1 value2  // 简化 这种形式只能在函数内部使用
var name = value // 省略type
var xx bool= value  // 布尔类型
```

#### 2. 常量

```go
const name type=value  // 常量不可修改
```

#### 3. 字符串

go中字符串是不可变的

```go
var s string = "hello"
s[0] = "c"  //报错：cannot assign to s[0] 
s[:2]//不可修改，但是可以切片，类似python
```

#### 4.错误类型

go内置有个error类型，专门用来处理错误信息，go的package中有errors包用来处理错误：

```go
err := errors.New("error info")
if err != nil{
  fmt.Println(err)
}
```

#### 5.iota枚举

`iota`  关键字用来声明`enum` 它默认开始值是0，const中每增加一行加1：

```go
package main

import (
	"fmt"
)

const (
	x = iota // x == 0
	y = iota // y == 1
	z = iota // z == 2
	w        // 常量声明省略值时，默认和之前一个值的字面相同。这里隐式地说w = iota，因此w == 3。其实上面y和z可同样不用"= iota"
)

const v = iota // 每遇到一个const关键字，iota就会重置，此时v == 0

const (
	h, i, j = iota, iota, iota //h=0,i=0,j=0 iota在同一行值相同
)

const (
	a       = iota //a=0
	b       = "B"
	c       = iota             //c=2
	d, e, f = iota, iota, iota //d=3,e=3,f=3
	g       = iota             //g = 4
)

func main() {
	fmt.Println(a, b, c, d, e, f, g, h, i, j, x, y, z, w, v)
}
```

#### 6.一些规则

* 大写字母开头的变量是可以导出的， 小写字母不可导出，是私有的
* 大写的函数相当于带有public，小写的不可导出，相当于带有private关键字

#### 7.array, slice, map

* array

```go
var arr [4] int
arr[0]=1
arr[2]=2

arr := [4] int {1, 2, 3}
```

由于长度也是数组类型的一部分，因此`[3]int`与`[4]int`是不同的类型，数组也就不能改变长度。数组之间的赋值是值的赋值，即当把一个数组作为参数传入函数的时候，传入的其实是该数组的副本，而不是它的指针。如果要使用指针，那么就需要用到后面介绍的`slice`类型了。

* slice

在很多场景中并不知道需要多大的数组，这时就用到slice类型， 即“动态数组”。在Go里面这种数据结构叫`slice` ，声明和数组一样， 只是并需要长度

```go
var fslice[] int
```

`slice`是引用类型，所以当引用改变其中元素的值时，其它的所有引用都会改变该值

* map

和python中的dict对应，声明方式：

```go
var numbers map[string]int  
numbers = make(map[string]int)   //第二种声明方式
```

