



我花了四个月时间培训了Java，刚培训完两个星期我就收到了美团的offer，还给我配了电动车 、大衣和头盔。未来可期！

# java环境配置

## jdk 的安装  

[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/)

## jdk配置

windows 环境变量的配置 

 我的电脑--属性--高级系统设置--环境变量   

在系统变量中增加  **JAVA_HOME** 指向 jdk安装目录；**JAVA_CLASS** 指向jre安装目录

编辑**path**环境变量 增加 %JAVA_HOME%\bin %JAVE_CLASS%\bin

---



# Java API

## API文档

> [**中文在线文档**](https://www.matools.com)

> [**本地文档**](F:\java\JDK_API_1.6_zh_中文.CHM)

​		**查找**：包->类->方法

​		**直接索引**

---

## main 方法static 修饰

> **static**静态方法是存储在**静态存储区内**的，可以通过类.方法名直接进行调用，**不需要进行实例化**。假设不使用static，那么main()方法在调用时必须先对其实例化，而**main()做为程序的主入口显然不可能先对其实例化**，所以使用static修饰，可以更方便的直接用类.main()对其调用。

# 变量

## 数据类型

```java
//java整型常量（具体值）默认为 int 型， 声明 long 型常量后必须加 ‘l’ 或 ‘L’（代码规范‘L’便于区分
//ava的浮点常量默认为double型， 声明 float 型常量必须在后面加 ‘f’ 或 ‘F’
//tips浮点数的比较应该限定一个精度范围，通过两个数的差值的绝对值在一定精度范围内比较
```

---

## 自动类型转换

- **细节1：**多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的数据类型，然后计算，结果也为最大精度类型

- **细节2：**大精度的数据类型赋值给小精度数据类型时，会报错

- **细节3：**byte , short 和 char 之间不会互相自动转换。 当把具体数据赋值给 byte 时：通过常量赋值，会先判断是否在 byte 范围内，如果时就可以赋值；通过变量赋值，则先判断类型

- **细节4：**byte , short, char 他们三者可以计算，**即使运算中只出现一种类型**，在计算时候首先转换为**int**类型

- **细节5**：boolean 类型不参与类型自动转换

---

## 强制数据类型转换

```java
(强制转换类型)数据；//注意精度丢失，溢出问题
```

- **1.**强制符只对最近的操作数有效

- **2.**char类型可以保存 int 常量值，不能保存 int 变量值，需要强转

- **3.**byte和short，char 类型在运算时，当做 int 类型处理

---

## 基本数据类型和String类型的转换

```java
//基本数据类型->String
//语法：将基本类型值+“” 即可
int n1 = 100;
float n2 = 1.1F;
String n3 = n1+"";
String n4 = n2+"";
System.out.println(n3 + "\n" + n4);

//String->对应的基本数据类型
//使用 基本数据类型对应的包装类 的相应方法，得到对应基本数据类型
String s1 = "123";
int num1 = Intege.parseInt(s1);
double num2 = Double.parseDouble(s1);
float num3 = Float.parseFloat(s1);
//...
//s1.charAt(0) 得到 s1 的第一个字符
System.out.println(s1.charAt(0));

//String 内容比较 方法equals
String name="林黛玉";
System.out.println(name.equals("林黛玉"));
System.out.println("林黛玉".equals(name));//推荐，可避免空指针（当name未被实例化时不会b）
```

**1.**转换时要确保String类型能够转换成有效数据，若格式不正确，就会抛出异常，程序终止

## 随机数生成

```java
(int)(Math.random() * 100) + 1;//1-100随机数 Math.random() 随机生成一个 [0,1) d
```



# 运算符

## 算术运算符

```java
//基本与c语言相通，java中 ‘+’ 可以用于字符串的相加。
// >> 算术右移，<< 算术左移，>>> 逻辑右移（无符号）右移
int i = 1;
int j = i++;//后++ 先赋值后加加 j=1,i=2
int k = ++i;//前++ 先加加后赋值 k=3,i=3

//面试题1
int i=1;
i=i++;//规则使用临时变量：右侧1.temp=i;2.i=i+1；3.此时会用temp保存的值去给左侧赋值 i=temp;
System.out.println(i);//1

//面试题2
int i = 1;
i = ++i;//1.i=i+1;2.temp=i;3.i=temp
System.out.println(i);
```

 ## 关系运算符

```java
//基本与c语言相通 ，运算结果都为boolean型 ，instanceof 检查是否是类的对象
```

## 逻辑运算符

- 1.短路运算：&& ，|| ，！ 结果为Boolean型

​	对于短路与&&而言第一个条件为false 则不会继续判断后面条件；短路或|| 第一个条件为    true，则不会继续判断后面条件。

- 2.逻辑运算，位运算：& ，|,  ^，~

#### 位运算详解

​	& 按位与，| 按位或，^ 按位异或，~ 按位取反

​	>> 算术右移，<< 算术左移，>>> 逻辑右移（无符号）右移，无逻辑左移

## 赋值运算符

​	=，+=，-=，/=，*=，%=，^=

## 三元运算符

​	条件？表达式1：表达式2

## 优先级

![java运算符优先级](F:\java\分享资料\20210408204132951.png)

---



# 标识符命名规范

- **1.包名：**多单词组成时所有字母都小写，例：aaa.bbb.ccc

- **2.类名，接口名：**多单词组成时所有单词的首字母大写，例：XxxYyyZzz

- **3.变量名，方法名：**多单词组成时，第一个单词字母小写，后续单词首字母大写，例：aaaBbbCcc

- **4.常量名：**所有字母大写，多单词时下划线隔开，例：XXX_YYY_ZZZ

- **5.[参考阿里编程规范](F:\java\泰山版阿里开发手册.pdf)**

---

# 键盘输入

## Scanner

扫描器（对象），就是Scanner 类

- **1.**导入该类所在的包，import java.util.*

- **2.**创建该类的对象实例

- **3.**调用里面的功能

```java
import java.util.Scanner;//导入该类所在的包，java.util.*
public class InputExercise01 {
    public static void main(String[] argc){
        //创建该类的对象实例,用于接收用户输入
        Scanner myScanner = new Scanner(System.in);
        System.out.println("输入名字");
        //调用里面的功能
        String name = myScanner.next();//Scanner.next()默认读取类型为String
        System.out.println("输入年龄");
        int age = myScanner.nextInt();
        System.out.println("输入收入");
        double salary = myScanner.nextDouble();
        System.out.println("姓名："+name+"\n年龄："+age+"\n收入："+salary);
    }
}
```

## 进制

```java
//n1 二进制 0b
int n1 = 0b1010;
//n2 八进制 0
int n2 = 01010;
//n3 十进制 无
int n3 = 1010;
//n4 十六进制 0x
int n4 = 0x1010;
```

# 控制

```java
//分支控制与c相通
//switch 一些细节
//1.switch 中表达式返回值类型，应该和case中数据类型一致或者可以自动转换成可相互比较的类型
//2.switch 中表达式的返回值必须是 byte，short，int，char，enum[枚举]，String
//3.case 子句中的值是常量，不能为变量
//4.如果没写break语句，程序会穿透执行，直到switch结尾，除非遇到下一个break，
char c=a;
switch(c){
    case 'a':
        System.out.println("ok1");break;
    case 11 :
        System.out.println("ok2");break;
    default:
        System.out.println("ok3");
}

//循环控制，基本与c相通
//do...while 先执行在判断，至少执行一次
循环变量初始化;
do{
    循环体;
    循环变量迭代;
}while(循环条件);
```

# 数组

## 数组

```java
//创建数组 [] 可以写在数组名后，也可写在数据类型后面
double[] example = {1,1.1,2,3};
//1.同样可以通过数组下标访问数组元素，下标从0开始
System.out.println(example[1]);
//2.可以通过 数组名.length 获取数组的长度
example.length;

//数组的使用
//动态初始化 1.先 new 一个数组， 后赋值
int a[] = new int[5];
//动态初始化 2.先声明, 再 new 之后为其分配空间， 再赋值
int b[];
b[] = new int[5];//分配了内存空间，可以存放数据

//静态初始化 语法：数据类型 数组名[] = {元素值，元素值，...}
int a[]={1,2,3};
```



**tips**

- **1.** 创建的数组若为赋值，初始值默认为 0

- **2.**数组内元素可以为任意数据类型，包括基本型和引用型，但不能混用

- **3.**数组属于引用类型，数组型的数据本质是对象（object）

## 数组赋值机制

```java
//1.基本数据类型赋值，这个值是具体的数据，而且互相不影响，值拷贝
int n1 = 2;
int n2 = n1;//n2不会影响n1的值
//2.数组再默认情况下是引用传递，赋的值是数组地址 类似于指针的值拷贝
int[] arr = {1,2,3};
int[] arr1 = arr;//arr1,arr 指向的同一个数组

//数组拷贝要求arr2 数组的 数据空间是独立的
//1.创建一个新的数组arr2 ，开辟新的数据空间
int[] arr2 = new int[arr.length];
//2.遍历arr ，把每个元素拷贝到 arr2 中
for(int i = 0;i < arr.length;i++){
    arr2[i]=arr[i];
}

//tips :java 中若堆空间中数据无变量引用，则会自动销毁

arr = arr2;//此时arr 指向arr2 的堆空间数据，而arr 原来堆空间的数据没有变量引用，则会销毁
```

## 二维数组

```java
//静态初始化
int[][] arr={{1,2,3},{0,6,0},{1,6,3}};//可以看作数组成员是一维数组的 数组
length1 = arr.length;
length2 = arr[1].length;

//动态初始化
int[][] arr1 = new int[2][3];
// java 中二维数组中没行元素个数 建议不同
int arr1 = new int[3][];
for(int i = 0;i < arr1.length;i++){
    //给每一个一维数组开辟内存空间
    //若没有给一维数组开辟空间，那么 arr1[i] 就是NULL
    arr[i] = new int[i+1];
}
```







# 面向对象编程基础（OOP）

## 类与对象

- **1.**类就是一个数据类型，可以自己定义  **类{权限，属性，行为}**

- **2.**对象就是类的一个具体实例

```JAVA
public static void main(String[] argc){
    Cat cat1 = new Cat();//cat1是对象名（对象引用），真正的对象是 new 在堆空间的数据
    cat1.name = "小白";
    cat1.age = 100;
    cat1.color = "白色";
}

class Cat{
    //属性 或称 成员变量，field(字段)
    String name;
    int age;
    String color;
    
    //行为
    
}
```

### 对象在内存中的存在形式

> 对象在栈空间中，存储一个**地址指向堆空间**中存储的该对象数据，**基本数据类型直接存储在堆**中，**引用类型**则是存储一个指向**方法区常量池**的地址，数据存储在常量池中，另外还会加载该**类**的**属性信息，方法信息到方法区**（第一步）中

### Java内存结构

- **1.**栈：一般存放基本数据类型（局部变量），对象引用

- **2.**堆：存放对象

- **3.**方法区：常量池（常量，对象中的引用数据类型），类加载信息（只会加载一次，会据此为对象在堆空间中分配内存）

### ==创建对象流程==

- **1.**先加载类信息到方法区
- **2.**根据方法区中的类信息，在堆中为对象分配内存空间，进行默认初始化，再显式初始化(在类中对属性有赋值)
- **3.**系统调用构造器进行初始化
- **4.**==把地址赋给对象引用，对象引用（对象名）指向对象==

tips :==new 一个新的对象或数组后 得到一个新的对象，并返回其对象引用==

##  属性

- **1.**属性的定义语法：访问权限  属性类型  属性名

- **2.**属性的定义类型可以为任意类型，包含基本数据类型和引用数据类型

- **3.**若属性不赋值，有默认值，规则同数组

## 成员方法

### 编写

```java
public class Method01 {
    public static void main(String[] argc){
        Person p1 = new Person();
        //调用该类内的公开方法
        p1.speak();
    }
}

class Person{
    String name;
    int age;
    //成员方法定义: 权限控制 返回值类型 方法名(形参列表){方法主体; return 返回值;}
    //1.public 表示该成员方法公开，类外可访问
    public void speak(){
        System.out.println("我是谁？");
    }
}
```

### 方法的调用机制

- **1.** 当程序执行到方法时，就会为其开辟栈空间
- **2.**方法执行完毕，或执行到 return 语句就会返回
- **3.**返回到调用该方法的地方
- **4.**返回后继续执行该行后续方法
- **5.**当main方法执行完毕，整个程序退出

### 方法注意点

- 方法体内不能嵌套**定义**方法
- **同一个类内**的方法调用，**不用实例化对象，直接调用**
- **跨类**的方法调用，需要通过对象名调用，先实例化对象，再通过对象调用
- **跨类**的方法调用权限，和方法的访问权限修饰相关

### ==成员方法传参机制==

参数 parameter

- 实参与形参间的参数传递是**值传递**， 形参的改变不会影响到实参
- 实参与形参间可以通过传递**引用**，来修改引用的数组或对象的数据内容

### 方法的递归调用

每次递归调用都会在栈空间中，为调用的方法开辟一片新空间，当方法执行到递归出口时会逐层返回至上一层方法。

- 执行一个方法时，就创建一个新的受保护的独立空间（栈空间）
- 方法的局部变量是独立的，不会相互影响
- 若方法中传递的是引用类型变量，就会共享该引用类型的数据
- 递归必须向退出递归的条件逼近
- 当一个方法执行完毕，或者return ，就会返回，遵守谁调用，就将结果返回给谁

### 方法的重载OverLoad

java中允许一个类中**多个同名方法**的存在，要求同名方法的**形参列表不同**，发生方法的重载

- 方法名必须相同，形参列表必须不同（形参名无影响），返回值类型无要求

### 可变参数 variable parameters

java中允许同一个类中**多个同名同功能**但==参数个数不同==的方法，封装成**一个**方法

> 基本语法
>
> 访问修饰符  返回类型	方法名(数据类型==...==	形参名){
>
> }

```java
class VarParameters{
    //int... 表示接受的可变参数，类型是int，即可接收多个int 型数据
    //使用可变参数时，可以当作数组来使用，即此处的 nums 可视为数组使用
    public int sum(int... nums){
        int res = 0;
        for(int i = 0;i < nums.length;i++){
            res += nums[i];
        }
        return res;
    }
}
```



tips

- 可变参数的实参可以为 0 或 任意多个
- 可变参数的实参可以是数组
- 可变参数的本质就是一个数组
- 可变参数可以和普通类型的参数一起放在形参列表，但必须保证可变参数在**最后**
- 一个形参列表**只能有一个**可变参数

---

## 作用域

- 在java中，主要的变量就是**属性**(成员变量)和**局部变量**

- **局部变量**一般指在**成员方法中定义的变量**

- java中作用域的分类

  > 全局变量：也就是**属性**，作用域是整个类，或其它类使用（通过对象调用）
  >
  > 局部变量：成员方法中定义的变量，作用域为定义它的方法中，只能在本类中对其定义的方法中使用

- 全局变量可以不赋值，会有默认值(构造方法会为属性进行赋值，若未自定义构造方法，系统会对其进行无参构造)，可直接使用；局部变量必须赋值后使用，无默认值

- 属性和局部变量可以**重名**，使用时**就近原则**

- 同一个成员方法作用域中，局部变量不可重名

- 属性，伴随着对象的创建而创建，伴随着其销毁而销毁。局部变量，伴随着它的代码块的执行而创建，伴随着代码块的结束而销毁

## 构造器/构造方法Constructor

基本语法

> 访问权限修饰符	方法名(形参列表){
>
> ​	构造方法体;
>
> }

```java
public class Constructor01{
    public static void main(String[] argc){
        Person p1 = new Person("tony ma", 50);
    }
}

class Person{
    String name;
    int age;
    Person(){
    }
    public Person(String pName, int pAge){
        name = pName;
        age = pAge;
    }
}
```

tips

- 构造器可以**重载**
- 构造器**没有返回值**
- 构造方法名必须和**类名相同**
- 构造方法的调用由**系统自动完成**
- 主要作用完成对新对象的**初始化**
- 若不自定义构造方法，系统会**自动**给类生成一个默认**无参构造器**
- **若自己定义了构造方法，默认构造就被覆盖了，就不能使用默认的无参构造器，除非自己显式的定义一下**

## this关键字

java虚拟机会给每个对象分配 **this** ，**代表当前对象**

- this关键字可以用来访问本类的属性，方法，构造器
- this用于区分当前类的属性和局部变量
- 通过this访问成员属性：**this.属性**;    访问成员方法：**this.方法名(参数列表)**;
- 访问构造器语法：**this(参数列表)**; ==只能在构造器中使用,必须在第一行==
- this 不能在类定义的外部使用，只能在类内定义的方法使用

----

## 包

### 包的三大作用

- 区分相同名字的类
- 当类很多时，可以很好的管理类
- 控制访问范围

### 基本语法

```java
package com.lzy;
//package 打包关键字
//com.lzy 表示包名
//作用声明当前类所在的包，需要放在类的最开头，一个类只能 package 一次
```

包的本质 实际上就是创建不同的文件夹来保存类文件

### 包的命名

**规则**：只能包含数字，字母，下划线，小圆点 . 	不能用数字开头，不能是关键字或保留字

**规范**：一般都是小写字母加小圆点，一般是 com.公司名.项目名.业务模块名

### 常用的包

- java.lang.*  //lang包是基本包，默认引入
- java.util.*   //util包，相同提供的开发工具包，工具类，例如Scanner
- jave.net.*   //网络包，网络开发
- java.awt.*   //是做java界面开发的，GUI

### 包的引入

```java
//语法 import 包
import java.util.Scanner;//只导入 util 包中的 Scanner 类
import java.util.*;//通配符，把 util 包内的所有类导入

//import 指令 放在package 的下面，在类定义前面，可引入多个包
```



### 访问修饰符

权限  package(默认)、private、public和protected

1. **package**是**默认**的保护模式，又叫做包访问，没有任何修饰符时就采用这种保护模式。包访问允许域和方法被**同一个包内**任何类的任何方法访问。(包内访问)

2. **private**标识的访问模式，表示私有的域和方法只能被**同一个类中**的其他方法访问，实现了数据隐藏；必要时，可以通过方法访问私有变量。(类内访问)

3. **public**修饰符用于暴露域和方法，以便在**类定义的包外部能访问它们**。对包和类中必要的接口元素，也需要使用这个级别；main()方法必须是public的，toString()方法也必须是public的。一般不会用public暴露一个域，除非这个域已经被声明为final。(跨包访问)

4. **protected**修饰符提供一个从包外部访问包(有限制)的方法。在域和方法前增加protected修饰符**不会影响同一个包内其他类和方法对它们的访问**。要从**包外部访问**包(其中含有protected成员的类)，**必须保证被访问的类是带有protected成员类的子类**。也就是说，希望包中的一个类被包之外的类继承重用时，就可以使用这个级别。一般应该慎用。(包中类被包外类继承重用)



- 修饰符可以修饰类中的属性，成员方法以及类
- 只有默认权限（引入包后也不能引用该类）和 public 才能修饰类，并且遵循上述访问权限的特点

## 面向对象三大特征

### 封装

封装（encapsulation）就是把抽象出的数据**[属性]**和对数据的操作**[方法]**封装在一起，数据被保护在内部，程序的其他部分只能通过被授权的操作**[方法]**，才能对数据进行操作。

封装的好处：隐藏实现细节，可以对数据进行验证，保证安全合理

**实现步骤**

1. 将属性进行私有化 private，不能直接修改属性
2. 提供一个公共的（public）set方法，用于对属性的判断并赋值
3. 提供一个公共的（public）get方法，用于获取属性的值

==可以使用快捷键 alt+ins 快速编写getXxx，setXxx方法，再去按需求修改，ctrl+左键可多选属性==

**我们可以将 setXxx 的调用写入构造器中，用于有参构造时，起到防护作用**



### 继承

提高代码复用性

#### 语法

>class	子类	==extends==	父类{
>
>}

- 子类继承了父类的所有属性和方法，非私有属性，成员可以直接在子类使用，但是**私有属性不能在子类直接访问**，需要通过公共的方法访问
- **子类必须调用父类的构造器，完成父类的初始化**，不管调用哪个子类的构造器都会**默认**添加 **super()；**语句，默认调用父类的无参构造，若父类中无默认无参构造器，则必须自己编写**super(指定调用的父类构造器的参数列表)；**语句显式调用父类的构造器
- super() 的使用必须在子类构造器的**第一行**，只能在构造器中使用（先父才能有子）
- **super()** 和 **this()** 都只能在构造器的**第一行**，因此两个方法不能共存在一个构造器中，当有**this()**或显式编写了**super()**时，则不会去执行默认的**super()**
- java所有类都是 Object 的子类
- 子类最多只能继承一个父类（指直接继承），即 java 是**单继承制**
- 不能滥用继承，子类和父类之间必须满足继承的逻辑关系

#### **继承的本质**

```java
public class ExtendsExercise01 {
    public static void main(String[] args) {
        Son son = new Son();
        //按照查找关系来返回信息，就近原则
        //1.看子类中是否有该属性
        //2.若子类有该属性，并且可以访问，则返回信息
        //3.若子类没有着属性，就看父类有无该属性（若父类有该属性，并可以访问，就返回信息）
        //4.若父类没有该属性，则按照3的规则，继续找上级父类，直到Object...,若还未找到则报错
        System.out.println(son.name);//直接在子类中找到，返回 大头儿子
        System.out.println(son.age);//子类无该属性，在父类中找到，返回 39
        System.out.println(son.hobby);//返回 旅游
    }
}

class GrandPa{
    String name = "大头爷爷";
    String hobby = "旅游";
}

class Father extends GrandPa{
    String name = "大头爸爸";
    int age = 39;
}

class Son extends Father{
    String name = "大头儿子";
}
```

#### super关键字

```java
public class Son extends Father{
    public void helloWord(){
        //访问父类属性，但不能访问父类的私有属性 super.属性名
        super.xx;
        //访问父类的方法，不能访问私有方法， super.方法(参数)
        super.method();
    }
    
    //访问父类的构造器，只能在构造器里访问，默认调用父类的无参构造 super()，不能与 this() 同时存在，通过this()调用的构造器里还会有super() 会重复构造父类，这是不允许的
    Son(){
        super(xx,xx);
    }
}
```

- 调用父类构造器，分工明确，各自初始化自己的属性
- 当子类中有和父类同名的成员时，为了访问**父类的同名**成员时，必须通过**super**，若不通过super访问成员，则就近原则，找不到报错
- 通过super 访问成员，父类不存在，会继续向上寻找，直到找到对应属性 或者 object
- **this 从本类开始查找，super 会跳过本类从父类开始查找**

#### final 关键字

final 可以修饰类，属性，方法和局部变量（final 修饰的变量，系统不会赋予默认初值）

- 当不希望类被继承时，可以用 final 修饰 **final class  A {}**，已经是 final 类，可以不必再用final修饰方法，因为已经没有子类继承，自然没有重写

- 可以用 final 修饰方法，子类可以继承，**不能重写**  **public final void xxx(){}**， **final不能修饰构造方法**

- final 修饰类的某个**属性**，该属性不可被修改，又叫**常量**，必须给常量**赋初值**，可在**定义时，代码块中，构造器中赋值**，静态常量不能在构造器中被赋值(类加载时，创建)

- final 修饰局部变量，不能被修改

- **final 和 static 往往搭配使用**，效率更高，**不会导致类的加载**

  ```java
  class main{
      public static void main(String[] argc){
          System.out.println(BBB.num);//只输出 1000，类不会被加载，代码块不会被执行
      }
  }
  
  
  class BBB{
      public final static int num = 1000;
      static{
          System.out.println("BBB静态代码块被执行了");
      }
  }
  ```

- 包装类 String, Integer，Float...都是 final 类，不可被继承

### 多态

#### 方法重写override

- 子类的方法的**形参列表，方法名称**，要和父类方法的参数，方法名称完全相同
- 子类方法的返回类型和父类方法**返回类型一样**，**或者是父类返回类型的子类**，比如父类返回类型是 Object，子类返回类型可以是String
- 子类重写父类的方法，不能缩小权限    public>protected>package默认>private

#### 多态的具体体现

1. 方法的多态，重写和重载就体现多态

2. ==**对象的多态**==

   >**一个对象的编译类型和运行类型可以不一致**
   >
   >**编译类型在定义对象时，就确定了，不能改变**
   >
   >**运行类型是可以变化的**
   >
   >**编译类型看定义时  = 号的左边， 运行类型看 = 号的右边**
   >
   >例：Animal animal = new Dog();  //animal 编译类型时Animal，运行类型 Dog
   >
   >animal = new Cat();  //animal 编译类型时Animal，运行类型 Cat
   >
   >==通过父类的对象引用指向子类对象，调用子类成员，发生多态==



#### 注意事项

1. 多态的前提是：两个类存在继承关系

2. 多态的**向上转型**，**父类的引用指向了子类对象**

   > 语法：父类类型    引用名 = new 子类类型();
   >
   > 编译类型看左边，运行类型看右边
   >
   > 该引用可以调用**父类的所有成员（遵守访问权限）**，但是**不能调用子类特有的成员**，因为在==编译阶段，能**调用哪些成员**，是**由编译类型决定**的==
   >
   > ==最终的运行效果看子类的具体实现，**运行效果由运行类型决定**==

3. 多态的**向下转型**

   >语法：子类类型    引用名 = (子类类型) 父类引用;
   >
   >只能强转**父类的引用**，**不能强转**父类的**对象**
   >
   >强转要求父类的引用**必须指向**的时候**强转目标类型的对象**
   >
   >强转后可以调用子类类型的所有成员

4. 属性没有重写之说，属性的值直接看编译类型

5. ==**instanceof **==比较操作符，用于判断**对象的运行类型**是否为XX类型或XX类型的子类型

### ==动态绑定机制==

1. 当调用对象方法，==该方法会和该对象的内存地址/运行类型==绑定
2. 当调用对象属性时候，==属性没有动态绑定机制==，哪里声明，哪里使用

口诀：访问属性看位置，方法调用看运行

## 多态的应用

#### 多态数组

- 数组的**定义类型为父类类型**，里面保存的**实际元素类型为子类类型**

应用实例：现有一个继承结构如下：父类为Person类，子类有 Teacher类， Student类，统一放在数组中, 并调用重写的 say()方法

子类调用各自特有的方法，如 Teacher 类中有一个 teach 方法，Student 类中有一个 study 方法

```java
public class PloyArray {
    public static void main(String[] args) {
        Person[] arr = new Person[5];
        arr[0] = new Person(10,"marry");
        arr[1] = new Student(23,"tony",100);
        arr[2] = new Student(21,"smith",59);
        arr[3] = new Teacher(50,"jack",1000);
        arr[4] = new Teacher(65,"mark",1500);
        for (int i = 0; i < arr.length; i++) {
            //重写方法的调用
            arr[i].say();
        }
        //特有方法的调用,先通过 instanceof 判断子类类型，再进行强转
        for (int i = 0; i < arr.length; i++){
            if(arr[i] instanceof Student){ 
            	((Student)arr[1]).study();
            }else if(arr[i] instanceof Theacher){
            	((Teacher)arr[3]).teach();
            }
        }
    }
}
```

#### 多态参数

在方法定义的**形参中为父类类型**，**实参类型允许是子类类型**

## Object 类详解

类Object 是类层次结构的根类。每个类都使用 Object 作为超类。 所有对象（包括数组）都实现这个类的方法。

==ctrl + b==跳转查看方法源码

### equals方法

**==** 与 **equals** 的对比

**==** 是一个比较运算符

>1. 即可以判断基本类型，又可以判断引用类型
>2.  判断**基本类型**时，判断的是**值**是否相等
>3. 判断**引用类型**时候，判断的是**对象的引用**是否相等，即**对象的地址**

**equals** 是Object 类中的方法，**只能比较引用类型**

- 默认判断地址是否相等，但是子类中往往重写方法，用于判断内容是否相等，比如 Integer, String 

**重写equals方法**

```java
public class EqualExercise{
    public static void main(String[] argc){
        Person p1 = new Person("jack", 10, '男');
        Person p2 = new Person("jack", 10, '男');
        System.out.println(p1.equals(p2));//ture
        //Person 类中未重写equals方法时，调用Object 类里的默认equals 方法，比较地址，重写后调用重写的equals方法
    }
}

class Person{
    private String name;
    private int age;
    private char gender;
    
    public Person(String name, int age, char gender){
        this.name = name;
        this.age = age;
        this.gender = gender;
    }
    //重写 equals 方法
    public boolean equals(Object obj){
        if(obj instanceof Person){//先判断对象类型是否是相同子类
            Person p = (Person)obj;//传入对象向下转型，不然无法访问子类特成员
            return this.name.equals(p.name) && this.age == p.age && this.gender = p.gender;
        }
        return false;
    }
}
```

### hashCode方法

1. 提高具有哈希结构的容器的效率
2. 两个引用，如果指向的是同一个对象，则哈希值肯定是一样的
3. 两个引用，若指向不同对象，则哈希值是不同的
4. 哈希值主要**根据地址**号来，不能完全把哈希值等价于地址

```java
obj.hashCode();
```

### toString方法

- 默认返回：全类名(包名加类名) + @ + 哈希值的十六进制，子类往往重写 **toString** 方法用于返回对象信息
- 重写 toString 方法，**打印对象或拼接对象**时，都会**自动调用**该对象的 **toString 形式**
- 当**直接输出**一个对象时，**toString** 方法会被**默认调用**

### finalize方法

当垃圾回收器确定不存在堆该对象的引用时，由该对象的垃圾回收器调用此方法

- 当对象被回收时，系统自动调用该对象的finalize方法。子类可以重写该方法，做一些**释放资源**的操作。（比如 断开数据库连接，关闭打开的文件...）
- 当该**对象没有任何引用**时，jvm就认为该对象是一个垃圾对象，就会使用垃圾回收器机制来回收对象，在**销毁该对象前**，会**先调用finalize**方法。
- 垃圾回收机制的调用由系统来决定，也可以通过**System.gc()** 来主动触发垃圾回收机制。

---

# 断点调试

==重要提示==：在断点调试过程中，是运行态的，是以对象的运行类型来执行的

## 快捷键

F7：跳入方法								 F8：逐行执行代码

shift + F8：跳出方法					  F9：resume 执行到下一个断点

---

# 静态

## 类变量/静态变量

### 语法

```java
class Child{
    private String name;
    //定义一个count 变量，是一个类变量/静态变量， static 修饰
    public static count = 0;
}
```

- **类变量会被该类的所有实例对象共享**
- 类变量直接可以**通过类名访问**
- 类变量和方法一样一个类只会在内存中保存一份，在加载类信息时即完成创建，不依赖于实例化对象

---

## 类方法/静态方法

- 静态方法和普通方法都只会在内存的方法区里存储一份，随着类的加载而加载
- 类方法中**无 this ，super 关键字**
- 普通方法可以访问静态成员，普通成员，**静态方法** 只能访问 **静态成员** 
- 静态方法可以通过**类名调用**，也可用对象名调用

**使用场景** ：当方法中不涉及任何和对象相关的成员，若我们不希望创建实例，也可以调用某个方法(即当做工具来使用)，这是把方法制作成静态方法非常合适

工具人没有对象啊！！！！

---

## main 方法

1. main() 方法是java虚拟机调用的
2. java虚拟机在执行main()方法，所以该方法访问权限必须是public
3. java虚拟机在执行main()方法时不必创建对象，所以该方法必须是static
4. 该方法接收String类型的数组参数，该数组中保存执行java命令时传递给所运行的类的参数(**命令行参数**)
5. 在main()方法中，我们可以直接调用main方法所在类的**静态成员**
6. 但是**不能直接访问该类的普通成员**，必须创建该类的一个实例对象后，才能通过对象去访问类中的非静态成员

---

## 代码块

代码块又称为**初始化块**，属于类中的成员，类似于方法，将逻辑语句封装在方法体中，通过**{}**包围起来。和方法不同，**没有方法名，没有返回，没有参数**，只有方法体，而且不能通过对象或类显式的调用，而是**加载类**的时候，或是**创建对象**的时候**隐式的调用**。

### **语法**

>[修饰符]{
>
>代码
>
>};

- 修饰符可选，static 或 无   => 静态代码块，普通代码块
- 逻辑语句可以为任何逻辑语句
- **；**可写可省略

### 应用场景

- 相当于另一种形式的构造器(对构造器的补充)，可以初始化操作
- 可以把多个构造器中的重复内容，抽取到一个代码块中，提高代码重用性
- 代码块的优先顺序优于构造器

### 使用细节

1. **static**修饰的代码块，静态代码块作用是对类进行初始化，**只能访问静态成员**，随着**类的加载**而执行，并且只会执行一次，若普通代码块，每创建一个对象，就执行一次。

2. 类什么时候加载(类信息只会**加载一次**)

   >创建对象实例时（new）
   >
   >创建子类对象实例，父类也会被加载（父类先加载，子类后加载）
   >
   >使用类的静态成员时

3. 普通代码块，创建对象实例时，会隐式的调用，被创建一次调用一次，若只使用类的静态成员时，普通代码块并不会被执行。

4. 创建一个对象时，**在==一个类==中**的调用顺序

   > ① **类加载时，调用静态代码块 和 静态属性初始化**（静态代码块 ，静态属性初始化，优先级一样，按照定义顺序执行）

   > ② **然后调用普通代码块和普通属性初始化**（按定义顺序）

   > ③ **调用构造器**

5. 构造器 的最前面其实隐含了 **super()** 和调用普通代码块

   ```java
   class A{
       public A(){
           super();//隐含
           调用普通代码块;//隐含
           构造器代码;
       }
   }
   ```

6. ==创建一个子类对象==时候（有继承关系） 记住**先加载类信息才能创建对象，有父才有子**

   >**①父类的静态代码块，静态属性初始化**
   >
   >**②子类的静态代码块和静态属性初始化**
   >
   >**③父类的普通代码块和普通属性初始化**
   >
   >**④父类的构造方法**
   >
   >**⑤子类的普通代码块和普通属性初始化**
   >
   >**⑥子类的构造方法**

---

## 单例模式(静态方法和属性的经典使用)

采取一定的方法保证在整个软件系统中，对某个类只能存在一个对象实例，并且该类只提供一个取得其对象实例的方法。

### 1.饿汉模式（类加载时即创建，实例可能长时间不被使用）

**构造器私有化(防止用户直接 new) -> 类的内部创建对象 -> 向外暴露一个静态的公共方法**

 ```java
 class GirlFriend{
     private String name;
     //1.构造器私有化
     private GirlFriend(String name){
         this.name = name;
     }
     //2.类的内部创建对象,为了能让静态方法使用，用static修饰
     private static GirlFriend gf = new GirlFriend("小明");
     //3.提供一个公共的静态方法，返回gf对象
     public static GirlFriend getInstance(){
         return gf;
     }
 }
 ```

### 2.懒汉式（不使用不创建实例）

**构造器私有化 -> 定义一个私有静态属性对象引用 -> 提供一个public static 方法，可以返回一个对象**

```java
class Cat{
    private String name;
    //定义一个私有静态属性对象引用
    private static Cat cat;
    //构造器私有化
    private Cat(String name){
        this.name = name;
    }
    //提供一个public static 方法，可以创建对象并返回一个对象引用
    public static getInstence(){
        if(cat == null){
            cat = new Cat("小白");
        }
        return cat;
    }
}
```

**两者区别**：

1. 创建时机不同
2. 饿汉式不存在线程安全问题，懒汉式存在线程安全问题
3. 饿汉式存在浪费资源的可能
4. java.lang.Runtime 就是经典的饿汉式

---

# 抽象类

-  父类中某些方法实现没有意义，将这些方法用 **abstract** 修饰 
- 有 **abstract 方法**的类**必须声明为抽象类**，该类声明应该 用 abstract 修饰
- **抽象类**通常有子类继承，通过子类重写其抽象方法
- 抽象类不能实例化
- **抽象类可以不一定有抽象方法**
- abstract 只能修饰 **类** 和 **方法**
- 子类继承若不重写父类 抽象方法 ，则仍需声明自己是抽象类
- 抽象类不能用 static，final, private 来修饰，子类无法重写

```java
abstract class A{
    abstract public void eat();
}
```

**模板设计模式**

---

# 接口 Interface

接口就是给出一些没有实现的方法，封装到一起，起到某个类要使用时，再根据具体情况把这些方法重写

---

## 语法

**定义一个接口**：

```java
interface 接口名{
	//属性
	//方法（1.抽象方法（接口中不用abstrac修饰） 2.默认的实现方法（default修饰）3.静态方法）
}
```

**调用实现**：

```java
class 类名 implements 接口{
	自己属性;
	自己方法;
	必须实现接口中的抽象方法;
}
```

---

## 注意点

1. 接口**不能实例化**对象
2. 接口中所有方法是 **public** 方法，接口中的抽象类可以省略 abstract
3. 一个普通类中实现接口，必须将接口的所有抽象方法实现
4. 抽象类实现接口，可以不用实现接口的方法
5. 一个类同时可以**实现多个接口**
6. 接口中的**属性**，只能是 **final** 的 （属性默认为 public static final）
7. 接口中属性访问形式：**接口名.属性名**
8. 接口不能继承其它类，但是能继承多个别的接口
9. 接口的修饰符 只能是 public 和默认，这点和类的修饰符一样

**接口 vs 继承**

- 当子类继承了父类，就自动拥有父类的功能
- 若子类需要扩展功能，可以通过实现接口的方式扩展
- 可以理解为 **实现接口 是对 java 单继承机制的一种扩展**
- 继承的价值在于：提高代码的复用性和可维护性
- 接口的价值在于：设计，设计好各种规范（方法），让其他类去实现这些方法
- 接口比继承更加灵活，继承满足 is -a 的关系，而接口只需要满足 like -a 的关系
- 接口在一定程度上实现代码的解耦 [接口规范 + 动态绑定]

---

## 接口的多态特性

多态参数，多态数组

==接口的**多态传递**现象==

```java
public class InterfacePolyPass{
    public static void main(String[] argc){
        //接口类型的变量引用，可以指向实现了该接口类的实例对象
        A1 a = new Test();
        //若A1 继承了A2 ,而且Test 实现了 A1 的接口
        //那么实际上相当于 Test 也实现了A2接口
        //这就是 j多态
        A2 a2 = new Test();
    }
}

interface A1 extends A2 {}
interface A2 {}
class Test implement A1{
    
}
```

---

# 内部类

一个类的内部嵌套了另一个类的结构。被嵌套的类称为内部类(inner class),嵌套其它类的类为外部类(outer class).内部类最大的特点就是可以直接访问私有属性，并且可以提现类与类的包含关系。

```java
class Outer{
    class inner{
        
    }
}
```

---

## 内部类分类

定义在外部类的局部位置（比如方法内）

1. **局部内部类（有类名）**

2. ==**匿名内部类（无类名，重要）**==

定义在外部类的成员位置上

1. **成员内部类（没有 static 修饰）**
2. **静态成员类（使用 static 修饰）**

---

## 局部内部类

```java
class Outer{
    private int n = 1;
    public void m1(){
    	//局部内部类定义在外部类的局部位置中，通常在方法中
        
        class Inner{//局部内部类
            //可以直接访问外部类的所有成员，包括私有
        }
    }
}
```

- **局部内部类定义在外部类的局部位置中，通常在方法中**
- **局部内部类不能添加访问修饰符，但是可以添加 final**
- **作用域仅在定义它的方法或代码块中**
- **可以直接访问外部类的所有成员，包括私有**
- **外部类在定义该内部类成员方法中，可以创建对象，然后通过调用该对象访问**
- 外部**其它**类不能访问局部内部类
- 外部类和内部类成员重名时，默认遵循就近原则，若想访问外部类同名成员，可以通过**外部类.this.成员**去访问

---

## ==匿名内部类==

1.本质是类 2.内部类 3.匿名 4.同时它还是个对象

```java
class Outer{
    private int n = 1;
    public void m1(){
        //匿名内部类
    	A1 a1 = new 类或接口(参数列表){//当为接口时，相当于在类体里实现了接口;类时，相当于继承，重写了父类方法；系统内部完成，会分配一个类名
            //创建匿名内部类时，立即创建实例化对象
            //匿名内部类只能使用一次，对象可多次使用
            类体;
            public void hi(){}
        };
        a1.hi();
        
        //匿名内部类已经是一个对象，若不想要对象引用接收，z调用一次，可以如下写
        new 类或接口(参数列表){
            public void hi(){}
        }.hi();
        }
    }
}
```

**匿名内部类的经典使用场景**

当做实参直接传递，代码简洁高效

```java
interface I1{
    void show();
}

public class Test{
    public static void main(String[] argc){
        //当作实参直接传递
        f1(new I1(){
           public void show(){
               System.out.println("匿名内部类作实参");
           } 
        });
    }
    
    public static void f1(I1 i1){
        il.show();
    }
}
```

---

## 成员内部类

是外部类的一个成员，无static修饰，所以也可以被外部其它类通过外部类的对象访问

```java
//外部其他类，使用成员内部类的2种方法
Outer outer1 = new Outer();
//1.
Outer.Inner inner1 = outer1.new Inner();
Outer.Inner inner2 = new Outer().new Inner();
//2.在外部类中编写一个方法，可以返回 new 内部类的引用
```

## 静态内部类

是外部类的一个成员，有static修饰

可访问外部类的所有静态成员，不能访问非静态



```java
package 包名;
class 类名 extends 父类 implements 接口{
    成员属性;
    代码块;
    构造方法;
    成员方法;
    内部类;
}
```

---

# 枚举

```java
//使用 enum 关键字实现枚举类
enum Season1{
    SPRING("春天","温暖"), SUMMER("夏天","炎热"), AUTUMN("秋天","凉爽"), WINTER("冬天","寒冷"), What;
    private String name;
    private String desc;
    
    private Season1(){
        
    }
    
    private Season1(String name,String desc){
        this.name = name;
        this.desc = desc;
    }
    
    public String getName(){
        return name;
    }
    
    public String getDesc(){
        return desc;
    }
}
```

- 当我们 **enum** 关键字实现枚举类时，会**自动继承 Enum 类 **，所以枚举类不能继承其他类
- 使用 **enum** 关键字替代 class
- **public static final Season SPRING = new Season("春天","温暖");** 直接使用 **SPRING("春天","温暖");** 解读 常量名(实参列表)
- 若有多个常量(对象)，可以用 **,** 间隔即可
- 若使用enum来实现枚举，要求定义的常量写在前面
- 若使用的是无参构造器，创建常量对象，可以省略 **()**
- **枚举类构造器默认私有**

##  Enum 类各种方法使用

1. **toString()** : Enum 类已经重写过，返回的是当前对象名，子类可以重写方法，用于返回子类属性信息
2. **name()**：返回当前对象名(常量名)，子类不能重写，建议优先使用 toString()
3. **ordinal()**：返回当前对象的位置号，默认从 0 开始
4. **values()**：返回当前枚举类中的所有常量
5. **valueOf()**：将字符串转换成枚举对象，要求字符串必须为已有常量名，否则报异常
6. **compareTo**：比较两个常量，比较的是位置号

---

# Annotation

使用 annotation 时 要在前面加上 **@** 并把该annotation当成一个修饰符使用

## **三个基本的annotation**

1. **@Override** :限定某个方法，是**重写**父类方法，该注解只能用于方法
2. **@Deprecated** ：用于表示某个程序元素（类,方法等）已**过时**
3. **@SuppressWarnings** : **抑制编译器警告**

   修饰注解的注解，为**元注解**

## 四种元注解

1. Retention: 指定注解作用范围 三种 SOURCE, CLASS, RUNTIME
2. Target ：指定注解可以在哪些地方使用
3. Documented ：指定注解是否在javadoc体现
4. Inherited ：子类会继承父类注解

---



# 异常 Exception

```java
class ExceptionExercise{
    public static void main(String[] argc){
        int n1 = 1;
        int n2 = 0;
        //若程序员，认为一段代码肯出现异常/问题，可以使用 try-catch 异常处理机制来解决
        //将代码段选中， ctrl + alt + t -> 选中 try/catch
        //若进行了异常处理，那么即使出现了异常，程序也可以继续运行
        try {
            int res = n1 / n2;
        }catch (Exception e){
            //e.printStackTrace(); 抛出异常
            System.out.println(e.getMessage());
        }
        
        System.out.println("程序继续运行。。。");
    }
}
```

---

## 执行过程中的异常事件

可以分为两类：

1. **Error(错误)** ：java虚拟机无法解决的严重内部问题。如，JVM系统内部错误，资源耗尽等严重错误，例：StackOverflowError 栈溢出 ，OOM（out of memory）。Error 是严重错误，程序会崩溃。
2. **Exception**：其它因编程错误或偶然的外在因素的一般问题，可以使用针对性代码进行处理。例如空指针访问，试图读取不存在的文件，网络连接中断等。Exception 分为两大类：==运行时异常== 程序运行时，发生的异常；==编译时异常==，编程时，编译器检查出异常,必须处理，否则编译不通过。

---

## 五大常见运行时异常

1. **NullPointerException** 空指针异常：当程序试图在需要对象的地方使用 null 时，抛出该异常。
2. **ArithmeticException** 数学运算异常：当出现异常的运算条件时，抛出此异常。
3. **ArrayIndexOutOfBoundsException** 数组下标越界异常 ：访问数组元素越界。
4. **ClassCastException** 类型转换异常：当试图将对象强转转换为不是实例的子类时，抛出该异常。
5. **NumberFormatException** 数字格式不正确异常：当语言程序设计试图将字符串转换成一种数值类型，但该字符不能转为适当的格式时，抛出该异常。

---

## 异常处理方式

1. **try-catch-finally** : 程序员在代码中捕获异常，自行处理

   ```java
   try{
       代码/可能有异常;
   }catch (Exception e){
       //捕获异常
       //1.当异常发生
       //2.系统将异常封装成 Exception 对象 e，传递给 catch
       //3.得到异常对象后，程序员，自己处理
       
       // try 中代码不发生异常，不会执行 catch 中代码
   }finally{
       //不管 try 中代码是否发生异常，始终都要执行 finally 中的代码
       //所以通常把释放资源的代码放在 finally 中
   }
   ```

   ```java
   class TryCatchFinally01{
       public static void main(String[] argc){
           //可以有多个 catch 语句，要求父类异常在后，子类异常在前
           //多个catch 只能捕获一个异常 ，当 try 中代码发生异常，就不会继续执行剩余代码
           //也可以直接使用try-finally ,相当于没有捕获异常，因此程序会直接崩溃，就是执行一段代码，不管发生什么异常，都必须执行
           try{
               String str = "hello";
               int a = Integer.parseInt(str);//NumberFormatException
               int n1 = 10, n2 = 0;
               int res = n1 / n2;//ArithmeticException
           }catch (NumberFormatException nfe){
               Syetem.out.println("数据格式不正确：" + nfe.getMessage());
           }catch (ArithmeticException ae){
               Syetem.out.println("算术异常：" + ae.getMessage());
           }catch (Exception e){
               Syetem.out.println(e.getMessage());
           }
       }
   }
   ```

   

2. **throws** ：将发生的异常抛出，**交给调用者(方法)来处理**，最顶级的处理者就是JVM，JVM处理异常：输出异常信息，退出程序。

   ```java
   public class Throws01{
       public static void main(String[] argc){
           
       }
       
       public void f1() throws FileNotFoundException,ArithmeticException{
           //这里的异常是一个 FileNotFoundException 编译异常
           //可以使用 try-catch-finally 处理
           //也可以用 throws 抛出异常，让调用 f1 方法的调用者处理
           //1. throws 后的异常类型可以是方法中产生的异常类型，也可以它的是父类
           //2. throws 后可以是异常列表，即可以抛出多种异常
           FileInputStream fis = new FileInputStream("d://aa.txt");
       }
   }
   ```

**注意事项**

- 对于**编译异常，程序中必须处理**， try-catch 或者 throws, 否则编译不通过

- 对于运行时异常，程序中若没有处理，默认就是 throws 方式处理

- 子类重写父类方法时，对抛出异常的规定：**子类重写的方法，所抛出的异常要么和父类抛出异常类型一致，要么为父类抛出异常的子类型**

  ```java
  class Father{
      public void method() throws RuntimeException{
      }
  }
  
  class Son extends Father {
      public void method() throws NullPointerException{
      }
  }
  ```

- **try-catch-finally** 和 **throws** 二选一，要么自己处理，要么把异常抛给上级处理。

- 被抛出的**编译异常**，调用者必须处理，继续 throws 或者 try-catch

---

## 自定义异常

1. 定义类：自定义异常类名 继承 Exception 或者 RuntimeException
2. 若继承 Exception 则为编译异常
3. 若继承 RuntimeException 则为运行异常(一般继承 RuntimeException )

```java
public class CustomException{
    public static void main(String[] argc){
        int age = 200;
        if(age < 18 || age >100){
            throw new MyException("年龄要在 18 ~ 100 ");
        }
        System.out.println("年龄正确");
    }
}
//自定义一个异常
//1.一般情况下，我们的自定义异常是继承 RuntimeException
//2.即把自定义异常做成 运行异常 ，好处是，我们可以使用默认的处理机制
//3.不然写为编译异常的话，还需要抛出异常才能够编译通过
class MyException extends RuntimeException{
    public MyException(String message){
        super(message);
    }
}
```

---

## throw 和 throws 的区别

|        | 意义                   | 位置       | 后面跟的东西 |
| ------ | ---------------------- | ---------- | ------------ |
| throws | 异常处理的一种方式     | 方法声明处 | 异常类型     |
| throw  | 手动生成异常对象关键字 | 方法体中   | 异常对象     |

---

# 常用类

## 包装类

1. 针对八种基本数据类型相应的引用类型--包装类
2. 有了类的特点，就可以调用类中的方法

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| boolean      | Boolean   |
| char         | Character |
| byte         | Byte      |
| short        | Short     |
| int          | Interger  |
| long         | Long      |
| flaot        | Float     |
| double       | Double    |

数字类型包装类的父类：Number

### 包装类和基本数据类型转换

以 int 和 Integer 为例

```java
public class Integer01{
    public static void main(String[] argc) {
        //演示 int <--> Integer 的装箱和拆箱
        //jdk5 以前是手动装箱拆箱
        //手动装箱
        int n1 = 100;
        Integer integer = new Integer(n1);
        Integer integer = integer.valueOf(n1);
        
        //手动拆箱
        int n2 = integer.intValue();
        
        //jdk5 后就可以自动装箱拆箱
        //自动装箱
        int n2 = 200;
        Integer integer2 = n2;//底层使用的仍然时候 Integer.valueOf(n2)
        //自动拆箱
        int n3 = integer2;//底层使用的仍然时候 Integer.intValue()
        
        //tips
        //当范围在 -128 ~ 127 时就直接在 Integer 的缓冲区数组中，类加载时已经存在，直接返回，所以m，n是同一个引用
        Integer m = 1;
        Integer n = 1;
        System.out.println(m == n);//true
        
        //当不在者范围时，自动装箱会 new 一个Integer对象
        Integer x = 128;
        Integer y = 128;
        System.out.println(x == y);//false,不是同一个引用
        
        //tips2 包装类和基本数据类型比较时会自动拆箱
    }
}
```

---

### 包装类和 String 类型的相互转换

以 Integer 和 String 为例

```java
public class WrapperVSString{
    public static void main(String[] argc){
        Integer i = 100;//自动装箱
        //Integer -> String
        //方式1
        String str1 = i + "";//返回一个新字符串，i本身不会改变
        //方式2
        String str2 = i.toString();
        //方式3
        String str3 = String.valueOf(i);
        
        //String -> Integer
        //方式1
        String str4 = "123";
        Integer i2 = Integer.parseInte(str4);//自动装箱
        //方式2
        Integer i3 = new Integer(str4);//构造器
    }
}
```

### 包装类的常用方法

以 Integer 和 Character 为例

```java
public class Wrapper01{
    public static void main(String[] argc){
        Integer.MIN_VALUE;//返回最小值
        Integer.MAX_VALUE;//返回最大值
        
        Character.isDigit('1');//判断是否是数字
        Character.isLetter('a');//判断是否为字母
        Character.isUpperCase('A');//大写
        Character.isLowerCase('a');//小写
        Character.isWhiteSpace(' ');//空格
        Character.toUpperCase('a');//转大写
        Character.toLowerCase('A');//转小写
    }
}
```

---

## String 类

1. String 对象用于保存字符串，也就是一组字符序列
2. 字符串常量的对象双引用号括起来的字符序列
3. 字符串的字符使用Unicod字符编码，一个字符(不区分字母还是汉字)占两个字节

### ==**两种创建String对象的区别**==

方式一：直接复制 **String s = "hello"**

>先从常量池查看是否有 **"hello"** 数据空间，若有，直接指向，若无，则重新创建，然后指向。**s 最终指向的是常量池的地址空间**。

方式二 ：调用构造器 **String s = new String("hello")**

>先在堆中创建空间，里面维护了**value属性**，**指向常量池**的**"hello"**空间。若常量池中没有"hello"，重新创建，若有，直接通过value指向。**s 最终指向的是堆中的空间地址**。

### **String 对象特性**

- String 是一个 **final** 类，代表不可变的字符序列
- 字符串是不可变的。一个字符串对象一旦被分配，其内容是不可变的

```java
public class StringExercise{
    public static void main(String[] argc){
        
        String a ="hello" + "world";//创建了一个对象
        //底层自动优化 -> 等价于 String a = "helloworld";
        
        String b = "hello";
        String c = "world";
        String d = b + c;
        //1.先创建一个 StringBuilder s = StringBuilder();
        //2.执行 s.append("hello");
        //3.执行 s.append("world");
        //4. String  c = s.toString();
        //toString() new 了一个String 对象，所以c最终指向的是堆中空间
        //最后其实是 c 指向堆中对象(String) value[] -> 池中 "helloworld"
        
        String d = d.intern();//会去找d字符串在常量区的地址,d 引用最终指向常量c
    }
}
```

==重要规则==：String a = "ab" + "cd"; **常量相加，看的是常量池**。String a = b + c; **变量相加，是在堆中**

### String类的常用方法

- **s.equals(a)**//区分大小写，判断内容是否相同
- **s.equalsIgnoreCase(a)**//不区分大小写，判断内容是否相同
- **s.length()**//获取字符个数，字符串长度
- **s.indexOf('a')**//获取字符在字符串中第一次出现的索引
- **s.lastIndexOf('a')**//获取字符在字符串中最后一次出现的索引
- **s.substring(0,4)**//截取指定范围子串 左闭右开
- **s.trim()**//去除前后空格
- **s.charAt(0)**//获取某索引处的字符
- **stoUpperCase()**//全部转换成大写
- **s.toLowerCase()**//全部替换成小写
- **s.concat(a)**//拼接字符串
- **s.replace("a","b")**//把a替换成b
- **s.split("a")**//以 a 来分割字符串 用一个 String[] 来接收
- **s.toCharArray()**//转换成字符数组 
- **s1.compareTo(s2)**//比较两个字符串的大小，字典序，前大于后返回 正值，小于 负值，相等 0
- **format**//格式字符串
- **s.contains(s1)**//s是否包含子串 s1

```java
String info1 = String.format("姓名 = %s, 年龄 = %d", name, age);

String formatStr = "姓名 = %s, 年龄 = %d";
String info2 = String.format(formatStr, name, age);
```

所有操作原字符串不会发生改变，会返回操作后的新字符串

---

## StringBuffer 类

很多方法和String 相同，但是 **StringBuffer** 是可变长度的。

**StringBuffer** 是一个容器。

### 创建

```java
public class StringBufferExercise{
    public static void main(String[] argc){
        //StringBuffer 的直接父类是 AbstractStringBuilder
        //StringBuffer 实现了 Serializable 可以串行化
        //在父类 AbstractStringBuilder 有属性 char[] value ,不是 final，该value数组存放字符串的内容，存放在堆中
        //StringBuffer 是一个 final 类 不可被继承
        
        //1.创建一个空的 StringBuffer 初始容量 16 的 char[]
        StringBuffer sbf = new StringBuffer();
        
        //2.通过构造器指定 char[] 的大小
        StringBuffer sbf1 = new StringBuffer(100);
        
        //3.通过一个 String 去创建 初始容量 str.length() + 16
        StringBuffer sb2 = new StringBuffer("hello")
        
    }
}
```

**String vs StringBuffer**

1. String 保存的是字符串常量，里面的值是不能更改的，每次String 类的更新实际上就是更改地址，效率较低// **private final char[] value**
2. StringBuffer 保存的是字符串变量，里面的值可以更改，没吃StringBuffer 的更新实际上可以更新内容，不用每次更新地址，效率极高。// **char[] value 这个在堆中**

### String 和 StringBuffer 的相互转换

```java
public class StringBufferExercise{
    public static void main(String[] argc){
        //String -> StringBuffer
        String str = "hello";
        //1.使用构造器
        StringBuffer sbf1 = new StringBuffer(str);
        
        //2.使用 append 方法
        StringBuffer sbf2 = new StringBuffer();
        sbf2.append(str);
        
        //StringBuffer -> String
        //1.使用 StringBuffer 的 toString 方法
        String str2 = sbf2.toString();
        
        //2.使用构造器
        String str3 = new String(sbf2);
    }
}
```

### StringBuffer 常用方法

- **sbf.append(str)**//增加
- **sbf.delete(start, end)**//删除 左闭右开
- **sbf.replace(start, end, str)**//用str替换 左闭右开
- **sbf.indexOf(str)**//查找子串第一次出现的索引
- **sbf.insert(insertIndex, str)**//在索引处插入字符串,该索引位置及后面字符后移一位
- **sbf.length()**//长度
- **sbf.reverse()**//翻转

---

## StringBuilder

1. 一个可变的字符串序列。此类提供一个与 StringBuffer 兼容的PI,但是不保证同步（StringBuilder 不是线程安全的）。该类被设计作用于 StringBuffer 的一个简易替换，**用在字符缓冲区被单个线程使用的时候**。若可能，建议优先采用该类，因为在大多数实现中， 它比StringBuffer 更快。
2. 在 StringBuiilder 上的主要操作是 append 和 insert 方法，可以重载这些方法，以接收任意类型数据。

**String，StringBuffer 和 StringBuilder 三者比较**

1. **StringBuffer 和 StringBuilder** 非常类似，均代表可变的字符序列，而**方法也是一样的**。

2. **String** **不可变**的字符序列，**效率低**，但是**复用率高**。

3. **StringBuffer** **可变**字符序列，**效率较高**（增删），**线程安全**

4. **StringBuilder** **可变**字符序列，**效率最高**，**线程不安全**

5. String使用注意说明

   > String s = "a";//创建了一个字符串
   >
   > s += "b";//实际上原来的 "a" 字符串对象已经丢弃，现在又产生了一个新的字符串 s + "b"(也就是 "ab")。若多次执行这样改变字符串内容的操作，会导致大量副本字符串对象留存在内存中，降低效率。若这样的操作放在循环中，会极大影响程序的性能 => 结论：**若我们对字符串有大量的修改，不要使用 String**

---

## Math

```java
public class Math01{
    public static void main(String[] argc){
        //Math常用方法(静态方法)
        //1.abs绝对值
        int abs = Math.abs(-1);
        //2.pow 求幂
        double pow = Math.pow(2,4);//2的4次方
        //3.ceil 向上取整 返回>= 该参数的最小整数(double类型)
        double ceil = Math.ceil(1.1);//2.0
        //4.floor 向下取整
        double floor = Math.floor(1.1);//1.0
        //5.round 四舍五入
        long round = Math.round(5.5);//6
        //6. sqrt 开方
        double sqrt = Math.sqrt(9.0);//3.0
        //7. random 随机数 返回一个 0 <= x < 1的一个随机整数
        int x = (int)(a + Math.random() * (b - a + 1));// [a,b]内的一个随机整数
        //8.max ,min
        int max = Math.max(1,9);//9
    }
}
```

---

## Arrays

Arrays 里面包含了一系列静态方法，用于管理或操作数组

```java
public class Arrays01{
    public static void main(String[] argc){
        Integer[] integers = {1, 2, 3, 9, 7}
        //1.返回字符串形式
        System.out.println(Arrays.toString(integers));
        
        //2.sort 排序
        //方式一： 默认比较，从小到大
        Arrays.sort(integers);
        System.out.println(Arrays.toString(integers));
        //方式二：自定义比较器 实现了一个Comparator的匿名内部类，重写比较器
        //接口编程 + 动态绑定 + 匿名内部类
        Arrays.sort(integers,new Comparator<Integer>(){
            @Override
            public int compare(Integer o1, Integer o2){
                return o2 - o1;//从大到小
            }
        });
        
        //3. binarySearch 二分查找，要求必须有序,不存在返回 一个负数
        int index = Arrays.binarySearch(integers,3);
        
        //4.数组拷贝 copyOf
        Integer[] newArr = Arrays.copyOf(integers,integers.length);
        
        //5.数组填充 fill
        Integer[] arr1 = new Integer(){0,1,2};
        Arrays.fill(arr1,99);// {0，1，2} -> {99, 99, 99}
        
        //6.equals 比较两个数组元素内容是否完全一致
        boolean res = Arrays.equals(arr1, newArr);
        
        //7.asList 将一组值转换成 一个 List 集合
        List asList1 = Arrays.asList(2, 3, 4, 5);
    }
}
```

---

## System

```java
public class System01{
    public static void main(String[] argc){
        //1.arraycopy : 复制数组元素，比较适合地产调用
        //一般用 Arrays.copyOf 完成数组复制
        //System.arraycopy(src, srcPos, dest, destPos, length);
        int[] src = {1, 2, 3};
        int[] dest = new in[3];
        System.arraycopy(src, 0, dest, 0, 3);
        
        //2.currentTimeMillis 返回当前时间距 1970-1-1的毫秒数
        long unix = System.currentTimeMillis();
        
        //3.exit 退出当前程序, 0 表示退出状态，0为正常退出
        System.exit(0);
    }
}
```

---

## 大数处理

BigInteger 和 BigDecimal 类

```java
public class BigInteger01{
    public static void main(String[] argc){
        BigInteger bI = new BigInteger("11111111111111111111111111111111111");
        BigInteger bI1 = new BigInteger("100");
        System.out.println(bI);
        
        //在对 BigInteger 进行加减乘除运算时，需要采用相应的方法，不能直接运算
        BigInteger res = bI.add(bI1);
        res = bI.subtract(bI1);
        res = bI.mutiply(bI1);
        res = bI.divide(bI1);
        
        //精度很高的小数 BigDecimal
        BigDecimal bD = new BigDecimal("1.11111111111111111111111111111111");
        BigDecimal bD1 = new BigDecimal("1.11");
        
        BigDecimal res1 = bD.add(bD1);
        res1 = bD.subtract(bD1);
        res1 = bD.mutiply(bD1);
        res1 = bD.divide(bD1);//小数相除除不尽时，会抛出ArithmeticException
        
        //解决小数相除出现的异常，调用除法时指定精度
        //BigDecimal.ROUND_CEILING,若有无限循环，就会保留分子的精度
        res1 = bD.divide(bD1,BigDecimal.ROUND_CEILING);
         
    }
}
```

---

## 日期

### Date

```java
import java.util.Date;

public class Date01{
    public static void main(String[] argc){
        
        Date d1 = new Date();//获取系统当前时间，默认国外日期格式
        //格式转换，日期格式的字母是规定好的
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日，hh:mm:ss E");
        String format = sdf.format(d1);
        System.out.println("当前日期=" + format);
        
        //可以把一个格式化字符串，转换成对应的 Date
        String str = "2022年5月20日，20:41:59 星期五";
        Date parse = sdf.parse(str);
        System.out.println(parse);
            
    }
}
```

### Calendar

```java
public class Calendar01{
    public static void main(String[] argc){
        Calendar c = Calendar.getInstance();//创建日历对象
        //获取日历某个字段,没有提供相应的格式化对象
        System.out.println("年" + c.get(Calendar.YEAR));
        System.out.println("月" + (c.get(Calendar.MONTH) + 1));//月份返回默认从0开始编号
        System.out.println("日" + c.get(Calendar.DAY_OF_MONTH));
        System.out.println("小时" + c.get(Calendar.HOUR));
        System.out.println("分" + c.get(Calendar.MINUTE));
        System.out.println("秒" + c.get(Calendar.SECOND));
    }
}
```

Calendar 存在的问题：可变性，偏移性，格式化，线程不安全，不能处理闰秒

已弃用

### 第三代日期

**LocalDate（日期），LocalTime（时间），LocalDateTime（日期时间）**

```java
public class LocalDateTime01{
    public static void main(String[] argc){
        LocalDateTime ldt = LocalDateTime.now();
        //LocalDate.now();//LocalTime.now();
        ldt.getYear();
        ldt.getMonthValue();//月份数字
        ldt.getMonth();//月份英文
        ldt.getDayofMonth();
        ldt.getHour();
        ldt.getMinute();
        ldt.getSecond();
        
        //格式日期类 使用 DateTimeFormatter
        DateTimeFormatter dtf = new DateTimeFormatter.ofPattern("yyyy年MM月dd日，HH小时mm分钟ss秒");//HH 24小时制，hh12小时 
        String format = dtf.format(ldt);
        System.out.println(format);
        
        //提供 plus 和 minus 方法可以对日期时间进行加减
        LocalDateTime ldt1 = ldt.pulsDays(100);
        System.out.println("100天后是" + dtf.format(ldt1));
        
        //时间戳 Instant
        //1.通过静态方法 now() 获取表示当前时间戳的对象
        Instant now = Instant.now(); 
        //2.通过from 可以把 Instant 转成 Date
        Date date = Date.from(now);
        //3.通过 date 的 toInstant() 可以把 date 转成 时间戳
        Instant instant = date.toInstant();
    }
}
```

---



# 集合

## 集合框架体系

1. **单列集合 Collection**

   >**list**
   >
   >> **ArrayList**
   >>
   >> **LinkedList**
   >>
   >> **Vector**
   >
   >**Set**
   >
   >>**HashSet**
   >>
   >>**TreeSet**

2. **双列集合 Map**

   >**HashMap**
   >
   >**TreeMap**
   >
   >**HashTable**
   >
   >**Properties**

- 单列集合 存放的都是单个的元素；双列结合 存放的数据都是以 键值对 的形式存储

## Collection接口 

### Collection 方法

Collection 接口的常用方法， 以实现子类 ArrayList 来演示

```java
public class Colletion01{
    public static void main(String[] argc){
        List ls = new ArrayList();
        //1.添加单个元素 add
        ls.add("tony");
        ls.add(10);//ls.add(new Integer(10));
        ls.add(true);
        
        //2.删除 remove
        ls.remove(0);//按 index 删除，返回一个boolean 值表示删除成功失败
        ls.remove("tony");//删除指定元素
        ls.remove((Integer)10);//删除指定整数元素 强转为包装类 自动装箱
        
        //3.查找元素是否存在 contains
        System.out.println(ls.contains("tony"));
        
        //4.获取集合元素个数 size
        System.out.println(ls.size());
        
        //5.判空 isEmpty
        System.out.println(ls.isEmpty());
        
        //6.清空集合
        ls.clear();
        
        //7.添加多个元素 addAll
        ArrayList ls1 = new ArrayList();
        ls1.add(1);
        ls1.add("jack");
        ls.addAll(ls1);
        
        //8.查找多个元素是否存在 containsAll
        System.out.println(ls.containsAll(ls1));
        
        //9.删除多个元素 removeAll
        ls.removeAll(ls1);
       
    }
}
```

### 迭代器遍历

1. Iterator 对象称为迭代器，主要用于遍历 Collection 集合中的元素
2. 所有实现了Collection 接口的对象都有一个 iterator() 方法，用以返回一个实现了 Iterator 接口的对象，即可以返回一个迭代器
3. Iterator 仅用于遍历集合，本身并不存放对象

```java
public class Iterator01{
    public static void main(String[] argc){
        Collection list = new ArrayList();
        list.add("tony");
        list.add("jack");
        list.add("tom");
        //用 Itetator 遍历 ArrayList
        
        //1.先得到 list 对应的 迭代器
        Iterator iterator = list.iterator();
        
        //2.使用 while 循环遍历
        //我们每次调用 迭代器.next() 前需先判断迭代器.hasNext()
        while(iterator.hasNext()){
            Object next = iterator.next();//默认返回 Object
            System.out.println(next);//next 运行类型为String
        }
        //while 循环快捷键 itit；ctrl + j 显示所有快捷键
        
        //3.当退出while循环后，这时 iterator迭代器，指向最后一个元素
        //4.再次遍历，重置迭代器
        iterator = list.iterator();
        
    }
}
```

**增强 for 循环**

可以替代 iterator 迭代器，特点：增强 for 循环就是简化版的 iterator， 本质一样

**for(元素类型 元素名 ：集合名或数组名){**

​			**访问元素；**

**}**

```java
public class Iterator01{
    public static void main(String[] argc){
        Collection list = new ArrayList();
        list.add("tony");
        list.add("jack");
        list.add("tom");
        //快捷键 I
        for(Object name : list){
             System.out.println(name);
        }
        //也可以用于数组
        
        int[] nums = {1, 2, 3};
        for(int i : nums){
            System.out.println(i);
        }
    }
}
```

### List 接口

#### list 方法

1. List 集合中的元素是有序的，且可以重复

2. List 集合中的每个元素都有其对应的索引，即支持索引

3. List 容器中的元素都对应一个整数型的序号记载其在容器中的位置，可根据序号存取容器中的元素

4. List 接口的实现类 常用的有： ArrayList, LinkedList, Vector

5. List 的三种遍历方式 [ArrayList, LinkedList, Vector] 

   >使用 iterator 遍历
   >
   >增强 for 循环
   >
   >普通 循环

```java
public class List01{
    public static void main(String[] argc){
        //1.添加顺序和取出顺序一致,且可重复
        List list = new ArrayList();
        list.add("tony");
        list.add("jack");
        list.add("tom");
        list.add("tony");
        System.out.println(list);
        
        //2.支持索引 获得指定索引处元素 list.get(index) 索引从0开始
        System.out.println(list.get(1));
        
        //3.在指定索引 插入元素 list.add(index,obj)
        list.add(2,"jennie");
        
        //4.返回对象在集合中首次出现的位置 indexOf(obj)
        System.out.println(list.indexOf("tom"));
        
        //5.返回对象在集合中最后出现的位置 lastIndexOf(obj)
        System.out.println(list.lastIndexOf("tony"));
        
        //6.移除指定 index 位置元素 remove(index)
        list.remove(0);
        
        //7.替换指定索引处元素 set(index,obj)
        list.set(1,"marry");
        
        //8.返回子集 subList(fromIndex, toIndex)
        List returnList = list.subList(0,2);//[0,2)
    }
}
```

#### ArrayList 动态数组 底层分析

1. ArrayList 中维护了一个 Object 类型的数组 elementData。 transient Object[] elementData;//transient 表示该属性不会被序列化
2. 当创建 ArrayList 对象时，若使用的是无参构造器，则 elementData  的初始容量为 0，第一次添加元素，则扩容至 10，若需要再次扩容，则扩容为 1.5 倍。
3. 若使用的是指定大小的构造器，则初始 elementData 容量为指定大小，若需要扩容，则扩容 1.5 倍。
4. **ArrayList 线程不安全**

#### Vetvor 动态数组 底层分析

1. Vector 底层也是一个对象数组， protected Object[] elementData;
2. **Vector 是线程同步的**，即线程安全，其余功能与 ArrayList 相同
3. 开发中，需要线程安全，考虑 Vector
4. 无参，默认 10 ，满后 2 倍扩容；指定大小，满了 2 倍扩容

#### LinkedList 双向链表 底层分析

1. LinkedList 底层实现了双向链表和双端队列特点
2. 可以添加任意元素，可重复
3. 线程不安全
4. LinkedList 中维护了两个属性 **first** 和 **last** 分别指向 首结点和尾结点
5. 每个结点（**Node** 对象）里面又维护了 **prev，next，item** 三个属性

### Set 接口

和 List 接口一样也是 Collection 的子接口，因此常用方法和 Callection 接口一样

**去重的，无序的**

**Set 接口遍历方式**：迭代器；增强for循环；**无索引**。

#### Set 方法

```java
//以 HashSet 为例
public class Set01{
    public static void main(String[] argc){
        Set set = new HashSet();
        set.add("tony");
        set.add("tom");
        set.add("mark");
        set.add(null);
        set.add(null);
        //Set 接口的实现类的对象是去重的，无序的
        //取出的顺序不同于添加的顺序，但是固定的
        
        //遍历
        //1. 迭代器
        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
        
        //2.增强 for
        for(Object obj : set){
            System.out.println(obj);
        }
        
    }
}
```

#### HashSet

1. HashSet 实现了 Set 接口

2. HashSet 底层通过 HashMap 实现

   >在 HashSet 中添加一个元素时，元素为 key，**其value 用一个常量 present 来填充**，**由 key 计算hash值 再由 hash 值计算得到索引**
   >
   >找到存储数据的 table 中，该索引位置是否已经存放对象（**即先比较 hash 值**）
   >
   >若没有元素，直接添加
   >
   >若存在元素，则**比较 key 值 | | 调用 equals 比较对象**，若相同，就放弃添加，若不同则继续向后比较至链表（或树）尾，则添加
   >
   >在 Java8 中，若一条链表元素个数 **>= TREELFY_THRESHOLD(默认 8)**，**表先扩容，重整链表上的结点 resize()**，直到 table 的大小 **>= MIN_TREELFY_CAPACITY(默认 64 )，就会转化为红黑树**
   >
   >扩容：1. 还未树化时链表元素个数 >= 8 ，元素个数 < 64；2.到达临界值
   >
   >​	第一次添加时，table 数组扩容到 16， **临界值（threshold）是 16 * 加载因子（loadFactor）是0.75 = 12**
   >
   >​	若 table 数组**到达临界值**，就会**扩容至 2 倍**，并且得到新临界值

3. 可以存放 null 值

#### LinkedHashSet

1. 底层是一个 LinkedHashMap，底层维护了一个**和HashSet一样 并增加一个双向链表**

2. LinkedHashSet 根据元素的 hashCode 值来决定存储位置，同时**使用双向链表维护元素次序**，看起来像是有序插入的

3. 每个结点三个指针域 **before，after，   LinkedHashMap$Entry 继承了 HashMap$Node** 所以也有 **next 域**

   >before, after 用于保存插入次序
   >
   >next 解决冲突的链表

#### TreeSet

**可以排序**

```java
public class TreeSet01{
    public static void main(String[] argc){
        //1.当我们使用无参构造器，创建TreeSet时，默认 键的类实现 接口 Comparable的 compareTo 方法
        //2.通过匿名内部类 实现 Comparator 接口的 compare 方法自定义排序规则
        //若以上两个方法都未实现，则往 TreeSet 中添加元素是会报 ClassCastException
        //3.TreeSet 底层是 TreeMap 实现 value 是 present 的常量
        //4.TreeMap 中 确定添加的元素是否相等是由 我们 自定义的 compare 方法决定的，返回 0 即认为加入的对象是相等的
        TreeSet treeSet = new TreeSet(new Comparator() {
            @Override
            public int compare(Object o1, Object o2){
                return ((String) o1).compareTo((String) o2);
            }
        });
        
        treeSet.add("jack");
        treeSet.add("tom");
        treeSet.add("tony");
        
        System.out.println(treeSet);
    }
}
```





## ==Map接口==

1. Map 用于保存具有映射关系的数据 **key-value**
2. Map 中的 key 和 value 可以说任意的引用类型的数据，会封装到 HashMap$Node 对象中
3. Map 中 key 值不允许重复，value 可以重复，都可以为 null
4. key 和 value 之间存在单一的一对一关系，通过 key 值总能找到对应的 value

```java
public class Map01{
    public static void main(String[] argc){
        //以 HashMap 为例
        Map map = new HashMap();
        map.put("no1","tony");
        map.put("no2","jack");
        map.put("no1","lily");//当有相同的 key 时，相当于替换对应 value 的值
        map.put(null,null);
        map.put(null,"abc");//value 替换
        map.put("no3",null);
        
        System.out.println(map);
        
        //1.k-v 最后是 HashMap$Node node = newNode(hash, key, value, null)
        //2.k-v 为了方便程序员遍历，还会创建一个 EntrySet 集合， 该集合存放的元素类型是 Entry，而一个 Entry 对象就要 k,v EntrySet<Entry<k,v>> 即 transient Set<Map.Entry<k,v>> entrySet;
        //3.entrySet 中，定义的类型是(运行类型) Map.Entry, 但是实际上存放的还是 HashMap$Node(运行类型)(多态集合，Node<k,v> 实现了 Map.Entry<k,v> 接口)
        //4.当把 HashMap$Node 对象到 entrySet 就方便我们的遍历，因为 Map.Entry 提供了重要的方法 k getKey(); v getValue();
        
        Set set = map.entrySet();
        System.out.println(set.getClass());//HashMap$EntrySet
        for(Object obj : set){
            Map.Entry entry = (Map.Entry) obj;
            Sytem.out.println(entry.getKey() + '-' + entry.getValue());
        }
        
    }
}
```

### Map 接口方法

```java
public class Map02{
    public static void main(String[] argc){
        //以 HashMap 为例
        Map map = new HashMap();
        
        //1.添加 put(key, value) 当有相同的 key 时，相当于替换对应 value 的值
        map.put("no1","tony");
        map.put("no2","jack");
        
        //2.remove 根据键删除映射关系
        map.remove("no1");
        
        //3.get 根据键获取值
        Object name = map.get("no1");
        
        //4. isEmpty() 判空
        System.out.println(map.isEmpty());
        
        //5. clear() 清空
        map.clear();
        
        //6. size() 获取元素个数
        System.out.println(map.size());
        
        //7. containsKey 查找键是否存在
        System.out.println(map.containsKe("no1"));
        
    }
}
```

### Map遍历方式

```java
public class Map02{
    public static void main(String[] argc){
        //以 HashMap 为例
        Map map = new HashMap();
        map.put("no1","tony");
        map.put("no2","jack");
        
        //方法一：先取出所有的 key 再通过 key 取出对应的 value
        Set keyset = map.keySet();
        //(1) 增强 for
        for(Object key : keyset){
            System.out.println(key + '-' + map.get(key));
        }
        //(2) 迭代器
        Iterator iterator = keyset.iterator();
        while(iterator.hasNext()){
            Object key = iterator.next();
            System.out.println(key + '-' + map.get(key));
        }
        
        //方法二：直接取出所有 value 值
        Collection values = map.values();
        //可以使用所有的 Collection 使用的遍历方式
        
        //方法三：通过 EntrySet 来获取 k-v
        Set entrySet = map.entrySet();
        //(1) 增强 for
        for (Object entry : entrySet){
            //将 entry 转成 Map.Entry
            Map.Entry m = (Map.Entry) entry;
            System.out.println(m.getKey() + '-' + m.getValue());
        }
        
        //(2) 迭代器
        Iterator iterator01 = entrySet.iteraror();
        while(iterator01.hasNext()){
            Map.Entry m = (Map.Entry) iterator01.next();
            System.out.println(m.getKey() + '-' + m.getValue());
        }
    }
}
```

### HashMap 小结

1. Map 接口常用的实现类：HashMap，HashTable ，Properties
2. HasMap  是以 key-val 对 的方式来存储数据的（HashMap$Node类型）
3. key不可重复，value可以重复，允许 null 做 键或值
4. 若添加相同的 key，则会覆盖原来的 key-val 映射，等同于修改
5. 与 HashSet 一样不保证映射顺序，底层以 hash 表的形式来存储
6. **HashMap 没有实现同步，线程不安全 **

### HashTable

1. 存放的元素是键值对
2. HashTable 的**键和值都不能为 null** ，否则会抛出 NullPointerException
3. HashTable 使用的方法基本和 HashMap 一样
4. HashTable 是**线程安全**的

底层机制：

>1. 底层有数组 HashTable$Entry[] 初始化大小为 11（HashTable$Entry 实现了 Map.Entry）
>2. 临界值 threshold 8 = 11 * 0.75
>3. 扩容：按照自己的扩容机制扩容
>4. 执行方法 addEntry(hash, key, value, index); 添加 k-v 封装到 Entry
>5. 当 count >= threshold 满足时，就进行扩容
>6. 按照 int newCapacity = (oldCapacity << 1) + 1 的大小扩容

### Properties

1. Properties 类继承值 HashTable 类，也是以键值对的形式来保存数据
2. 他的使用特点和 HashTable 类似
3. Properties 还可以用于从 xxx.properties 文件中，加载数据到 Properties 类对象，并进行读取和修改
4. 工作中 xxx.properties 文件通常作为配置文件



#### TreeMap

## Collections工具类

1. Collections 是一个操作 Set, List 和 Map 等集合的工具类
2. Collections 中提供了一系列静态方法对集合的元素进行排序，查询，修改等操作

```java
public class Collections{
    public static void main(String[] argc){
        List list = new ArrayList();
        lsit.add("tony");
        list.add("mark");
        lsit.add("tom");
        
        //1.翻转 list 中元素次序
        Collections.reverse(list);
        
        //2.打乱 list 元素顺序
        Collections.shuffle(list);
        
        //3.根据元素自然顺序排序
        Collections.sort(list);
        
        //4.自定义排序
        Collections.sort(list, new Comparator{
           	@Override
            public int compare(Object o1, Object o2){
                return ((String) o1).compareTo((String) o2);
            }
        });
        
        //5.交换 list 中 index i 和 j 处的元素
        Colletions.swap(list, 1, 2); 
        
        //6.返回自然顺序最大/小的元素
        System.out.println(Collectons.max(lsit));
        System.out.println(Collectons.min(lsit));
        
        //7.返回自定义比较的最大/小元素
        System.out.println(Collectons.max(lsit, new Comparator(){
            @Override
            public int compare(Object o1, Object o2){
                return ((String) o1).length() - ((String) o2).length();
            }
        }));
        
        //8.统计指定元素的词频
        int fre = Collections.frequency(list,"tom");
        
        //9.将 src 中的内容复制到 dest 中 dest.size() 应该大于等于 src.size()
        ArrayLsit dest = new ArrayList();
        for(int i = 0;i < list.length();i++){
            dest.add("");
        }
        Collections.copy(dest, src);
        
        //10. 使用新值替换所有原来的旧值
        Collections.replaceAll(list,"tony","托尼")
        
    }
}
```

---



# 泛型

使用传统方法，不能对加入到集合中的数据类型进行约束（这是不安全的），遍历的时候，需要进行类型转换，对效率有影响。引入泛型解决。

泛型好处：编译时，检查添加数据类型，提高了安全性；减少了类型转换的次数，提高了效率。

## 泛型语法

1. 泛型又称参数化类型
2. 在类声明或实例化时重要指定好需要的具体的数据类型即可
3. Java泛型可以保证若程序在编译时没有发出警告，运行时也不会产生ClassCastException异常
4. 泛型的作用是：可以在类声明时通过一个标识表示内部的某个属性的类型，或者是某个方法 的返回值类型，或者是参数类型。
5. 泛型具体的数据类型在实例化对象的时候指定，即在编译期间确定泛型是什么数据类型。

```java
public class Generic01{
    public static void main(String[] argc){
        //以 ArrayList 为例
        //1.当我们 ArrayLisr<Integer> 表示存放到 ArrayList 集合中元素是 Integer
        //2.若编译器发现添加的类型，不满足要求，就会报错
        //3.在遍历的时候，可以直接取出 Integer 类型，而不是 Object 类型
        //4.public class ArrayList<E> {} E称为泛型，那么我们则指定 Integer->E
        ArrayLisr<Integer> arrayList = new ArrayList<Integer>();
        
        Person<String> person = new Person<String>("tony");//指定泛型 E 为 String
        //泛型指定简写，编译器会进行类型推断
        Person<String> person1 = new Person<>("tony");
    }
}
//泛型可以是任意字母
class Person<E>{ //自定义泛型类
    E s;//泛型标识属性
    public Person(E s){//泛型标识函数参数类型
        this.s = s;
    }
    public E f(){//泛型标识函数返回值类型
        return s;
    }
}
//自定义泛型接口
interface Test<T>{}

class Test1{
    //自定义泛型方法
    public <T,R> void run(T r, R r){} 
}
```

tips

- 给泛型指定的类型 必须是引用类型，不能是基本数据类型
- 给泛型指定类型后，传入的数据类型也可以为指定类型的子类类型
- 当我们实例化对象不指定泛型类型时，默认为 Object



## 自定义泛型

**class 类名<T,R,...>{**

​	**成员**

**}**

1. 普通成员可以使用泛型
2. 使用**泛型数组**，**不能初始化**
3. 静态方法中不能使用类的泛型
4. 泛型类的类型，是在创建对象时确定的
5. 若创建对象时，没有指定类型，默认 Object

**interface 接口名<T,R,...>{**

**}**

1. 接口中，静态成员不能使用泛型
2. 泛型接口的类型，在**继承接口**或者**实现接口时**确定
3. 不指定，默认为 Object



**修饰符 <T,R,...> 返回类型 方法名(参数列表) {**

**}**

1. 泛型**方法被调用时，指定泛型类型**，当调用方法时，传入参数，编译器会自动确定类型
2. 泛型方法，可以定义在普通类中，也可以定义在泛型类中
3. 例 **public void run(E e){}** ,修饰符后没有 <T,R,..> ，该方法就不是泛型方法，而是使用了泛型的方法。

## 泛型的继承和通配符

1. 泛型没有继承性

   >例： List<Object> lsit = new ArrayList<String>();//这是错误的
   >
   >泛型指定后应该是唯一的，虽然 String 是 Object 的子类，当时仍给泛型指定了两个类型，这是错误的

2. **<?>** : 支持任意泛型

3. **<? extends A> **: 支持 A 类以及 A 类的子类，规定了泛型的上限

4. **<? super A>** : 支持A 类以及 A 类的父类，规定了泛型的下限



## JUnit

1. 一个类有很多功能代码需要测试，为了测试，就需要写入 main 方法中
2. 若多个功能代码测试，就需要来回注销，很麻烦
3. 可以使用 JUnit 单元测试框架 来直接运行一个方法，就方便很多

```java
package com.JUnit_;

import org.junit.jupiter.api.Test;

public class JUnit_ {
    public static void main(String[] args) {
        //传统方法,需要 new 一个对象才能调用
        new JUnit_().m1();
        new JUnit_().m2();
    }
	//添加 @Test 快捷键 alt + enter 导入文件后可以对方法进行单元测试
    @Test
    public void m1(){
        System.out.println("方法一");
    }
    @Test
    public void m2(){
        System.out.println("方法二");
    }
}

```

# JAVA事件处理机制

Java 事件处理是采取“委派事件模型”。当事件发生时，产生事件的对象，会把“信息”传递给“事件监听者”处理，这里所说的“信息”实际上就是 java.awt.event 事件库里的某个类所创建的对象，把它称为“事件的对象”。

1. 事件源：事件源是一个产生事件的对象，比如按钮，窗口等
2. 事件：事件就是承载事件源状态改变时的对象，比如当键盘事件，鼠标事件，窗口事件等等，会产生一个事件对象，该对象保存着当前事件的很多信息，比如 KeyEvent 对象有含义被按下键的 Code 值。java.awt.event 包 和 javax.swing.event 包中定义了各种事件类型。

3. 事件类型：

| 事件类          | 说明                                                 |
| --------------- | ---------------------------------------------------- |
| ActionEvent     | 通常在按下按钮，或双击一个列表项或选中某个菜单时发生 |
| AdjustmentEvent | 当操作一个滚动条时发生                               |
| ComponentEvent  | 当一个组件隐藏，移动，改变大小时发生                 |
| ContainerEvent  | 第一个组件从容器中加入或删除时发生                   |
| FocusEvent      | 当一个组件获得或失去焦点时发生                       |
| ItemEvent       | 当一个复选框或列表项被选中，选择框或选择菜单被选中   |
| KeyEvent        | 当从键盘的按键被按下，被松开时发生                   |
| MouseEvent      | 当鼠标移动，点击时发生                               |
| TextEvent       | 当文本区和文本域的文本发生改变时发生                 |
| WindowEvent     | 当一个窗口激活，关闭，失效，恢复，最小化，...        |

4. 事件监听器接口

   >当事件源产生一个事件，可以传给事件监听者处理

   >事件监听者实际上是一个类，该类实现了某个事件监听器接口
   >
   >一个类可以实现多个事件监听接口

---

# 多线程基础

## 线程使用

在 java 中线程使用有两种方式

1. **继承 Thread 类，重写 run 方法**
2. **实现 Runnable 接口，重写 run方法**

```java
public class Test{
    public static void mian(String[] argc){
       
        //一 继承 Thread 类
        //创建 Test1 对象 可以当作线程使用
        Test1 t1 = new Test1;
        //启动线程 最终会执行 Test1 中的 run 方法
        t1.start();
        //当main 线程启动一个子线程 Thread-0 ，主线程不会阻塞，会继续执行
        
        //直接调用run 方法，并不会启动线程，只是一个普通的方法调用
        t1.run();
        
        //二 实现 Runnable 接口
        Test2 t2 = new Test2();
        Thread thread = new Thread(t2);
        thread.start();
    }
}


//1.当一个类继承了 Thread 类，该类就可以当作线程使用
//2.我们会重写 run 方法，写上自己的业务代码
//3. run Thread 类实现了 Runnable 接口的 run 方法
class Test1 extends Thread{
   public void run(){
       System.out.println("test1");
       try{
           Thread.sleep(1000);//单位毫秒
       }catch ( InterrupteException){
           e.printStackTrace();
       }
   } 
}

class Test2 implements Runnable{
    ublic void run(){
       System.out.println("test2");
       try{
           Thread.sleep(1000);//单位毫秒
       }catch ( InterrupteException){
           e.printStackTrace();
       }
   } 
}
```

终端 jconsole 命令调出控制台，可以查看进程，线程

**继承 Thread 类 vs 实现 Runnable 接口的区别**

1. 从 java 的设计来看，通过继承 Thread 或者实现 Runnable 接口来创建线程本质上没有区别，从 jdk 帮助文档中可以看到 Thread 类本身就实现了 Runnable 接口
2. 实现 Runnable 接口方式**适合多个线程共享一个资源**的情况，并且**避免了单继承的限制**，建议使用 实现 Runnable 接口

**线程终止**

1. 当线程完成任务，会自动退出
2. 还可以使用变量来控制 run 方法退出的方式停止线程，即通知方式

## 线程常用方法

```java
public class ThreadMethod{
    public static void main(){
        //测试相关方法
        T  t = new T();
        
        //设置线程名 .setName("tony");
        t.setName("tony");
        
        //设置优先级 .setPriorty(Thread.MIN_PRIORTY);
        //优先级范围 min ~ max,MIN_PRIORTY 1, NORM_PRIORTY 5 (默认), MAX_PRIORTY 10
        t.setPriorty(Thread.MIN_PRIORTY);
        
        //启动线程 .start();
        t.start();
        
        //获取线程名  .getName();
        System.out.println(t.getName());
        
        //获取线程优先级 .getPriorty();
        System.out.println(t.getPriorty());
        
        //获取线程状态 .getState();
        System.out.println(t.getState());
        
        //中断线程 .interrupt();
        t.interrupt();
    }
}

class T extends Thread {//自定义的线程类
    @Override
    public void run(){
        //获取线程名 .getName();
        System.out.println("当前线程名：" + Thread.currentThread().getName());
        
        try{
            System.out.println(Thread.currentThread().getName() + "休眠");
            //休眠 .sleep(time);
            Thread.sleep(20000);//单位毫秒， 20秒
        }catch (InterruptedException e){
            //当该线程执行到一个 interrupt 方法时，就会 catch 一个异常，可以加入自己业务代码
            //InterruptedException 是捕获到一个中断异常
            System.out.println(Thread.currentThread().getName() + "被 interrupt");
        }
    }
}
```

1. **yield** :线程的礼让。**让出cpu**，让其它线程执行，但礼让的时间不确定，所以也不一定礼让成功。cpu较空闲时，可能礼让了，而其它线程已经获得cpu资源，所以**不一定成功**，cpu 忙碌时更容易成功。
2. **join**：线程的插队。插队**一定成功**，插队的线程一旦插队成功，则**肯定先执行完插入的线程的所有任务**

```java
public class ThreadMethod01{
    public static void main(String[] argc){
        T t = new T();
        t.start();
        
        for(int i = 0; i <= 20 ; i++){
            Thread.sleep(1000);
            System.out.println("主线程 i =" + i);
            if(i == 5){
                System.out.println("主线程让子线程先执行");
                t.join();//这里相当于让 t 子线程插队先执行
                //Thread.yield();//礼让，不一定成功
                System.out.println("子线程执行完毕，主线程继续执行");    
            }
        }
    }
}


class T extends Thread {//自定义的线程类
    @Override
    public void run(){
        for(int i = 0; i <= 20; i++){
            try{
                Thread.sleep(1000);
            }catch (InterruptedException e){
                e.printStackTrace();
            }
            System.out.println("子线程 i =" + i);  
     	}
    }
}
```

## 守护线程

1. 用户线程：也叫工作线程，当线程的任务执行完或通知方式结束
2. 守护线程：一般是为工作线程服务的，当所有的用户线程结束，守护线程自动结束
3. 常见的守护线程：垃圾回收机制

```java
public class ThreadMethod{
    public static void main(String[] argc) throws InterruptedException{
        MyDeamonThread myDT = new MyDeamonThread();
        
        //若我们希望当main线程结束后，子线程自动退出
        //只需将子线程设置为守护线程 .setDeamon(true);
        //先设置，再启动
        myDT.setDeamon(true);
        myDT.start();
        
        for(int i = 0; i <= 20 ; i++){
            System.out.println("main");
            Thread.sleep(1000);
        }
    }
}

class MyDeamonThread extends Thread{
    public void run(){
        for(;;){
            System.out.println("myDT");
        }   
    }
}
```

---

## 线程七大状态

1. **new**: 创建态

2. **runnable**：可运行态

   >**Ready**: 就绪态  线程被调度器选中执行 Ready -> Running
   >
   >**Running** ：运行态  线程被挂起，Thread.yield  Running -> Ready

3. **TimeWaiting** : 超时等待  Thread.sleep(time), o.wait(time), t.join(time), LockSupport.parkNanos(), LockSupport.parkUntil() 时间到自动唤醒

4. **Waiting**: 等待  o.wait(), t.join(), LockSupport.park()   需要通过 o.notify(), o.notifyAll(), LockSupport.unpark() 唤醒

5. **Blocked**: 阻塞  等待进入同步代码块的锁 进入， 获得锁后不在阻塞

6. **Teminated**: 终止 

---

## 线程同步

### 线程同步机制

在多线程编程中，一些敏感的数据不允许被多个线程同时访问，此时就使用同步访问技术，保证数据在任何同一时刻，最多一个线程访问，以保证数据的完整性。

**同步的具体方法 Synchronized**

1. 同步代码块

   >**synchronized (对象) {//得到对象的锁，才能操作同步代码**
   >
   >​	**//需要同步的代码**
   >
   >**}**

2. synchronized 还可以放在方法声明中，表示整个方法为同步方法

   >**public synchronized void method(参数列表){**
   >
   >​	**//需要被同步的代码**
   >
   >**}**

### 互斥锁

1. java 语言中引入了**对象互斥锁**的概念，来保证共享数据的完整性
2. 每个对象都对应于一个可称为“互斥锁” 的标记，这个标记用来保证在任意时刻，只能有一个线程访问该对象
3. 关键字 synchronized 来与对象的互斥锁联系。当某个对象用 synchronized 修饰时，表明该对象在任意时刻只能由一个线程访问 
4. 同步的局限性：导致程序的执行效率降低
5. 同步方法（非静态）的锁可以是 this，也可以是其它对象引用（要求指向同一个对象）
6. 同步方法（静态）的锁当前类本身的
7. 尽量使用同步代码块

```java
class Test implements Runnable{
    public void run(){
        this.method01();
        this.method02();
        this.method03();
	}
    
    //public synchronized void method01() {} 就是一个同步方法
    //这时锁在 this 对象上
    //也可以在代码块上写 synchronized，同步代码块
    public /*synchronized*/ void method01(){
        synchronized (this){
            System.out.println("同步代码块");
        }
    }
    
    
   //同步方法是静态的，其锁为当前类本身
   public synchronized static void method02(){
       System.out.println("同步静态方法");
   }
   //静态方法里的同步代码块 synchronized (当前类.class){代码块}
    public static void method03(){
        synchronized (Test.class){
            System.out.println("静态方法同步代码块");
        }
    }
}
```

---

### 锁的释放

以下操作会释放锁

1. 当前线程的同步方法，同步代码块执行结束
2. 当前线程在同步代码块，同步方法中遇到 break， return
3. 当前线程在同步代码块，同步方法中出现了未处理的 Error 或 Exception ，导致异常结束
4. 当前线程在同步代码块，同步方法中执行了线程对象的 **wait()** 方法，当前线程暂停，并释放锁

下面操作不会释放锁：

1. 当前线程在同步代码块，同步方法时，调用了 Thread.sleep(), Thread.yield() 方法暂停当前线程的执行，不会释放锁
2. 线程执行同步代码块时，其它线程调用了该线程的 suspend() 方法将该线程挂起，该线程不会释放锁
3. 应该尽量避免使用 suspend() 和 resume() 来控制线程

---

# IO流

## 文件

### 文件创建

**创建文件对象**

1. **new File(String pathName);**//根据路径构建一个文件对象
2. **new File(File parent, String child);**//根据父目录文件 + 子路径创建
3. **new File(String parent, String child);**//根据父目录 + 子路径构建

**根据文件对象创建文件**

1. **file.createNewFile();**// 创建新文件
2. **file.mkdir();**//创建单级目录文件
3. **file.mkdirs();**//创建多级目录

```java
public class FileCreate{
    public static void main(String[] argc){
        
    }
   
    //1.new File(String pathName);
    public void create01(){
        String filePath = "e:\\news1.txt";
        File file = new File(filePath);
        
        try{
            file.createNewFile();//此处才真正的创建了文件
        }catch (IOException e){
            e.printStackTrace();
        }
        
    }
    
    //2.new File(File parent, String child);
    public void create02(){
        File parent = new File("e:\\");//父目录文件对象
        String fileName = "news2.txt";
        File file = new File(parent, fileName);
        
        try{
            file.createNewFile();
        }catch (IOException e){
            e.printStackTrace();
        }
    }
    
    //3.new File(String parent, String child);
    public void create03(){
        String parentName = "e:\\";
        String fileName = "news3.txt";
        File file = new File(parentName, fileName);
        
        try{
            file.createNewFile();
        }catch (IOException e){
            e.printStackTrace();
        }
        
    }
}
```

### 获取文件信息

```java
public class FileInformation {
    public static void main(String[] argc){
        
    }
    
    public void fileInformation(){
        //创建文件对象
        File test = new File("e:\\news1.txt");
        
        //获取相应信息的方法
        System.out.println("文件名 = " + file.getName());
        System.out.println("绝对路径 = " + file.getAbsolutePath());
        System.out.println("文件父级目录 = " + file.getParent());
        System.out.println("文件大小 = " + file.length());//以字节统计
        System.out.println("文件是否存在 = " + file.exists());
        System.out.println("是否是一个普通文件 = " + file.isFile());
        System.out.println("是否是一个目录文件 = " + file.isDirectory());
    }
}
```

### 目录的操作和文件删除

```java
public class Directory01{
    public static void main(String[] argc){
        
    }
    
    //判断 e:\\news.txt 文件是否存在，若存在就删除
    public void deleteFile(){
        String path = "e:\\news.txt";
        File file = new File(path);
        if(file.exists()){
            if(file.delete()){//文件删除会返回一个 布尔值表示是否成功删除
                System.out.println("删除成功");
            }else{
                System.out.println("删除失败");
            }
        }else{
             System.out.println("文件不存在");
        }
    }
    
    //判断 e:\\dir1 目录是否存在，若存在就删除(该目录为空)
    //目录也是一种特殊的文件，空目录可以直接删除                               
    public void deleteDir(){
        String path = "e:\\dir1";
        File dir = new File(path);
        if(dir.exists()){
            if(dir.delete()){//文件删除会返回一个 布尔值表示是否成功删除
                System.out.println("删除成功");
            }else{
                System.out.println("删除失败");
            }
        }else{
            if(dir.mkdir()){//mkdir 创建目录 mkdirs 创建多级目录，返回布尔值表示创建成功与否
                System.out.println("目录创建成功");
            }else{
                System.out.println("创建失败");
            }
        }
    }                                                                      
}
```

---

## IO流原理级流分类

### **流的分类**

1. 按操作数据的单位不同分为：字节流（8 bit）二进制文件，字符流（按字符）文本文件

2. 按数据流向不同分为：输入流，输出流

3. 按流的角色的不同分为：节点流，处理流/包装流

   >节点流可以从一个**特定的数据源读写数据**，如 FileReader，FileWriter 等
   >
   >处理流（又叫**包装流**）是**”连接“在已存在的流（节点流或处理流）之上**，为程序提供更为强大的读写功能，如BufferedReader，BufferedWriter，...

| 抽象基类 | 字节流       | 字符流 |
| -------- | ------------ | ------ |
| 输入流   | InpuStream   | Reader |
| 输出流   | OutputStream | Writer |

---

### IO 节点流的常用类

#### 1.**FileInputStream** 的使用（字节输入流 文件 --> 程序）

```java
public class FileInputStream01{
    public static void main(String[] argc){
        
    }
    
    public void readFile01() {
        String filePath = "e:\\news1.txt";
        int readData = 0;
        
        byte[] buf = new byte[8];//一次读8个字节
        int readLen = 0;
        
        FileInputStream fileInputStream = null;
       try{
           //创建 FileInputStream 对象，用于读取文件
           fileInputStream = new FileInputStream(filePath);
           //1.从输入流读取一个字节的数据,若返回 -1 表示读取结束
           //while((readData = fileInputStream.read())! = -1){
           //    System.out.print((char)readData);
           //}
           
           //2.读取到buf中 readLen 接收返回的读取字节数，不足 8 个时，按实际返回
           while((readLen = fileInputStream.read(buf)) != -1){
               System.out.print(new String(buf, 0, readLen));
           }
           
       }catch (IOException e){
           e.printStackTrace();
       }finally{
           //关闭文件流，释放资源
           try{
               fileInputStream.close();
           }catch (IOException e){
               e.printStackTrace();
           }
       }
    }
}
```

#### 2.**FileOutputStream** 的使用（字节输出流 程序 --> 文件）

```java
public class FileInputStream01{
    public static void main(String[] argc){
        
    }
    
    public void readFile01() {
        String filePath = "e:\\news1.txt";
        int readData = 0;
        
        byte[] buf = new byte[8];//一次读8个字节
        int readLen = 0;
        
        FileInputStream fileInputStream = null;
       try{
           //创建 FileInputStream 对象，用于读取文件
           fileInputStream = new FileInputStream(filePath);
           //1.从输入流读取一个字节的数据,若返回 -1 表示读取结束
           //while((readData = fileInputStream.read())! = -1){
           //    System.out.print((char)readData);
           //}
           
           //2.读取到buf中 readLen 接收返回的读取字节数，不足 8 个时，按实际返回
           while((readLen = fileInputStream.read(buf)) != -1){
               System.out.print(new String(buf, 0, readLen));
           }
           
       }catch (IOException e){
           e.printStackTrace();
       }finally{
           //关闭文件流，释放资源
           try{
               fileInputStream.close();
           }catch (IOException e){
               e.printStackTrace();
           }
       }
    }
}
```

```java
public class FileOutputSream01{
    public static void main(String[] argc){
        
    }
    //字节流写入
    public void writeFile01{
        //创建 FileOutputStream 对象
        FileOutputStream fileOutputStream = null;
        String filePath = "e:\\news4.txt";
        
        try{
            //得到 FileOutputStream 对象
            //一.该创建方式，的文件流对象写入是覆盖写
            fileOutputStream = new FileOutputStream(filePath);
            //写入时,若文件不存在，会创建文件
            //1.写入一个字节
            fileOutputStream.write('a');
           
            //2.写入字符串
            String str = "hello,world!";
            //str.getBytes() 可以把一个字符串转换为 字节数组
            fileOutputStream.write(str.getBytes());
            
            //3.通过字节数组写入
            fileOutputStream.write(str.getBytes(), 0, str.length());
            
            //二.非覆盖写的 FileOutputStream 对象创建方式 传入 append 为 true 的参数 
            fileOutputStream = new FileOutputStream(filePath, true);
            
        }catch (IOException e){
            e.printStackTrace();
        }finally{
            try{
                fileOutputStream.close();
            }catch(IOException e){
                e.printStackTrace();
            }
        }
    }
    
    //文件拷贝
    public void fileCopy(){
        //1.创建文件输出流
        //2.创建文件输入流
        String srcFilePath = "e:\\news.txt";
        String destFilePath = "d:\\news.txt";
        FileInputStream fileInputStream = null;
        FileOutputStream fileOutputStream = null;
        
        try{
            
            //3.创建对应文件的文件流对象
            fileInputStream = new FileInputStream(srcFilePath);
            fileOutputStream = new FileOutputStream(destFilePath);
            
            //4.创建一个 buf 数组提高效率
            byte[] buf = new byte[1024];
            int readLen = 0;
            
            while((readLen = fileInputStream.read(buf)) != -1){
                //5.边读边写
                fileOutputStream.write(buf, 0, readLen);
            }
            
        }catch (IOException e){
            e.printStackTrace();
        }finally{
            try{
                fileInputStream.close();
                fileOutoutStream.close();
            }catch (IOException e){
                e.printStackTrace();
            }
        }
        
    }
}
```



#### 3.**FileReader** 字符输入流

```java
public class FileReader01{
 	public static void mian(String[] argc){
        String filePath = "e:\\news.txt";
        FileReader fileReader = null;
        //1.创建 FileReader 对象
        try{
            fileReader = new FileReader(filePath); 
            //1.按单个字符读取
            //int data = ' ';
            //while((data = fileReader.read()) != -1){
            //    System.out.print((char) data);
            //}
            
            
            //2.按字符数组读取
            char[] buf = new char[8];
            int readLen = 0;
            while((readLen = fileReader.read(buf)) != -1){
                System.out.print(new String(buf, 0, readLen));
            }
            
        }catch (IOException e){
            e.printStackTrace();
        }finally{
            try{
                fileReader.close();
            }catch(IOException e){
                e.printStackTrace();
            }
        }
    
    }  
}
```

#### 4.**FileWriter**字符输出流

```java
public class FileWriter01{
    public static void main(String[] argc){
        String filePath = "e:\\news1.txt";
        FileWriter fileWriter = null;
        
        try {
            //append 传入 true 追加写
            //对于 FileWriter ，写完一定要关闭流 close()(close() 中 会自动调用 flush() )，或者 flush() 才能真正把数据写入到文件
            fileWriter = new FileWriter(filePath, true);
            
            //1.写入单个字符
            fileWriter.write('h');
            
            //2.写入指定数组
            char[] chars = {'e','l', 'l'};
            fileWriter.write(cahrs);
            
            //3.写入指定数组的指定部分
            fileWriter.write("helloworld".toCharArray(), 4, 6);
            
            //4.写入字符串
            fileWriter.write("or");
            
            //5.写入字符串的指定部分
            fileWriter.write("helloworld", 8, 10);
            
        }catch (IOException e) {
            e.printStackTrace();
        }finally {
           	try{
                fileWriter.close();
            }catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

---

### 处理流

#### 处理流(包装流)设计模式

1. 节点流是 底层流/低级流 ，直接与数据源相连接

2. 处理流包装节点流，既可以消除不同节点间的实现差异，也可以提供更方便的方法来完成输入输出

3. 处理流对节点流进行包装，使用了修饰器设计模式，不会直接与数据源相连

4. 处理流的功能主要体现在以下两个方面：

   >性能的提高：只要以增加缓冲的方式来提高输入输出的效率
   >
   >操作的便捷：处理流可能提供了一系列便捷的方法来一次输入输出大批量的数据，使用更加灵活方便

#### BufferedReader 字符流的读取处理流

```java
public class BufferedReader01{
    public static void main(String[] argc) throws IOException{
        
        String filePath = "e:\\news.txt";
        //1.创建 BufferedReader 处理流对象
        BufferedReader bufferedReader = new BufferedReader(new FileReader(filePath));
        //2.读取
        String line;
        //按行读取
        //当返回的是 null 时，表示文件读取完毕
        //BufferedReader.readLine() 是读取一行内容，但是没有换行符
        while ((line = bufferedReader.readLine()) != null){
            System.out.println(line);
        }
        
        //关闭流，这里只需要关闭 BufferedReader， 因为底层会自动去关闭 节点流
        bufferedReader.close();
    }
}
```

#### BufferedWriter 字符流的写入处理流

```java
public class BufferedWriter01{
    public static void main(String[] argc) throws IOException{
        String filePath = "e:\\news.txt";
        //创建BufferedWrite
        //是否追加，需要在节点流中传参控制
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(filePath, true));
        //写入
        bufferedWriter.write("hello");
        //写入换行
        bufferedWriter.newLine();
        bufferedWriter.write("world");
        
        //关闭流
        bufferedWriter.close();
    }
}
```

```java
public class BufferedCopy{
    public static void main(String[] argc){
        String srcPath = "e:\\src.txt";
        String destPath = "e:\\dest.txt";
        //BufferedReader, BufferedWriter 是针对字符流的操作
        //不要去操作 二进制文件 如：音频，视频，doc文档，pdf文档，.会出错
        BufferedReader bufferedReader = null;
        BufferedWriter bufferedWriter = null;
        
       	try{
            bufferedReader = new BufferedReader(new FileReader(srcPath));
            bufferedWriter = new BufferedWriter(new FileWriter(destPath, true));
            String line;
            while((line = bufferedReader.readLine()) != -1){
                bufferedWriter.write(line);
                bufferedWriter.newLine();
            }
            
        }catch (IOException e){
            e.printStackTrace();
        }finally{
            try{
                if(bufferedReader != null){
                    bufferedReader.close();
                }
                if(bufferedWriter != null){
                    bufferedWriter.close();
                }
                
            }catch (IOException e){
                e.printStackTrace();
            }
        }
        
    }
}
```

#### BufferedInputStream BufferedOutoutStream 字节处理流

```java
//字节流可以操作二进制文件，也可以操作文本文件
public class BufferedIOStream{
    public static void main(String[] argc){
        String srcFilePath = "e:\\test.jpg";
        String destFilePath = "e:\\test1.jpg";
        
        BufferedInputStream bis = null;
        BufferedOutPutStream bos = null;
        
        try{
            bis = new BufferedInputStream(new FileInputStream(srcFilePath));
            bos = new BufferedOutputStream(new FileOutputStream(destFilePath));
            
            byte[] buff = new byte[1024];
            int readLen = 0;
            while((readLen = bis.read(buf)) != -1){
                bos.write(buf, 0, readLen);
            }
        }catch (IOException e){
            e.printSatckTrace();
        }finally {
            try{
                if(bis != null){
                    bis.close();
                }
                if(bos != null){
                    bos.close();
                }
            }catch (IOException e){
                e.printStackTrace();
            }  
        }
    }
}
```



#### ObjectInputStream ObjectOutputStream 对象 处理流

能够将基本数据类型或者对象进行序列化或反序列化操作

**序列化 和 反序列化**

1. 序列化就是保存数据的时候，保存==数据的值==和==数据类型==

2. 反序列化就是在恢复数据的时，恢复==数据的值== 和==数据类型==

3. 需要让某个对象支持序列化机制，则必须让其类是可序列化的，为了让某个类可序列化则**该类必须实现以下两个接口之一**：

   >**Serializable** //这是一个标记接口 （内部无任何方法）
   >
   >**Externalizable**//该接口有方法需要实现，所以一般使用 serializable

**ObjectInputStream ** ：提供了反序列化功能

**ObjectOutputStream ** ：提供了序列化功能

```java
public class ObjectOutputStream01 throws Exception {
    //序列化后，保存的文件格式，不再是纯文本，而是按照他的格式来保存
    String filePath = "e:\\data.dat";
    
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputSream(filePath));
    
    //序列化数据 到 e:\data.dat
    //基本数据类型
    oos.writeInt(100);// int -> Integer 自动装箱，且Integer实现了 Serializable
    oos.writeBoolean(true);
    oos.writeChar('a');
    oos.writeDouble(1.1);
    oos.writeUTF("ABC");
    
    oos.writeObject(new Dog("tony", 10));
    
    oos.close()
    
}

