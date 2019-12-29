// songguoqiang 2019.12.26
1. golang select是随机的还是顺序的

   随机的

2. golang局部变量是分配在堆上还是栈上

   golang编译器会做逃逸分析，如果变量的作用域没有逃出函数范围，则分配在栈上，否则分配在堆上

3. golang中make和new的区别

   new(T)是为一个T类型分配空间，并将此空间初始化为T的零值，返回这块内存空间的地址，也就是*T;

   make(T)返回的是初始化之后的T，而且T的类型只能为slice map chan这三种类型

4. 对golang中的nil的理解

   nil是golang中pointer,pointer, channel, func, interface, map, slice类型的零值的字面量表示。下面列出有关nil的各种事实和细节

   + golng中的nil是一个预定义标识符

     可以直接使用nil而不用声明

   + nil不是默认类型

     golang中的每个其他预定义标识符都有一个默认类型，比如：

     - ture和false的默认类型为bool类型

     - iota的默认类型是int

     但是nil没有默认类型，编译器会从上下文中推导出nil的类型

     ```go
     	var _ *struct{} = nil
     	var _ []int = nil
     	var _ map[string]int = nil
     	var _ chan string = nil
     	var _ func() = nil
     	var _ interface{} = nil
     ```

   + golang中的nil不是一个关键字

     预定义的nil可以被覆盖

     ```go
     package main
     
     import (
     	"fmt"
     )
     
     
     func main() {
     	nil := 123
     	fmt.Printf("%v", nil)
     }
     ```

   + 不同类型的nil值的size可能不一样

     ```go
     package main
     
     import (
     	"fmt"
     	"unsafe"
     )
     
     func main() {
     	var p *struct{} = nil // 8
     	fmt.Println(unsafe.Sizeof(p))
     
     	var s []int = nil // 24
     	fmt.Println(unsafe.Sizeof(s))
     
     	var m map[int]int = nil // 8
     	fmt.Println(unsafe.Sizeof(m))
     }
     ```

     大小是编译器和架构相关的。

5. 如何获取 golang程序运行时的协程数量, gc 时间, 对象数, 堆栈信息

   调用runtime.ReadMemStats可以获得信息，但此接口会触发STW(Stop The World)

6. 一般怎么调试 golang 的 bug 以及性能问题的

   - panic调用栈来捕获panic信息
   - pprof工具性能优化
   - 火焰图
   - go build -race来进行竞争检测
   - 查看系统 磁盘IO/网络IO/内存占用/CPU占用

   

   

   

   

   

   

   

   
