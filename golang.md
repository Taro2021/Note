

# **Taro 的 golang 学习笔记**

# 区别

```go
package main
import "fmt" 
func main(){
	fmt.Println("hello,world!")
}
```

- **package main** 表示 hello.go 文件所在的包是 main，在go 中，每个文件都必须归属于一个包
- **import "fmt"** 表示引入 fmt 包，引入够可以使用该包内的函数
- **func** 是一个关键字，表示一个函数 ，**main** 是函数名
- **fmt.Println()** 表示调用 fmt 的 Println 函数

**编译运行**

go build *.go

直接以脚本程序形式运行 go run *.go

# 开发注意事项

1. go 应用程序的执行入口是 main() 函数
2. go 语言严格区分大小写
3. go 方法由一条条语句语句构成，不用加 ；
4. go 编译器是一行一行的编译的，我们一行就写一条语句，不能写多条在同一行
5. go 语言==定义变量==或者==import的包==，若未使用，编译不通过

# 变量

```go
package main
import "fmt"

func main(){
    //var 变量名 数据类型 = 值
    var i int = 10
	var j int
	var k = 1.1
	a := i

    fmt.Println("i=",i,"\nj=",j,"\nk=",k,"\na=",a)
}
```

- go 中变量三种使用方式

  >1. 指定变量类型，声明后若不赋值，使用默认值
  >2. 根据值自行判断变量数据类型(类型推导)
  >3. 省略 var ，注意  **:=** (两步定义加赋值)左侧的变量不应该是已经声明过的，否则会导致编译错误

**一次性声明多个变量**

```go
package main
import "fmt"
var n9 = 100
var n10 =101

var(
	n11 = 11
    n12 = 12
)

func main(){
	var n1, n2, n3, n4 int
	var n5, name, n6 = 100, "tom", 12
	n7, name1, n8 := 100, "tom", 12 
}
```

# 包

- 给每个文件打包时，该包对应一个文件夹，包名通常和文件夹名一致，为小写字母
- 当一个文件要使用其它包的函数或变量时，需要先引入包
- 打包指令在第一行 **package** ，然后是 **import** 指令引入其他包
- 在 import 包时，路径从 $GOPATH 的src 下开始，不带src，编译器会自动从src下开始引入
- 包内方法名 **首字母小写**表示仅包内可用，**不可导出**（类似private）
- 包内方法名 **首字母大写**，表示该方法**可导出**（类似public）
- 访问其它包函数时，语法为 **包名.函数名**
- 如果包名较长，Go支持给包取别名，在**取别名后，原包名即不可用**
- 在同一个包内，不能有相同的函数名，**不支持重载**
- 若你要**编译一个可执行文件**，就需要将这个包声明为 **main** 包，这个就是一个语法规范，若写一个库，包名可以自定义

# 函数

```go
//go中一个函数可以有多个返回值
func 函数名(形参列表)(返回值类型列表){

}

//返回多个值时，在接收时，若希望忽略某个返回值，则使用 _ 符号占位忽略
//单个返回值可以不用（）
```

- Golang中，函数调用机制的内存分析 和 c 十分相似

- 基本数据类型 和 **数组** 是值传递
- go中 **函数也是一种数据类型** ，可以赋值给一个变量，则该变量就是一个函数类型的变量。通过该变量对函数调用
- 函数既然是一一种数据类型，因此在go 中 函数可以作为形参并且调用

```go
func getSum(n1 int, n2 int) int {
    return n1 + n2
}
//函数类型形参， 变量名 func(形参数据类型列表) (返回值类型列表)
func myFun(funvar func(int, int) int, num1 int, num2 int ) int{
    return funvar(num1, num2)
}

func main(){
    //把getSum函数 做为参数传入
    test := myFun(getSum, 1, 2)
}
```

- go 支持自定义数据类型的使用  **type**  **自定义数据类型名** **数据类型**  相当于去了一个别名

```go
//给int取了别名，在go中 myInt 和 int 虽然都是int类型，但go认为 myInt 和 int 不同
type myInt int
```

- 支持对函数返回值的命名

```go
func getSumAndSub(n1 int, n2 int)(sum int, sub int){
    sub = n1 - n2
    sum = n1 + n2
    return
}
```

- 支持可变参数

```go
//支持0到多个参数，若存在可变参数，需要放在x'c
func sum(args... int) sum int{
    
}
//args 是切片，通过args[index] 可以访问各个值
```

## init 函数

每一个源文件都有一个 **init函数** 该函数会在main() 函数调用前，被Go框架调用，也就是说 **init** 

函数可以原来完成一些初始化工作

- 在一个文件里有 **全局变量定义 > init 函数 > main 函数 **
- 若有引入包则先完成 **引入包的 全局变量定义 > init 函数**

## 匿名函数

若我们某个函数只是希望调用一次，可以考虑匿名函数，匿名函数也可以实现多次调用

### 使用方法

1. 在**定义**匿名函数时，就调用，只调用一次

2. 将**匿名函数赋给一个变量**，可多次调用

3. **全局匿名函数** 将匿名函数赋给一个全局变量

   ```go
   package main
   import "fmt"
   
   var (
       //3.res3 就是一个全局匿名函数
       res3 := func(n1 int, n2 int) int{
           return n1 + n2
       }
   )
   
   func main(){
       //1.定义时直接调用，定义时直接给匿名函数传入参数
       res := func(n1 int, n2 int) int{
           return n1 + n2
       }(10, 20)
       
       fmt.Println(res)
       
       //2.将匿名函数定义赋给一个变量，通过该变量调用
       res1 := func(n1 int, n2 int) int{
           return n1 + n2
       }
       
       fmt.Println(res1(10, 20))
   }
   ```

## 闭包

闭包是一个**函数** 和其**相关引用环境**的组合的**一个整体**(实体)

```go
func AddUpper() func(int) int{
    //---------闭包----------
    var n int = 10
    return func(x int) int {
        n += x
        return n
    }
    //----------------------
}

func main(){
    f := AddUpper() //返回一个闭包
    fmt.Println(f(1)) //11
    fmt.Println(f(2)) //13
}
```

- AddUpper 是一个函数， 返回的数据类型是 **func(int) int**
- **闭包的说明** 返回的是一个匿名函数，但是这个匿名函数引用了函数外的 n  => 因此**该匿名函数**就和**变量 n** 形成一个整体，构成闭包

## defer

函数执行后需要及时释放资源 ，go 提供了 **defer** 机制(延时机制) 

```go
func sum(n1 int, n2 int) int {
    //当执行到defer 时，暂时不执行，会将defer后面的语句压入到独立的栈（defer栈）
    //当函数执行完时，再从defer栈，依次弹栈执行
    //defer 语句入栈时，也会将相关的值拷贝进栈
    defer fmt.Println(n1)
    defer fmt.Println(n2)
    return n1 + n2
}

func main(){
    res := sum(10, 20)
    fmt.Println(res)
}
```

## 参数传递