class Dog implements Serializable{
    private String name;
    private int age;
    
    public Dog(String name,int age){
        this.name = name;
        this.age = age;
    }
}
```

```java
public class ObjectIutputStream01 throws Exception {
    //指定反序列化文件
    String filePath = "e:\\data.dat";
    
    ObjectIutputStream ois = new ObjectIutputStream(new FileIutputSream(filePath));
    
    //反序列化数据的顺序 需要与 序列化数据时的顺序 一致
    System.out.println(ois.readInt());
    System.out.println(ois.readBoolean());
    System.out.println(ois.readChar());
    System.out.println(ois.readDouble());
    System.out.println(ois.readUTF());
    
    System.out.println( (Dog) ois.readObject());
    
    ois.close();
}

class Dog implements Serializable{
    private String name;
    private int age;
    
    public Dog(String name,int age){
        this.name = name;
        this.age = age;
    }
    
    public String toString(){
        return this.name + " " + this.age;
    }
}
```

tips:

1. 读写顺序要一致
2. 要求序列化或反序列化对象，需要实现 Serializable
3. 序列化的类中建议添加 SerialVersionUID ,为了提高版本兼容性
4. 序列化对象时，默认将里面所有的属性进行序列化，但**除了 static 或 transient 修饰的成员**
5. 序列化对象时，要求里面的**属性的类型也需要实现序列化接口**
6. **序列化具备可继承性**，也就是若某类已经实现了序列化，则它的所有子类也已经默认实现了序列化

#### 标准输入输出流

```java
public class SystemIO1{
    public static void main(String[] argc){
        //System 类的 public final static InputStream in = null;
        //编译类型 InputStream，运行类型 BufferedInputStream
        //表示的标准输入 键盘输入
        System.out.println(System.in.getClass());
        
        //System.out public final static PrintStream out = null;
        //编译类型 PrintStream， 运行类型 PrintStream
        //表示标准输出 显示器
        System.out.println(System.out.getClass());
       
    }
}
```

#### 转换流 InputStreamReader 和 OutputStreamWrite

1. InputStreamReader ：Reader 的子类，可以将 InputStream（字节流）包装成 Reader（字符流）
2. OutputStreamWrite ：Writer 的子类，可以将 OutputStream（字节流）包装成 Writer（字符流）
3. 当处理纯文本数据时，若使用字符流效率更高，并且可以有效解决中文问题，所以建议将字节流转换为字符流
4. 可以在使用时指定编码格式（比如 UTF-8, GBK, GB2312, ISO8859-1 等）

```java
public class InputStreamReader01 throws Exception{
    public static void main(String[] argc){
        String filePath = "e:\\a.txt";
        
        //1. 把 FileInputStream 转成 InputStreamReader
        //2. 指定编码 例 gbk
        InoutStreamReader isr = new InputStreamReader(new FileInputStream(filePath), "gbk");
        //3. 把 InputStreamReader 传入 BufferedReader
        BufferedReader br = new BufferedReader(isr);
        
        //可将 2，3合写
        BufferedReader br1 = new BufferReader(new InputStreamReader(new FileInputStream(filePath), "gbk"));
        
        //4. 读取
        String s = br.readLine();
        System.out.println("读取内容" + s);
        
        //关闭流
        br.close();
    }
}
```

```java
public class OutputStreamWriter01 throws Exception{
    String filePath = "e:\\a.txt";
    //指定编码格式输出文件
    OutputStreamWriter osw = new OutputStreamWriter(FileOutputStream(filePath), "gbk");
    osw.write("hello");
    osw.close();
}
```

#### 打印流 PrintStream 和PrintWriter

打印流只有输出流

```java
public class PrintStream01 throws Exception{
    public static void main(String[] argc){
        PrintStream out = System.out;
        //在默认情况下， PrintStream 输出的数据位置是标准输出 即显示器
        out.print("hello world");
        //因为print 底层是使用 write 实现的，所以可以直接调用 write 进行打印输出
        out.write("hello".getBytes());
        
        out.close();
        
        //我们可以修改打印流的输出位置/设备
        //输出修改到 e:\t1.txt
        //"hello" 就会输出到 e:\t1.txt
        System.setOut(new PrintStream("e:\\t1.txt"));
        System.out.println("hello");
                
    }
}
```

```java
public class PrintWriter01 throws Exception{
    public static void main(String[] argc){
        PrintWriter printWriter = new PrintWriter(System.out);
        printWriter.print("hello");
        printWriter.close();
        
        PrintWriter pw = new PrintWriter(new FileWriter("e:\\t.txt"));
        pw.print("hello");
        pw.close();
    }
}
```

---

## Properties 类

Properties 类方便的实现配置文件

1. Properties 类 是 HashTbale 的一个子类

2. 专门用于读写配置文件的集合类

   >配置文件格式：
   >
   >**键=值**

3. 注意：键值对不需要有空格，值也不需要用引号括起来。默认类型是 String

**常用方法**

```java
public class PropertiesMethod {
    public static void mian(String[] argc) throws Exception{
        //使用 Properties 类来读取 mysql.properties 文件
        
        //1. 创建 Properties 对象
        Properties properties = new Properties();
        
        //2.加载配置文件 .load();
        properties.load(new FileReader("src:\\mysql.properties"));
        
        //3. 把 k-v 显示到控制台
        properties.list(System.out);
        
        //4. 根据一个 key 获得 value   .getProperty(key);
        String usr = properties.getProperty("user");
        System.out.println(usr);
        
        //使用 Properties 类来创建 配置文件，修改配置文件内容
        Properties p = new Properties();
        //创建
        //若该文件没有该 key 即创建，已有该 key z
        p.setProperty("usr","lzy");
        p.setProperty("pwd","1234");
        
        //将 k-v 存储到配置文件中 .store();
        //若有中文，回存储器 unicode 码
        p.store(new FileOutputStream("src:\\mysql2.properties"), null);
    }
}
```



---

# 网络编程

## InetAddress 类

1. **getLocalHost** 获取本机的 **InetAddress** 对象
2. **getByName** 根据指定的主机名/域名获取 ip 地址对象
3. **getHostName** 获取 **InetAddress** 对象的主机名
4. **getHostAddress** 获取 **InetAddress** 对象的地址

```java
public class InetAddress01{
    public static void main(String[] argc){
        //1.获取本机的 InetAddress 对象
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println(localHost);//LAPTOP-F15QS7UI/192.168.146.1
        
        //2.根据指定的主机名/域名获取 ip 地址对象
        InetAddress host1 = InetAddress.getByName("LAPTOP-F15QS7UI");
        System.out.println(lhost1);//LAPTOP-F15QS7UI/192.168.146.1
        
        //3. 获取 InetAddress 对象的主机名
        System.out.println(lhost1.getHostName());//LAPTOP-F15QS7UI
        
        //4. 获取 InetAddress 对象的ip地址
        System.out.println(lhost1.getHostAddress());//192.168.146.1
    }
}
```

**Socket套接字**

1. 通信两端都要有 socket ，是两台机器通信的端点

2. Socket 通信允许程序把网络连接当成一个流，数据在两个 Socket 间通过 IO传输

3. Server 端端口通过 ServerSocket 类来指定，客户端与其建立连接，客户会被随机分配一个端口号 与客户端建立连接

   

## TCP网络通信编程

### 字节流编程

**Server**

```java
public class SocketTCPServer01 {
    public static void main(String[] args) throws IOException {
        //1. 在本机 9999 端口监听，等待连接
        //这个 ServerSocket 可以通过 accept() 返回多个 Socket[多个客户端的连接]
        ServerSocket serverSocket =  new ServerSocket(9999);
        System.out.println("服务器等待连接。。。");

        //2.当没有客户端连接时，程序会阻塞，等待连接
        // 当有客户端连接时，程序会返回一个 Socket 对象,程序继续
        Socket socket = serverSocket.accept();
        System.out.println("服务器 socket 返回 =" + socket.getClass());

        //3.通过 socket.getInputStream() 读取 客户端写入到数据通道的数据
        InputStream inputStream = socket.getInputStream();

        //4.IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while((readLen = inputStream.read(buf)) != -1 ){
            System.out.println(new String(buf, 0 ,readLen));
        }
        
