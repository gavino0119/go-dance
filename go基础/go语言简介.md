## 一、Go语言的特色

- 没有继承多态的OO
- 强一致类型
- interface不需要显示声明(Duck Typing)
- 没有异常处理(Error is value)
- 基于首字母的访问特性
- 不用的import或者变量引起编译错误
- 完整而卓越的标准库包



## 二、学习路线

## 三、

## 四、入门案例

### （一）、helloworld

```go
//定义了包名，必须在源文件中非注释的第一行指明这个文件属于哪个包
package main
//告诉go编译器这个程序需要使用fmt包，fmt包实现了格式化IO的函数
import "fmt"

//func main() 是程序入口
//main函数一般是启动后第一个执行的函数，如果有init()函数则会先执行init()函数
func main()  {
	/* CTRL+SHIFT+/  块注释*/
	fmt.Print("hello word！")
}
```

### （二）、编码规范

1. Go语言的空格

   > - Go 语言中变量的声明必须使用空格隔开，如 `var age int`
   > - 

2. 语句的结尾

   > - Go程序中，一行代表一个语句结束，不需要`;`结尾

3. 可见性原则

   > - Go语言中，使用大小写来决定标识符（）是否可以被外部包所调用。
   > - 以大写字母开头，如同面向对象语言中的`public`
   > - 以小写字母开头，如同面向对象语言中的`private`,对包外是不可见的。

4. d 

### （三）、打印输出格式化

- 通用
  - %v	v表示value,值的默认格式表示，**会将任意变量以易读的形式打印出来**
  - %T    T表示type,值的类型的Go语法表示,**打印变量的类型**
- 布尔值
  - %t    t表示true,单词true或false，即获取布尔值的值，此时效果和%v一样
- 整数
  - %b	b表示binary,表示为二进制
  - %c    c表示char,该值对应的unicode码值
  - %d    d表示digital，表示为十进制
  - %q    q表示quotation,
  - %x     表示为十六进制
  - %X     表示为十六进制
  - %U     表示为Unicode格式: 
- 浮点数与复数的两个组分
  - %F,%f	f表示float，等价于%.6f(=%.6f)即有6位小数部分，如123.456789
- 字符串和[]byte
  - %s	直接输出字符串或者 []byte  string,**对字符串原样输出，是不带""的输出**
  - %q   该值对应的双引号括起来的go语法字符串字面值，必要时会采用安全的转义表示，**输出的字符串带有""， 带双引号的字符串 "abc" 或 带单引号的 rune 'c'** 
  - %x   每个字节用两字符十六进制数表示(使用a-f)
  - %X   每个字节用两字符十六进制数表示(使用A-F)
- 指针
- 其它

**代码示例**

```go
package main

import "fmt"
/**
通过type关键词可定义一个结构体
 */
type student struct {
	x,y int
}
func main() {
	/**
	通用
	 */
	str := "gavino"
	//有多少个%,则相应有几个变量，而且所有的%是写到一个“”里面的
	fmt.Printf("%T","%v",str,str)//string%!(EXTRA string=gavino, string=gavino)string,gavino
	fmt.Printf("%T,%v\n",str,str)//string,gavino

	var a  rune = '一'
	fmt.Printf("%T,%v\n",a,a)//int32,19968

	s := student{1,2}
	fmt.Printf("%T,%v \n",s,s)//main.student,{1 2}

	/**
	布尔
	 */
	fmt.Printf("%T,%t \n",true,true)//bool,true

	/**
	整型
	 */
	fmt.Printf("%T,%d \n",123,123)//int,123
	fmt.Printf("%T,%d \n",123,123.234)//int,%!d(float64=123.234)
	//给定整型长度，不足时前面以空格补充
	fmt.Printf("%T,%5d \n",123,123)//int,  123
	//给定整型长度，不足时前面指定以0补充，等于或超过指定长度时则以实际为准
	fmt.Printf("%T,%05d \n",123,123)//int,00123
	fmt.Printf("%T,%05d \n",12345,12345)//int,12345
	fmt.Printf("%T,%05d \n",123456,123456)//int,123456

	//十进制转为二进制
	fmt.Printf("%T,%b\n",123,123)//int,1111011
	//对于进制的转换，fmt.Sprintf()返回转化后进制对应值的字符串
	strd_b := fmt.Sprintf("%b",123)
	fmt.Println(strd_b)//1111011

	fmt.Printf("%x \n",123)//7b
	fmt.Printf("%X \n",123)//7B
	fmt.Printf("%U \n",'a')//U+0061
	fmt.Printf("%U \n",'一')//U+4E00

	/**
	浮点型
	 */
	fmt.Printf("%T,%f \n",123,123)//int,%!f(int=123)
	fmt.Printf("%T,%f \n",123.123,123.123)//float64,123.123000
	fmt.Printf("%T,%F \n",123.123,123.123)//float64,123.123000
	fmt.Printf("%T,%.3f \n",123.123,123.123)//float64,123.123
	//注意是  [%.3f]  而不是  [%3f],不要把点.丢掉
	fmt.Printf("%T,%3f \n",123.123,123.123)//float64,123.123000
	//四舍五入切割
	fmt.Printf("%.2f \n",123.1234)//123.12
	fmt.Printf("%.2f \n",123.1955)//123.20
	//科学记数法
	fmt.Printf("%e \n",123.1234)//1.231234e+02
	fmt.Printf("%.1e \n",123.1234)//1.2e+02
	//默认为6位，希望科学计数法保留更多位，注意.不要丢
	fmt.Printf("%.10e \n",123.1234)//1.2312340000e+02

	/**
	字符串
	 */
	fmt.Printf("%s \n","学习go语言")//学习go语言
	fmt.Printf("%q \n","学习go语言")//"学习go语言"
	fmt.Printf("%s \n","")//看不到输出
	fmt.Printf("%q \n","")//""
	fmt.Printf("%q \n",rune('a'))//'a' 

	//字节数组
	arr := [4]byte{97,98,99,65}
	fmt.Printf("%T,%s \n",arr,arr)//[4]uint8,abcA
	fmt.Printf("%T,%q \n",arr,arr)//[4]uint8,"abcA"

	//rune数组
	arr1 := []rune{'a','b','c','一'}
	//必须是[] byte 或 字符串
	fmt.Printf("%T,%s \n",arr1,arr1)//[]int32,[%!s(int32=97) %!s(int32=98) %!s(int32=99) %!s(int32=19968)]
	//%x	每个字节用两字符十六进制数表示(使用a-f)
	//%X	每个字节用两字符十六进制数表示(使用A-F)
	arr2 := []byte{'A','s','K','w'}
	fmt.Printf("%x \n",arr2)//41734b77
	fmt.Printf("%X \n",arr2)//41734B77
}

```