值传递，引用传递

**值类型：**基本数据类型 int 系列，float 系列，bool，string，**数组** 和 结构体

**引用类型：**指针，slice 切片，map，管道 chan，interface 等

go 中也有垃圾回收机制，当一个引用指向的变量，没有任何地方引用时，会被gc当作垃圾回收

## 系统提供的常用函数

### 字符串常用函数

```go
package main
import(
	"fmt"
    "strconv"
    "strings"
)
// go中字符编码统一为 utf-8
func main(){
    //1.字符串长度， len(str)
    str := "hello王"
    fmt.Println("str len =", len(str))
    
    //2.字符串遍历有中文，同时处理有中文的问题先 rune 的切片 r := []rune(str)
    str1 := []rune(str)
    for i := 0; i < len(str1); i++{
        fmt.Printf("字符是 = %c\n", str1[i])
    }
    
    //3.字符串转整形： n, err := strconv.Atoi("123")  n接收结果，err接收错误信息
    n, err := strconv.Atoi("123")
    if err != nil {
        fmt.Println("转换错误"，err)
    }else{
        fmt.Println("转换结果是",n)
    }
    
    //4.整形转字符串
    str2 = strconv.Itoa(1234)
    fmt.Printf("str2=%v, str2=%T\n",str2, str2)
    
    //5.字符串转 []byte
    bytes := []byte("hello world")
    fmt.Printf("bytes = %v\n", bytes)
    
    //6. []byte 转 字符串
    str3 := string([]byte{97,98,99})
    fmt.Printf("str3 = %v\n", str3)
    
    //7. 10进制转 2，8，16
    str4 := strconv.FormatInt(123,2)//2 -> 8,16,即转成对应进制，返回字符串
    
    //8.查找子串是否在字符串中
    strings.Contains("seafood","foo")//返回true
    
    //9.统计一个字符串有几个指定子串
    strings.Count("cheese","e")//返回3
    
    //10.不区分大小写的字符串比较(==是区分大小写的)
    strings.EqualFold("abc","ABC")//返回true
    
    //11.返回子串在字符串中第一次出现的 index
    strings.Index("ABC_abc", "abc")//返回4，不存在返回-1
    
    //12.将指定子串替换成 另外一个子串strings.Replace("go go hello","指定子串","替换成该子串",n) n表示替换几个，-1表示全部替换
    str4 := strings.Replace("go go hello","go","golang",2)
    //原串并未改变，返回了一个替换后的新串
    
    //13.按照指定字符进行分割，返回一个字符串数组
    strArr := strings.Split("hello,world,hi", ",")
    
    //14.将字符串的字符进行大小写进行转换
    str5 := strings.ToLower("ABC")//abc
    str6 := strings.ToUpper("abc")//ABC
    
    //15.将字符串两边的空格去掉
    str7 := strings.TrimSpace("  hello world  ")//返回"hello world"
    
    //16.将字符串两边指定的字符串
    str8 := strings.Trim("!hello world!","!")//返回"hello world"
    
    //17.将字符串左右两边的字符串去掉
    str9 := strings.TrimLeft("!hello","!")
    str10 := strings.TrimRight("hello!","!")
    
    //18.判断字符串是否以指定字符串开头
    strings.HasPrefix("ftp://192.168.10.1","ftp")//返回true
    
    //19.判断字符串是否以指定字符串结尾
    strings.HasSuffix("abc.jpg","jpg")//t
}
```

 ### 日期相关函数

```go
package main
import(
	"fmt"
    "time"
)

func main(){
    //time.Time 类型用于表示时间
    //1.获取当前时间
    now := time.Now()//time.Time类型
    fmt.Printf("now = %v, type = %T",now , now)
    
    //2.通过 now 获取其它日期信息
    fmt.Printf("年= %v, 月 = %v, 日 = %v, 时 = %v, 分 = %v, 秒 = %v", now.Year(), now.Month(), now.Day(), now.Hour(), now.Minute(), now.Second())
    
    //3.格式化日期时间 time.Format()
    fmt.Printf(now.Format("2006/01/02 15:04:05"))
    //"2006/01/02 15:04:05" 这个字符串各个数字是固定的，必须怎么写，可以自由组合自定义格式
    
    //4.时间的常量 Hour , Minute, Second, Millisecond, Nanosecond Duration, 
    //5.用时间常量获得指定时间单位的时间，来休眠程序
    time.Sleep(100 * time.Millisecond) //休眠 100ms
    
    //6.时间戳 Unix 和 UnixNano 纳秒时间戳(可用来记录时间，或者获取随机数)
    fmt.Printf("Unix = %v ,UnixNao = %v",now.Unix(), now.UnixNano())
    
}
```

---

### 内置函数

1. **len** ：用来求长度，比如 string，array，slide，map，
2. **new** ：用来分配内存，主要用来分配**值类型**，如 int, float32, struct... 返回指针

```go
ptr := new(int)//ptr 是一个指针
```

3. **make** ：用来分配内存，主要用来分配**引用类型**，比如 channel，map，slice

---

### 利用时间戳作为 seed 生成随机数

```go
import (
	"time"
    "math/rand"
)

func main(){
    rand.Seed(time.Now().UnixNano())
    fmt.Println(rand.Intn(100)) //输出一个 [0, 100)的随机整数
}
```

---

# golang 错误处理机制



1. 在默认情况下，当发生错位（panic）后，程序会退出，崩溃
2. 若我们希望，在发生错误后，可以捕获错误，并进行处理，保证程序可以继续执行。
3. 在这里需要用到错误处理机制

## **错误处理机制**

go 中引入的处理方式为：**defer, panic, recover**

go 中可以抛出一个 panic 的异常，然后 defer 中通过 recover 捕获这个异常，然后处理

## **使用 defer + recover 来处理错误**

```go
package main
import "fmt"

func test() {
    //使用 defer + recover 来捕获异常
    defer func(){
        err := recover() //recover() 是内置函数，可以捕获异常
        if err != nil{
            fmt.Println("err = ",err)
        }
    }()
    nums := 1
    nums1 := 0
    res := nums / nums1
    fmt.Println("res =",res)
}

func main() {
    test();
    fmt.Println("main()剩余代码...")
}
```

## 自定义错误

使用 **errors.New** 和 **panic** 内置函数

1. **error.New("错误说明")**,会返回一个 error 类型的值，表示一个错误
2. **panic** 内置函数，接收一个 **interface{}** 类型的值（也就是任何值了）作为参数。可以接收 error 类型的变量，**输出错误信息，并退出程序**

```go

import (
	"error"
	"fmt"
)
//例子：读取配置文件信息，若文件名不对返回一个自定义错误
func readConf(name string) (err error) {
    if name == "confih.ini" {
        //读取。。。
        return nil
    }else{
        //返回一个自定义错误
        return errors.New("读取文件错误")
    }
}

func test() {
    err := readConf("config.ini")
    if err != nil {
        //若读取文件发生错误，就输出错误，并终止程序
        panic(err)
    }
}

func main() {
    test();
    fmt.Println("main()剩余代码...")
}
```