        //5. 获取 socket 相关联的输出流 socket.getOutputStream()
        OutputStream outputStream = socket.getOutputStream();
        outputStream.write("hello,client!".getBytes());
        //设置发送结束标志
        socket.shutdownOutput();

        //6.关闭 IO 流, socket, ServerSocket
        inputStream.close();
        outputStream.close();
        socket.close();
        serverSocket.close(); 
    }
}
```

**Client**

```java
public class SocketTCPClient01 {
    public static void main(String[] args) throws IOException {
        //1.连接服务端（IP，端口）
        //此处测试客户/服务器都在本地，所以客户端去连接服务器的 ip 只要获取本地ip
        //连接成功，返回 Socket 对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket 返回 =" + socket.getClass());

        //2.连接上后，生成 Socket，通过 socket.getOutputStream()
        //得到和这个 socket 对象关联的 输出流
        OutputStream outputStream = socket.getOutputStream();

        //3.通过输出流，写入数据到通道
        outputStream.write("hello,server!".getBytes());
        //设置发送结束标志
        socket.shutdownOutput();
        
        //4.获取 socket 相关联的输入流 socket.getInputStream()
        InputStream inputStream = socket.getInputStream();
        byte[] buf = new byte[1024];
        int readLen = 0;
        while((readLen = inputStream.read(buf)) != -1){
            System.out.println(new String(buf, 0, readLen));
        }

        //5.关闭对象和 socket
        inputStream.close();
        outputStream.close();
        socket.close();
    }
}
```

tips: 通信过程中，发送完毕应该设置一个结束标记通知对端自己已经发送结束。

**socket.shutdownOutput()**

### 字符流

使用转换流 将 socket 相关的IO字节流 转换为字符流

**Server**

```java
public class SocketTCPServer02 {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(9000);

