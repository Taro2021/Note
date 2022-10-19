# Lambda 表达式

Lambda 是一个**匿名函数**，是一段可以传递的代码。本质是作为函数式接口的实例。

**`(形参列表，就是接口中抽象方法的形参列表)-> 重写抽象方法体`**：lambda 操作符

```java
public class LambdaTest {
    @Test
    public void test1(){
        Runnable r1 = new Runnable() {
            @Override
            public void run() {
                System.out.println("普通写法");
            }
        };
        r1.run();
        System.out.println("-------------------------------");

        Runnable r2 = () -> System.out.println("Lambda表达式写法");
        r2.run();
        
        //lambda 表达式写法
        Comparator<Integer> com = (o1, o2) -> Integer.compare(o1, o2);
        System.out.println(com.compare(1,2));
        
        //方法引用
        Comparator<Integer> com1 = Integer :: compare;
        System.out.println(com.compare(1,2));
    }
}
```

## Lambda表达式使用的情况

1. 无参，无返回值

   ```java
   Runnable r2 = () -> {System.out.println("Lambda表达式写法");};//{ ;}可以省略
   ```

2. 需要一个参数，无返回值，参数类型可以省略，参数的小括号也可以省略

   ```java
   Consumer<String> con = (str)-> System.out.println(str);
   Consumer<String> con1 = str-> System.out.println(str);
   ```

3. 多个参数，多条语句，可以有返回值

   ```java
   Comparator<Integer> com = (o1, o2)-> {
       System.out.println(o1);
       System.out.println(o2);
       return o1.compareTo(o2);
   };
   ```

4. lambda 体只有一条返回语句的时候，可以省略 return 与大括号

   ```java
   Comparator<Integer> com = (o1, o2) -> o1.compareTo(o2);
   ```

无歧义能省则省。

---

# 函数式(Functional)接口

1. 若一个接口中，只声明了一个抽象方法，则此接口称为函数式接口。
2. 可以通过 lambda 表达式创建函数式接口的实例。
3. 可以在接口上使用 `@FunctionalInterface`注解，这样可以检验它是否是一个函数式接口。
4. 在 java.util.function 包下定义了 java8 的丰富的函数是接口。
5. 之前的匿名实现类都可以用 lambda 表达式来写。

## 内置的四大核心函数式接口

![image-20221019125608143](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125608143.png)

```java
@Test
public void test3(){
    consumerTest(100, o1 -> System.out.println(o1));
}

public void consumerTest(int a, Consumer<Integer> con){
    con.accept(a);
}
```

# 方法引用/构造器引用

1. 当要传递给 lambda 体的操作，已经有了实现的方法，可以使用方法引用

2. 实现接口的抽象方法的参数列表和返回值类型，必须与方法引用的方法的参数列表和返回值相同

3. 使用操作符 `::` 将要引用方法所属的类或对象与方法名隔开

4. 三种情况

   > 对象 `::`实例方法名
   >
   > 类 `::`实例方法名
   >
   > 类 `::`静态方法名

---

# Stream API

使用 Stream API 对集合数据进行操作，就类似于使用 sql 执行的数据库查询。

Stream 是数据渠道，用于操作数据源（集合，数组等）所生成的元素序列。

注意：

1.  Stream 不会自己存储数据。
2. Stream 不会改变源对象。会返回一个持有结果的新 Stream。
3. Stream 操作是延迟执行的，这意味着他们会等到需要结果的时候才执行。

![image-20221019125641680](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125641680.png)

## Stream 的创建

```java
public class StreamAPITest {
    //创建 Stream 方式一：通过集合
    @Test
    public void test1(){
        ArrayList<Integer> list = new ArrayList<>();
        for(int i = 0;i < 10; ++i) list.add(i);

        //返回一个顺序流
        Stream<Integer> stream = list.stream();

        //返回一个并行流，并行取数据，不一定顺序获取数据
        Stream<Integer> integerStream = list.parallelStream();
    }

    //创建方式二：数组
    @Test
    public void test2(){
        Integer[] arr = {0, 1, 2, 3, 4, 5};
        //调用 Arrays 工具类的 static <T> stream<T> stream(T[] array)：返回一个流
        Stream<Integer> stream = Arrays.stream(arr);
    }

    //创建方式三：通过 Stream 自身的 of()
    @Test
    public void test3(){
        Integer[] arr = {0, 1, 2, 3, 4, 5};
        Stream<Integer> stream = Stream.of(arr);
    }

    //创建方式四：创建无限流
    @Test
    public void test4(){
        //迭代 public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f)
        //遍历前前 10 个偶数，输出打印
        Stream.iterate(0,t -> t + 2).limit(10).forEach(System.out :: println);

        //生成 public static<T> Stream<T> generate(Supplier<T> s)
        //生成 10 个随机数
        Stream.generate(Math::random).limit(10).forEach(System.out :: println);
    }
}
```

---

## Stream 中间操作

### 筛选与切片

![image-20221019125657845](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125657845.png)