# 数组和**切片**

==在 go 中数组是**值**类型==，在默认情况下是值传递，因此会进行值拷贝

## 数组的使用

```go
import "fmt"

func main(){
    //1.定义一个数组, 默认值 全部的二进制0
    var arr [2]int
    //2.赋值
    arr[0] := 1
    arr[1] := 2
    //3.遍历方式
    //常规
    for i := 0 ; i < len(arr); ++i{
        fmt.Println(arr[i])
    }
    // for-range 结构遍历 类似 java增强for
    /*
    可以用 若不想接收index 可以用_ 占位符
    for index, value := range array {
    ...
    }
    */
    for index, value := range arr{
        fmt.Println("index = %v, value = %v", index, value)
    }
    
    var arr1 []int = [3]int{1, 2, 3 }
    //类型推导
    var arr2 = [3]int{1, 2, 3}
    //...固定写法
    var arr3 = [...]int{1, 2, 3}
    //指定对应下标的值
    var arr4 = [...]int{1: 100, 0: 200, 2: 200}
}
```

tip

- 一个数组申请后就是一个 slice 切片
- 长度是数组类型的一部分，在传递函数参数时，应考虑数组长度，不同长度数组是不同数据类型

---

## slice

- 切片是数组的一个引用，是**引用类型**，遵循引用传递机制
- 切片长度可变，是一个可以动态变化的数组，使用类似数组
- 定义的基本语法 `var sliceName []type`  

```go
package main
import "fmt"

func main(){
    var arr = [...]int{0, 1, 2, 3, 4}
    //切片使用方式
    //1. 声明一个切片，然后让切片去引用一个创建好的数组
    slice := arr[1:3]//表示引用arr 下标 [1,3) 的部分
    
    //2.通过 make 来创建切片 var 切片名 []type = make([]type, len, cap)
    //cap 可选
    var slice1 []int = make([]int, 4, 10)
    
}
```

方式一和方式二的区别：

- 方式一是直接引用的数组，这个数组是事先创建的，程序员可见
- 方式二通过 make 来创建切片， make 也会创建一个数组，是由切片在底层维护的，程序员不可见

### append

```go
//切片引用的简写 起始为 0，结尾为 len(arr) 时可省略(这两值为默认值)
var slice = arr[0:len(arr)]
=> var slice = arr[:len(arr)]
=> var slice = arr[0:]
=> var slice = arr[:]
//切片可以继续切片
slice1 := slice[1:3]
//对切片的动态追加 append
var slice2 []int = []int{1, 2, 3}
slice2 = append(slice2, 4, 5)
//通过append 追加一个切片
slice1 = append(slice1, slice2...)
```

append 底层原理：

- 本质是对数组的扩容
- go 底层会创建一个新的数组（扩容后大小）
- 将原 slice 的元素拷贝到新数组中
- slice 重新引用到新的数组

### copy

```go
//切片使用 copy 内置函数完成拷贝
var slice []int = []int{1,2,3}
var slice1 []int = make([]int, 10)
copy(slice1, slice)
```

- copy 要求的两个参数必须都是切片 copy(dest, src)
- 以上代码 copy 后 slice 和 slice1 的数据空间是独立的

### string 和 slice

```go
str := "hello,world!"
//使用切片获得 hello
slice := str[0:5]

arr := []byte(str)
arr[0] = 'a'
str = string(arr) //aello,world!
//转 []byte 后可以来处理英文和数字，但是不能处理中文
```

- string 底层是一个 byte 数组，因此也可以进行切片
- string 是不可变的，不能通过类似 `str[0] = 'a'` 的方式来修改字符串
- 若要修改字符串，可以先将 `string` -> `[]byte` 或者 `[]rune`  修改，再重写回 `string`

### sort

```go
import "sort"

func main(){
    arr := []int{2,4,5,1}
    //对切片进行排序，sort 默认升序
    sort.Ints(arr)
}
```



---

# map

**map的声明**：`var mapName map[keyType]valueType`

**初始化**：需要`make`分配内存

```go
func main(){
    //方式一 声明，make
    var myMap map[string]string
    myMap = make(map[string]string)
    myMap["a"] = "b"
    myMap["c"] = "d"
    //方式二 声明直接make
    var myMap1 = make(map[string]string)
    //方式三 声明make直接赋值
    myMap2 := make(map[string]string{
        "a" : "b",
    })
    
    //map 的增加和更新 map[key] = value 
    //若key 不存在则增加，已经存在则更新 value
    myMap["a"] = "c"
    
    //删除 delete(mapName, key), go中没有方法一次删除所有key，需遍历删除
    delete(myMap, "a")
    
    //查找 返回两个值 value,tag  tag表示 key 是否存在于 map 中
    val, tag := myMap["a"]
    
    //map 的遍历 只能使用 for-range 结构遍历
    for key, value := range mayMap{
        fmt.Println("key = %v, value = %v", key, value)
    }
     
   //len 也可以获得 map 的大小
    fmt.Println("myMap length = %v", len(myMap))
}
```

- map 是引用类型
- map 容量满后，再添加 k-v 会自动扩容，自动增长

---

# golang 的面向对象编程

并不是纯粹的面向对象，支持面向对象编程的特性

## struct

```go
type person struct{
    Name string
    Age i
}

func main(){
    //创建结构体变量
    //方式一
    var p1 Person
    //方式二
    var p2 = Person{"jack", 10}
    p3 := Person{"jack", 10}
    //方式三
    var p4 = Person{
        Name :"tony",
        Age :20,
    }
    
    //方式四
    var ptr1 *Person = new(Person)//ptr3 := new(Person)
    (*p3).name = "lily" //在 go 中也可以写做 p3.name = "lily"
    p3.age = 20
    //方式五
    ptr2 := &Person{"tom", 25}//ptr4 := &Person{}
    var ptr3 = &Person{
        Name : "tom",
        Age : 56,
    }
    
}
```

结构体是**值类型**

1. 结构体的所有字段在内存中是连续分布的
2. 结构体是用户单独定义的类型，和其他类型进行转换时需要完全相同的字段（成员名，个数，类型）
3. 结构体进行 type 重新定义（相当于取别名），golang 认为是**新的数据类型**，但是可以**相互间强转** `type p person`
4. struct 的每个字段上，可以写上一个 tag，该 tag 可以通过**反射机制**获取，常见的使用场景就是序列化和反序列化

```go
package main
import (
	"fmt"
    "encoding/json"
)

type Person struct{
    Name string `json:"name"`//`json:"name"`就是一个结构体 tag, 当被 json 包内方法调用时候，Name 会被替换为我们设定的 tag name
    Age int `json:"age"`
}

func main(){
    person := Person{"mark", 10}
    //将 person 序列化为 json 格式字串
    // json.Marshal() z
    jsonStr, err := json.Marshal(person)
    if err != nil {
        fmt.Println("json 错误", err)
    }
    fmt.Println("jsonStr",str(jsonStr))
}
```