        Socket socket = serverSocket.accept();

        //使用转换流，将 socket 关联的字节流转换为字符流
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        String s = bufferedReader.readLine();
        System.out.println(s);

        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
        bufferedWriter.write("hello,client");
        //字符流 可以使用 newLine() 为结束标记，但是对端必须以 readLine() 读取才能识别
        bufferedWriter.newLine();
        //使用字符流需要手动刷新，否则数据不会写入通道
        bufferedWriter.flush();


        bufferedReader.close();
        bufferedWriter.close();
        socket.close();
        serverSocket.close();
    }
}
```

**Client**

```java
public class SocketTCPClient02 {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(), 9000);

        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
        bufferedWriter.write("hello,server");
        bufferedWriter.newLine();
        bufferedWriter.flush();

        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        String s = bufferedReader.readLine();
        System.out.println(s);

        bufferedReader.close();
        bufferedWriter.close();
        socket.close();
    }
```



### 文件的收发

**server**

```java
public class TCPFileReceive {
    public static void main(String[] args) throws Exception {
        String filePath = "F:\\java\\code\\InetCode\\src\\test.jpg";
        BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream(filePath));

        ServerSocket serverSocket = new ServerSocket(8888);
        Socket socket = serverSocket.accept();

        BufferedInputStream bufferedInputStream = new BufferedInputStream(socket.getInputStream());
        byte[] bytes = StreamUtil.streamToByteArray(bufferedInputStream);