```java
//筛选与切片
@Test
public void test1(){
    ArrayList<Integer> list = new ArrayList<>();
    for(int i = 0; i < 10; ++i) list.add(i);
    list.add(9);

    //1. filter(Predicate p) 过滤，接收 lambda，从流中排除某些元素
    //获取偶数
    //forEach(Comsumer<T> )
    list.stream().filter(o1 -> o1 % 2 == 0).forEach(System.out::println);

    //2. limit(n) 截断流，是获取元素不超过给定值
    list.stream().limit(5).forEach(System.out::println);

    //3. skip(n) 跳过前 n 个元素
    list.stream().skip(5).forEach(System.out::println);

    //distinct 去重
    list.stream().distinct().forEach(System.out::println);
}
```

### 映射

![image-20221019125714366](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125714366.png)

```java
//映射
@Test
public void test2(){
    List<String> list = Arrays.asList("aa", "bb", "cc", "dd");
    //map(Function f) 接收一个函数作参数，将元素转换成其他形式或提取信息，
    // 该函数会被应用到每一个元素上，并将其映射为一个新元素。
    System.out.print("map: ");
    list.stream().map(str -> str.toUpperCase() + " ").forEach(System.out::print);
    System.out.println();

    //map(集合里面套集合) 与 flatmap(将嵌套的集合打散) 的区别
    Stream<Stream<Character>> streamStream = list.stream().map(StreamTest2::fromStringToStream);
    streamStream.forEach(s -> s.forEach(o -> System.out.print(o + " ")));
    System.out.println();

    //flatMap(Function f) 接收一个函数作参数，将流中的每一个值都替换成另一个流
    // 然后把所有流连成一个流。
    System.out.print("flatmap: ");
    list.stream().flatMap(StreamTest2::fromStringToStream).forEach(o1 -> System.out.print(o1 + " "));
}

//将字符串中的多个字符构成的集合转换为对应的 Stream 实例
public static Stream<Character> fromStringToStream(String str){
    ArrayList<Character> list = new ArrayList<>();
    for(Character c : str.toCharArray()) list.add(c);
    return list.stream();
}
```

![](F:\java\spring5\photo\snipaste_20220720_170833.jpg)

### 排序

![image-20221019125732670](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125732670.png)

```java
//排序
@Test
public void test3(){
    List<Integer> list = Arrays.asList(2, 3, 5, 1, 6, 7, 9, 8, 0);
    list.stream().sorted().forEach(o -> System.out.print(o + " "));
    System.out.println();

    list.stream().sorted((o1, o2) -> o2 - o1).forEach(o -> System.out.print(o + " "));
}
```

![](F:\java\spring5\photo\snipaste_20220720_171046.jpg)

## Stream 终止操作

### 匹配与查找

![image-20221019125744150](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125744150.png)

```java
@Test
public void test4(){
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 7, 5 ,8, 9, 6, 0);
    //allMatch 检查是否匹配所有元素
    boolean b = list.stream().allMatch(o -> o > 5);
    System.out.println(b);//false

    //anyMatch 任一匹配
    boolean b1 = list.stream().anyMatch(o -> o > 5);
    System.out.println(b1);//true

    //noneMath 检查是否没有匹配元素
    boolean b2 = list.stream().noneMatch(o -> o > 5);
    System.out.println(b2);//false

    //findFirst 返回第一个元素
    Optional<Integer> first = list.stream().sorted().findFirst();
    System.out.println(first);

    //findAny 返回流中任一个元素
    Optional<Integer> anyOne = list.stream().findAny();
    System.out.println(anyOne);

    //count 统计流中元素个数
    long count = list.stream().filter(o -> o > 5).count();
    System.out.println(count);

    //max(Comparator c) 返回流中最大值
    Optional<Integer> max = list.stream().max(((o1, o2) -> o1 - o2));
    System.out.println(max);

    //min(Comparator c) 返回流中最小值
    Optional<Integer> min = list.stream().min((o1, o2) -> o1 - o2);
    System.out.println(min);

    //forEach(Consumer c) 内部迭代
    list.stream().sorted().forEach(o -> System.out.print(o + " "));
}
```

### 规约

![image-20221019125755639](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125755639.png)

```java
@Test
public void test5(){
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7 ,8, 9, 10);
    //reduce(T identity, BinaryOperator) 可以将流中的数据反复结合起来，得到一个值
    // identity 初始值， BinaryOperator<T> 继承了二元函数函数式接口 extends BiFunction<T, T, T>
    Integer sum = list.stream().reduce(0, Integer::sum);
    System.out.println(sum);

    //reduce(BinaryOperator)
    Optional<Integer> sum1 = list.stream().reduce((o1, o2) -> o1 + o2);
    System.out.println(sum1);
}
```

### 收集

![](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125755639.png)

![image-20221019125836569](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125836569.png)

```java
@Test
public void test6(){
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7 ,8, 9, 10);
    //查找返回大于5的数，结果返回一个 List 或者 Set
    List<Integer> list1 = list.stream().filter(o1 -> o1 > 5).collect(Collectors.toList());
    System.out.println(list1);
    Set<Integer> set = list.stream().filter(o -> o > 5).collect(Collectors.toSet());
    System.out.println(set);
}
```

---

# Optional 类

![image-20221019125905371](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125905371.png)

![image-20221019125929726](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20221019125929726.png)



