## 方法

1. golang 的方法可以与自定义数据类型进行绑定
2. 绑定后，该方法只能通过绑定的数据类型的变量来调用，而不能直接调用，也不能使用其它类型的变量来调用该方法
3. `func (p Person) test(){}`中`p`表示哪个`Person`变量调用该方法，这个`p`是一个==副本==也可以看作是一个绑定的方法传参，方法和一般函数一样仍然可以传递参数

```go
type Person struct{
    Name string
}
//此处 test 方法与 Person 结构体数据类型绑定+
func (p Person) test(){
    fmt.Println(p.Name)
}

func main(){
    var p Person
    p.Name = "tony"
    p.test() //调用绑定方法
}
```

```go
func (recevier type) methodName(parameters,...) (ret,...){}
```

**工厂模式**：

> 定义的**结构体名首字母小写，或者字段首字母小写**，私有化不能跨包使用，通过编写**同包内的方法**首字母**大写**，来跨包操作包内私有的结构体或字段

## **golang 的封装** 

通过私有化包内结构体，字段，再提供工厂模式的函数实现对私有化内容操作。

## **golang 的继承**

golang 中通过**嵌入匿名结构体**实现继承性

```go
//基本语法
type Goods struct {
    Name string
    Price int
}

func (g *Goods) ShowInfo(){
    fmt.Println("Name: %v , Price: %v", g.Name, g.Price)
}

type Books struct{
    Goods//这里就是嵌套的匿名结构体
    Writer string
}

type Test struct {
	good Goods//有名结构体
    //若一个结构体嵌套了一个有名结构体，这种模式就是组合，那么访问组合的结构体的方法和字段时，必须带上结构体的名字
}

func main(){
    //当我们嵌套了匿名结构体使用方法会发生变化
    book := &Books{}
    book.Goods.Name = "book"
    book.Goods.Price = 10
    book.Writer = "tony"
    book.Goods.ShowInfo()
    
    //简写
    //1.当我们直接通过 book 去访问嵌入的 Goods 的字段，当编译器发现 book 中没有该字段时，会去嵌套的结构体中去找是否有该字段，依此类推。
    //2.若有相同字段就近原则
    //3.嵌套结构体的字段不论私有与否，都能被被嵌套的结构体访问
    //4.嵌套了多个结构体中有相同字段，访问需要指明是哪个结构体的字段来区分
    book.Name = "test"
    book.Price =20
    
    //5.嵌套匿名结构体后，也可以创建结构体变量时，直接指定匿名结构体字段的值
    b1 := Books{Goods{"b1", 25},}
}


```

## golang 接口

golang 的多态特性主要通过接口实现

 ```go
 package main
 
 import (
 	"fmt"
 )
 //定义一个接口
 type Usb interface{
     //声明了两个没有实现的方法
     Start()
     Stop()
 }
 
 type Phone struct {
     
 }
 
 //让 Phone 实现 Usb 接口的方法
 func(p Phone) Start(){
     fmt.Println("手机开始工作")
 }
 func(p Phone) Stop(){
     fmt.Println("手机停止工作")
 }
 
 //计算机
 type Computer struct{
     
 }
 
 //编写一个方法 Working，接收一个 Usb 接口类型变量
 //只要实现了 Usb 接口（所谓实现 Usb 接口，就是指实现了 Usb 接口声明的所有方法）
 func (c Computer) Working(usb Usb){
     //通过 Usb 接口变量来调用 Start 和 Stop 方法
     usb.Start()
     usb.Stop()
 }
 func main(){
     computer := Computer{}
     phone := phone{}
     
     computer.Working(phone)
 }
 ```

- `interface`类型可以定义一系列方法，但是这些不需要实现，不能有方法体。并且 `interface`不能包含任何变量。到某个自定义类型要使用的时候，再根据具体情况把这些方法写出来。
- `type 接口名 interfac{ method1(参数列表) 返回值列表 ...}`
- golang 中的接口不需要显式的实现。只要一个变量，含有接口类型中的所有方法，那么这个变量就实现了这个接口。
- 接口不能实例化，但是可以接收实现了接口所有方法的结构体的引用

```go
//例子
package main

import(
	"fmt"
    "sort"
    "math/rand"
)
//1.声明一个 Person 结构体
type Person struct{
    Name string
    Age int
}
//2.定义一个 Person 结构体的切片类型
type PersonSlice []Person
//3.实现 sort 包里的 Sort(data Inteface) data接口里的方法
func(ps PersonSlice) Len() int {
    return len(ps)
}

func (ps PersonSlice) Less(i, j int) bool {
    return ps[i].age < ps[j].age
}

func (ps Person) Swap(i, j int) {
    ps[i], ps[j] = ps[j], ps[i]
}


func main(){
    var persons PersonSlice
    for i := 0; i < 10; i++ {
        person := Person{
            Name : fmt.Sprintf("person%d", rand.Intn(100))
            Age : rand.Intn(100)
        }
        persons = append(persons, person)
    }
    
    
    //调用 sort 包 Sort 方法，因为 PersonSlice 实现了 Sort(data Inteface) data接口里的方法,可以作为参数传入该方法
    sort.Sort(persons)
    
}
```

## 类型断言

由于接口是一般类型，不知道具体类型，如果要转成具体类型，需要使用到类型断言

```go
package main
import "fmt"
type Point struct{
    x int
    y int
}
func main(){
    var a interface{}//a 是一个空接口，可以接收任意类型
    point := Point{1, 2}
    a = point //可以
    //如何将一个接口 a 赋给一个 Point 变量
    var b Point
    //b = a不可以
    //使用类型断言
    b = a.(Point)    
}

//断言使用例子
//一.
//定义一个接口
type Usb interface{
    //声明了两个没有实现的方法
    Start()
    Stop()
}

type Phone struct {}

//让 Phone 实现 Usb 接口的方法
func(p Phone) Start(){
    fmt.Println("手机开始工作")
}
func(p Phone) Stop(){
    fmt.Println("手机停止工作")
}
//Phone 独有的方法
func (p Phone) Call(){
    fmt.Println("打电话")
}

//计算机
type Computer struct{}

func (computer Computer) Working(usb Usb) {
    usb.Start()
    //若 usb 是指向 Phone 挤乳沟提变量，则还要调用 Call 方法
    //类型断言的使用
    if phone, ok := usb.(Phone); ok == true {
        phone.Call()
    }
    usb.Stop()
}


//二.
func TypeJudge(items... interface{}) {
    for index, x := range items {
        switch x.(type) {
            case bool :
            	fmt.Printf("第%v个数是 bool 类型，值是%v", index, x)
            case float32, float64 :
            	fmt.Printf("第%v个数是浮点类型，值是%v", index, x)
            case int, int32, int64 :
            	fmt.Printf("第%v个数是整数类型，值是%v", index, x)
		   case string :
            	fmt.Printf("第%v个数是字符串，值是%v", index, x)
            default :
            	fmt.Printf("参数类型不确定")
        }
    }
}
```