        bufferedOutputStream.write(bytes);
        bufferedOutputStream.close();


        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
        bufferedWriter.write("接收完毕");
        bufferedWriter.newLine();
        bufferedWriter.flush();

        bufferedInputStream.close();
        bufferedWriter.close();
        socket.close();
    }
}
```

**client**

```java
public class TCPFileSend {
    public static void main(String[] args) throws Exception {
        String filePath = "C:\\Users\\lzy\\Pictures\\Screenshot_2021-07-10-22-55-10-907_com.taobao.taobao.jpg";
        BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream(filePath));

        Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
        BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(socket.getOutputStream());

        byte[] bytes = StreamUtil.streamToByteArray(bufferedInputStream);

        bufferedOutputStream.write(bytes);
        bufferedInputStream.close();
        socket.shutdownOutput();


        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        String s = bufferedReader.readLine();
        System.out.println(s);

        bufferedOutputStream.close();
        bufferedReader.close();
        socket.close();
    }
}

```

```java

public class StreamUtil {

    public static byte[] streamToByteArray(InputStream inputStream) throws Exception{
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
        byte[] b =new byte[1024];

        int len;
        while((len = inputStream.read(b)) != -1){
            byteArrayOutputStream.write(b, 0, len);
        }

        byte[] array = byteArrayOutputStream.toByteArray();
        byteArrayOutputStream.close();
        return array;
    }
}
```

### netstat 指令

 netstat -an 可以查看当前主机网络情况，包括端口监听情况和网络连接情况

 netstat -an | more 分页显示

---

## UDP 网络编程

1. 没有明确的服务端和客户端，演变成数据的发送端和接收端
2. 接收数据的发送数据通过 **DatagramSocket** 对象完成
3. 将数据封装到 **DatagramPacket** 对象/装包
4. 当接收到 **DatagramPacket** 对象，需要进行拆包，取出数据
5. **DatagramSocket** 可以指定在哪个端口接收数据
6. 每个数据报的大小限制在 64k 以内，不适合传输大量数据
7. 发送完数据无需释放连接

**基本流程**

>1. 核心的两个类/对象 **DatagramSocket** 和 **DatagramPacket** 、
>2. 建立发送端，接收端
>3. 建立数据包
>4. 调用 **DatagramSocket** 的发送，接收方法
>5. 关闭 **DatagramSocket** 

**receiver**

```java
public class UDPReceive01 {
    public static void main(String[] args) throws IOException {
        //1.创建一个 DatagramSocket 对象，准备在端口 9999 接收数据
        DatagramSocket socket = new DatagramSocket(9);

        //2. 构建一个 DatagramPacket 对象，准备接收数据
        byte[] buf = new byte[1024];
        DatagramPacket datagramPacket = new DatagramPacket(buf, buf.length);

        //3.调用接收方法，将通过网络传输的 DatagramPacket 对象 填充到我们创建的 datagramPacket 中去
        //当有数据包发送到对应端口，就会接收数据
        //没有数据时，就会在该方法阻塞
        socket.receive(datagramPacket);

        //4. 可以把 datagramPacket 进行拆包，取出数据，显示
        int length = datagramPacket.getLength();//实际接收数据的长度
        byte[] data = datagramPacket.getData();
        String s = new String(data, 0, length);

        System.out.println(s);
        //5. 关闭资源
        socket.close();
    }
}
```

**sender**

```java
public class UDPSend01 {
    public static void main(String[] args) throws IOException {
        //1.创建 DatagramSocket 对象，udp socket 中指定的端口为接收数据的端口
        DatagramSocket socket = new DatagramSocket(9998);

        //2. 将需要发送的数据封装到 DatagramPacket 中去
        byte[] bytes = "hello,world!".getBytes();
        //封装 datagramPacket 对象的 参数列表：数据， 数据长度，接收方主机(ip)，接收方端口
        DatagramPacket datagramPacket = new DatagramPacket(bytes, bytes.length,
                InetAddress.getLocalHost(), 9999);

        //3.发送包
        socket.send(datagramPacket);

        //4.关闭资源
        socket.close();

    }
```

---

# 反射

## 反射机制

```java
package com.lzy;

public class Cat {
    private String name = "tom";
    public int age = 10;
    public String address = "abc" 
    public Cat(int age){
        this.age = age;
    }
    public void hi(){
        System.out.println(name + " say hi");
    }
}
```

```properties
classfullpath=com.lzy.cat
method=hi
```

```java
package com.lzy.reflection.test;

public class ReflectionTest {
    public static void main(String[] argc) throws IOException{
        //根据配置文件 re.properties 指定信息， 创建 Cat 对象，并调用方法 hi
        
        //传统方法 new 一个 Cat 对象 -> 调用方法
        Cat cat = new Cat();
        cat.hi();
        
        //1. 使用 Properties 类 获取配置信息
        Properties properties = new Properties;
        Properties.load(new FileInputStream("src\\re.properties"));
        String classfullpath = properties.get("classfullpath").toString();
        String methodName = properties.get("method").toString();
        
        //2. 创建对象。 classfullpath 是一个类名的全路径的字符串，并不是类名的全路径，不能直接通过其 new 对象实例 -> 反射机制解决
        //new classfullpath(); 错误的
        
        //3.反射机制解决
        //(1) 加载类，返回Class类型的对象 cls
        Class cls = Class.forName(classfullpath);
        
        //(2) 通过 cls 得到你加载的类 com.lzy.Cat 的对象实例
        Object o = cls.newInstance();
        System.out.println("o 的运行类型 = " + o.getClass());//o 的运行类型就是 com.lzy.Cat 
        
        //(3) 通过 cls 得到你加载的类 com.lzy.Cat 的 读取配置信息获得的方法名 methodName 的方法对象
        //   即： 在反射中，可以把方法视为对象
        Method method01 = cls.getMethod(methodName);
        
        //(4) 通过 method01 调用方法：即通过方法对象来实现调用方法
        method01.invoke(o);//反射机制 方法.invoke(对象)
        
        //java.lang.reflect.Field: 代表类的成员变量,Filed 对象表示某个类的成员变量
        //得到 name 字段
        //getFiled不能得到私有属性
        Field field = cls.getField("age");
        System.out.println(field.get(o));
        
        //java.lang.reflect.Constructor : 代表类的构造器, Constructor 对象表示构造器
        Constructor constructor = cls.getConstructor(Integer.class);// ()中可以指定构造器的参数类型
        
    }
}
```

1. 反射机制允许程序在执行期间借助于 **Reflection** API 取得任何类的内部信息（比如成员变量，构造器，成员方法等），并能操作对象的属性以及方法。反射在设计模式和框架底层都会用到。
2. 加载完类后，在堆中就产生了一个 **Class** 类型的对象（一个类只有一个 Class 对象），这个对象包含了类的完整结构信息。这个对象就像一面镜子，透过这个镜子看到类的结构，所以，形象的称之：反射。

**反射相关的主要类**

1. java.lang.Class:代表一个类， Class对象表示某个类加载后在堆中的对象
2. java.lang.reflect.Method : 代表类的方法
3. java.lang.reflect.Field: 代表类的成员变量
4. java.lang.reflect.Constructor : 代表类的构造器

---

## Class 类

1. Class 也是类，继承于 Object 类
2. Class 类对象不是 new 出来的， 而系统创建的
3. 对于某个类的 Class 对象，在内存中只有一份，因为类只加载一次
4. 没个类的实例都会记录自己是由 哪个 Class 实例所生成的
5. 通过 Class 可以完整地得到一个类的完整结构，通过一系列 API
6. Class 对象存放在堆中
7. 类的字节码是二进制数据， 放在方法区，有的地方称之为元数据

### **常用方法**

```java
public class Class01{
    public static void main(String[] argc){
        String classAllPath = "com.lzy.Cat";
        //1.获取到 Cat 类，对于的 Class 对象
        //<?> 表示不确定的 java 类型
        Class<?> cls = Class.forName(classAllPath);
        
        //2.输出 cls
        System.out.println(cls);//显示 cls 对象，是哪个类的Class对象 com.lzy.Cat
        System.out.println(cls.getClass());//输出 cls 的运行类型 java.lang.class
        
        //3.获取包名
        System.out.println(cls.getPackage().getName());//com.lzy
        
        //4.得到全类名
        System.out.println(cls.getName());//com.lzy.Cat
        
        //5.通过 cls 创建对象实例
        Cat cat = (Cat) cls.newInstance();
        
        //6.通过反射获取属性
        Field age = cls.getField("age");
        System.out.println(age.get(cat));
        
        //7.一次获得所有属性（字段）
        Field[] fields = cls.getFields();
        
    }
}
```

---

### 获取 Class 类对象

1. 前提：已知一个全类名，且该类在类路径下, 可通过 Class 类的静态方法 **forName()** 获取，可能抛出ClassNotFoundException，例：**Class cls = Class.forName("com.lzy.Cat");** ==应用场景：==多用于配置文件，读取全类名，加载类

2. 前提：若已知具体的类，通过类 class 获取，该方式最为安全可靠，程序性能最高。例：**Class cls = Cat.class;** ==应用场景==：多用于参数传递，比如通过反射得到对应的构造器对象

3. 前提：已知某个类的实例，调用该实例的 **getClass()** 方法获取 Class 对象，例：**Class cls = 实例对象.getClass();//运行类型** ==应用场景==：通过创建好的对象，获取 Class 对象

4. 其它方式：**ClassLoader cl = 实例对象.getClass().getClassLoader();**

   ​				  **Class cls = cl.loadClass("类的全类名");**

5. 基本数据类型，按如下方法得到 Class 类

   **Class cls = 基本数据类型.class;**

6. 基本数据类型对应的包装类，可以通过 **.TYPE** 得到 Class 对象

   **Class cls = 包装类.TYPE**

---

### 有 Class 对象的类型

1. 外部类，成员内部类，静态内部类，局部内部类，匿名内部类
2. 接口
3. 数组
4. 枚举类
5. 注解
6. 基本数据类型
7. void

---

### 类加载

**反射机制是java实现动态语言的关键，也就是通过反射实现类的动态加载**

1. 静态加载：编译时加载相关的类，若没有则报错，依赖性太强
2. 动态加载：运行时加载需要的类，若运行时不用该类，即使不存在该类，则不报错，降低了依赖性。

**类加载的时机**

1. 当创建对象实例时（new）
2. 当子类被加载时，父类也加载
3. 调用类中的静态成员
4. 通过反射

**类加载五个阶段**

1. **加载阶段**

   >JVM 在该阶段的主要目的是将字节码从不同的数据源（可能是 class 文件，也可能是 jar 包，甚至网络）转化为==二进制字节流加载到内存中==，并生成一个代表该类的 java.lang.Class 对象

2. **链接阶段-验证**

   >- 目的是为了确保 Class 文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身安全
   >- 包括：文件格式验证（是否以魔数 oxcafebabe 开头），元数据验证，字节码验证和符号引用验证
   >- 可以考虑使用 -Xverify:none 参数来关闭大部分的类验证措施，缩短虚拟机类加载的时间

3. **链接阶段-准备**

   >- JVM 会在该阶段**对静态变量，分配内存并默认初始化**（对应数据类型 的默认初始化）。这些变量所使用的内存都将在方法区中进行分配
   >- 普通变量：不分配
   >- 静态变量（static）：分配内存并默认初始化
   >- 常量（static final）：分配内存并赋值

4. **链接阶段-解析**

   >- 虚拟机将常量池内的符号引用（通过符号记录了类间的引用关系）替换为直接引用（分配的内存地址）的过程

5. **Initialization 初始化**

   >- 到初始化阶段，才真正开始执行类中定义的 java 程序代码，此阶段是执行 <clinit>() 方法的过程
   >- <clinit>() 方法是由编译器按照语句在源文件中的出现顺序，依次自动收集类中的所有==静态变量==的**赋值动作**和==静态代码块==中的**语句**，并进行合并
   >- 虚拟机会保证一个类的 <clinit>() 方法在多线程环境中被正确的加锁，同步，若多个线程同时去初始化一个类，那么只会有一个线程去执行这类的 <clinit>() 方法，其它线程都要阻塞等待，直到活动线程执行 <clinit>() 方法 完毕

---

## 通过 Reflection 获取类结构信息

```java
package com.lzy.reflection;
    
public class ReflectionUtils{
    public static void mian(String[] argc){
        
    }
    
