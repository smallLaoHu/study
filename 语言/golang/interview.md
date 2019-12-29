1. defer执行顺：

defer执行顺序是先进后出。在协程遇到panic时，会遍历本协程的defer链表，并执行defer。在遇到recover时，则停止Panic，返回recover处继续向下执行。如果没有遇到recover，遍历完本协程的defer链表，向stderr抛出panic信息。

2. 下面代码有什么问题

```go
type student struct {
    Name string
    Age  int
}

func pase_student() {
    m := make(map[string]*student)
    stus := []student{
        {Name: "zhou", Age: 24},
        {Name: "li", Age: 23},
        {Name: "wang", Age: 22},
    }
    for _, stu := range stus {
        m[stu.Name] = &stu
    }

}
```

m中的值都一样，正确的写法为：

```go
for i := 0; i < len(stus); i++ {
		m[stus[i].Name] = &stus[i]
}
```

3. 下面的代码会输出什么

```

```

```go
func main() {
    runtime.GOMAXPROCS(1)
    wg := sync.WaitGroup{}
    wg.Add(20)
    for i := 0; i < 10; i++ {
        go func() {
            fmt.Println("A: ", i)
            wg.Done()
        }()
    }
    for i := 0; i < 10; i++ {
        go func(i int) {
            fmt.Println("B: ", i)
            wg.Done()
        }(i)
    }
    wg.Wait()
}
```

第一个循环，是一个闭包（函数+引用环境），输出完全随机，取决于goroutine执行的i是多少；

第二个循环，因为P的个数为1，而且代码执行时间很低，所以输出为0-9的顺序输出，如果更改P的数目，输出就可能是0-9的随机输出。

4. 下面代码能编译通过吗

```go
package main

import (
	"fmt"
)

type People interface {
	Speak(string) string
}

type Stduent struct{}

func (stu *Stduent) Speak(think string) (talk string) {
	if think == "bitch" {
		talk = "You are a good boy"
	} else {
		talk = "hi"
	}
	return
}

func main() {
	var peo People = Stduent{}
	think := "bitch"
	fmt.Println(peo.Speak(think))
}
```

不能，Student的方法集没有实现接口的方法，应该改为

```go
var peo people = &Student{}
```

5. interface内部结构

```go
type eface struct {      //空接口
    _type *_type         //类型信息
    data  unsafe.Pointer //指向数据的指针(go语言中特殊的指针类型unsafe.Pointer类似于c语言中的void*)
}
type iface struct {      //带有方法的接口
    tab  *itab           //存储type信息还有结构实现方法的集合
    data unsafe.Pointer  //指向数据的指针(go语言中特殊的指针类型unsafe.Pointer类似于c语言中的void*)
}
type _type struct {
    size       uintptr  //类型大小
    ptrdata    uintptr  //前缀持有所有指针的内存大小
    hash       uint32   //数据hash值
    tflag      tflag
    align      uint8    //对齐
    fieldalign uint8    //嵌入结构体时的对齐
    kind       uint8    //kind 有些枚举值kind等于0是无效的
    alg        *typeAlg //函数指针数组，类型实现的所有方法
    gcdata    *byte
    str       nameOff
    ptrToThis typeOff
}
type itab struct {
    inter  *interfacetype  //接口类型
    _type  *_type          //结构类型
    link   *itab
    bad    int32
    inhash int32
    fun    [1]uintptr      //可变大小 方法集合
}
```