# 文件操作

**打开文件**：`func Open(filePath string) (file *File, err error)`

**关闭文件**：`func (f *File) Close() err error`

```go
package main
import(
	"fmt"
    "os"
    "bufio"
    "io"
    "io/ioutil"
)

func main(){
    
    //一 读文件
    file, err := os.Open("d:/test.txt")
    if err != nil {
        fmt.Println("open file err =", err)
    }    
    fmt.Printf("file = %v", file)
    ///defer 当函数退出时关闭文件
    defer file.Close()
    //文件操作
	//1.创建一个 *Reader，是带缓冲的，默认 4096 字节
    reader := bufio.NewReader(file)
    //2.读取文件内容
    for {
        str, err := reader.ReadString('\n')//每次读取至遇到换行符
        fmt.Print(str)
        if err == io.EOF {//io.EOF 文件末尾
            break;
        }
    }
    
    //使用 io/ioutil ioutil.ReadFile 一次性读取文件
    file1 := "d:/test.txt"
    content, err1 := ioutil.ReadFile(file1)
    if err1 != nil {
        fmt.Printf("read file err = %v", err1)
    }
    //显示读取内容
    fmt.Print("%v", content)//[]byte
    fmt.Print("%v", string(content))
    
    
    //二 写文件
    //1.创建文件
    filePath := "d:/abc.txt"
    file2, err2 := os.OpenFile(filePath, os.O_WRONLY | os.O_CREATE, 0666)
    if err2 != nil {
        fmt.Prinln("open file err = %v\n", err2)
        return
    }
    
    str1 := "Hello,world!\n"
    //写入时，使用带缓存的 *Writer
    writer := bufio.NewWriter(file2)
    for i := 0; i < 5; i++ {
        writer.WriterString(str1)
    }
    //因为 Writer 是带缓存的，因此内容是先写入缓存中的
    //写入缓存后，需要 Flush 才能写入磁盘
    writer.Flush()
    
    //2.打开已有文件 os.TRUNC 覆盖写，os.O_APPEND 追加写
    file3, err3 := os.OpenFile(filePath, os.O_WRONLY | os.O_TRUNC, 0666)
    if err3 != nil {
        fmt.Prinln("open file err = %v\n", err3)
        return
    }
}
```

## **命令行参数获取**

```go
package main
import (
	"fmt"
    "os"
    "flag"
)

func main(){
    fmt.Println("命令行参数有", len(os.Args))
    for i, v := range os.Args{
        fmt.Println("args[%v] = %v\n", i, v)
    }
    //flag 包来解析命令行参数
    //定义几个变量，来接收命令行参数
    var user string
    var pwd string
    
    //&user 就是接收命令行中输入 -u 后面的参数
    //"u", 就是 -u 指定参数
    //"",默认值
    //"用户名，默认为空",说明
    flag.StringVar(&user, "u", "", "用户名，默认为空")
    flag.StringVar(&pwd, "p", "", "密码，默认为空")
    
    //转换，必须执行的操作
    flag.Parse()
    
    fmt.Printf("user = %v, pwd = %v\n",user , pwd)
    
}
```

## JSON

```go
import (
	"fmt"
    "encoding/json"
)

type Person struct {
    Name string `json: "name"`
    Age int `json : "age"`
}

func testSrtuct() {
    person := Person{
        Name : "lzy"
        Age : 18
    }
    //1. json 序列化
    //结构体，map，slice都可以序列化
    //将 person 序列化为 []byte
    data, err := json.Marshal(&person)
    if err != nil {
        fmt.Println("序列化错误，err=%v\n", err)
    }
    
    fmt.Printf("person 序列化后：%v", data)
    
    //2.反序列化
    var person1 Person
    //接收数据是一个字符串时，应该转化为 []byte, []byte(str)
    err := json.Unmarshal(data, &person)
}
```

# 单元测试

1. 测试用例文件名必须以 `_test.go` 结尾。 比如 `cal_test.go , cal` 不是固定的。 　　
2. 测试用例函数必须以`Test` 开头，一般来说就是 `Test+被测试的函数名`，比如 `TestAddUpper`
3. `TestAddUpper(t *tesing.T) `的形参类型必须是 `*testing.T` 【看一下手册】 　　
4. 一个测试用例文件中，可以有多个测试用例函数，比如 TestAddUpper、TestSub 　　
5. 运行测试用例指令 (1)`cmd>go test `[如果运行正确，无日志，错误时，会输出日志] 　(2)`cmd>go test -v `[运行正确或是错误，都输出日志]
6. 当出现错误时，可以使用 `t.Fatalf `来格式化输出错误信息，并退出程序 　　
7. `t.Logf `方法可以输出相应的日志
8. 测试用例函数，并没有放在 main 函数中，也执行了，这就是测试用例的方便之处.
9. `PASS `表示测试用例运行成功，`FAIL` 表示测试用例运行失败 　　
10. 测试单个文件，一定要带上被测试的原文件： `go test -v cal_test.go cal.go `　
11. 测试单个方法：`go test -v -test.run TestAddUpper`

```go
//创建一个 cal_test.go 文件 _test 是固定文件后缀
package cal

import(
	_"fmt"
	"testing"
)
//Test 是命名规范必须有这个前缀
func TestAddUpper(t * .T){
	//调用 cal.go 下的函数
    res := addUpper(10)
	if res != 55 {
		t.Fatalf("addUpper(10) 执行错误 ，期望值=%v 实际结果=%v\n",55,res)
	} 

	//成功 输出日志
	t.Logf("addUpper(10) 执行成功")
}
```

```shell
go test ：有错误提示错误信息，正确没有提示信息
go test -v ： 有没有错误都有提示信息
go test -v cal_test.go cal.go : 执行指定文件
go test -v -test.run TestAddUpper : 测试单个方法
go test -v -run TestAddUpper
```

# ==goroutine 协程==

案例

```go
package main

import (
	"fmt"
	"strconv"
	"time"
)

func test() {
	for i := 0 ; i < 10; i++ {
		fmt.Println("test() hello, world!" + strconv.Itoa(i))
		time.Sleep(time.Second)
	}
}
func main(){

	go test() //开启一个协程

	for i := 0; i < 10; i++ {
		fmt.Println("main () hello, world!" + strconv.Itoa(i))
		time.Sleep(time.Second)
	}
}
```

## 简介

1. 主线程是一个物理线程，直接作用在 cpu 上。是重量级的，非常消耗 cpu 资源
2. 协程从主线程开启的，是轻量级的线程，是**逻辑态**的，对资源消耗相对较少
3. golang 的协程机制是其重要的特点，可以轻松开启上万个协程。其它语言的并发机制一般基于线程的，开启过多线程，资源消耗大。

**goroutine的调度模型 MPG模式**