    public void api_01(){
        //得到 Class 对象
        Class<Test> testCls = Class.forName("com.lzy.reflection.Test");
        
        //1.获取全类名 getName
        System.out.println(testCls.getName());//com.lzy.reflection.Test
        
        //2.获取简单类名 getSimpleName
        System.out.println(testCls.getSimpleName());//Test
        
        //3.获取所有 public 修饰的属性包括本类以及父类 getFields
        Field[] fields = testCls.getFields();
        for(Field field : fields){// a,name
            System.out.println(filed.getName());
        }
        
        //4.获取本类的所有属性 getDeclaredFields
        Field[] fields1 = testCls.getDeclaredFields();
        for(Field field : fields1){// name,age,job,sal
            System.out.println(filed.getName());
        }
        
        //5.获取所有的 public 方法包括本类以及父类 getMethods
        Method[] methods = testCls.getMethods();
        for(Method method : methods){//m1, hi,...
            System.out.println(method.getName());
        }
        
        //6.获取本类的所有方法 getDeclaredMathods
        Method[] methods = testCls.getDeclaredMathods();
        for(Method method : methods){//m1, m2,m3,m4
            System.out.println(method.getName());
        }
        
        //7.获取所有 public 本类的构造器 getConstructors
        Constructor<?>[] constructors = testCls.getConstructors();
        for(Constructor constructor : constructors){
            System.out.println(constructor.getName());
        }
         
        //8. 获取本类中的所有构造器 getDeclaredConstructors
        Constructor<?>[] constructors = testCls.getDeclaredConstructors();
        for(Constructor constructor : constructors){
            System.out.println(constructor.getName());
        }
        
        //9.返回包信息 getPackage
        System.out.println(testCls.getPackage());//com.lzy.reflection
        
        //10.以Class返回父类信息 getSuperclass
        System.out.println(testCls.getSuperclass());
        
        //11.以 Class[] 返回实现接口信息 getInterfaces
        Class<?>[] interfaces = testCls.getInterfaces();
        for(Interface anInterface : interfaces){
            System.out.println(anInterface);
        }
        
        //12.以 Annotation[] 形式返回，获取注解信息 getAnnotations
        Annotation[] annotations = testCls.getAnnotations;
        for(Annotation annotation : annotations){
            System.out.println(annotation);
        }
    }
    
    
    public void api_02(){
    	//得到 Class 对象
        Class<Test> testCls = Class.forName("com.lzy.reflection.Test");
        //获取本类的所有属性 getDeclaredFields
        //1.getModifiers 以 int 的形式返回修饰符
  	    //默认修饰符：0，public：1，private：2，protected：4，static: 8,final: 16 多个修饰符即取和
        //2.getType 返回该属性对应的类的 Class 对象
        Field[] fields1 = testCls.getDeclaredFields();
        for(Field field : fields1){// name,age,job,sal
            System.out.println("本类属性：" + field.getName()" 该属性修饰符值 " + field.getModifiers() + " 该属性的类型：" + field.getType());
        	}
        
        //方法也可以 getModifiers getName
        //1.getReturnType 返回返回值对应的类的 Class 对象
        //2.getParameterTypes 返回形成列表对应的类的 Class[] 对象数组
        
        //构造器和方法类似
        
        }
	}
}


class A {
    public String a;
    public void hi(){}
}

interface IA {
}

class Test extends A implements IA{
    //属性
    public String name;
    protected int age;
    String job;
    private double sal;
    
    //方法
    public void m1(){}
    protected void m2(){}
    void m3(){}
    private void m4(){}
}
```



---

## 反射暴破

### **通过反射创建对象**

1. 方式一：调用类中的 public 修饰的无参构造器

2. 方式二：调用类中的指定构造器

3. 方式三：Class 类的相关方法

   >**newInstance**：调用类中的无参构造器，获取对应类的对象
   >
   >**getConstructor(Class...clazz)**：根据参数列表，获取相应的构造器对象
   >
   >**getDecalaredConstructor(Class...clazz)**：根据参数列表，获取对应的构造器对象

4. 方式四：Constructor 类相关方法

   >==setAccessible(true)==：暴破[暴力破解]，使用反射可以访问 private 构造器/方法/属性
   >
   >**newInstance(Object...obj)**：调用构造器

### **通过反射访问类中的成员**

**操作属性**

1. 根据属性名获取 Field 对象 Field f = 类对象.getDeclaredField(属性名);

2.  ==暴破== ：f.==setAccessible(true)==;// f 为 Field

3. 访问 

   >f.==set(o, 值)==;//o 表示对象
   >
   >f.==get(o)==;// o 表示对象

4. 注意：若是**静态属性**，则 set 和 get 中的**参数 o ，可以写做 null**

**操作方法**

1. 根据方法名和参数列表获取 Method 方法对象：Method m = 类对象.getDeclaredMrthod(方法名, XX.class(方法的参数类型) );                                  
2. 获取对象：Object o = 类对象.newInstance();
3. ==暴破==：m.==setAccessible(true)==;
4. 访问：Object returnValue = m.==invoke(o, 实参列表)==;
5. 注意：若是**静态方法**，则 invoke 的**参数 o ，可以写为 null**

例

```java
package com.exercise6_1;

public class PrivateTest {
    private String name = "lzy";
    public String getName(){
        return name;
    }
}
```

```java
public class RefectionExercise {
    public static void main(String[] args) throws Exception {
		//获取类对象
        Class<?> cls = Class.forName("com.exercise6_1.PrivateTest");
        //由类对象创建对象实例
        Object o = cls.newInstance();
		
        //创建该类的 getName 公开方法对象
        Method m = cls.getDeclaredMethod("getName");
        //通过反射调用该实例对象的方法
        System.out.println(m.invoke(o));
		
        //创建该类的 name 私有属性对象
        Field f = cls.getDeclaredField("name");
        //暴破，设置私有属性可被访问
        f.setAccessible(true);
        //修改改实例对象的 私有属性 n
        f.set(o, "ctl");

        System.out.println(m.invoke(o));
    }
}
```

---

# JDBC

**简介**

1. JDBC为访问不同的数据库提供了统一的接口，为使用者屏蔽了细节问题
2. JDBC是 java 提供一套用于数据库操作的接口 API，**java程序员只需要面向这套接口编程即可**，不同的数据库厂商，需要针对这套接口，提供不同的实现。
3. 相关类和接口在 java.sql 和 javax.sql 包中

**mysql的jar包: ([MySQL :: Download Connector/J](https://dev.mysql.com/downloads/connector/j/))**

## JDBC程序编写步骤

1. 注册驱动 -- **加载 Driver 类**
2. 获取链接 -- 得到 **Connection**
3. 执行增删改查 -- 发生 SQL 指令给 mysql 执行
4. 释放资源   

### 连接数据库的五种方式：方式一

直接使用` com.mysql.cj.jdbc.Driver()`，属于静态加载，灵活性差，依赖强

```java
package com.lzy.jdbc.myjdbc;

import com.mysql.cj.jdbc.Driver;

import java.sql.*;
import java.util.Properties;
import java.util.logging.Logger;

public class JDBC_Exercise01 {
    public static void main(String[] args) throws SQLException {
        //准备工作： 在项目下建立一个库文件夹
        //将 mysql 的链接 jar 包拷贝到该目录下，并 add to project...加入到项目中

        //1.注册驱动
        Driver driver = new Driver();

        //2.建立链接
        //(1) jdbc:mysql:// 表示规定好的协议，通过 jdbc 的方式连接 mysql
        //(2) 连接的数据库ip地址:端口号
        //(3) 数据库名
        String url = "jdbc:mysql://192.168.146.128:3306/test";
        //将 用户名和密码放入到 Properties 对象
        // user, password 是规定好的，后面根据实际内容填写，这样驱动才能正确读取配置文件
        Properties properties = new Properties();
        properties.setProperty("user", "root");//用户
        properties.setProperty("password", "1234");//获取连接
        Connection connect = driver.connect(url, properties);

        //3.执行sql
        String sql = "insert into person(FirstName,LastName,age,addr) values('test','lei',25,'beijing')";
        //得到一个 statement 对象
        Statement statement = connect.createStatement();
        int rows = statement.executeUpdate(sql);//若是 dml 语句，返回的影响的行数
        System.out.println(rows > 0 ? "success" : "fail");

        //4.释放资源
        statement.close();
        connect.close();
    }
}
```

---

### 方式二：利用反射机制

```java
public class Exercise02 {
    public static void main(String[] args) throws ClassNotFoundException, InstantiationException, IllegalAccessException, SQLException {
        //使用反射加载 Driver 类
        Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
        Driver driver = (Driver)aClass.newInstance();

        String url = "jdbc:mysql://192.168.146.128:3306/test";

        Properties properties = new Properties();
        properties.setProperty("user", "root");
        properties.setProperty("password", "1234");

        Connection connect = driver.connect(url, properties);
        System.out.println("方式二 = " + connect);
    }
}
```

---

### 方式三：DriverManager 替代 Driver 进行统一管理

```java
public class Exercise03 {
    public static void main(String[] args) throws ClassNotFoundException, SQLException, InstantiationException, IllegalAccessException {
        //使用反射加载Driver
        Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
        Driver driver = (Driver)aClass.newInstance();

        //创建url ,user, password
        String url = "jdbc:mysql://192.168.146.128:3306/test";
        String user = "root";
        String password = "1234";

        DriverManager.registerDriver(driver);//注册 Driver驱动

        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("方式三 =" + connection);
    }
}
```

---

### ==方式四==：使用 Class.forName 自动完成驱动注册

```java
public class Exercise04 {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //使用反射加载 Driver 类
        //在加载 Driver 类时，系统完成了注册
        //源码中的静态代码块，在类加载时，会自动执行一次注册
        Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");

        //创建url ,user, password
        String url = "jdbc:mysql://192.168.146.128:3306/test";
        String user = "root";
        String password = "1234";

        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("方式四 =" + connection);
    }
}
```

tips:

- mysql 驱动 5.1.6 后可以无需 `Class.forName("com.mysql.cj.jdbc.Driver");`
- 从 jdk1.5 以后使用了 jdbc4，就不需要显式的调用 `Class.forName()` 去注册驱动而是自动调用驱动 jar 包下 `MATE-INF\services\java.sql.Driver` 文本中的类名去注册

---

### ==方式五==：使用配置文件，连接数据库更加灵活(4上改进)

推荐使用

`mysql.properties`

```properties
user=root
password=1234
url=jdbc:mysql://192.168.146.128:3306/test
driver=com.mysql.cj.jdbc.Driver
```

```java
public class Exercise05 {
    public static void main(String[] args) throws IOException, ClassNotFoundException, SQLException {
        //通过 Properties 对象获取配置文件信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));

        //获取相关配置信息
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String url = properties.getProperty("url");
        String driver = properties.getProperty("driver");

        Class<?> aClass = Class.forName(driver);//建议写上

        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("方式五 =" + connection);
    }
}
```

---

## ResultSet

`select`语句查询结果用 `ResultSet`接收

```java
public class Exercise05 {
    public static void main(String[] args) throws IOException, ClassNotFoundException, SQLException {
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));

        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String url = properties.getProperty("url");
        String driver = properties.getProperty("driver");

        Class<?> aClass = Class.forName(driver);

        Connection connection = DriverManager.getConnection(url, user, password);
        Statement statement = connection.createStatement();

        String sql = "select * from person";
        ResultSet resultSet = statement.executeQuery(sql);

        while(resultSet.next()){
            int id = resultSet.getInt(1);//读取第一列
            String firstName = resultSet.getString(2);//读取第二列
            String lastName = resultSet.getString(3);
            int age = resultSet.getInt(4);
            String address = resultSet.getString(5);
            int score = resultSet.getInt(6);

            System.out.println(id + "\t" + firstName + lastName + "\tage = " + age
                + "\taddress= " + address + "\tscore= " + score);
        }

        statement.close();
        connection.close();

    }
}
```

## SQL注入

1. Statement 对象 用于执行静态SQL语句并返回起生成的结果的对象
2. 在建立连接后，需要对数据库进行访问，执行命名或是SQL语句，可以通过：
   - Statement 存在 sql 注入风险
   - ==PreparedStatement== 预处理
   - CallableStatement 存储过程
3. Statement 对象执行 sql 语句，存在 sql 注入风险
4. sql 注入是利用某些系统没有对用户输入的数据进行充分的检查，而在用户输入数据中注入非法的 sql 语句段或命令，恶意攻击数据库。
5. 要防范 sql 注入，只要用 PreparedStatement 取代 Statement 就可以了。

---

## 预编译处理查询

1. `PreparedStatement `执行` sql` 语句中的参数用 `?`来表示，调用 `PreparedStatement`对象的 `setXxx()`方法来设置这些参数。`setXxx()`方法有两个参数，第一个参数是要设置 `sql`语句中的参数的索引(从 1 开始)，第二个是设置 `sql`语句中的参数的值。
2. 调用 `PreparedStatement `的`executeQuery()`方法返回 `ResultSet`对象
3. 调用 `PreparedStatement `的`executeUpdate()`方法: 执行更新，包括增，删，改查

**预编译处理的好处**：

1. 不在使用 + 来拼接 sql 语句，减少语法错误
2. 有效的解决了 sql 注入问题
3. 大大减少了编译次数，效率较高

```java
public class PreparedStatement_ {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in);

        //让用户输入管理员名和密码
        System.out.print("请输入管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); //如果希望看到SQL注入，这里需要用nextLine
        System.out.print("请输入管理员的密码: ");
        String admin_pwd = scanner.nextLine();

        //通过Properties对象获取配置文件的信息

        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");

        //1. 注册驱动
        Class.forName(driver);//建议写上

        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);

        //3. 得到PreparedStatement
        //3.1 组织SqL , Sql 语句的 ? 就相当于占位符
        String sql = "select name , pwd  from admin where name =? and pwd = ?";
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        //3.3 给 ? 赋值
        preparedStatement.setString(1, admin_name);
        preparedStatement.setString(2, admin_pwd);

        //4. 执行 select 语句使用  executeQuery
        //   如果执行的是 dml(update, insert ,delete) executeUpdate()
        //   这里执行 executeQuery ,不要再写 sql

        ResultSet resultSet = preparedStatement.executeQuery(sql);
        if (resultSet.next()) { //如果查询到一条记录，则说明该管理存在
            System.out.println("恭喜， 登录成功");
        } else {
            System.out.println("对不起，登录失败");
        }
        
        //dml 语句
        String sql2 = "update admin set pwd = ? where name = ?";
        PreparedStatement preparedStatement1 = connection.prepareStatement(sql);
        preparedStatement1.setString(1, admin_pwd);
        preparedStatement1.setString(2, admin_name);
        int rows = preparedStatement1.executeUpdate();//返回受影响行数

        //关闭连接
        resultSet.close();
        preparedStatement.close();
        connection.close();

    }
}
```

## API总结

**`DriverManager`**驱动管理类

> `getConnection(url, user, password)`获取链接

**`Connection`**接口

> `createStatement`创建 Statement 对象
>
> `preparedStatement(sql)`生成预处理对象与 sql 语句绑定

**`Statement`**接口

> `executeUpdate(sql)` 执行 dml 语句，返回影响行数
>
> `executeQuery(sql)` 执行查询，返回`ResultSet`对象
>
> `execute(sql)` 执行任意 sql 语句，返回布尔值

**`PreparedStatement`**接口

> `executeUpdate(sql)` 执行 dml 语句，返回影响行数
>
> `executeQuery(sql)` 执行查询，返回`ResultSet`对象
>
> `execute(sql)` 执行任意 sql 语句，返回布尔值
>
> `setXxx(占位符索引, 要在占位符处设置的值)` 解决 sql 注入
>
> `setObject(占位符索引, 要在占位符处设置的值)` 

**`ResultSet`**结果集

> `next()` 向下一行移动，若没有下一行，返回 `false`,因此也可以用来判断是否有查询结果
>
> `previous()` 先上移动一行
>
> `getXxx(列索引/列名)`获取指定列的数据，接收类型为` Xxx`
>
> `getObject(列索引/列名)`

---

## 事务

1. JDBC 程序中当一个 Connection 对象创建时，默认情况下是自动提交 事务：每次执行一个 sql 语句时，若执行成功，就会向数据库自动提交，而不能回滚
2. JDBC 程序中为了让多个 sql 语句作为一个整体执行，需要使用事务
3. 调用 Connection 的 ==**`setAutoCommit(false)` **==可以取消自动提交
4. 在所有的 sql 语句都执行成功后，调用 Connection 的 **`commit();`**方法提交事务
5. 在某个操作失败或出现异常，调用 **`rollback([savepoint]);`**方法回滚是事务

```java
public void useTransaction() {

        //操作转账的业务
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "update account set balance = balance - 100 where id = 1";
        String sql2 = "update account set balance = balance + 100 where id = 2";
        PreparedStatement preparedStatement = null;
        //3. 创建PreparedStatement 对象
        try {
            //JDBCUtils 自己写的 JDBC 的工具类
            connection = JDBCUtils.getConnection(); // 在默认情况下，connection是默认自动提交
            //将 connection 设置为不自动提交
            connection.setAutoCommit(false); //开启了事务
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.executeUpdate(); // 执行第1条sql

            int i = 1 / 0; //抛出异常
            preparedStatement = connection.prepareStatement(sql2);
            preparedStatement.executeUpdate(); // 执行第3条sql

            //这里提交事务
            connection.commit();

        } catch (Exception e) {
            //这里我们可以进行回滚，即撤销执行的SQL
            //默认回滚到事务开始的状态.
            System.out.println("执行发生了异常，撤销执行的sql");
            try {
                connection.rollback();
            } catch (SQLException throwable) {
                throwable.printStackTrace();
            }
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtils.close(null, preparedStatement, connection);
        }
    }
```

---

## 批处理

1. 当需要成批插入或者更新记录时，可以采用 java 的批量更新机制，这一机制允许多条语句一次性提交给数据库批量处理。

2. JDBC 的批处理语句包含下面方法：

   > `addBatch()`:添加需要批处理的 sql 语句或者参数
   >
   > `executeBatch()`:执行批处理语句
   >
   > `clearBatch()`:清空批处理语句

3. JDBC 链接 mysql 时，若需要使用批处理功能，需要在 url 中添加参数==`rewriteBatchedStatements=true`==

4. 批处理往往和 `PreparedStatement`一起搭配使用，可以减少编译次数，又减少运行次数

`mysql.properties`

```properties
user=root
password=1234
url=jdbc:mysql://192.168.146.128:3306/test?rewriteBatchedStatements=true
driver=com.mysql.cj.jdbc.Driver
```

```java
public class Batch_ {

    //传统方法，添加5000条数据到admin2

    @Test
    public void noBatch() throws Exception {

        Connection connection = JDBCUtils.getConnection();
        String sql = "insert into admin2 values(null, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        System.out.println("开始执行");
        long start = System.currentTimeMillis();//开始时间
        for (int i = 0; i < 5000; i++) {//5000执行
            preparedStatement.setString(1, "jack" + i);
            preparedStatement.setString(2, "666");
            preparedStatement.executeUpdate();
        }
        long end = System.currentTimeMillis();
        System.out.println("传统的方式 耗时=" + (end - start));//传统的方式 耗时=10702
        //关闭连接
        JDBCUtils.close(null, preparedStatement, connection);
    }

    //使用批量方式添加数据
    @Test
    public void batch() throws Exception {

        Connection connection = JDBCUtils.getConnection();
        String sql = "insert into admin2 values(null, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        System.out.println("开始执行");
        long start = System.currentTimeMillis();//开始时间
        for (int i = 0; i < 5000; i++) {//5000执行
            preparedStatement.setString(1, "jack" + i);
            preparedStatement.setString(2, "666");
            //将sql 语句加入到批处理包中 -> 看源码
            /*
            //1. //第一就创建 ArrayList - elementData => Object[]
            //2. elementData => Object[] 就会存放我们预处理的sql语句
            //3. 当elementData满后,就按照1.5扩容
            //4. 当添加到指定的值后，就executeBatch
            //5. 批量处理会减少我们发送sql语句的网络开销，而且减少编译次数，因此效率提高
            public void addBatch() throws SQLException {
                synchronized(this.checkClosed().getConnectionMutex()) {
                    if (this.batchedArgs == null) {

                        this.batchedArgs = new ArrayList();
                    }

                    for(int i = 0; i < this.parameterValues.length; ++i) {
                        this.checkAllParametersSet(this.parameterValues[i], this.parameterStreams[i], i);
                    }

                    this.batchedArgs.add(new PreparedStatement.BatchParams(this.parameterValues, this.parameterStreams, this.isStream, this.streamLengths, this.isNull));
                }
            }

             */
            preparedStatement.addBatch();
            //当有1000条记录时，在批量执行
            if((i + 1) % 1000 == 0) {//满1000条sql
                preparedStatement.executeBatch();
                //清空一把
                preparedStatement.clearBatch();
            }
        }
        long end = System.currentTimeMillis();
        System.out.println("批量方式 耗时=" + (end - start));//批量方式 耗时=108
        //关闭连接
        JDBCUtils.close(null, preparedStatement, connection);
    }
}
```



## 数据库连接池

1. JDBC 的数据库连接池使用 `javax.sql.DataSource` 来表示,`DataSource`只是一个接口，该接口通常由第三方实现。
2. ==`C3P0`==数据库连接池，速度相对较慢，稳定性不错(`hibernate, spring`)
3. `DBCP`数据库连接池，速度相对`C3P0`较快，但是不稳定
4. `Proxool`数据库连接池，由监控连接池状态的功能，稳定性比`C3P0`差一点
5. `BoneCP`数据库连接池，速度快
6. ==`Druid`==德鲁伊连接池是阿里提供的数据库连接池，综合性能较好

### `C3P0`

先导入 `C3P0`的`jar`包，在`src`包下创建配置文件 `c3p0-config.xml`

`mysql.properties`

```properties
user=root
password=1234
url=jdbc:mysql://192.168.146.128:3306/test?rewriteBatchedStatements=true
driver=com.mysql.cj.jdbc.Driver
```

 `c3p0-config.xml`

```xml
<c3p0-config>
    <!-- 数据源名称代表连接池 -->
  <named-config name="lzyPool">
<!-- 驱动类 -->
  <property name="driverClass">com.mysql.cj.jdbc.Driver</property>
  <!-- url-->
  	<property name="jdbcUrl">jdbc:mysql://192.168.146.128:3306/test</property>
  <!-- 用户名 -->
  		<property name="user">root</property>
  		<!-- 密码 -->
  	<property name="password">1234</property>
  	<!-- 每次增长的连接数-->
    <property name="acquireIncrement">5</property>
    <!-- 初始的连接数 -->
    <property name="initialPoolSize">10</property>
    <!-- 最小连接数 -->
    <property name="minPoolSize">5</property>
   <!-- 最大连接数 -->
    <property name="maxPoolSize">50</property>

	<!-- 可连接的最多的命令对象数 -->
    <property name="maxStatements">5</property> 
    
    <!-- 每个连接对象可连接的最多的命令对象数 -->
    <property name="maxStatementsPerConnection">2</property>
  </named-config>
</c3p0-config>
```

```java
public class C3P0_ {

    //方式1： 相关参数，在程序中指定user, url , password等
    @Test
    public void testC3P0_01() throws Exception {

        //1. 创建一个数据源对象
        ComboPooledDataSource comboPooledDataSource = new ComboPooledDataSource();
        //2. 通过配置文件mysql.properties 获取相关连接的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //读取相关的属性值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String url = properties.getProperty("url");
        String driver = properties.getProperty("driver");

        //给数据源 comboPooledDataSource 设置相关的参数
        //注意：连接管理是由 comboPooledDataSource 来管理
        comboPooledDataSource.setDriverClass(driver);
        comboPooledDataSource.setJdbcUrl(url);
        comboPooledDataSource.setUser(user);
        comboPooledDataSource.setPassword(password);

        //设置初始化连接数
        comboPooledDataSource.setInitialPoolSize(10);
        //最大连接数
        comboPooledDataSource.setMaxPoolSize(50);
        //测试连接池的效率, 测试对mysql 5000次操作
        long start = System.currentTimeMillis();
        for (int i = 0; i < 5000; i++) {
            Connection connection = comboPooledDataSource.getConnection(); //这个方法就是从 DataSource 接口实现的
            //System.out.println("连接OK");
            connection.close();
        }
        long end = System.currentTimeMillis();
        //c3p0 5000连接mysql 耗时=391
        System.out.println("c3p0 5000连接mysql 耗时=" + (end - start));

    }

    //第二种方式 使用配置文件模板来完成

    //1. 将c3p0 提供的 c3p0.config.xml 拷贝到 src目录下
    //2. 该文件指定了连接数据库和连接池的相关参数
    @Test
    public void testC3P0_02() throws SQLException {
		//写上数据源名称
        ComboPooledDataSource comboPooledDataSource = new ComboPooledDataSource("lzyPool");

        //测试5000次连接mysql
        long start = System.currentTimeMillis();
        System.out.println("开始执行....");
        for (int i = 0; i < 500000; i++) {
            Connection connection = comboPooledDataSource.getConnection();
            //System.out.println("连接OK~");
            connection.close();
        }
        long end = System.currentTimeMillis();
        //c3p0的第二种方式 耗时=413
        System.out.println("c3p0的第二种方式(500000) 耗时=" + (end - start));//1917

    }


}
```

---

### DRUID

`druid.properties`

```properties
#key=value
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://192.168.146.128:3306/test?rewriteBatchedStatements=true
username=root
password=1234
#initial connection Size
initialSize=10
#min idle connecton size 空闲连接
minIdle=5
#max active connection size
maxActive=50
#max wait time (5000 mil seconds)
maxWait=5000
```

```java
public class Druid_ {

    @Test
    public void testDruid() throws Exception {
        //1. 加入 Druid jar包
        //2. 加入 配置文件 druid.properties , 将该文件拷贝项目的src目录
        //3. 创建Properties对象, 读取配置文件
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\druid.properties"));

        //4. 创建一个指定参数的数据库连接池, Druid连接池
        DataSource dataSource =
                DruidDataSourceFactory.createDataSource(properties);

        long start = System.currentTimeMillis();
        for (int i = 0; i < 500000; i++) {
            Connection connection = dataSource.getConnection();
            System.out.println(connection.getClass());
            //System.out.println("连接成功!");
            connection.close();
        }
        long end = System.currentTimeMillis();
        //druid连接池 操作5000 耗时=412
        System.out.println("druid连接池 操作500000 耗时=" + (end - start));//539


    }
}
```

**使用 `Druid`连接池编写数据库连接池工具类**

```java
public class JDBCUtilsByDruid {

    private static DataSource ds;

    //在静态代码块完成 ds初始化
    static {
        Properties properties = new Properties();
        try {
            properties.load(new FileInputStream("src\\druid.properties"));
            ds = DruidDataSourceFactory.createDataSource(properties);
        } catch (Exception e) {
            e.printStackTrace();
        }

    }