1. M：操作系统的主线程
2. P：协程执行需要的上下文
3. G：协程

# channel管道

不同 goroutine 间通信

1. 全局变量的互斥锁，低水平的解决方式
2. 使用管道 channel 解决

## **全局变量上锁**

```go
package main
import (
	"fmt"
	"sync"
	"time"
)

//解决同步问题，方法一 互斥锁
var (
	myMap = make(map[int]int, 10)
	//声明一个全局的互斥锁
	lock sync.Mutex
)
//test() 计算 n!, 放入到 myMap
func test( n int){
	res := 1
	for i := 1; i <= n; i++ {
		res *= i
	}

	//对全局 map 操作前上锁
	lock.Lock()
	myMap[n] = res
	lock.Unlock()
	//操作完，解锁
}


func main() {
	
	//开启 20 个协程
	for i := 1; i <= 20; i++ {
		go test(i)
	}
	//人工设置休眠时间，等待全部协程完成
	time.Sleep(time.Second * 10)

	//输出结果
	lock.Lock()
	for k, v := range myMap {
		fmt.Printf("key = %v, value = %v\n", k, v)
	}
	lock.Unlock()
}
```

## channel

1. channel 本质是一个队列
2. 数据是先进先出的
3. 线程安全，多goroutine访问时，不需要加锁
4. channel 是有类型的，例 一个 string 的 channel 只能存放 string 类型的数据

**语法**：`var 管道名 chan 数据类型` ，使用 make 初始化：`管道名 = make(chan 指定的数据类型, capacity)`

类型推导 `管道名 := make(chan 数据类型, capacity)`

1. channel 是引用类型
2. channel 必须初始化才能写入数据，即 make 后才能使用
3. 管道是有类型的，只能写入已经指定的数据类型

```go
package main
import (
	"fmt"
	"time"
)

func main() {
	
	//1.创建一个可以存放 3 个 int 类型的管道
	var intChan chan int 
	intChan = make(chan int, 3)

	//2.向管道写入数据
	intChan<- 10
	num := 211
	intChan<- num
	intChan<- 11

	//当我们向管道写入数据时，不能超过设定的容量，不会自动扩充
	//满了需要读取数据后，才能继续写入

	//3.从管道读取数据
	var num2 int
	num2 = <-intChan//FIFO，取出的是 10
    <-intChan

	//在没有使用协程的情况下，若管道里的数据已经全部取出，再取数据会报错

}
```

```go
package main

import (
	"fmt"
)

//channel 的关闭
func main(){
	intChan := make(chan int, 3)
	intChan<- 100
	intChan<- 200
	//关闭后不能继续向管道写入，可以读取，close() 应该在发送端执行
	close(intChan)
	//管道的遍历需要关闭管道,否则会出现 deadlock 错误
	for value := range intChan {
		fmt.Printf("value = %v\n", value)
	}
	
}
```

## channel 和 goroutine 结合使用

```go
//轮询方式
package main
import (
	"fmt"
)

//channel 和 goroutine 结合使用
func writeData(intChan chan int){
	for i:= 0; i < 50; i++ {
		intChan<- i
		fmt.Printf("writeData 写入数据 = %v\n", i)
	}
	close(intChan)
}

func readData(intChan chan int, exitChan chan bool) {
	for {
		v, ok := <-intChan
		if !ok {
			break;
		}
		fmt.Printf("readData 读到数据 = %v\n", v)
	}
	//readData 读取完数据，即任务完成
	exitChan<- true
	close(exitChan)
}

func main(){
	//创建两个管道
	intChan := make(chan int, 50)
	exitChan := make(chan bool, 1)//通知退出信息

	go writeData(intChan)
	go readData(intChan, exitChan)

	for {
		_, ok := <-exitChan
		if !ok {
			break;
		}
	}
}
```

- channel 可以指定只读或只写 ，只写：`var 管道名 chan<- 数据类型`；只读：`var 管道名 <-chan 数据类型`\

## select

```go
package main

import (
	"fmt"
)

func main(){
	//使用 select 可以解决从管道取数据的阻塞问题

	intChan := make(chan int, 10)
	for i := 0; i < 10 ; i++ {
		intChan<- i
	}

	stringChan := make(chan string, 5)
	for i := 0; i < 5; i++{
		stringChan<- "hello" + fmt.Sprintf("%d", i)
	}

	//传统方法在遍历管道时，若不关闭会导致阻塞
	//可以使用 select 解决	
	for {
		select {
			//这里，若intChan一直没有关闭，不会阻塞，二会自动到笑一个case匹配
			case v := <-intChan :
				fmt.Printf("从intChan中读取的数据 %d\n", v)
			case v := <-stringChan :
				fmt.Printf("从stringChan中读取的数据 %v\n", v)
			default :
				fmt.Println("都取不到")
				return 
		}
	}
}
```

## 协程 panic 的捕获

```go
package main

import (
	"fmt"
	"time"
)

func sayHello() {
	time.Sleep(time.Second)
	fmt.Println("hello,world!")
}

func test(){
	//这里我们可以使用 defer + recover
	defer func() {
        //捕获 test() 抛出的 panic
		if err := recover(); err != nil {
			fmt.Printf("err = %v\n", err)
		}
	}()
	//定义了一个 map，没有make直接存入数据的错误
	var myMap map[int]string
	myMap[0] = "golang"//error
}

func main() {
	//不想因为一个协程的崩溃而导致整个程序崩溃
	//可以捕获错误
	go test()
	go sayHello()

	time.Sleep(time.Second)
	fmt.Println("main is ok!")
}
```

# 反射

利用反射机制编写适配器，桥连接

```go
package main
import (
	"reflect"
)

//使用一个函数专门用于做反射
func test(b interface{}){
	//1.如何将 interface{} 转成 reflect.Value
	rVal := reflect.ValueOf(b)

	//2.如何将 reflect.Value 转化成 interface{}
	iVal := rVal.interface{}

	//3.如何将 interface{} 转成原来的变量类型，使用断言
	v := iVal.()
}
```

## 简单演示

```go
package main

import (
	"fmt"
	"reflect"
)

//使用一个函数专门用于做反射
func test01(b interface{}){
	//通过反射获取变量的 type, kind, value
	//1.获取反射数据类型
	rTyp := reflect.TypeOf(b)
	fmt.Printf("rType = %v, type = %T\n", rTyp, rTyp)//rType = int, type = *reflect.rtype
	//2.获取反射数据值
	rVal := reflect.ValueOf(b)
	fmt.Printf("rVal = %v, type = %T\n", rVal, rVal)//rVal = 100, type = reflect.Value

	//将 rVal 转成 interface{}
	iV := rVal.Interface()
	//将 interface{} 通过断言转成需要类型
	num2 := iV.(int)
	fmt.Println("num2 = ", num2)
}

type Student struct {
	Name string
	Age int
}

func test02(b interface{}){
	
	rTyp := reflect.TypeOf(b)
	fmt.Printf("rType = %v, type = %T\n", rTyp, rTyp)
	rVal := reflect.ValueOf(b)
    fmt.Printf("rVal kind = %v", rVal.Kind())
    
	iV := rVal.Interface()
	fmt.Printf("iV = %v, iV type = %T\n", iV, iV)
	//将 interface{} 通过断言转成需要类型
	//这里使用带检测的类型断言，可以使用 switch 更加灵活
	stu, ok := iV.(Student)
	if ok {
		fmt.Printf("stu.Name = %v\n", stu.Name)
	}
}

func main(){

	var num int = 100
	test01(num)

	stu := Student{
		Name : "tom",
		Age : 18,
	}
	test02(stu)
}
```