    //编写getConnection方法
    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }

    //关闭连接, 在数据库连接池技术中，close 不是真的断掉连接
    //而是把使用的Connection对象放回连接池
    public static void close(ResultSet resultSet, Statement statement, Connection connection) {

        try {
            if (resultSet != null) {
                resultSet.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```

使用例子

```java
public class JDBCUtilsByDruid_USE {

    @Test
    public void testSelect() {

        System.out.println("使用 druid方式完成");
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "select * from actor where id >= ?";
        PreparedStatement preparedStatement = null;
        ResultSet set = null;
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtilsByDruid.getConnection();
            System.out.println(connection.getClass());//运行类型 com.alibaba.druid.pool.DruidPooledConnection
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1, 1);//给?号赋值
            //执行, 得到结果集
            set = preparedStatement.executeQuery();

            //遍历该结果集
            while (set.next()) {
                int id = set.getInt("id");
                String name = set.getString("name");//getName()
                String sex = set.getString("sex");//getSex()
                Date borndate = set.getDate("borndate");
                String phone = set.getString("phone");
                System.out.println(id + "\t" + name + "\t" + sex + "\t" + borndate + "\t" + phone);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtilsByDruid.close(set, preparedStatement, connection);
        }
    }
}
```

---

### Apache_DBUtils

```java
public class Actor {

    private Integer id;
    private String name;
    private String sex;
    private Date borndate;
    private String phone;
	
    ...;
}
```

```java
//关闭 Connection 后，ResultSet 就不可用了
//土方法来解决ResultSet =封装=> Arraylist
@Test
public ArrayList<Actor> testSelectToArrayList() {

    System.out.println("使用 druid方式完成");
    //1. 得到连接
    Connection connection = null;
    //2. 组织一个sql
    String sql = "select * from actor where id >= ?";
    PreparedStatement preparedStatement = null;
    ResultSet set = null;
    ArrayList<Actor> list = new ArrayList<>();//创建ArrayList对象,存放actor对象
    //3. 创建PreparedStatement 对象
    try {
        connection = JDBCUtilsByDruid.getConnection();
        System.out.println(connection.getClass());//运行类型 com.alibaba.druid.pool.DruidPooledConnection
        preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setInt(1, 1);//给?号赋值
        //执行, 得到结果集
        set = preparedStatement.executeQuery();

        //遍历该结果集
        while (set.next()) {
            int id = set.getInt("id");
            String name = set.getString("name");//getName()
            String sex = set.getString("sex");//getSex()
            Date borndate = set.getDate("borndate");
            String phone = set.getString("phone");
            //把得到的resultset 的记录，封装到 Actor对象，放入到list集合
            list.add(new Actor(id, name, sex, borndate, phone));
        }

        System.out.println("list集合数据=" + list);
        for(Actor actor : list) {
            System.out.println("id=" + actor.getId() + "\t" + actor.getName());
        }

    } catch (SQLException e) {
        e.printStackTrace();
    } finally {
        //关闭资源
        JDBCUtilsByDruid.close(set, preparedStatement, connection);
    }
    //因为ArrayList 和 connection 没有任何关联，所以该集合可以复用.
    return  list;
}

```

**为更好的解决上述问题**：

`commons-dbutils`是`Apache`组织提供的一个开源 JDBC 工具类，它是对 JDBC 的封装，使用 `dbutils`能极大的简化 JDBC 编码的工作量

**`Dbtuils`类**：

1. **`QueryRunner`**类：该类封装了 sql 的执行，是线程安全的。可以实现增，删，改，查，批处理
2. 使用**`QueryRunner`**类实现了查询
3. **`ResultSetHandler`**接口：该接口用于处理`java.sql.ResultSet`，将数据按要求转换为另一种形式

```java
public class DBUtils_USE {

    //使用apache-DBUtils 工具类 + druid 完成对表的crud操作
    @Test
    public void testQueryMany() throws SQLException { //返回结果是多行的情况

        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();
        //4. 就可以执行相关的方法，返回ArrayList 结果集
        //String sql = "select * from actor where id >= ?";
        //   注意: sql 语句也可以查询部分列
        String sql = "select id, name from actor where id >= ?";
        
        //(1) query 方法就是执行sql 语句，得到resultset ---封装到 --> ArrayList 集合中
        //(2) 返回集合
        //(3) connection: 连接
        //(4) sql : 执行的sql语句
        //(5) new BeanListHandler<>(Actor.class): 在将resultset -> Actor 对象 -> 封装到 ArrayList
        //    底层使用反射机制 去获取Actor 类的属性，然后进行封装
        //(6) 1 就是给 sql 语句中的? 赋值，可以有多个值，因为是可变参数Object... params
        //(7) 底层得到的resultset ,会在query 关闭, 关闭PreparedStatment
        /**
         * 分析 queryRunner.query方法:
         * public <T> T query(Connection conn, String sql, ResultSetHandler<T> rsh, Object... params) throws SQLException {
         *         PreparedStatement stmt = null;//定义PreparedStatement
         *         ResultSet rs = null;//接收返回的 ResultSet
         *         Object result = null;//返回ArrayList
         *
         *         try {
         *             stmt = this.prepareStatement(conn, sql);//创建PreparedStatement
         *             this.fillStatement(stmt, params);//对sql 进行 ? 赋值
         *             rs = this.wrap(stmt.executeQuery());//执行sql,返回resultset
         *             result = rsh.handle(rs);//返回的resultset --> arrayList[result] [使用到反射，对传入class对象处理]
         *         } catch (SQLException var33) {
         *             this.rethrow(var33, sql, params);
         *         } finally {
         *             try {
         *                 this.close(rs);//关闭resultset
         *             } finally {
         *                 this.close((Statement)stmt);//关闭preparedstatement对象
         *             }
         *         }
         *
         *         return result;
         *     }
         */
        List<Actor> list =
                queryRunner.query(connection, sql, new BeanListHandler<>(Actor.class), 1);
        System.out.println("输出集合的信息");
        for (Actor actor : list) {
            System.out.print(actor);
        }


        //释放资源
        JDBCUtilsByDruid.close(null, null, connection);

    }

    //演示 apache-dbutils + druid 完成 返回的结果是单行记录(单个对象)
    @Test
    public void testQuerySingle() throws SQLException {

        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();
        //4. 就可以执行相关的方法，返回单个对象
        String sql = "select * from actor where id = ?";
        
        // 因为我们返回的单行记录<--->单个对象 , 使用的Hander 是 BeanHandler
        Actor actor = queryRunner.query(connection, sql, new BeanHandler<>(Actor.class), 10);
        System.out.println(actor);

        // 释放资源
        JDBCUtilsByDruid.close(null, null, connection);

    }

    //演示apache-dbutils + druid 完成查询结果是单行单列-返回的就是object
    @Test
    public void testScalar() throws SQLException {

        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();

        //4. 就可以执行相关的方法，返回单行单列 , 返回的就是Object
        String sql = "select name from actor where id = ?";
        //因为返回的是一个对象, 使用的handler 就是 ScalarHandler
        Object obj = queryRunner.query(connection, sql, new ScalarHandler(), 4);
        System.out.println(obj);

        // 释放资源
        JDBCUtilsByDruid.close(null, null, connection);
    }

    //演示apache-dbutils + druid 完成 dml (update, insert ,delete)
    @Test
    public void testDML() throws SQLException {

        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();

        //4. 这里组织sql 完成 update, insert delete
        //String sql = "update actor set name = ? where id = ?";
        //String sql = "insert into actor values(null, ?, ?, ?, ?)";
        String sql = "delete from actor where id = ?";

        //(1) 执行dml 操作是 queryRunner.update()
        //(2) 返回的值是受影响的行数 (affected: 受影响)
        //int affectedRow = queryRunner.update(connection, sql, "林青霞", "女", "1966-10-10", "116");
        int affectedRow = queryRunner.update(connection, sql, 1000 );
        System.out.println(affectedRow > 0 ? "执行成功" : "执行没有影响到表");

        // 释放资源
        JDBCUtilsByDruid.close(null, null, connection);

    }
}
```

---

### BasicDao

自己编写一个 BasicDao 类，来提高对不同表的操作的代码复用率

```java
package com.lzy.dao_.dao;

import com.lzy.dao_.utils.JDBCUtilsByDruid;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;

import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;

//开发BasicDAO , 是其他DAO的父类
public class BasicDAO<T> { //泛型指定具体类型

    private QueryRunner qr =  new QueryRunner();

    //开发通用的dml方法, 针对任意的表
    public int update(String sql, Object... parameters) {

        Connection connection = null;

        try {
            connection = JDBCUtilsByDruid.getConnection();
            int update = qr.update(connection, sql, parameters);
            return  update;
        } catch (SQLException e) {
           throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }

    }

    //返回多个对象(即查询的结果是多行), 针对任意表

    /**
     *
     * @param sql sql 语句，可以有 ?
     * @param clazz 传入一个类的Class对象 比如 Actor.class
     * @param parameters 传入 ? 的具体的值，可以是多个
     * @return 根据Actor.class 返回对应的 ArrayList 集合
     */
    public List<T> queryMulti(String sql, Class<T> clazz, Object... parameters) {

        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return qr.query(connection, sql, new BeanListHandler<T>(clazz), parameters);

        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }

    }

    //查询单行结果 的通用方法
    public T querySingle(String sql, Class<T> clazz, Object... parameters) {

        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return  qr.query(connection, sql, new BeanHandler<T>(clazz), parameters);

        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }
    }

    //查询单行单列的方法,即返回单值的方法

    public Object queryScalar(String sql, Object... parameters) {

        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return  qr.query(connection, sql, new ScalarHandler(), parameters);

        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }
    }

}
```

---

# 正则表达式

文本处理

## 基本语法

```java
public class RegTheory {
    public static void main(String[] args) {

        String content = "1998年12月8日";
        //目标：匹配所有四个数字
        //说明
        //1. \\d 表示一个任意的数字
        String regStr = "(\\d\\d)(\\d\\d)";
        //2. 创建模式对象[即正则表达式对象]
        Pattern pattern = Pattern.compile(regStr);
        //3. 创建匹配器
        //说明：创建匹配器matcher， 按照 正则表达式的规则 去匹配 content字符串
        Matcher matcher = pattern.matcher(content);

        //4.开始匹配
        /**
         *
         * matcher.find() 完成的任务 （考虑分组）
         * 什么是分组，比如  (\d\d)(\d\d) ,正则表达式中有() 表示分组,第1个()表示第1组,第2个()表示第2组...
         * 1. 根据指定的规则 ,定位满足规则的子字符串(比如(19)(98))
         * 2. 找到后，将 子字符串的开始的索引记录到 matcher对象的属性 int[] groups;
         *    2.1 groups[0] = 0 , 把该子字符串的结束的索引+1的值记录到 groups[1] = 4
         *    2.2 记录1组()匹配到的字符串 groups[2] = 0  groups[3] = 2
         *    2.3 记录2组()匹配到的字符串 groups[4] = 2  groups[5] = 4
         *    2.4.如果有更多的分组.....
         * 3. 同时记录oldLast 的值为 子字符串的结束的 索引+1的值即35, 即下次执行find时，就从35开始匹配
         *
         * matcher.group(0) 分析
         *
         * 源码:
         * public String group(int group) {
         *         if (first < 0)
         *             throw new IllegalStateException("No match found");
         *         if (group < 0 || group > groupCount())
         *             throw new IndexOutOfBoundsException("No group " + group);
         *         if ((groups[group*2] == -1) || (groups[group*2+1] == -1))
         *             return null;
         *         return getSubSequence(groups[group * 2], groups[group * 2 + 1]).toString();
         *     }
         *  1. 根据 groups[0]=31 和 groups[1]=35 的记录的位置，从content开始截取子字符串返回
         *     就是 [31,35) 包含 31 但是不包含索引为 35的位置
         *
         *  如果再次指向 find方法.仍然安上面分析来执行
         */
        while (matcher.find()) {
            //小结
            //1. 如果正则表达式有() 即分组
            //2. 取出匹配的字符串规则如下
            //3. group(0) 表示匹配到的子字符串
            //4. group(1) 表示匹配到的子字符串的第一组字串
            //5. group(2) 表示匹配到的子字符串的第2组字串
            //6. ... 但是分组的数不能越界.
            System.out.println("找到: " + matcher.group(0));
            System.out.println("第1组()匹配到的值=" + matcher.group(1));
            System.out.println("第2组()匹配到的值=" + matcher.group(2));


        }
    }
}
```

---

## 各种元字符功能

- 正则表达式里的元字符的转义符使用**`\\`**需要使用转义符的字符有：**`. * () $ / \ ? [] ^ {} |`**

  > 1. 限定符
  >
  >    > **`*`**指定字符重复 **0 次或 多次**， 例 `(abc)*`仅包含任意个 abc 的字符串
  >    >
  >    > **`+`**指定字符重复 **1 次或 多次，** 例 `m + (abc)*`至少以一个 m 开头，后接任意个 abc 的字符串
  >    >
  >    > **`?`** 指定字符重复**0 次或 1次**， 例 `m + (abc)?`至少以一个 m 开头，后最多接1个 abc 的字符串
  >    >
  >    > **`{n}`**只能输入 n 个字符，例 `[abcd]{3}`，由abcd中字母组成的任意长度为3 的字符串，
  >    >
  >    > **`{n,}`**指定至少 n 个匹配
  >    >
  >    > **`{n,m}`**指定至少 n 个匹配不多于 m 个匹配，例 `a{4,5}`java匹配默认**贪婪匹配**优先匹配 5个a
  >
  > 2. 选择匹配符
  >
  >    > **`|`** 选择匹配 例：`a|b|c`匹配 a或b或c
  >
  > 3. 分组组合符和反向引用符
  >
  >    > **`(pattern)`** 非命名分组。捕获匹配的子串。编号为 **0**  的**第一个捕获是由整个正则表达式模式匹配的文本**，其它的捕获结果则**根据括号分组的顺序从 1 开始自动编号**。
  >    >
  >    > **`(?<name> pattern)`**命名捕获将匹配的子串捕获到一个组名称或编号名称中。用于 name 的字符串不能包含任何标点符号，并且不能以数字开头。可以用单引号代替尖括号 例`(?'name' pattern)`
  >    >
  >    > **`(?:pattern)`**:非捕获分组匹配，匹配 pattern，但是不捕获，是 `|`更加经济的写法 例 `abcd|abce|abcf` 可以写成 `abc(?:d|e|f)`
  >    >
  >    > **`(?=pattern)`**例 `windows(?=95|98|2000)` 会匹配 `windows95`中的 windows 但是不会匹配`windows3.1` 中的 windows
  >    >
  >    > **`(?!pattern)`**例 `windows(?=95|98|2000)` 会匹配`windows3.1` 中的 windows 但是不会匹配`windows95` 中的 windows
  >
  > 4. 特殊字符
  >
  > 5. 字符匹配符
  >
  >    > **`[]`** 表示接收的字符序列， 例 `[abc]` 表示a,b,c中任意一个字符 `[]`内部除转移字符，其余特殊字符表示本身
  >    >
  >    > **`[^]`**表示不接收的字符序列
  >    >
  >    > **`-`** 连字符， 例 `A-Z` 表示任意一个大写字母
  >    >
  >    > **`.`**匹配除`\n`以外的任何字符，例 `a..b` 表示a开头，b结尾，中间两个任意字符
  >    >
  >    > **`\\d`**匹配单个数字字符相当于 `[0-9]` 例 `\\d{3}(\\d)?`3个或4个数字的字符串
  >    >
  >    > **`\\D`**匹配单个非数字字符相当于 `[^0-9]` 例 `\\D(\\d)*` 以单个非字符开头后接任意个数字
  >    >
  >    > **`\\w`**匹配单个数字，大小写字母,下划线 相当于`[0-9a-zA-z_]`
  >    >
  >    > **`\\W`**匹配单个非数字，大小写字母 ,下划线相当于`[^0-9a-zA-z_]`
  >    >
  >    > **`\\s`**匹配任何空白字符 制表符，空格
  >    >
  >    > **`\\S`**匹配任何非空白字符
  >
  > 6. 定位符
  >
  >    > **`^`**指定起始字符 例`^[0-9]+[a-z]*`至少以一个数字开头(**文本开头**)，后接任意个小写字母
  >    >
  >    > **`$`**指定结束字符 例`^[0-9]+[A-Z]+$`至少以一个数字开头，后接任意个小写字母，至少以一个大写字母结尾(**文本结尾**)
  >    >
  >    > **`\\b`** 匹配目标串的子串右边界，指的是子串以空格分割
  >    >
  >    > **`\\B`**匹配目标字符串的非边界

- java 正则表达式**默认是区分字母大小写**的，如何实现不区分大小写：

  > **`(?i)abc`** 表示abc都不区分大小写
  >
  > **`a((?i)b)c`**表示只有 b 不区分大小写
  >
  > 还可以在 `Pattern`类中设置 **`Pattern pattern = Pattern.compile(regEx, Pattern.CASE_INSENSITIVE)`**

  

## 正则表达式常用类

1. **`Pattern`**类

   > `pattern`对象是一个正则表达式对象。`Pattern`类没有公共的构造方法。创建一个 `Pattern`对象，调用其公共静态方法，返回一个 `Pattern`对象。该方法接收一个正则表达式作为它的第一个参数，例：**`Pattern p = Pattern.compile(pattern)`**

2. **`Matcher`**类

   > `Matcher`对象是对输入的字符串进行解释和匹配的引擎。和`Pattern`类一样，`Matcher`类也没有公共构造方法。需要调用 `Pattern` 对象的 `matcher`方法来获得一个 `Matcher`对象

3. **`PatternSyntaxException`**

   > 是一个非强制异常类，它表示一个正则表达式中的语法错误



## 反向引用

**圆括号的内容被捕获**后，可以在这个**括号后被使用**，从而写出一个比较实用的匹配模式，被称为**反向引用**，这种引用即可以在正则表达式内部用**`\\分组号`**，也可以在外部**`$分组号`**

例：

1. 需要匹配两个连续相同的数字：`(\\d)\\1`
2. 需要匹配5个连续相同的数字：`(\\d)\\1{4}`
3. 要匹配个位与千位相同，十位与百位相同的数：`(\\d)(\\d)\\2\\1`

```java
package com.lzy.regexp;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegExp13 {
    public static void main(String[] args) {
        String content = "我....我要....学学学学....编程java!";

        //1. 去掉所有的.

        Pattern pattern = Pattern.compile("\\.");
        Matcher matcher = pattern.matcher(content);
        content = matcher.replaceAll("");
	/*
         System.out.println("content=" + content);

         //2. 去掉重复的字  我我要学学学学编程java!
         //思路
         //(1) 使用 (.)\\1+
         //(2) 使用 反向引用$1 来替换匹配到的内容
         //注意：因为正则表达式变化，所以需要重置 matcher
        pattern = Pattern.compile("(.)\\1+");//分组的捕获内容记录到$1
        matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到=" + matcher.group(0));
        }

        //使用 反向引用$1 来替换匹配到的内容
        content = matcher.replaceAll("$1");
        System.out.println("content=" + content);
	*/
        //3. 使用一条语句 去掉重复的字  我我要学学学学编程java!
        content = Pattern.compile("(.)\\1+").matcher(content).replaceAll("$1");

        System.out.println("content=" + content);

    }
}
```



## String使用正则表达式

- `replaceAll(String regex,  String replacement)`  用给定的替换字符串去替换与给定的**正则表达式匹配的**此字符串的每个子字符串。 返回 `String`

- `matches(String regex)`  告诉这个字符串是否匹配给定的**正则表达式** 。 返回 `boolean`

- `split(String regex)`  将这个字符串由给定的**正则表达式**的匹配来拆分。返回 `String[]`

---

## 正则表达式模板

```
一、校验数字的表达式

1 数字：^[0-9]*$
2 n位的数字：^\d{n}$
3 至少n位的数字：^\d{n,}$
4 m-n位的数字：^\d{m,n}$
5 零和非零开头的数字：^(0|[1-9][0-9]*)$
6 非零开头的最多带两位小数的数字：^([1-9][0-9]*)+(.[0-9]{1,2})?$
7 带1-2位小数的正数或负数：^(\-)?\d+(\.\d{1,2})?$
8 正数、负数、和小数：^(\-|\+)?\d+(\.\d+)?$
9 有两位小数的正实数：^[0-9]+(.[0-9]{2})?$
10 有1~3位小数的正实数：^[0-9]+(.[0-9]{1,3})?$
11 非零的正整数：^[1-9]\d*$ 或 ^([1-9][0-9]*){1,3}$ 或 ^\+?[1-9][0-9]*$
12 非零的负整数：^\-[1-9][]0-9"*$ 或 ^-[1-9]\d*$
13 非负整数：^\d+$ 或 ^[1-9]\d*|0$
14 非正整数：^-[1-9]\d*|0$ 或 ^((-\d+)|(0+))$
15 非负浮点数：^\d+(\.\d+)?$ 或 ^[1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0$
16 非正浮点数：^((-\d+(\.\d+)?)|(0+(\.0+)?))$ 或 ^(-([1-9]\d*\.\d*|0\.\d*[1-9]\d*))|0?\.0+|0$
17 正浮点数：^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$ 或 ^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$
18 负浮点数：^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$ 或 ^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$
19 浮点数：^(-?\d+)(\.\d+)?$ 或 ^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$

二、校验字符的表达式

1 汉字：^[\u4e00-\u9fa5]{0,}$
2 英文和数字：^[A-Za-z0-9]+$ 或 ^[A-Za-z0-9]{4,40}$
3 长度为3-20的所有字符：^.{3,20}$
4 由26个英文字母组成的字符串：^[A-Za-z]+$
5 由26个大写英文字母组成的字符串：^[A-Z]+$
6 由26个小写英文字母组成的字符串：^[a-z]+$
7 由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$
8 由数字、26个英文字母或者下划线组成的字符串：^\w+$ 或 ^\w{3,20}$
9 中文、英文、数字包括下划线：^[\u4E00-\u9FA5A-Za-z0-9_]+$
10 中文、英文、数字但不包括下划线等符号：^[\u4E00-\u9FA5A-Za-z0-9]+$ 或 ^[\u4E00-\u9FA5A-Za-z0-9]{2,20}$
11 可以输入含有^%&',;=?$\"等字符：[^%&',;=?$\x22]+
12 禁止输入含有~的字符：[^~\x22]+

三、特殊需求表达式

1 Email地址：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
2 域名：[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(/.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+/.?
3 InternetURL：[a-zA-z]+://[^\s]* 或 ^https://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$
4 手机号码：^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\d{8}$
5 电话号码("XXX-XXXXXXX"、"XXXX-XXXXXXXX"、"XXX-XXXXXXX"、"XXX-XXXXXXXX"、"XXXXXXX"和"XXXXXXXX)：^(\(\d{3,4}-)|\d{3.4}-)?\d{7,8}$ 
6 国内电话号码(0511-4405222、021-87888822)：\d{3}-\d{8}|\d{4}-\d{7}
7 身份证号：
		15或18位身份证：^\d{15}|\d{18}$
		15位身份证：^[1-9]\d{7}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}$
		18位身份证：^[1-9]\d{5}[1-9]\d{3}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{4}$
8 短身份证号码(数字、字母x结尾)：^([0-9]){7,18}(x|X)?$ 或 ^\d{8,18}|[0-9x]{8,18}|[0-9X]{8,18}?$
9 帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$
10 密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：^[a-zA-Z]\w{5,17}$
11 强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在8-10之间)：^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$ 
12 日期格式：^\d{4}-\d{1,2}-\d{1,2}
13 一年的12个月(01～09和1～12)：^(0?[1-9]|1[0-2])$
14 一个月的31天(01～09和1～31)：^((0?[1-9])|((1|2)[0-9])|30|31)$ 
15 钱的输入格式：
16 1.有四种钱的表示形式我们可以接受:"10000.00" 和 "10,000.00", 和没有 "分" 的 "10000" 和 "10,000"：^[1-9][0-9]*$ 
17 2.这表示任意一个不以0开头的数字,但是,这也意味着一个字符"0"不通过,所以我们采用下面的形式：^(0|[1-9][0-9]*)$ 
18 3.一个0或者一个不以0开头的数字.我们还可以允许开头有一个负号：^(0|-?[1-9][0-9]*)$ 
19 4.这表示一个0或者一个可能为负的开头不为0的数字.让用户以0开头好了.把负号的也去掉,因为钱总不能是负的吧.下面我们要加的是说明可能的小数部分：^[0-9]+(.[0-9]+)?$ 
20 5.必须说明的是,小数点后面至少应该有1位数,所以"10."是不通过的,但是 "10" 和 "10.2" 是通过的：^[0-9]+(.[0-9]{2})?$ 
21 6.这样我们规定小数点后面必须有两位,如果你认为太苛刻了,可以这样：^[0-9]+(.[0-9]{1,2})?$ 
22 7.这样就允许用户只写一位小数.下面我们该考虑数字中的逗号了,我们可以这样：^[0-9]{1,3}(,[0-9]{3})*(.[0-9]{1,2})?$ 
23 8.1到3个数字,后面跟着任意个 逗号+3个数字,逗号成为可选,而不是必须：^([0-9]+|[0-9]{1,3}(,[0-9]{3})*)(.[0-9]{1,2})?$ 
24 备注：这就是最终结果了,别忘了"+"可以用"*"替代如果你觉得空字符串也可以接受的话(奇怪,为什么?)最后,别忘了在用函数时去掉去掉那个反斜杠,一般的错误都在这里
25 xml文件：^([a-zA-Z]+-?)+[a-zA-Z0-9]+\\.[x|X][m|M][l|L]$
26 中文字符的正则表达式：[\u4e00-\u9fa5]
27 双字节字符：[^\x00-\xff] (包括汉字在内，可以用来计算字符串的长度(一个双字节字符长度计2，ASCII字符计1))
28 空白行的正则表达式：\n\s*\r (可以用来删除空白行)
29 HTML标记的正则表达式：<(\S*?)[^>]*>.*?|<.*? /> (网上流传的版本太糟糕，上面这个也仅仅能部分，对于复杂的嵌套标记依旧无能为力)
30 首尾空白字符的正则表达式：^\s*|\s*$或(^\s*)|(\s*$) (可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式)
31 腾讯QQ号：[1-9][0-9]{4,} (腾讯QQ号从10000开始)
32 中国邮政编码：[1-9]\d{5}(?!\d) (中国邮政编码为6位数字)
33 IP地址：\d+\.\d+\.\d+\.\d+ (提取IP地址时有用)
```





