1. `reflect.Value.Kind` 获取的变量类别（int, char, struct,...），是一个 `const` 值
2. `rValue.Elem().SetXxx(要设定的值)`，`rValue.Elem()`返回的是`rValue`保管数据或接口的指针

## 反射的最佳实践

1. 使用反射来遍历结构体的字段，调用结构体的方法，并获取结构体标签的值

```go
package main

import (
	"fmt"
	"reflect"
)

type Person struct {
	Name string
	Age int
}

func (p Person) Print(){
	fmt.Println(p)
}

func (p Person) GetSum(n1 int, n2 int) int {
	return n1 + n2;
}

func (p Person) Set(name string, age int) {
	p.Name = name;
	p.Age = age;
}

func TestStruct(a interface{}){
	typ := reflect.TypeOf(a)
	val := reflect.ValueOf(a)
	kd := val.Kind()
	if kd != reflect.Struct {
		fmt.Println("expect struct")
		return 
	}

	num := val.NumField()
	fmt.Printf("a struct has %d fields\n", num)
	for i := 0; i < num; i++ {
		fmt.Printf("field %d: value = %v\n", i, val.Field(i))
		//获取 struct 的标签，注意需要通过 reflect.Type 来获取 tag 标签的值
		tagVal := typ.Field(i).Tag.Get("json")
		if tagVal != "" {
			fmt.Printf("field %d: tag = %v\n", i, tagVal)
		}
	}

	numOfMethod := val.NumMethod()
	fmt.Printf("struct has %d methods\n", numOfMethod)
	//Method(idx) 获取第二个方法(函数名的字典序)，Call(parament[,...])调用该方法
	val.Method(1).Call(nil)

	//调用第一个方法
	var params []reflect.Value
	params = append(params, reflect.ValueOf(10))
	params = append(params, reflect.ValueOf(40))
	res := val.Method(0).Call(params)//传入的参数是 []reflect.Value,返回[]reflect.Value
	fmt.Println("res=", res[0].Int())

}

func main(){
	var p Person  = Person{
		Name : "tony",
		Age : 25,
	}

	TestStruct(p)
}
```

```
输出
a struct has 2 fields
field 0: value = tony
field 1: value = 25
struct has 3 methods
{tony 25}
res= 50
```

2. 使用反射方式来获取结构体的 tag 标签，遍历字段的值，**修改字段值**，调用结构体方法(要求：**通过传递地址的方式完成**，在前面的案例上修改即可)

   > `tag := type.Elem().Field(0).Tag.Get("json")`



---

# TCP

案例

服务器端

```go
package main
import (
	"fmt"
	"net" //net包包含网络编程所需的方法函数
)

func process(conn net.Conn){
	//协程循环接收客户端发送的数据
	defer conn.Close()

	for {
		//创建一个切片用于接收数据
		buf := make([]byte, 1024)
		//等待客户端通过 conn 发送数据
		//若客户端没有 Write,那么该协程会堵塞在这里
		n, err := conn.Read(buf)//从 conn 读取
		if err != nil {
			fmt.Println("conn.Read err =", err)
		}
		//显示接收的数据
		fmt.Print(string(buf[:n]))
		break;
	}
}

func main() {
	fmt.Println("正在监听。。。")
	//Listen("协议", "IP:端口")
	listen, err := net.Listen("tcp", "0.0.0.0:8888")

	if err != nil {
		fmt.Printf("Listen() err = %v\n", err)
		return
	}

	defer listen.Close() //延时关闭 listen
	//循环等待客户端连接
	for {
		conn, err1 := listen.Accept()
		if err1 != nil {
			fmt.Println("Accept() err =", err)
		}else {
			fmt.Printf("Accept() success, conn = %v\n", conn)
			go process(conn)
		}
	}
}
```

客户端

```go
package main
import (
	"fmt"
	"net"
	"bufio"
	"os"
)

func main() {
	conn, err := net.Dial("tcp","192.168.146.128:8888")
	if err != nil {
		fmt.Println("client dial err =", err)
		return 
	}
	fmt.Println("conn success : ", conn)

	reader := bufio.NewReader(os.Stdin) //创建一个标准输入的 Reader
	//从终端读取一行输入，准备发送给服务器
	line, err := reader.ReadString('\n')
	if err != nil {
		fmt.Println("readString err =", err)
	}
	//发送至服务器
	n, err := conn.Write([]byte(line))
	if err != nil {
		fmt.Println("conn.Write err =", err)
	}
	fmt.Printf("客户端发送了 %d 字节的数据", n)

}
```

# Redis

1. Redis 是 NoSQL 数据库，不是传统的关系型数据库
2. Remote Dictionary Server 远程站点服务器，高性能，通常适合做缓存，也可以持久化
3. 开源免费，高性能的**分布式内存数据库**，基于内存运行并支持持久化的 NoSQL 数据库，是最热门的 NoSQL 数据库之一，也称为**数据结构**服务器

## redis 指令

[Redis 命令参考 — Redis 命令参考 (redisdoc.com)](http://redisdoc.com/)

Redis 安装好后，默认有 16 个数据库，**初始默认使用 0 号库**，编号是 0, 1, ..., 15

**通用命令：**

1. 添加 key-val : `set key value`
2. 查看当前 redis 库的所有 key ：`keys *`
3. 获取 key 对应的 value : `get key`
4. 切换 redis 库：`select index`
5. 查看当前库的 key-value 的数量：`dbsize`
6. 清空当前数据库的 key-value 和清空所有库的 key-value : `flushdb, flushall`
7. `keys pattern` 查找所有符合给定类型的 key
8. `exists key` 检查给定的 key 是否存在
9. `type key` 返回给定的 key 的类型
10. `ttl key` 返回给定的 key 的最长存活时间
11. `delete key` 若 key 存在删除 key



## redis的五大数据类型

String, Hash, List, Set, zset(有序集合)

### String

string 是 redis 最基本的数据类型，一个 key 对应 一个 value

string 类型是二进制安全的。除普通的字符串外，也可以存放图片等数据。

redis 中 string 的 value 最大为 512M

- `set [key存在就相当于修改，不存在即添加] value`
- `setex key seconds value`键秒值，可以设置 key-value 的存活时间
- `mset key value [key value ...]`一次性设置多对 key-value
- `mget key [key ...]`一次性获得多个 key 的 value

### hash

redis hash 是一个键值对的**集合**

redis hash 是一个 string 类型的 field 和 value 的映射表， hash 非常适合存储对象

- `hset hashKey field value [field value ...]` 设置 hash 的域和值
- `hget hashKey field [field ...]`获取 域的值
- `hgetall hashKey` 获取所有域和值 ，域，值，[域，值，...]
- `hdel hashKey field [field ...]` 删除域
- `hlen hashKey`获取 hash 的长度
- `hexists hashKey field `查看域是否存在

### List

redis 中 List 的元素是有序的，元素可以重复

- `lpush listKey element [element ...]` 左侧插入元素
- `rpush listKey element [element ...]`右侧插入元素
- `lpop listKey`弹出左端第一个元素
- `rpop listKey`弹出右端第一个元素
- `lrange listKey start stop`查看 list 元素 [start, stop] 负数表示倒数
- `llen listKey`
- `del listKey`删除整个 list

### Set

底层是 hashTable 的结构，set 也是存放很多字符串元素，元素是无序的，而且元素值不能重复

- `sadd setKey member [member ...]`
- `smembers setKey`显示 set 的所有元素
- `sismember setKey member`判断该值是否在 set 中
- `srem setKey member`删除指定值 

### Sorted Set

sorted set 有序集合是 string 类型元素的集合，且不允许重复的成员。每个元素都会关联一个 double 类型的分数（score）。redis 正是通过分数来为集合的成员进行从小到大排序。有序集合的成员是唯一的，但是分数可以重复。

- `zadd key score1 memeber1[score2 member2 ...]`相有序集合添加一个或者多个成员，或者更新已经存在成员的分数
- `zrange key start stop [withscores]` 通过索引区间返回有序集合中指定区间内分数的成员
- `zincrby key increment member` 有序集合中对指定成员的分数上加上一个增量
- `zrem key member [member ...]` 移除一个或多个成员

# golang操作redis

## redis库的安装

在 `$GAPATH`下安装第三方开源库 `go get github.com/garyburd/redigo/redis `

**` redis.Dial("协议", "IP:端口")`**

**`conn.Do(拼接 redis 命令行的操作指令)`**

```go
package main 
import (
	"fmt"
	"github.com/garyburd/redigo/redis"
)

func main() {
	//1.连接redis库
	c, err := redis.Dial("tcp", "127.0.0.1:6379")
	if err != nil {
		fmt.Println("conn redis err =", err)
		return
	}
	defer c.Close()//网络编程不要忘了延时关闭连接
	//2.添加 key-value
	_, err = c.Do("set", "name", "tony")
	if err != nil {
		fmt.Println(err)
		return
	}
    //3.读取数据, c.Do() 获取的数据返回的是 interface{}类型的，需要使用 redis 包中的方法 转换
	r, err := redis.String(c.Do("get", "name"))
	if err != nil {
		fmt.Println("get name err =", err)
		return
	}

	fmt.Println(r)
}
```

**操作 hash 为例**

`_, err := conn.Do("hset", "hashKey", "filed", "value"[, "field", "value", ...])`

`r, err := redis.接收的数据类型(conn.Do("hget", "hashKey", "field"))`

**批量操作**

`_, err := conn.Do("hmset", "hashKey", "filed", "value"[, "field", "value", ...])`

`r, err := redis.接收的数据类型s(conn.Do("hmget", "hashKey", "field"[,"field", ...]))`返回的是一个切片

```go
package main 
import (
	"fmt"
	"github.com/garyburd/redigo/redis"
)

func main() {
	c, err := redis.Dial("tcp", "127.0.0.1:6379")
	if err != nil {
		fmt.Println("conn redis err =", err)
		return
	}
	defer c.Close()
	
	_, err = c.Do("hmset", "person" ,"name", "tony", "age", 18)

	if err != nil {
		fmt.Println(err)
		return
	}

	r, err := redis.Strings(c.Do("hmget", "person", "name","age"))
	if err != nil {
		fmt.Println(err)
		return
	}
	for idx, val := range r {
		fmt.Println(idx,":",val)
	}
}
```

**给数据设置有效时间**

`_, err := conn.Do("expire", "key", seconds)`

[**另外的redis操作库**](https://github.com/go-redis/redis)

同样在 `$GOPATH`下安装库`go get gopkg.in/redis.v4`

编程时导入包`import "gopkg.in/redis.v4"`

---

## redis连接池

```go
package main 
import (
	"fmt"
	"github.com/garyburd/redigo/redis"
)
//定义一个连接池指针全局bianliang
var pool *redis.Pool
//init() 程序启动时自动执行，完成连接池初始化
func init() {
	pool = &redis.Pool{
		MaxIdle : 8,//最大空闲连接数
		MaxActive: 0,//表示最大和数据库连接数，0 表示无限制
		IdleTimeout: 100,//最大空闲时间
		Dial: func() (redis.Conn, error) {
			return redis.Dial("tcp", "127.0.0.1:6379")
		},
	}
}

func main(){
	defer pool.Close()
	
	//先从 pool 中取出一个链接
	conn := pool.Get()
	defer conn.Close()

	_, err := conn.Do("Set", "name1", "tom")
	if err != nil {
		fmt.Println(err)
	}

	r, err := redis.String(conn.Do("get", "name1"))
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(r)
}
```

## golang连接mysql

`go get github.com/go-sql-driver/mysql `

```go
package main
import (
	"fmt"
	"database/sql"
	_"github.com/go-sql-driver/mysql"
)

func main(){
	//数据库驱动类型，用户名:密码@[连接方式](主机:端口)/数据库名
	// Open() 方法在执行是不会真正的和数据库进行连接，只是设置数据库的参数 ping()方法才是连接数据库
	db, err := sql.Open("mysql","root:1234@(192.168.146.128:3306)/test")
	if err != nil {
		fmt.Println(err)
	}
	defer db.Close()

	err = db.Ping()//真正连接到数据库
	if err != nil {
		fmt.Println(err)
	}else {
		fmt.Println("连接成功")
	}

	//数据处理
	sql := "insert into stu value(2, 'tom')"
	ret, _ := db.Exec(sql)
	n, _ := ret.RowsAffected()//受影响的行数
	fmt.Println("受影响的行数：",n)

	//执行预处理
	stu := [2][2]string{{"3","tony"},{"4","mark"}}
	stmt, _ := db.Prepare("insert into stu values(?,?)")//获取预处理语句对象
	for _,s := range stu{
		stmt.Exec(s[0], s[1])
	} 

	//单行查询
	var id,name string
	row:= db.QueryRow("select * from stu")//获取一行
	row.Scan(&id, &name)
	fmt.Println(id,"-",name)

	//多行查询
	rows,_ := db.Query("select * from stu")
	for rows.Next() {//用 Next() 取出每一行，取完返回 false
		rows.Scan(&id, &name)
		fmt.Println(id,"-",name)
	}
}
```













































