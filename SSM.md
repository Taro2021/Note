# Spring5

# Spring框架概述

**Spring两个核心部分**：

- **IOC**：控制反转，把创建对象的过程交给 Spring 进行管理
- **AOP**：面向切面，不修改源码进行功能增强

[Spring jar包下载](https://repo.spring.io/artifactory/release/org/springframework/spring/)

**入门案例**：

1. jar 包的下载

2. idea 创建 java 工程

3. 导入 jar 包

4. 创建一个普通类，并创建一个普通方法

   ```java
   public class User {
       public void add(){
           System.out.println("add...");
       }
   }
   ```

5. 创建 Spring 配置文件，在配置文件中配置要创建的对象

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <!-- 配置 User 对象的创建 id 对象名, class 类路径 -->
       <bean id="user" class="com.lzy.sping5.User"></bean>
   </beans>
   ```

6. 测试（仅演示效果，开发中并不会如此使用）

   ```java
   public class TestSpring5 {
       @Test
       public void testAdd(){
           //1. 加载 Spring 的配置文件
           ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
   
           //2.获取配置创建的对象
           User user = context.getBean("user", User.class);
   
           System.out.println(user);
           user.add();
       }
   
   }
   ```

   ![](F:\java\spring5\photo\snipaste_20220714_153517.jpg)

maven 配置

```xml
<dependencies>
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>

```



# IOC 概念和原理

**IOC**:

- 使用对象时，由主动new产生对象转换成，从外部提供对象，在这个过程中，对象的创建控制权由程序转移到外部，此思想称为控制反转。
- 使用 IOC 的目的：降低耦合度

IOC基本操作需要的 jar：`spring-beans-5.2.6.RELEASE.jar, spring-context-5.2.6.RELEASE.jar, spring-core-5.2.6.RELEASE.jar, spring-expression-5.2.6.RELEASE.jar `



## 底层原理

​	主要用到的技术 xml 解析，**工厂模式**，反射。

1. IOC 思想基于 IOC 容器完成，IOC 容器底层就是对象工厂

2. Spring 提供 IOC 容器实现的两种方式：(两个接口)

   > **`BeanFactory`**：IOC 容器的基本实现，是 Spring 内部的使用接口，一般不提供开发人员使用。加载配置文件的时候，不会去创建对象，而在获取对象和使用对象的时候才会去创建 bean 对象(**懒加载**)。
   >
   > **`ApplicationContext`**：`BeanFactory` 接口的子接口，提供更强大的功能，供开发人员使用。加载配置文件的时候，就会创建对应的 bean 对象。

3. **`ApplicationContext`**接口的实现类：

   > **`FileSystemXmlApplicationContext`**：配置文件的磁盘路径
   >
   > **`ClassPathXmlApplicationContext`**：配置文件的类路径



## IOC 操作 Bean 管理 基于xml

**Bean 管理**：Spring 创建对象，Spring 注入属性

**Bean 管理两种方式**：

- 基于 xml 配置文件方式实现

- 基于注解方式实现

  

### **基于 xml 配置文件创建对象**

```xml
<bean id="user" class="com.lzy.sping5.User"></bean>
```

1. 在 Spring 配置文件中，使用 **bean** 标签，标签里添加相应的属性，就可以实现对象的创建

2. bean 标签中的属性：

   >id 属性：给创建的对象的唯一标识，可以通过 id 获取对象
   >
   >class 属性：类全路径(包类路径)
   >
   >name 属性：效果与 id 相同，name可以相同，id 唯一

3. 创建对象的时候，默认执行无参构造，本质是使用反射实现 `Class.forName("User").newIntance();`

### **基于 xml 配置文件注入属性**

**DI dependency injection**：依赖注入，是 IOC 的一种具体实现

> 第一种方式：使用 **set** 注入
>
> ```xml
> <bean id="user" class="com.lzy.sping5.User">
>        <!-- 使用 property 完成属性的注入
>             name：类里面属性的名称
>             value：向属性注入的值
>         -->
>        <property name="username" value="lzy"></property>
>        <property name="age" value="18"></property>
> </bean>
> ```
>
> **简化**：p 名称空间注入
>
> ```xml
> <!-- 第一步在配置文件中添加 p 名称空间-->
> <bean
>        xmlns:p="http://www.springframework.org/schema/p"
>       ...
> >
> </bean>
> ```
>
> ```xml
> <bean id="user" class="com.lzy.sping5.User" p:username="lzy" p:age="18">
> </bean>
> ```
>
> 第二种方式：有参构造注入
>
> ```xml
> <bean id="user" class="com.lzy.sping5.User">
>        <!--
>   有参构造有多个参数需要注入，使用多个 constructor-arg 标签
>  -->
>        <constructor-arg name="username" value="lzy"></constructor-arg>
>        <constructor-arg name="age" value="18"></constructor-arg>
> </bean>
> ```

#### **字面量**：

1. 空值注入

   ```xml
   <property name="username">
   	<null/>
   </property>
   ```

2. 特殊字符

   ```xml
   <!-- 属性值包含特殊字符：1.转义 &lt: &gt: ；2.把特殊符号内容写到 CDATA -->
   <property name="username">
   	<value><![CDATA[含特殊字符<<"1"sss>>内容]]></value>
   </property>
   ```

#### **外部 Bean**:

1. 创建两个类 service 类和 dao 类
2. 在 service 调用 dao 里面的方法
3. 在 Spring 配置文件中进行配置

```java
public interface UserDao {
    public void update();
}
```

```java
public class UserDaoImpl implements UserDao{
    public void update() {
        System.out.println("dao, update...");
    }
}
```

```java
public class UserService {

    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    public void add(){
        System.out.println("service, add...");
	    userDao.update();
        /**
         * 原始方法
         * UserDao userDao = new UserDaoImpl();
         * userDao.update();
         */
    }
}
```

```xml
<!-- service 和 dao 对象的创建 -->
<bean id="userService" class="com.lzy.sping5.service.UserService">
    <!-- 注入 userDao 对象 对象数据类型注入需要使用属性 ref
            ref 属性：创建 userDao 对象 bean 标签 id 值
        -->
    <property name="userDao" ref="userDaoImpl"></property>
</bean>
<bean id="userDaoImpl" class="com.lzy.sping5.dao.UserDaoImpl"></bean>
```

```java
//测试
@Test
public void test1(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");

    UserService userService = context.getBean("userService", UserService.class);

    userService.add();
}
```

![](F:\java\spring5\photo\snipaste_20220714_172814.jpg)



#### 内部 Bean 

一对多关系：以实体类之间的演示一对多关系

例：

```java
//现在有一个部门类和一个员工类
public class Dept {
    private String dName;

    public void setdName(String dName) {
        this.dName = dName;
    }
}

public class Emp {

    private String eName;
    private String gender;
    //员工属于某一个部门，使用对象形式表示
    private Dept dept;

    public void setDept(Dept dept) {
        this.dept = dept;
    }

    public void seteName(String eName) {
        this.eName = eName;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }
}
```

在 Spring 配置文件中进行相关配置

```xml
<!-- 内部 Bean -->
<bean id="emp" class="com.lzy.sping5.bean.Emp">
    <!-- 设置两个普通属性 -->
    <property name="eName" value="lzy"></property>
    <property name="gender" value ="男"></property>
    <!-- 设置对象类型属性 -->
    <property name="dept">
        <!-- 在内部在定义一个 bean 标签 -->
        <bean id="dept" class="com.lzy.sping5.bean.Dept">
            <property name="dName" value="保安部"></property>
        </bean>
    </property>
</bean>
```

#### 级联赋值

```xml
<!-- 写法1 -->
<bean id="emp" class="com.lzy.sping5.bean.Emp">
    <!-- 设置两个普通属性 -->
    <property name="eName" value="lzy"></property>
    <property name="gender" value ="男"></property>
    <!-- 级联赋值 -->
    <property name="dept" ref="dept"></property>
</bean>

<bean id="dept" class="com.lzy.sping5.bean.Dept">
    <property name="dName" value="保安部"></property>
</bean>


<!-- 写法2 -->
<bean id="emp" class="com.lzy.sping5.bean.Emp">
    <!-- 设置两个普通属性 -->
    <property name="eName" value="lzy"></property>
    <property name="gender" value ="男"></property>
    <!-- 级联赋值 -->
    <property name="dept" ref="dept"></property>
    <property name="dept.dname" ref="保安部"></property>
</bean>

<bean id="dept" class="com.lzy.sping5.bean.Dept"></bean>
```

### xml 注入集合属性

```xml
<!-- 集合属性类型的注入 -->
<bean id="stu" class="com.lzy.sping5.collectiontype.Stu">
    <!-- 1. 数组类型的注入 -->
    <property name="courses">
        <!-- array 标签 和 list 标签都可以用来注入数值-->
        <array>
            <!-- value 标签来设置数组元素 -->
            <value>java入门到入土</value>
            <value>如何快速送外卖</value>
        </array>
    </property>

    <!-- List 类型集合注入 -->
    <property name="list">
        <list>
            <value>111</value>
            <value>222</value>
        </list>
    </property>


    <!-- Map 类型的注入 -->
    <property name="map">
        <map>
            <entry key="key1" value="value1"></entry>
            <entry key="key2" value="value2"></entry>
        </map>
    </property>

    <!-- Set 集合的注入 -->
    <property name="set">
        <set>
            <value>111</value>
            <value>222</value>
        </set>
    </property>

</bean>
```

```java
public class Stu {
    //1.数值类型的属性
    private String[] courses;

    //2.集合类型的属性
    private List<String> list;

    //3. map 类型的属性
    private Map<String, String> map;

    //4. set 类型的属性
    private Set<String> set;

    public void setSet(Set<String> set) {
        this.set = set;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public void setMap(Map<String, String> map) {
        this.map = map;
    }

    public void setCourses(String[] courses) {
        this.courses = courses;
    }

    public void test(){
        System.out.println(Arrays.toString(courses));
        System.out.println(list);
        System.out.println(map);
        System.out.println(set);
    }
}
```

![](F:\java\spring5\photo\snipaste_20220714_204325.jpg)

   

### 注入集合中设置对象类型

```java
public class Course {
    private String cName;
    public void setcName(String cName) {
        this.cName = cName;
    }
}
```

```java
public class Stu {
    //集合中为对象类型
    private List<Course> courseList;

    public void setCourseList(List<Course> courseList) {
        this.courseList = courseList;
    }

    public void test(){
        System.out.println(Arrays.toString(courseList));
    }
}
```

```xml
<bean id="stu" class="com.lzy.sping5.collectiontype.Stu">  
    <!-- 注入 List 集合类型，集合内数据为对象类型 -->
    <property name="courseList" >
        <list>
            <!-- bean 属性写上外部创建的对象的 id 属性值 -->
            <ref bean="course1"></ref>
            <ref bean="course2"></ref>
        </list>
    </property>

</bean>

<!-- 创建多个 bean 对象 -->
<bean id="course1" class="com.lzy.sping5.collectiontype.Course">
    <property name="cName" value="java入门到入土"></property>
</bean>
<bean id="course2" class="com.lzy.sping5.collectiontype.Course">
    <property name="cName" value="美团入职技巧"></property>
</bean>
</beans>
```

![](F:\java\spring5\photo\snipaste_20220714_205636.jpg)

### 提取集合注入部分 util 约束

1. 首先在 Spring 配置文件中引入名称空间 util 约束

   ```xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:util="http://www.springframework.org/schema/util"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">
       <!-- 集合注入的提取 -->
   </beans>
   ```

2. 使用 util 标签完成 List 集合的注入提取，是一个 list 的 bean

   ```xml
   <!-- 集合注入的提取 -->
   <util:list id="bookList">
       <value>java入门到入土</value>
       <value>美团入职指南</value>
   </util:list>
   
   <!-- 提取的集合注入的使用 -->
   <bean id="book" class="com.lzy.sping5.collectiontype.Book">
       <property name="list" ref="bookList"></property>
   </bean>
   ```

3. 测试调用

   ```java
   @Test
   public void test2(){
       ApplicationContext context = new ClassPathXmlApplicationContext("bean6.xml");
       Book book = context.getBean("book", Book.class);
       System.out.println(book);
   }
   ```

   ![](F:\java\spring5\photo\snipaste_20220714_212649.jpg)

---

### FactoryBean

Spring 有两种类型的 bean，一种是普通 bean，另外一种是工厂 bean( FactoryBean，注意与BeanFactory 的区别，BeanFactory 是 Spring 提供给我们注入创建 bean 对象的接口)

**普通 bean**：我们自己创建的 bean 对象实例，需要我们自己去定义类型。在 Spring 的配置文件定义的 bean 类型就是返回类型。

**FactoryBean**：在配置文件中定义 bean 类型可以和返回的类型不一样。

> 第一步：创建类，让这个类作为工厂 bean，实现接口 FactoryBean
>
> 第二步：实现接口内的方法，在实现的方法中定义返回的 bean 类型

```java
public class MyFactoryBean implements FactoryBean<Course> {
    /**
     * 定义返回 bean
     * @return
     * @throws Exception
     */
    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setcName("lzy");
        return course;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return FactoryBean.super.isSingleton();
    }
}
```

```xml
<bean id="myBean" class="com.lzy.sping5.MyFactoryBean"></bean>
```

```java
@Test
public void test3(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean7.xml");
    Course course = context.getBean("myBean", Course.class);
    System.out.println(course);
}
```

![](F:\java\spring5\photo\snipaste_20220714_214606.jpg)

### bean 作用域

1. 在 Spring 中，可以设置创建 bean 实例是单实例还是多实例。

2. **默认情况**下，参加的 bean 是一个**单实例**对象。

   ```java
   @Test
   public void test2(){
       ApplicationContext context = new ClassPathXmlApplicationContext("bean6.xml");
       Book book1 = context.getBean("book", Book.class);
       Book book2 = context.getBean("book", Book.class);
   
       System.out.println(book1);
       System.out.println(book2);
   }
   ```

   ![](F:\java\spring5\photo\snipaste_20220714_215052.jpg)

   可以看到，两次获取的对象地址相同，是同一个对象。

3. 单实例，多实例的配置

   > 在 Spring 配置文件的 bean 标签里有属性 `scope`用于设置单实例还是多实例
   >
   > `scope`属性值：默认值`singleton`单实例；`prototype`模板，多实例对象；`request`；`session`。
   >
   > ```xml
   > <bean id="book" class="com.lzy.sping5.collectiontype.Book" scope="prototype">
   >     <property name="list" ref="bookList"></property>
   > </bean>
   > ```
   >
   > ![](F:\java\spring5\photo\snipaste_20220714_215552.jpg)
   >
   > 获取实例对象地址不同，创建了多个实例

4. `singleton`特点：

   > 单实例时，在加载配置文件的时候就会创建单实例对象。

5. `prototype`特点：

   >多实例时，是在调用 getBean 方法的时候创建实例对象。

### ==bean 生命周期==

1. 通过构造器创建 bean 对象**实例（无参构造）**
2. **依赖注入**，为对象的属性赋值和对其他 bean 的引用（调用 **set 方法**）
3. **把 bean 实例传递到 bean 后置处理器的方法**`postProcessBeforeInitialization`
4. 调用 bean 的**初始化方法**（需要进行配置初始化的方法 bean 标签的 **`init-method`** 属性进行配置）
5. **把 bean 实例传递到 bean 后置处理器的方法**`postProcessAfterInitialization`
6. 获取到 bean 实例对象
7. 当 ioc 容器关闭时，调用的 bean 的**销毁方法**（需要进行配置销毁方法  bean 标签的  **`destroy-method`** 属性进行配置）

**后置处理器的添加**：

- 创建类，实现接口 `BeanPostProcessor`

  ```java
  public class MyBeanPost implements BeanPostProcessor {
  
      @Override
      public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
          System.out.println("在初始化之前执行的方法");
          return bean;
      }
  
      @Override
      public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
          System.out.println("在初始化之后执行的方法");
          return bean;
      }
  }
  ```

- 在 Spring 的 xml 配置文件中配置，会对当前 ioc 容器中的每一个 bean 的生命周期起效

  ```xml
  <!-- 配置后置处理器 -->
  <bean id="myBeanPost" class="com.lzy.sping5.bean.MyBeanPost"></bean>
  ```

- 通过 Spring 注入创建的 bean 对象实例都会调用该后置处理器

---

### xml 自动装配

​	根据指定装配的规则（属性名称或者属性类型），Spring 自动将匹配的属性值注入。

```xml
<!--实现自动装配
        bean 标签中 autowire 属性配置自动装配
        autowire 属性常用的两个值：
            byName 根据属性名注入，注入值的 bean id值需要和类的属性名一样；
            byType 根据属性类型注入
    -->
<bean id="emp" class="com.lzy.sping5.bean.Emp" autowire="byName">
    <!-- 手动装配 <property name="dept" ref="dept"></property> -->

</bean>
<bean id="dept" class="com.lzy.sping5.bean.Dept">
    <property name="dName" value="保安部"></property>
</bean>
```

```xml
<!-- 根据属性类型
	byType 自动装配时：需要自动装配的 bean 对象不能有多个。 
-->
<bean id="emp" class="com.lzy.sping5.bean.Emp" autowire="byType"></bean>
<bean id="dept" class="com.lzy.sping5.bean.Dept">
    <property name="dName" value="保安部"></property>
</bean>
```

### 引入外部文件注入

以导入 druid 连接池为例

依赖

```xml
<!-- MySQL驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.16</version>
</dependency>
<!-- 数据源 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.0.31</version>
</dependency>
```

1. **引入 `context`命名空间**

   ```xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          
          xmlns:context="http://www.springframework.org/schema/context"
          
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
       ...
   ```

2. **在 Spring 标签中引入外部配置文件**

   ```xml
   <!-- 引入外部属性文件 -->
   <context:property-placeholder location="jdbc.properties"/>
   
   <!--配置连接池为例 -->
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
       <!-- ${key} 可以取到 properties 文件中的 值 -->
       <property name="driverClassName" value="${jdbc.driverClassName}"></property>
       <property name="url" value="${jdbc.url}"></property>
       <property name="username" value="${jdbc.username}"></property>
       <property name="password" value="${jdbc.password}"></property>
   </bean>
   ```

   ```properties
   jdbc.driverClassName=com.mysql.jdbc.Driver
   jdbc.url=jdbc:mysql://192.168.146.129:3306/ssm?serverTimezone=UTC&rewriteBatchedStatements=true
   jdbc.username=root
   jdbc.password=root
   ```

   

---



## IOC 操作 Bean 管理 基于注解

1. 注解是代码中的特殊标记，格式 `@注解名(属性名=属性值[,属性名=属性值,...])`
2. 使用注解，注解作用在类上面，方法上面，属性上面
3. 简化 xml 配置

**基于注解的IOC所需 jar：**`spring-aop-5.2.6.RELEASE.jar`

---

### Spring 针对 Bean 管理中创建对象提供的注解

1. `@Component`
2. `@Service` 常用在 service 层
3. `@Controller` 常用在 web 层
4. `@Repository` 常用在 dao 层

*上面四个注解功能是一样的，都可以用来创建 bean 实例*

---

### 注解方式实现对象创建

1. 引入 jar 包

2. 开启组件扫描

   > Spring 的 xml 文件中引入 `context`命名空间
   >
   > ```xml
   > <beans ...
   >        xmlns:context="http://www.springframework.org/schema/context"
   >        xsi:schemaLocation="...
   >                            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
   >     <!-- 开启组件扫描 -->
   >     <!-- component-scan 组件扫描， base-package 属性指定扫描的包
   >          1.逗号隔开可添加多个包
   >          2.直接写上层目录                          -->
   >     <context:component-scan base-package="com.lzy.study715.dao,
   > com.lzy.study715.service"></context:component-scan>
   > </beans>
   > ```

3. 在类上面添加创建对象的注解

   ```java
   /**
    * 在注解里value属性值可以省略不写
    * 默认值是类名，是字母小写
    * 只写 @Component 默认 value 是 UserService -> userService
    */
   @Component(value = "userService") //写法类似 <bean id="userService" class="..."/>
   public class UserService {
       public void add(){
           System.out.println("add...");
       }
   }
   ```

**组件扫描的配置细节**：例子

```xml
<!-- use-default-filters="false" 表示不使用默认 filter，自己配置 filter -->
<context:component-scan base-package="com.atguigu.springmvc" use-default-filters="false">
    <!-- context:include-filter，设置扫描哪些内容 -->
	<context:include-filter type="annotation"
           expression="org.springframework.stereotype.Controller"/>
</context:component-scan>


<context:component-scan base-package="com.atguigu.springmvc">
    <!-- context:exclude-filter，设置不扫描哪些内容 -->
	<context:exclude-filter type="annotation"
        	expression="org.springframework.stereotype.Controller"/>
</context:component-scan>

```

---

### 注解属性注入

1. `@AutoWired`：根据属性类型进行自动注入
2. `@Qualifier`：根据属性名称注入
3. `@Resource`：可以根据类型注入，可以根据属性名称注入
4. `@Value`：注入普通类型属性

**步骤**：以在 service 中注入 dao 类型属性为例

1. 把 service 和 dao 对象创建，在 service 和 dao 类添加创建对象添加注解

   ```java
   @Repository
   public class UserDaoImpl implements UserDao{
       @Override
       public void add() {
           System.out.println("UserDaoImpl.add()...");
       }
   }
   /*----------------------------------------------------------------------*/
   
   @Service
   public class UserService {  
       public void add(){
           System.out.println("userService.add()...");
       }
   }
   ```

2. 在 service 注入 dao 对象，在 service 类添加 dao 类型属性，在属性上使用属性注入注解

   ```java
   @Service
   public class UserService {
   
       //定义 dao 属性，不需要添加 set 方法
       @Autowired
       private UserDao userDao;
   
       public void add(){
           System.out.println("userService.add()...");
           userDao.add();
       }
   }
   ```

   ![](F:\java\spring5\photo\snipaste_20220715_230356.jpg)



`@Qualifier`需要和 `@AutoWired`一起使用

```java
@Service
public class UserService {
    
    @Autowired //根据类型注入，一个接口若有多个实现类时候，无法判断注入哪个实现类
    @Qualifier(value = "userDaoImpl01") //这是使用 Qualifier 指定名称
    private UserDao userDao;

    public void add(){
        System.out.println("userService.add()...");
        userDao.add();
    }
}
```

### 完全注解开发

1. 编写一个配置类，替代 xml 配置文件

   ```java
   @Configuration //作为配置类，替代 xml 配置文件
   @ComponentScan(basePackages = {"com.lzy.study715"}) //开启对 com.lzy.study715 包的组件扫描
   public class SpringConfig {
   }
   ```

2. 获取 context 对象的方法也不同

   ```java
   @Test
   public void test2(){
       ApplicationContext context
           = new AnnotationConfigApplicationContext(SpringConfig.class);
       UserService userService = context.getBean("userService", UserService.class);
       userService.add();
   }
   ```




---

# AOP

​	面向切面编程（**横向抽取**，重复代码与核心代码交织在一起而非连续，传统的面向对象是纵向继承机制，只能对连续的代码进行纵向抽取，此时需要利用 AOP 来完成对重复代码的横向抽取），利用 AOP 可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，提高开发效率。不通过修改源代码的形式，在主干功能里添加新功能。

​	代码简化，动态增强

## AOP 底层原理 ：代理模式

### AOP底层使用动态代理 

1. 第一种情况：有接口，使用 JDK 动态代理

   创建接口实现类的代理对象，增强类的方法

   ![](F:\java\spring5\photo\snipaste_20220716_134356.jpg)

2. 第二种情况：没有接口，使用 CGLIB 动态代理

   创建子类的代理对象，增强类的方法

   ![](F:\java\spring5\photo\snipaste_20220716_134640.jpg)

以 JDK 动态代理实现 AOP 为例演示：

1. 使用 Proxy 类里面的方法创建代理对象

   ![](F:\java\spring5\photo\snipaste_20220716_135923.jpg)

   `newProxyInstance(类加载器, 增强方法所在的类实现的接口(可多个), 增强方法的代理对象)`

```java
public class JDKProxy {

    public static void main(String[] args) {
        //创建接口实现类的代理对象
        Class[] interfaces = {UserDao.class};
        UserDaoImpl userDao = new UserDaoImpl();
        UserDao dao = (UserDao)Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces,
                new UserDaoProxy(userDao));
        dao.add();
        System.out.println("result:" + dao.sub(1, 2));
    }
}


//创建代理对象代码
class UserDaoProxy implements InvocationHandler {

    //1.创建了谁的代理对象，就把谁传递过来
    //有参构造传递
    private Object obj;
    public UserDaoProxy(Object obj){
        this.obj = obj;
    }

    //增强的逻辑
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //方法之前
        System.out.println("方法执行前" + method.getName() + "：传递的参数..." + Arrays.toString(args));

        //被增强的方法执行
        Object ret = method.invoke(obj, args);

        //方法之后
        System.out.println("方法之后执行..." + obj);

        return ret;
    }
}
```

![](F:\java\spring5\photo\snipaste_20220716_142550.jpg)

Spring 框架中对这些操作进行了封装

---



### AOP 操作术语

1. 切入点（横切关注点）：实际真正被增强的方法，称为切入点；从每个方法中横向抽取出来的同一类非核心业务

2. 通知（增强）：实际增强的逻辑部分，实现横切关注点上所需业务的方法

   > 前置通知
   >
   > 后置通知
   >
   > 环绕通知
   >
   > 异常通知
   >
   > 最终通知

3. 切面：是动作，把通知应用到切入点的过程，封装通知方法的类

4. 目标：被代理的目标对象

5. 代理：对目标对象应用通知之后，创建的代理对象

6. 连接点：类里的哪些方法可以被增强，称为连接点，即抽取横切关注点的位置

---



## **`AspectJ`**实现 AOP 操作

Spring 框架一般基于**`AspectJ`**实现 AOP 操作，`AspectJ`不是 Spring  的组成部分，独立 AOP 框架，一般把 `AspectJ` 和 Spring 框架一起使用进行 AOP 操作。

准备：引入相关依赖 `spring-aspects-5.2.6.RELEASE.jar`,`com.springsource.net.sf.cglib-2.2.0.jar`, `com.springsource.org.aopalliance-1.0.0.jar`, `com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar`

### 切入点表达式

1. 切入点表达式：知道对哪个类的哪个方法进行增强

2. 语法结构：`execution([权限修饰符][返回类型][类全路径][方法名称]([参数列表]))`

   > 例：对 com.lzy.dao.UserDao 类里的 add 进行增强  `execution(public int com.lzy.dao.UserDao.sub(..))`
   >
   > 对 com.lzy.dao.UserDao 类里所有方法进行增强  `execution(* com.lzy.dao.UserDao.*(..))`
   >
   > 对 com.lzy.dao 包里所有类所有方法进行增强  `execution(* com.lzy.dao.*.*(..))`
   >
   > 权限可以使用通配符，返回类型可省略



**语法细节：**

1. 用`*`号代替“权限修饰符”和“返回值”部分表示“权限修饰符”和“返回值”不限 
2. 在包名的部分，一个`*`号只能代表包的层次结构中的一层，表示这一层是任意的。 例如：`*.Hello`匹配`com.Hello`，不匹配`com.atguigu.Hello`
3. 在包名的部分，使用`*..`表示包名任意、包的层次深度任意 
4. 在类名的部分，类名部分整体用`*`号代替，表示类名任意 
5. 在类名的部分，可以使用`*`号代替类名的一部分 例如：`*Service`匹配所有名称以`Service`结尾的类或接口 
6. 在方法名部分，可以使用`*`号表示方法名任意 
7. 在方法名部分，可以使用`*`号代替方法名的一部分 例如：`*Operation`匹配所有方法名以`Operation`结尾的方法 
8. 在方法参数列表部分，使用`(..)`表示参数列表任意 
9. 在方法参数列表部分，使用`(int,..)`表示参数列表以一个`int`类型的参数开头 
10. 在方法参数列表部分，基本数据类型和对应的包装类型是不一样的，切入点表达式中使用 `int` 和实际方法中 `Integer` 是不匹配的 
11. 在方法返回值部分，如果想要明确指定一个返回值类型，那么必须同时写明权限修饰符 例如：`execution(public int ..Service.*(.., int))` 正确 例如：`execution(* int ..Service.*(.., int))` 错误

![image-20220728201648885](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220728201648885.png)

---

### ==AspectJ 注解 AOP 操作==

依赖：在 ioc 所需的依赖的基础上再加入一下依赖

```xml
<!-- spring-aspects会帮我们传递过来aspectjweaver -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>5.3.1</version>
</dependency>
```



#### 操作步骤

1. 创建类，在类里面定义方法

   ```java
   public class User {
       public void add(){
           System.out.println("add()...");
       }
   }
   ```

2. 参加增强类，编写增强方法

   ```java
   //增强类
   public class UserProxy {
       //前置通知
       public void before(){
           System.out.println("before...");
       }
   }
   ```

3. 进行通知的配置

   开启注解扫描

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
   
       <context:component-scan base-package="com.lzy.study715.aopanno"/>
   
   </beans>
   ```

   使用注解创建 User 和 UserProxy

   ```java
   @Component
   public class User {...}
   
   @Component
   public class UserProxy {...}
   ```

   在增强类上面添加注解 `@Aspect`

   ```java
   @Component
   @Aspect//标记当前组件为切面
   public class UserProxy {...}
   ```

   在 Spring 配置文件中开启生成代理对象

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans ...
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="...
               http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <context:component-scan base-package="com.lzy.study715.aopanno"/>
   
       <!-- 配置文件中开启 AspectJ 生成代理对象 -->
       <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
   </beans>
   ```

4. 配置不同类型的通知

   在增强类的里面，在作为通知方法上面添加通知类型注解，使用切入点表达式配置

   ```java
   //增强类
   @Component
   @Aspect
   /*
   	在切面中，需要通过指定的注解将方法标识为通知方法
   */
   public class UserProxy {
       //前置通知，会在被增强方法执行前执行。 public int 可以使用通配符匹配
       @Before(value="execution(* com.lzy.study715.aopanno.User.add(..))")
       public void before(){
           System.out.println("before...");
       }
   
       //后置通知，方法之后执行，不管异常与否都会执行
       @After(value="execution(* com.lzy.study715.aopanno.User.add(..))")
       public void after(){
           System.out.println("after...");
       }
   
       //最终通知，返回值之后执行，有异常不会执行
       @AfterReturning(value="execution(* com.lzy.study715.aopanno.User.add(..))")
       public void afterReturning(){
           System.out.println("afterReturning...");
       }
   
       //异常通知
       @AfterThrowing(value="execution(* com.lzy.study715.aopanno.User.add(..))")
       public void afterThrowing(){
           System.out.println("afterThrowing...");
       }
   
       //环绕通知，被增强方法之前，之后都执行
       @Around(value="execution(* com.lzy.study715.aopanno.User.add(..))")
       public void around(ProceedingJoinPoint point) throws Throwable {
           System.out.println("around before...");
           //被之增强方法
           point.proceed();
   
           System.out.println("around after...");
       }
   }
   ```

5. 测试

   ```java
   @Test
   public void test3(){
       ApplicationContext context
           = new ClassPathXmlApplicationContext("bean1.xml");
       User user = context.getBean("user", User.class);
       user.add();
   }
   ```

   ![](F:\java\spring5\photo\snipaste_20220716_155827.jpg) 异常时：![异常时](F:\java\spring5\photo\snipaste_20220716_155948.jpg)

   

---



 #### 基于注解的公共切入点的抽取

   ```java
   @Component
   @Aspect
   public class UserProxy {
   
       //相同切入点的抽取
       @Pointcut(value="execution(* com.lzy.study715.aopanno.User.add(..))")
       public void point(){}
   	
       //然后在通知的注解处添加该抽取了切入点的方法名称
       @Before(value="point()")
       public void before(){
           System.out.println("before...");
       }
       
       ...
   }
   ```

---



#### 多个增强类对同一个方法增强，设置增强优先级

在增强类上面添加一个注解 `@Order(数字类型值)`，数字类型越小优先级越高

```java
@Component
@Aspect
@Order(1)
public class TestProxy {

    @Before(value="execution(* com.lzy.study715.aopanno.User.add(..))")
    public void before(){
        System.out.println("Test before...");
    }
}
```

```java
@Component
@Aspect
@Order(2)
public class UserProxy {
    
    @Pointcut(value="execution(* com.lzy.study715.aopanno.User.add(..))")
    public void point(){}

    @Before(value="point()")
    public void before(){
        System.out.println("User before...");
    }
}
```

![](F:\java\spring5\photo\snipaste_20220716_161609.jpg)

---

### xml 配置 AOP 操作

1. 创建被增强类，增强类

2. 在 Spring xml配置文件中创建两个类对象

   ```xml
   <bean id="book" class="com.lzy.study715.aopxml.Book"></bean>
   <bean id="bookProxy" class="com.lzy.study715.aopxml.BookProxy"></bean>
   ```

3. 在 Spring xml配置文件中配置切入点

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                   http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
       <!-- 创建对象 -->
       <bean id="book" class="com.lzy.study715.aopxml.Book"></bean>
       <bean id="bookProxy" class="com.lzy.study715.aopxml.BookProxy"></bean>
   
       <!-- 配置 AOP 增强 -->
       <aop:config>
           
           <!-- 配置一个公共切入点 -->
           <aop:pointcut id="point" expression="execution(* com.lzy.study715.aopxml.Book.buy(..))"/>
   
           <!-- 配置切面 -->
           <aop:aspect ref="bookProxy">
               <!-- 配置增强作用在具体的方法上 -->
               <aop:before method="before" pointcut-ref="point"></aop:before>
           </aop:aspect>
           
       </aop:config>
   </beans>
   ```
   
   

### AOP完全注解开发

创建配置类

```java
@Configuration
@ComponentScan(basePackages = {"com.lzy.study715"})
@EnableAspectJAutoProxy(proxyTargetClass = true)
public class ConfigAOP {
}
```

---

# JDBC  Template

​	Spring 框架对 JDBC 进行封装，使用 JDBC  Template 方便实现对数据库的操作。



## **准备工作**	

 1. jar：`mysql-connector-java-5.1.7-bin.jar`,`druid-1.1.9.jar`,`spring-jcl-5.2.6.RELEASE.jar`,`spring-tx-5.2.6.RELEASE.jar`,`spring-orm-5.2.6.RELEASE.jar`，`spring-jdbc-5.2.6.RELEASE.jar`

    ```xml
    <dependencies>
        <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!-- Spring 持久化层支持jar包 -->
        <!-- Spring 在执行持久化层操作、与持久化层技术进行整合过程中，需要使用orm、jdbc、tx三个
    jar包 -->
        <!-- 导入 orm 包就可以通过 Maven 的依赖传递性把其他两个也导入 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!-- Spring 测试相关 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!-- junit测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <!-- MySQL驱动 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.16</version>
        </dependency>
        <!-- 数据源 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.0.31</version>
        </dependency>
    </dependencies>
    ```

 2. 连接池配置：

    ```xml
    <!-- 数据库连接池 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
          destroy-method="close">
        <property name="url" value="jdbc:mysql://192.168.146.128/user_db?characterEncoding=utf8&amp;serverTimezone=UTC&amp;useSSL=FALSE" />
        <property name="username" value="root" />
        <property name="password" value="1234" />
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
    </bean>
    ```

 1. 配置 JDBCTemplate 对象，注入 Datasource

    ```xml
    <!-- JDBCTemplate对象注入 -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <!-- 注入 dataSource-->
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    ```

 2. 创建 service 类，创建 dao 类，在 dao 类注入 JDBCTemplate 对象

    ```xml
    <!-- 组件扫描 -->
    <context:component-scan base-package="com.lzy.jdbcexercise"/>
    ```

    ```java
    @Service
    public class BookService {
        //注入 dao
        @Autowired
        private BookDao bookDao;
    }
    
    @Repository
    public class BookDaoImpl implements BookDao{
        //注入 JdbcTemplate
        @Autowired
        private JdbcTemplate jdbcTemplate;
    }
    ```

---

## JDBC  Template 操作数据库

增删改：update ；查询： query 多个， queryForObject 单个

1. 建表

   ```mysql
   create table t_user(`userid` int primary key auto_increment, `username` varchar(128), `userstatus` varchar(128));
   ```

2. 对应数据表创建 bean

   ```java
   public class UserBean {
       private int userId;
       private String userName;
       private String userStatus;
   	...
   }
   ```

3. 编写 service 和 dao

   在 dao 进行数据库添加操作, 调用==`jdbcTemplate.update(sql, args...);`== 写入 sql 语句

   ```java
   @Repository
   public class UserDaoImpl implements UserDao {
   
       //注入 JdbcTemplate
       @Autowired
       private JdbcTemplate jdbcTemplate;
   
       @Override
       public void add(UserBean user) {
           //1.创建 sql，同理修改删除
           String sql = "insert into t_user values(?,?,?)";
           //2.调用 jdbcTemplate.update()
           int update = jdbcTemplate.update(sql, user.getUserId(), user.getUserName(), user.getUserStatus());
           System.out.println(update);
       }
   }
   ```

4. 测试

   ```java
   @Test
   public void test01(){
       ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
       UserService userService = context.getBean("userService", UserService.class);
       userService.addUser(new UserBean(1, "lzy", "healthy"));
   }
   ```

   ![](F:\java\spring5\photo\snipaste_20220716_180400.jpg)

---

## 查询操作

**查询返回某个值**

```java
//service
public int findCount(){
    return bookDao.selectCount();
}
```

```java
//dao
@Override
public int selectCount() {
    String sql = "select count(*) from t_user";
    Integer cnt = jdbcTemplate.queryForObject(sql, Integer.class);
    return cnt;
}
```

### 查询返回对象

`queryForObject(String sql, RowMapper<T> rowMapper, Object... args)`

1. sql 语句
2. RowMappe 是接口，返回不同值的数据类型，使用这个接口里面的实现类完成数据封装
3. sql 语句值

```java
@Override
public UserBean findUserById(Integer id) {
    String sql = "select * from t_user where userid = ?";
    //BeanPropertyRowMapper<UserBean>(UserBean.class) 泛型指定输出对象类型，参数该对象的类对象
    UserBean userBean = (UserBean) jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<UserBean>(UserBean.class), id)
        return userBean;
}
```

### 查询返回集合

```java
@Override
public List<UserBean> findAll() {
    String sql = "select * from t_user";
    List<UserBean> query = jdbcTemplate.query(sql, new BeanPropertyRowMapper<UserBean>(UserBean.class));
    return query;
}
```

### 实现批量修改

`batchUpdate(String sql, List<Object[]> batchArgs)`:批量更新

```java
@Override
public void batchAddUsers(List<Object[]> batchArgs) {
    String sql = "insert into t_user values(?,?,?)";
    int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
    System.out.println(ints);
}
```

```java
@Test
public void test04(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
    UserService userService = context.getBean("userService", UserService.class);

    List<Object[]> batchArgs = new ArrayList<>();
    Object[] o1 = {3, "java", "a"};
    Object[] o2 = {4,"c++", "b"};
    Object[] o3 = {5, "go", "c"};
    batchArgs.add(o1);
    batchArgs.add(o2);
    batchArgs.add(o3);

    userService.batchAdd(batchArgs);
}
```

# Spring 事务操作

1. 建表

   ```mysql
   create table t_acount(`id` varchar(128) not null primary key, `username` varchar(128), `acount` int);
   ```

2. 创建 service，搭建 dao，完成对象的注入：service 注入 dao， dao 注入 JdbcTemplate，在 JdbcTemplate 注入 DataSource

   ```java
   @Service
   public class UserService {
       //注入 dao
       @Autowired
       private UserDao userDao;
   }
   ```

   ```java
   @Repository
   public class UserDaoImpl implements UserDao{
       @Autowired
       private JdbcTemplate jdbcTemplate;
   }
   ```

   ```xml
   <!-- 数据库连接池 -->
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
         destroy-method="close">
       <property name="url" value="jdbc:mysql://192.168.146.128/user_db?characterEncoding=utf8&amp;serverTimezone=UTC&amp;useSSL=FALSE"/>
       <property name="username" value="root" />
       <property name="password" value="1234" />
       <property name="driverClassName" value="com.mysql.jdbc.Driver" />
   </bean>
   
   <!-- JDBCTemplate对象注入 -->
   <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
       <!-- 注入 dataSource-->
       <property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

3. service 层写业务逻辑；dao 层操作数据库

   一般在 service 层中对 事务 进行 try-catch 没有异常提交事务，捕获到异常回滚，异常抛出

---



## Spring 事务管理

1. 事务一般添加在 JavaEE 三层结构里的 Srevice 层(业务逻辑层)

2. 两种方法：编程式事务管理（自己写 try-catch 中的所有代码）和 声明式事务管理

3. 声明式事务管理：

   基于注解；基于 xml 配置文件

4. 在 Spring 进行声明式事务管理，**底层使用 AOP 原理**

5. 提供一个接口 `PlatformTransactionManager`代表事务管理器，这个接口针对不同的框架提供不同的实现类。

---



## 基于注解实现声明式事务操作

1. 在 Spring 配置文件中配置事务管理器

   ```xml
   <!-- 创建事务管理器 -->
   <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
       <!-- 注入数据源 -->
       <property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

2. 在 Spring 配置文件，开启**事务注解**

   > 引入名称空间 tx
   >
   > ```xml
   > <beans ...
   >     xmlns:tx="http://www.springframework.org/schema/tx"
   >     xsi:schemaLocation="...
   >              http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
   >  ...
   > </beans>
   > ```
   >
   > 开启事务注解
   >
   > ```xml
   > <!-- 开启事务注解 transaction-manager 属性写上配置的事务管理器 -->
   > <!-- 本质是一个 around 通知，通过注解 @Transactional 作用到连接点上-->
   > <tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
   > ```

3. 在 service 类上面，或者 service 类里面的方法上面，添加事务注解 `@Transactional`

   若添加到类上，表示对类里面的所有方法添加事务注解。

   ```java
   @Service
   @Transactional //事务注解，异常会回滚 
   public class UserService {
       @Autowired
       private UserDao userDao;
       public void accountMoney(){
           userDao.updateMoney();
       }
   }
   ```

**`@Transactional`**参数属性配置

![](F:\java\spring5\photo\snipaste_20220718_174316.jpg)

1. `propagation`：事务传播行为，多事务方法直接进行调用过程，如何进行管理

   ![](F:\java\spring5\photo\snipaste_20220718_174923.jpg)

   ```java
   @Service
   @Transactional(propagation = Propagation.REQUIRED) //事务注解
   public class UserService {...}
   ```

2. `ioslation`：隔离级别

   不考虑隔离性会产生三个读的问题：

   脏读：一个未提交的事务读取到另一个未提交事务的数据。

   不可重复读：一个未提交的事务读取到另一个提交事务的修改数据。

   幻读：一个未提交事务读取到另一个事务的添加数据。

   ![](F:\java\spring5\photo\snipaste_20220718_180657.jpg)

   ```java
   @Service
   @Transactional(isolation = Isolation.REPEATABLE_READ) //默认也是可重复读
   public class UserService {...}
   ```

3. `timeout`：超时时间，事务需要在一定时间内提交，若不提交，则会自动回滚；默认值 -1不超时，设置时间单位为 秒。

   ```java
   @Service
   @Transactional(timeout = 10)
   public class UserService {...}
   ```

4. `readOnly`：只读，默认 false，可以查询，添加修改删除。

5. `rollbackFor`：回滚，设置值为异常类型

   设置出现哪些异常进行事务回滚

6. `noRollbackFor`：不回滚

   设置哪些异常不进行的事务进行回滚

**完全注解方式**：配置类的编写

```java
@Configuration
@ComponentScan(basePackages = "com.lzy")
@EnableTransactionManagement
public class TXConfig {
    //参加数据库连接池
    @Bean
    public DruidDataSource getDruidDataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName("com.mysql.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://192.168.146.129/user_db?characterEncoding=utf8");
        dataSource.setUsername("root");
        dataSource.setPassword("1234");

        return dataSource;
    }

    //创建 JdbcTemplate
    @Bean
    //这里参数的含义是，到 ioc 容器中找到 dataSource，按类型注入 dataSource 到 JdbcTemplate
    public JdbcTemplate getJdbcTemplate(DataSource dataSource){
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        //注入 dataSource
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }

    //创建事务管理器
    @Bean
    public DataSourceTransactionManager getDataSourceTransactionManager(DataSource dataSource){
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }
}
```



---

## 基于 xml 实现声明式事务操作

1. 配置事务管理器

   ```xml
   <!-- 创建事务管理器 -->
   <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
       <!-- 注入数据源 -->
       <property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

2. 配置通知

   ```xml
   <!-- 配置通知 -->
   <tx:advice id="txadvice" transaction-manager="transactionManager">
       <!-- 配置事务参数 -->
       <tx:attributes>
           <!-- 指定在哪种规则的方法上面添加事务-->
           <tx:method name="accountMoney" propagation="REQUIRED"/>
       </tx:attributes>
   </tx:advice>
   ```

3. 配置切入点和切面

   ```xml
   <!-- 配置切入点和切面 -->
   <aop:config>
       <!--  配置切入点 -->
       <aop:pointcut id="pt" expression="execution(* com.lzy.study715.service.*(..))"/>
       <!-- 配置切面 -->
       <aop:advisor advice-ref="txadvice" pointcut-ref="pt"/>
   </aop:config>
   ```

   

---

# Spring5框架新功能

1. 整个 Spring5 框架基于 java8，运行时兼容 jdk9

2. Spring5 框架自带类通用的日志封装

   > Spring5 已经移除了 `Log4jConfigListener`，官方建议使用 `Log4j2`

---

## Spring5 整合 Log4j2 日志框架

1. jar ：`log4j-api-2.11.2.jar, log4j-core-2.11.2.jar, log4j-slf4j-impl-2.11.2.jar, slf4j-api-1.7.30 `

2. 创建配置文件 `log4j2.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!--日志级别以及优先级排序: OFF > FATAL > ERROR > WARN > INFO > DEBUG > TRACE > ALL -->
   <!--Configuration后面的status用于设置log4j2自身内部的信息输出，可以不设置，当设置成trace时，可以看到log4j2内部各种详细输出-->
   <configuration status="INFO">
       <!--先定义所有的appender-->
       <appenders>
           <!--输出日志信息到控制台-->
           <console name="Console" target="SYSTEM_OUT">
               <!--控制日志输出的格式-->
               <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
           </console>
       </appenders>
       <!--然后定义logger，只有定义了logger并引入的appender，appender才会生效-->
       <!--root：用于指定项目的根日志，如果没有单独指定Logger，则会使用root作为默认的日志输出-->
       <loggers>
           <root level="info">
               <appender-ref ref="Console"/>
           </root>
       </loggers>
   </configuration>
   ```

3. 该日志框架，配置文件名必须为  `log4j2.xml`，Spring5 自动回去调用

---

## Spring5 核心容器支持`@Nullable`注解

`@Nullable`可以使用在方法上面，属性上面，参数上面，表示方法可以返回为空，属性值可以为空，参数值可以为空。

---

## 支持函数式风格创建对象，交给 sping 管理

函数式风格：`GenericApplicationContext`，`AnnotationConfigApplicationContext`

```java
@Test
public void test03(){
    //1. 创建 GenericApplicationContext 对象
    GenericApplicationContext context = new GenericApplicationContext();
    //2. 调用 context 的方法对非 spring 创建的对象进行注册
    context.refresh();
    context.registerBean(User.class, ()-> new User());
    //3. 获取在 spring 中注册对象,name 属性填写全路径
    User user = (User)context.getBean("com.lzy.jdbcexercise.entity.User");
    System.out.println(user);
}
```

---

## 支持整合 JUnit5

整合 JUnit4：引入 jar `spring-test-5.2.6.RELEASE.jar`

```java
@RunWith(SpringJUnit4ClassRunner.class)//单元测试框架版本
@ContextConfiguration("classpath:bean1.xml")//加载配置文件
public class JTest {
    @Autowired
    private UserService userService;

    @Test
    public void test(){
        userService.accountMoney();
    }
}
```

整合 JUnit5 ：先添加 JUnit5  的 jar

```java
@ExtendWith(SpringExtension.class)
@ContextConfiguration("classpath:bean1.xml")
public class JTest5 {
    @Autowired
    private UserService userService;

    @Test
    public void test1(){
        userService.accountMoney();
    }
}
```

测试的复合注解

```java
@SpringJUnitConfig(locations = "classpath:bean1.xml")
public class JTest5 {
    @Autowired
    private UserService userService;

    @Test
    public void test1(){
        userService.accountMoney();
    }
}
```

---

## ==SpringWebFlux==

学完 springMvc 在看

----

# SpringMVC

MVC 是一种软件架构的思想，将软件按照模型，视图，控制器来划分

**M** ：model，模型层，指工程中的 javaBean，作用是处理数据

> javaBean 分为两类：
>
> 1. 实体类 Bean ：专门存储业务数据
> 2. 业务处理 Bean ：指 Service 或 Dao 对象，专门用于处理业务逻辑和数据访问

**V** ：view 视图层，指工程中的 html 或 jsp 页面，作用是接收请求和响应浏览器

**C** ：controller，控制层，指工程中的 servlet，作用是接收请求和响应浏览器

---



## thymeleaf 

​	thymeleaf 是用来帮助我们做视图渲染(render)的一个技术。在 html 页面上加载 java 内存中的数据，这个过程我们称之为渲染。

依赖：

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring5</artifactId>
    <version>3.0.12.RELEASE</version>
</dependency>
```



## 入门案例

### 1.创建 maven 工程

1. 创建 web 模块

2. 在 pom.xml 中设置打包模式为 war 

   ```xml
   <packaging>war</packaging>
   ```

3. 引入依赖

   ```xml
   <dependencies>
       <!-- SpringMVC -->
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-webmvc</artifactId>
           <version>5.3.1</version>
       </dependency>
       <!-- 日志 -->
       <dependency>
           <groupId>ch.qos.logback</groupId>
           <artifactId>logback-classic</artifactId>
           <version>1.2.3</version>
       </dependency>
       <!-- ServletAPI -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>javax.servlet-api</artifactId>
           <version>3.1.0</version>
           <scope>provided</scope>
       </dependency>
       <!-- Spring5和Thymeleaf整合包 -->
       <dependency>
           <groupId>org.thymeleaf</groupId>
           <artifactId>thymeleaf-spring5</artifactId>
           <version>3.0.12.RELEASE</version>
       </dependency>
   </dependencies>
   ```



### 2.配置 web.xml

注册SpringMVC的前端控制器DispatcherServlet

**默认配置方式**：

​	此配置作用下，SpringMVC的配置文件默认位于WEB-INF下，默认名称为- servlet.xml，例如，以下配置所对应SpringMVC的配置文件位于WEB-INF下，文件名为springMVCservlet.xml

```xml
<!-- 配置SpringMVC的前端控制器，对浏览器发送的请求统一进行处理 -->
c
    <servlet-name>springMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>springMVC</servlet-name>
    <!--
设置springMVC的核心控制器所能处理的请求的请求路径
/所匹配的请求可以是/login或.html或.js或.css方式的请求路径
但是/不能匹配.jsp请求路径的请求
-->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

**扩展配置**：

​	可通过init-param标签设置SpringMVC配置文件的位置和名称，通过load-on-startup标签设置 SpringMVC前端控制器DispatcherServlet的初始化时间

```xml
<!-- 配置SpringMVC的前端控制器，对浏览器发送的请求统一进行处理 -->
<servlet>
    <servlet-name>springMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!-- 通过初始化参数指定SpringMVC配置文件的位置和名称 -->
    <init-param>
        <!-- contextConfigLocation为固定值 -->
        <param-name>contextConfigLocation</param-name>
        <!-- 使用classpath:表示从类路径查找配置文件，例如maven工程中的
src/main/resources -->
        <param-value>classpath:springMVC.xml</param-value>
    </init-param>
    <!--
作为框架的核心组件，在启动过程中有大量的初始化操作要做
而这些操作放在第一次请求时才执行会严重影响访问速度
因此需要通过此标签将启动控制DispatcherServlet的初始化时间提前到服务器启动时
-->
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>springMVC</servlet-name>
    <!--
设置springMVC的核心控制器所能处理的请求的请求路径
/所匹配的请求可以是/login或.html或.js或.css方式的请求路径
但是/不能匹配.jsp请求路径的请求
-->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```



### 3. 创建请求控制器

​	由于前端控制器对浏览器发送的请求进行了统一的处理，但是具体的请求有不同的处理过程，因此需要 创建处理具体请求的类，即请求控制器。

​	请求控制器中每一个处理请求的方法成为控制器方法。

​	因为 SpringMVC 的控制器由一个 POJO（普通的Java类）担任，因此需要通过 @Controller 注解将其标识 为一个控制层组件，交给 Spring 的 IOC 容器管理，此时 SpringMVC 才能够识别控制器的存在

```java
@Controller
public class HelloController {
}
```



### 4. 创建SpringMVC的配置文件

配置 SpringMVC 的前端控制器 DispatcherServlet。是由 SpringMVC 自动完成创建的，所以需要将配置文件放在默认的位置，使用默认名称。

默认位置：WEB-INF 下

默认名称：`<servlet-name>-servlet.xml`，当前即为`SpringMVC-servlet.xml`

```xml
<!-- 自动扫描包 -->
<context:component-scan base-package="com.atguigu.mvc.controller"/>
<!-- 配置Thymeleaf视图解析器 -->
<bean id="viewResolver"
      class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
    <property name="order" value="1"/>
    <property name="characterEncoding" value="UTF-8"/>
    <property name="templateEngine">
        <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
            <property name="templateResolver">
                <bean
                      class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                    <!-- 视图前缀 -->
                    <property name="prefix" value="/WEB-INF/templates/"/>
                    <!-- 视图后缀 -->
                    <property name="suffix" value=".html"/>
                    <property name="templateMode" value="HTML5"/>
                    <property name="characterEncoding" value="UTF-8" />
                </bean>
            </property>
        </bean>
    </property>
</bean>
<!--
处理静态资源，例如html、js、css、jpg
若只设置该标签，则只能访问静态资源，其他请求则无法访问
此时必须设置<mvc:annotation-driven/>解决问题
-->
<mvc:default-servlet-handler/>
<!-- 开启mvc注解驱动 -->
<mvc:annotation-driven>
    <mvc:message-converters>
        <!-- 处理响应中文内容乱码 -->
        <bean
              class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="defaultCharset" value="UTF-8" />
            <property name="supportedMediaTypes">
                <list>
                    <value>text/html</value>
                    <value>application/json</value>
                </list>
            </property>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```



### 5. 测试

实现对首页的访问：在请求控制器中创建处理请求的方法

```java
// @RequestMapping注解：处理请求和控制器方法之间的映射关系
// @RequestMapping注解的value属性可以通过请求地址匹配请求，/表示的当前工程的上下文路径
// localhost:8080/springMVC/
@RequestMapping("/")
public String index() {
    //返回逻辑视图名称
    return "index";
}
```

通过超链接跳转到指定页面：在主页index.html中设置超链接

```xml
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
    <head>
        <meta charset="UTF-8"/>
        <title>首页</title>
    </head>
    <body>
        <h1>首页</h1>
        <!-- 路径若写 "/hello" 不会具有上下文信息 http://localhost:8080/hello
	"@{/hello}" thymeleaf 会补全上下文 http://localhost:8080/SpringMVC/hello
		-->
        <a th:href="@{/hello}">HelloWorld</a><br/>
    </body>
</html>
```

在请求控制器中创建处理请求的方法

```java
@RequestMapping("/hello")
public String HelloWorld() {
    return "target";
}
```



## @RequestMapping 注解

​	`@RequestMapping`注解的作用就是将请求和处理请求的控制器方法关联 起来，建立映射关系。SpringMVC 接收到指定的请求，就会来找到在映射关系中对应的控制器方法来处理这个请求。



### 注解位置

`@RequestMapping`标识一个类：设置映射请求的请求路径的初始信息 

`@RequestMapping`标识一个方法：设置映射请求请求路径的具体信息

```java
@Controller
@RequestMapping("/test")
public class RequestMappingController {

    @RequestMapping("/hello")
    public String hello(){
        return "target";
    }
}
```

```xml
<a th:href="@{/test/hello}">HelloWorld</a><br/>
```



### value 属性值

`@RequestMapping` 注解的value属性通过请求的请求地址匹配请求映射 

`@RequestMapping` 注解的value属性是一个字符串类型的数组，表示该请求映射能够匹配多个请求地址所对应的请求 

`@RequestMapping` 注解的value属性必须设置，至少通过请求地址匹配请求映射

```java
@Controller
public class RequestMappingController {

    @RequestMapping("/hello", "/test")
    public String hello(){
        return "target";
    }
}
```

```xml
<a th:href="@{/hello}">测试@RequestMapping的value属性-->/hello</a><br>
<a th:href="@{/test}">测试@RequestMapping的value属性-->/test</a><br>
```



### method 属性值

`@RequestMapping `注解的 method 属性通过请求的请求方式（get或post）匹配请求映射 。`@RequestMapping` 注解的 method 属性是一个RequestMethod 枚举类型的数组，表示该请求映射能够匹配 多种请求方式的请求。

​	若当前请求的请求地址满足请求映射的value属性，但是请求方式不满足method属性，则浏览器报错 405：Request method 'POST' not supported。

```java
@Controller
@RequestMapping("/test")
public class RequestMappingController {

    @RequestMapping(
        value = "/hello",
        method = {RequestMethod.GET, RequestMethod.POST}
    )
    public String hello(){
        return "target";
    }
}
```



### @RequestMapping 的派生注解

1. 对于处理指定请求方式的控制器方法，SpringMVC中提供了@RequestMapping的派生注解 

   > 处理get请求的映射 @GetMapping 
   >
   > 处理post请求的映射 @PostMapping 
   >
   > 处理put请求的映射 @PutMapping 
   >
   > 处理delete请求的映射 @DeleteMapping

2. 常用的请求方式有get，post，put，delete

   > 但是目前浏览器只支持get和post，若在form表单提交时，为method设置了其他请求方式的字符 串（put或delete），则按照默认的请求方式get处理
   >
   > 若要发送put和delete请求，则需要通过spring提供的过滤器HiddenHttpMethodFilter



### params 属性

`@RequestMapping`注解的 params 属性通过请求的请求参数匹配请求映射 

`@RequestMapping`注解的 params 属性是一个字符串类型的数组，可以通过四种表达式设置请求参数 和请求映射的匹配关系

`param`：要求请求映射所匹配的请求必须携带param请求参数

`!param`：要求请求映射所匹配的请求必须不能携带param请求参数

`param=value`：要求请求映射所匹配的请求必须携带param请求参数且param=value 

`param!=value`：要求请求映射所匹配的请求必须携带param请求参数但是param!=value

```XML
<!-- 参数也可以写为 "@{/test?username=admin&password=123456" -->
<a th:href="@{/test(username='admin',password=123456)">测试@RequestMapping的
params属性-->/test</a><br>
```

```java
@RequestMapping(
    value = {"/testRequestMapping", "/test"},
    method = {RequestMethod.GET, RequestMethod.POST},
    params = {"username","password!=123456"}
)
public String testRequestMapping(){
    return "success";
}
```



### headers属性

`@RequestMapping`注解的headers属性通过请求的请求头信息匹配请求映射 

`@RequestMapping`注解的headers属性是一个字符串类型的数组，可以通过四种表达式设置请求头信 息和请求映射的匹配关系 

`header`：要求请求映射所匹配的请求必须携带header请求头信息 

`!header`：要求请求映射所匹配的请求必须不能携带header请求头信息 

`header=value`：要求请求映射所匹配的请求必须携带header请求头信息且 header=value 

`header!=value`：要求请求映射所匹配的请求必须携带header请求头信息且 header!=value 

​	若当前请求满足@RequestMapping注解的value和method属性，但是不满足headers属性，此时页面 显示404错误，即资源未找到



### SpringMVC支持ant风格的路径

`？`：表示任意的单个字符，不能匹配自己，以为在地址中 ? 是地址和属性设置的分隔符

`*`：表示任意的0个或多个字符 

`**`：表示任意层数的任意目录，注意：在使用`**`时，只能使用/**/xxx的方式



### SpringMVC支持路径中的占位符

原始方式：`/deleteUser?id=1` 

rest方式：`/user/delete/1`

​	SpringMVC路径中的占位符常用于RESTful风格中，当请求路径中将某些数据通过路径的方式传输到服 务器中，就可以在相应的 @RequestMapping 注解的 value 属性中通过占位符 {xxx} 表示传输的数据，再通过 @PathVariable 注解，将占位符所表示的数据赋值给控制器方法的形参

```xml
<a th:href="@{/testRest/1/admin}">测试路径中的占位符-->/testRest</a><br>
```

```java
@RequestMapping("/testRest/{id}/{username}")
public String testRest(@PathVariable("id") String id, @PathVariable("username")
                       String username){
    System.out.println("id:"+id+",username:"+username);
    return "success";
}
//最终输出的内容为-->id:1,username:admin
```





## SpringMVC 获取请求参数



### 1. 通过 servletAPI 获取请求参数

```java
@RequestMapping("/param/servletAPI")
//只需要在控制器的形参中设置 HttpServletRequest 类型的形参，就可以在控制器方法中获取使用 HttpServletRequest 对象获取请求参数， response 同理
public String getParamByServletAPI(HttpServletRequest request){
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    System.out.println("username: " + username + " password: " + password );
    return "target";
}
```

```xml
<form th:action="@{/param/servletAPI}" method="post">
    用户名：<input type="text" name="username"/><br/>
    密码：<input type="password" name="password"/><br/>
    <input type="submit" value="登录"/><br/>
</form>
```



### 通过控制器方法的形参获取请求参数

```java
@RequestMapping("/param")
//只要在控制器的形参位置设置形参，形参的名字需要与请求的参数名字一样
public String getParamByParamname(String username, String password){
    System.out.println("username: " + username + " password: " + password );
    return "target";
}
```

```xml
<form th:action="@{/param}" method="post">
    用户名：<input type="text" name="username"/><br/>
    密码：<input type="password" name="password"/><br/>
    <input type="submit" value="登录"/><br/>
</form>
```

通过 @RequestParam 注解自己建立形参映射

@RequestParam 是将请求参数和控制器方法的形参创建映射关系 

@RequestParam注解一共有三个属性： 

> value：指定为形参赋值的请求参数的参数名 
>
> required：设置是否必须传输此请求参数，默认值为true。设置为true时，则当前请求必须传输value所指定的请求参数，若没有传输该请求参数，且没有设置 defaultValue属性，则页面报错400：Required String parameter 'xxx' is not present；若设置为 false，则当前请求不是必须传输value所指定的请求参数，若没有传输，则注解所标识的形参的值为 null 
>
> defaultValue：不管required属性值为true或false，当value所指定的请求参数没有传输或传输的值为 "" 时，则使用默认值为形参赋值

```java
@RequestMapping("/param")
public String getParamByParamname(@RequestParam("username") String name, @RequestParam("password")String pwd){
    System.out.println("username: " + name + " password: " + pwd );
    return "target";
}
```

​	同理的还有 @RequestHeader : 将请求头信息和控制器方法的形参绑定；@CookieValue：将 cookie 数据和控制器方法的形参绑定。



**通过设置实体类形参获取参数**

​	在控制器方法的形参位置设置实体类型的形参，要保证实体类中的属性名与请求参数的名字一致，就可以通过实体类的形参获取请求参数。

```java
@RequestMapping("/param/pojo")
public String getParamByPojo(User user){
    System.out.println(user);
    return "target";
}
```

```xml
<form th:action="@{/param/pojo}" method="post">
    用户名：<input type="text" name="username"/><br/>
    密码：<input type="password" name="password"/><br/>
    <input type="submit" value="登录"/><br/>
</form>
```



### 解决获取参数的乱码问题

​	使用 SpringMVC 提供的编码过滤器 CharacterEncodingFilter，但必须在 web.xml 中进行配置。

```xml
<!--配置springMVC的编码过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

SpringMVC 中处理编码的过滤器一定要配置到其他过滤器之前，否则无效



## 域对象共享数据



### 使用 StreamAPI 向 request 域对象共享数据

```java
@RequestMapping("/testServlet")
public String testServletAPI(HttpServletRequest request){
    request.setAttribute("testScope", "hello, servletAPI");
    return "target";
}
```



### 使用 ModelAndView 向 request 域共享数据，常用

```java
//使用了 ModelAndView，必须返回 ModelAndView
@RequestMapping("/testModelAndView")
public ModelAndView testModelAndView(){
    /**
	* ModelAndView有Model和View的功能
	* Model主要用于向请求域共享数据
	* View主要用于设置逻辑视图，实现页面跳转
	*/
    ModelAndView mav = new ModelAndView();
    //向请求域共享数据
    mav.addObject("testScope", "hello,ModelAndView");
    //设置视图，实现页面跳转
    mav.setViewName("target");
    return mav;
}
```

跳转至 target 页面使用域中共享数据 `${域对象名}`

```xml
<p th:text="${testScope}"></p>
```



### 使用 Model 向 request 域对象共享数据

```java
@RequestMapping("/testModel")
public String testModel(Model model){
    model.addAttribute("testScope", "hello,Model");
    return "target";
}
```



### 使用 map 向 request 域对象共享数据

```java
@RequestMapping("/testMap")
public String testMap(Map<String, Object> map){
    map.put("testScope", "hello,Map");
    return "success";
}
```



### 使用ModelMap向request域对象共享数据

```java
@RequestMapping("/testModelMap")
public String testModelMap(ModelMap modelMap){
    modelMap.addAttribute("testScope", "hello,ModelMap");
    return "success";
}
```



### 向session域共享数据

```java
@RequestMapping("/testSession")
public String testSession(HttpSession session){
    session.setAttribute("testSessionScope", "hello,session");
    return "success";
}
```

获取

```xml
<p th:text="${session.testSessionScope}"></p>
```



### 向application域共享数据

```java
@RequestMapping("/testApplication")
public String testApplication(HttpSession session){
    ServletContext application = session.getServletContext();
    application.setAttribute("testApplicationScope", "hello,application");
    return "success";
}
```

获取

```xml
<p th:text="${application.testApplicationScope}"></p>
```



## SpringMVC的视图

​	SpringMVC中的视图是View接口，视图的作用渲染数据，将模型Model中的数据展示给用户。

​	SpringMVC视图的种类很多，默认有转发视图和重定向视图 

​	当工程引入jstl的依赖，转发视图会自动转换为JstlView 

​	若使用的视图技术为Thymeleaf，在SpringMVC的配置文件中配置了Thymeleaf的视图解析器，由此视 图解析器解析之后所得到的是ThymeleafView



### ThymeleafView

​	当控制器方法中所设置的视图名称没有任何前缀时，此时的视图名称会被 SpringMVC 配置文件中所配置的视图解析器解析，视图名称拼接视图前缀和视图后缀所得到的最终路径，会通过转发的方式实现跳转。

```java
@RequestMapping("/test/view/thymeleaf")
public String testThymeleaf(){
    return "target";
}
```



### 转发视图

​	SpringMVC中默认的转发视图是InternalResourceView 

​	SpringMVC中创建转发视图的情况： 当控制器方法中所设置的视图名称以`forward:`为前缀时，创建 InternalResourceView 视图，此时的视图名称不会被 SpringMVC 配置文件中所配置的视图解析器解析，而是会将前缀`forward:`去掉，剩余部 分作为最终路径通过转发的方式实现跳转。

```java
@RequestMapping("/testForward")
public String testForward(){
    return "forward:/testHello";
}
```



### 重定向视图

​	SpringMVC 中默认的重定向视图是 RedirectView。

​	当控制器方法中所设置的视图名称以`redirect:`为前缀时，创建 RedirectView 视图，此时的视图名称不会被 SpringMVC 配置文件中所配置的视图解析器解析，而是会将前缀`redirect:`去掉，剩余部分作为最终路径通过重定向的方式实现跳转。

```java
@RequestMapping("/testRedirect")
public String testRedirect(){
    return "redirect:/testHello";
}
```



### 视图控制器view-controller

​	控制器方法中，仅仅用来实现页面跳转，即只需要设置视图名称时，可以将处理器方法使用viewcontroller 标签进行表示

```xml
<!-- 开启 mvc 的注解驱动 -->
<mvc:annotation-driven/>
<!--
path：设置处理的请求地址
view-name：设置请求地址所对应的视图名称
-->
<mvc:view-controller path="/testView" view-name="success"></mvc:view-controller>
```

​	当 SpringMVC 中设置任何一个 view-controller 时，其他控制器中的请求映射将全部失效，此时需要在 SpringMVC 的核心配置文件中设置开启 mvc 注解驱动的标签：`<mvc:annotation-driven/>`



## RESTful

REST 风格：Representational State Transfer，表现层资源状态转移。

1. 资源 ：

   > 资源是一种看待服务器的方式，即，将服务器看作是由很多离散的资源组成。每个资源是服务器上一个 可命名的抽象概念。因为资源是一个抽象的概念，所以它不仅仅能代表服务器文件系统中的一个文件、 数据库中的一张表等等具体的东西，可以将资源设计的要多抽象有多抽象，只要想象力允许而且客户端 应用开发者能够理解。与面向对象设计类似，资源是以名词为核心来组织的，首先关注的是名词。一个 资源可以由一个或多个URI来标识。URI既是资源的名称，也是资源在Web上的地址。对某个资源感兴 趣的客户端应用，可以通过资源的URI与其进行交互。

2. 资源的表述:

   > 资源的表述是一段对于资源在某个特定时刻的状态的描述。可以在客户端-服务器端之间转移（交 换）。资源的表述可以有多种格式，例如HTML/XML/JSON/纯文本/图片/视频/音频等等。资源的表述格 式可以通过协商机制来确定。请求-响应方向的表述通常使用不同的格式。

3. 状态转移:

   >状态转移说的是：在客户端和服务器端之间转移（transfer）代表资源状态的表述。通过转移和操作资 源的表述，来间接实现操作资源的目的。



### RESTful的实现

​	具体说，就是 HTTP 协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。 它们分别对应四种基本操作：GET 用来获取资源，POST 用来新建资源，PUT 用来更新资源，DELETE 用来删除资源。 

​	REST 风格提倡 URL 地址使用统一的风格设计，从前到后各个单词使用斜杠分开，不使用问号键值对方 式携带请求参数，而是将要发送给服务器的数据作为 URL 地址的一部分，以保证整体风格的一致性。

![image-20220730160227294](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220730160227294.png)



### Rest 风格编写查询功能

```xml
<a th:href="@{/user}">查询所有用户信息</a>
<a th:href="@{/user/1}">查询id为1的用户</a>
<form th:action="@{/user}" method="post">
    <input type="submit" value="添加用户信息"/>
</form>
```

```java
@Controller
public class TestRestController {

    @RequestMapping(value = "/user", method = RequestMethod.GET)
    public String getAllUsers(){
        System.out.println("查询所有用户信息-->/user-->get");
        return "target";
    }
    
	//Rest 风格只有值没有键，使用占位符与注解 @PathVariable 和形参绑定
    @RequestMapping(value ="/user/{id}", method = RequestMethod.GET)
    public String getUserById(@PathVariable("id") Integer id){
        System.out.println("根据 id 查询用户信息-->/user/" + id + "-->get");
        return "target";
    }
    
    @RequestMapping( value = "/user", method = RequestMethod.POST)
    public String addUser(){
        System.out.println("添加用户信息-->/user-->post");
        return "target";
    }
}
```

![image-20220731210135872](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220731210135872.png)

#### put 和 delete 请求

​	原先提供的 http 请求只有 get 和 post (浏览器只能实现这两个请求)，若要使用 put， delete 请求需要我们自己**配置过滤器**。

```xml
<!-- 设置处理请求方式的过滤器 -->
<filter>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

​	想要使用这两个请求，在 html 页面中的必须设置请求方式为 **post**，并且在当前请求中需要传输一个参数 `_method` ，设置 **`name="_method"`**，在**`value`**属性中设置**真正的请求方式**。

```xml
<form th:action="@{/user}" method="post">
    <!-- 该参数与用户无关，只是我们用来设置请求方式的，所以最好设置=在隐藏域中 -->
    <input type="hidden" name="_method" value="put"/>
    <input type="submit" value="修改用户信息"/>
</form>    

<form th:action="@{/user}" method="post">
    <input type="hidden" name="_method" value="delete"/>
    <input type="submit" value="删除用户信息"/>
</form>
```

```java
@RequestMapping( value = "/user", method = RequestMethod.PUT)
public String updateUser(){
    System.out.println("修改用户信息-->/user-->put");
    return "target";
}

@RequestMapping( value = "/user", method = RequestMethod.DELETE)
public String deleteUser(){
    System.out.println("删除用户信息-->/user-->put");
    return "target";
}
```

![image-20220731212009216](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220731212009216.png)



## Rest 风格模拟案例

### EmployeeController

```java
@Controller
public class EmployeeController {

    @Autowired
    private EmployeeDao employeeDao;

    @RequestMapping(value = "/employee", method = RequestMethod.GET)
    public String getAllEmployee(Model model){
        //获取员工数据
        Collection<Employee> all = employeeDao.getAll();
        //将所有的员工信息在请求域中共享
        model.addAttribute("all", all);
        //跳转到列表页面
        return "employee_list";
    }

    @RequestMapping(value = "/employee", method = RequestMethod.POST)
    public String addEmployee(Employee employee){
        employeeDao.save(employee);
        //需要重定向到员工列表功能，让用户看到更新后的结果
        return "redirect:/employee";
    }

    @RequestMapping(value = "/employee/{id}", method = RequestMethod.GET)
    public String updateEmployee(@PathVariable("id") Integer id, Model model){
        Employee employee = employeeDao.get(id);
        //将员工信息共享到请求域中
        model.addAttribute("employee", employee);
        return "employee_update";
    }

    @RequestMapping(value = "/employee/{id}", method = RequestMethod.PUT)
    public String putEmployee(Employee employee){
        employeeDao.save(employee);
        return "redirect:/employee";
    }

    @RequestMapping(value = "/employee/{id}", method = RequestMethod.DELETE)
    public String deleteEmployee(@PathVariable("id") Integer id){
        employeeDao.delete(id);
        return "redirect:/employee";
    }
}
```

### employee_list

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>员工列表</title>
</head>
<body>
    <div id="app">
        <table>
            <tr>
                <th colspan="5">员工列表</th>
            </tr>
            <tr>
                <th>id</th>
                <th>lastName</th>
                <th>email</th>
                <th>gender</th>
                <th>options (<a th:href="@{/toAdd}" >add</a>)</th>
            </tr>
            <tr th:each="employee : ${all}">
                <td th:text="${employee.id}"></td>
                <td th:text="${employee.lastName}"></td>
                <td th:text="${employee.email}"></td>
                <td th:text="${employee.gender}"></td>
                <td>
                    <a @click="deleteEmployee()" th:href="@{'/employee/' + ${employee.id}}">delete</a>
                    <a th:href="@{'/employee/' + ${employee.id}}">update</a>
                </td>
            </tr>
        </table>
        <form method="post">
            <input type="hidden" name="_method" value="delete"/>
        </form>
    </div>
	<!-- vue -->
    <script type="text/javascript" th:src="@{/static/js/vue.js}"></script>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app",
            methods:{
                deleteEmployee(){
                    //获取 form 表单
                    var form = document.getElementsByTagName("form")[0];
                    //将超链接的 href 值赋值给 form 表单的 action 属性
                    //event.target 表示当前触发事件的标签
                    form.action = event.target.href;
                    //表单提交
                    form.submit();
                    //阻止超链接的默认行为
                    event.preventDefault();
                }
            }
        });
    </script>
</body>
</html>
```

### employee_add

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>add employee</title>
</head>
<body>
    <form th:action="@{employee}" method="post">
        <table>
            <tr>
                <th colspan="2">add employee</th>
            </tr>
            <tr>
                <td>lastName</td>
                <td>
                    <input type="text" name="lastName">
                </td>
            </tr>
            <tr>
                <td>email</td>
                <td>
                    <input type="text" name="email">
                </td>
            </tr>
            <tr>
                <td>gender</td>
                <td>
                    <input type="radio" name="gender" value="1">male
                    <input type="radio" name="gender" value="0">female
                </td>
            </tr>
            <tr>
                <td colspan="2">
                    <input type="submit" name="add">
                </td>
            </tr>
        </table>
    </form>
</body>
</html>
```

### employee_update

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>employee_update</title>
</head>
<body>
<form th:action="@{employee}" method="post">
    <input type="hidden" name="_method" value="put">
    <input type="hidden" name="id" th:value="${employee.id}">
    <table>
        <tr>
            <th colspan="2">add employee</th>
        </tr>
        <tr>
            <td>lastName</td>
            <td>
                <input type="text" name="lastName" th:value="${employee.lastName}">
            </td>
        </tr>
        <tr>
            <td>email</td>
            <td>
                <input type="text" name="email" th:value="${employee.email}">
            </td>
        </tr>
        <tr>
            <td>gender</td>
            <td>
                <input type="radio" name="gender" value="1" th:field="${employee.gender}">male
                <input type="radio" name="gender" value="0" th:field="${employee.gender}">female
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <input type="submit" name="update">
            </td>
        </tr>
    </table>
</form>
</body>
</html>
```





## SpringMVC 处理 ajax 请求



### axios 格式

```javascript
/*
* axios({
    url:"",//请求路径
    method:"",//请求方式
    params:{},//请求参数 name=value&name=value，
    //参数会被拼接到请求地址后
    //可以通过 request.getParameter() 方式获取
    data:{}//请求参数以 json 格式发送，
    //请求参数会被保存到请求报文的请求体中
	}).then(response=>{
    	console.log(response.data);
	});
 */            
var vue = new Vue({
    el:"#app",
    methods:{
        testAjax(){
            axios.post(
                "/SpringMVC/test/ajax?id=1001",
                {username:"admin", password:"12324"}
            ).then(response=>{
                console.log(response.data);
            });
        }
    }
});
```

处理 ajax 请求

```java
@RequestMapping("/test/ajax")
public void testAjax(Integer id, HttpServletResponse response) throws IOException {
    System.out.println("id: " + id);
    response.getWriter().write("hello, axios");
}
```

<img src="https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220801205713941.png" alt="image-20220801205713941" style="zoom:80%;" /><img src="https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220801205727959.png" alt="image-20220801205727959" style="zoom:80%;" />



### @RequestBody 注解

```java
/**
* @RequestBody ：将请求体中的内容和控制器中的内容进行绑定
*/
@RequestMapping("/test/ajax")
// ajax 请求不能跳转页面，所有返回值为 void
public void testAjax(Integer id, @RequestBody String requestBody, HttpServletResponse response) throws IOException {
    System.out.println("requestBody" + requestBody);
    System.out.println("id: " + id);
    response.getWriter().write("hello, axios");
}
```

![image-20220801210540395](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220801210540395.png)

​	但是这样直接获取的字符串形式并没有意义，仍然需要我们自己去解析。需要将传输的 json 对象转换为我们需要的对象。

引入依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.1</version>
</dependency>
```

开启注解驱动

```xml
<!--开启mvc的注解驱动-->
<mvc:annotation-driven />
```



```javascript
var vue = new Vue({
    el:"#app",
    methods:{
        testRequestBody() {
            axios.post(
                "/SpringMVC/test/requestBody/json",
                {username: "admin", password: "12324"}
            ).then(response => {
                console.log(response.data);
            });
        }
    }
});
```

```java
/**
     * @RequestBody ：将请求体中的内容和控制器中的内容进行绑定
     * 使用 @RequestBody 注解将 json 格式的请求参数转换为 java 对象
     * 1.导入 jackson 的依赖来实现
     * 2.在 SpringMVC 中设置 <mvc:annotation-driven />
     * 3.在处理请求的方法的形参位置，注解设置 json 格式的请求参数要转换的 java 对象，使用 @RequestBody 注解
*/
@RequestMapping("/test/requestBody/json")
public void testRequestBody(@RequestBody User user, HttpServletResponse response) throws IOException {
    System.out.println(user);
    response.getWriter().write("hello, requestBody");
}
```

![image-20220801214113412](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220801214113412.png)

同样对象数据也可以用一个 map 来接收



### @ResponseBody 注解

 	在控制器的方法上添加 @ResponseBody 注解，我们只需要返回 java 对象， json 的序列化会由 SpringMVC 来帮我们完成。

```java
@RequestMapping("/test/responseBody")
/**
     * @ResponseBody 将所标记的控制器方法的返回值作为响应报文的响应体响应到浏览器
     * 使用 @RequestBody 注解响应浏览器 json 格式的数据
     * 1.导入 jackson 的依赖来实现
     * 2.在 SpringMVC 中设置 <mvc:annotation-driven />
     * 3.将需要转换为 json 字符串的 java 对象直接作为控制器的返回值，使用 @ResponseBody 标识方法，就可以将 java 对象返回 json 字符串，并响应到浏览器
     */
@ResponseBody
public User testResponseBody(){
    User user = new User("root", "123");
    return user;
}
```

```javascript
var vue = new Vue({
    el:"#app",
    methods: {                    
        testResponseBody() {
            axios.post("/SpringMVC/test/responseBody").then(response=>{
                console.log(response.data);
            });
        }
    }
});
```

![image-20220801220445052](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220801220445052.png)



### @RestController注解

@RestController 注解是springMVC提供的一个复合注解，标识在控制器的类上，就相当于为类添加了 @Controller 注解，并且为其中的每个方法添加了@ResponseBody 注解



## 文件上传下载的实现



### 文件下载

```java
/**
     * @param session
     * @return ResponseEntity 可以作为控制方法的返回值，表示响应到浏览器的完整响应报文
     * @throws IOException
     */
@RequestMapping("/test/down")
public ResponseEntity<byte[]> testResponseEntity(HttpSession session) throws
    IOException {
    //获取ServletContext对象
    ServletContext servletContext = session.getServletContext();
    //获取服务器中文件的真实路径
    String realPath = servletContext.getRealPath("/static/img/1.jpg");
    //创建输入流
    InputStream is = new FileInputStream(realPath);
    //创建字节数组
    byte[] bytes = new byte[is.available()];
    //将流读到字节数组中
    is.read(bytes);
    //创建HttpHeaders对象设置响应头信息
    MultiValueMap<String, String> headers = new HttpHeaders();
    //设置要下载方式以及下载文件的名字
    headers.add("Content-Disposition", "attachment;filename=1.jpg");
    //设置响应状态码
    HttpStatus statusCode = HttpStatus.OK;
    //创建ResponseEntity对象
    ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(bytes, headers, statusCode);
    //关闭输入流
    is.close();
    return responseEntity;
}
```

 

### 文件下载

```xml
<form th:action="@{/test/up}" method="post" enctype="multipart/form-data">
    头像：<input type="file" name="photo"/><br/>
    <input type="submit" value="上传"/><br/>
</form>
```

依赖

```xml
<!--https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload-->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>
```

SpringMVC.xml 中添加配置

```xml
<!--必须通过文件解析器的解析才能将文件转换为MultipartFile对象-->
<bean id="multipartResolver"      class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
</bean>
```

Controller

```java
/**
* 文件上传的要求：
* 1.form 请求方式必须为 post
* 2.form 表单必须设置属性 enctype="multipart/form-data"
*/
@RequestMapping("/test/up")
public String testUp(MultipartFile photo, HttpSession session) throws
    IOException {
    //获取上传的文件的文件名
    String fileName = photo.getOriginalFilename();
    //处理文件重名问题
    //取出后缀，文件名设置为 UU
    String hzName = fileName.substring(fileName.lastIndexOf("."));
    fileName = UUID.randomUUID().toString() + hzName;
    //获取服务器中photo目录的路径
    ServletContext servletContext = session.getServletContext();
    String photoPath = servletContext.getRealPath("photo");
    //创建 photoPath 对应的文件对象
    File file = new File(photoPath);
    //判断 file 所在的目录是否存在
    if(!file.exists()){
        file.mkdir();
    }
    //最终的上传路径
    String finalPath = photoPath + File.separator + fileName;
    //实现上传功能
    photo.transferTo(new File(finalPath));
    return "target";
}
```



## 拦截器

SpringMVC 中的拦截器用于拦截控制器方法的执行 

SpringMVC 中的拦截器需要实现 HandlerInterceptor 

SpringMVC 的拦截器必须在 SpringMVC 的配置文件中进行配置

```xml
<bean class="com.atguigu.interceptor.FirstInterceptor"></bean>
<ref bean="firstInterceptor"></ref>
<!-- 以上两种配置方式都是对DispatcherServlet所处理的所有的请求进行拦截 -->
<mvc:interceptor>
    <mvc:mapping path="/**"/>
    <mvc:exclude-mapping path="/testRequestEntity"/>
    <ref bean="firstInterceptor"></ref>
</mvc:interceptor>
<!--
以上配置方式可以通过 ref 或 bean 标签设置拦截器，通过mvc:mapping设置需要拦截的请求，通过
mvc:exclude-mapping设置需要排除的请求，即不需要拦截的请求
-->
```



### 拦截器的三个抽象方法 

SpringMVC中的拦截器有三个抽象方法：

> 1. preHandle：控制器方法执行之前执行preHandle()，其boolean类型的返回值表示是否拦截或放行，返 回true为放行，即调用控制器方法；返回false表示拦截，即不调用控制器方法 
> 2. postHandle：控制器方法执行之后执行postHandle() 
> 3. afterCompletion：处理完视图和模型数据，渲染视图完毕之后执行afterCompletion()



### 多个拦截器的执行顺序

①若每个拦截器的 preHandle() 都返回 true 

> 此时多个拦截器的执行顺序和拦截器在 SpringMVC 的配置文件的配置顺序有关： preHandle() 会按照配置的顺序执行，而 postHandle() 和 afterCompletion() 会按照配置的反序执行 

②若某个拦截器的 preHandle() 返回了 false 

> preHandle() 返回 false 和它之前的拦截器的 preHandle() 都会执行，postHandle() 都不执行，返回false 的拦截器之前的拦截器的 afterCompletion() 会执行





## 异常处理器

### 基于配置的异常处理

SpringMVC提供了一个处理控制器方法执行过程中所出现的异常的接口：

> HandlerExceptionResolver 接口，其实现类有：DefaultHandlerExceptionResolver 和 SimpleMappingExceptionResolver

SpringMVC提供了自定义的异常处理器SimpleMappingExceptionResolver，使用方式：

```xml
<bean
      class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <property name="exceptionMappings">
        <props>
            <!--
properties的键表示处理器方法执行过程中出现的异常
properties的值表示若出现指定异常时，设置一个新的视图名称，跳转到指定页面
-->
            <prop key="java.lang.ArithmeticException">error</prop>
        </props>
    </property>
    <!--
exceptionAttribute属性设置一个属性名，将出现的异常信息在请求域中进行共享
-->
    <property name="exceptionAttribute" value="ex"></property>
</bean>
```



### 基于注解的异常处理

```java
//@ControllerAdvice将当前类标识为异常处理的组件
@ControllerAdvice
public class ExceptionController {
    //@ExceptionHandler用于设置所标识方法处理的异常
    @ExceptionHandler(ArithmeticException.class)
    //ex表示当前请求处理中出现的异常对象
    public String handleArithmeticException(Exception ex, Model model){
        model.addAttribute("ex", ex);
        return "error";
    }
}
```



## 完全注解配置 SpringMVC

### 创建初始化类，代替web.xml

​	在 Servlet3.0 环境中，容器会在类路径中查找实现 javax.servlet.ServletContainerInitializer 接口的类， 如果找到的话就用它来配置 Servlet 容器。 Spring 提供了这个接口的实现，名为 SpringServletContainerInitializer ，这个类反过来又会查找实现 WebApplicationInitializer 的类并将配置的任务交给它们来完成。Spring3.2 引入了一个便利的 WebApplicationInitializer 基础实现，名为 AbstractAnnotationConfigDispatcherServletInitializer，当我们的类扩展了 AbstractAnnotationConfigDispatcherServletInitializer 并将其部署到Servlet3.0容器的时候，容器会自动发现它，并用它来配置 Servlet 上下文。

```java
public class WebInit extends
    AbstractAnnotationConfigDispatcherServletInitializer {
    /**
	* 指定spring的配置类
	* @return
	*/
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }
    /**
	* 指定SpringMVC的配置类
	* @return
	*/
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{WebConfig.class};
    }
    /**
	* 指定DispatcherServlet的映射规则，即url-pattern
	* @return
	*/
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
    /**
	* 添加过滤器
	* @return
	*/
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter encodingFilter = new CharacterEncodingFilter();
        encodingFilter.setEncoding("UTF-8");
        encodingFilter.setForceRequestEncoding(true);
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new
            HiddenHttpMethodFilter();
        return new Filter[]{encodingFilter, hiddenHttpMethodFilter};
    }
}
```



### 创建SpringConfig配置类，代替spring的配置文件

```java
@Configuration
public class SpringConfig {
    //ssm整合之后，spring的配置信息写在此类中
}
```



### 创建WebConfig配置类，代替SpringMVC的配置文件

```java
//将类标识为配置类
@Configuration
//扫描组件
@ComponentScan("com.atguigu.mvc.controller")
//开启MVC注解驱动
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
    //使用默认的servlet处理静态资源
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer
configurer) {
        configurer.enable();
    }
    //配置文件上传解析器
    @Bean
    public CommonsMultipartResolver multipartResolver(){
        return new CommonsMultipartResolver();
    }
    //配置拦截器
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        FirstInterceptor firstInterceptor = new FirstInterceptor();
        registry.addInterceptor(firstInterceptor).addPathPatterns("/**");
    }
    //配置视图控制
    /*@Override
public void addViewControllers(ViewControllerRegistry registry) {
registry.addViewController("/").setViewName("index");
}*/
    //配置异常映射
    /*@Override
public void
configureHandlerExceptionResolvers(List<HandlerExceptionResolver> resolvers) {
SimpleMappingExceptionResolver exceptionResolver = new
SimpleMappingExceptionResolver();
Properties prop = new Properties();
prop.setProperty("java.lang.ArithmeticException", "error");
//设置异常映射
exceptionResolver.setExceptionMappings(prop);
//设置共享异常信息的键
exceptionResolver.setExceptionAttribute("ex");
resolvers.add(exceptionResolver);
}*/
    //配置生成模板解析器
    @Bean
    public ITemplateResolver templateResolver() {
        WebApplicationContext webApplicationContext =
            ContextLoader.getCurrentWebApplicationContext();
        // ServletContextTemplateResolver需要一个ServletContext作为构造参数，可通过
        //WebApplicationContext 的方法获得
        ServletContextTemplateResolver templateResolver = new
            ServletContextTemplateResolver(
            webApplicationContext.getServletContext());
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setCharacterEncoding("UTF-8");
        templateResolver.setTemplateMode(TemplateMode.HTML);
        return templateResolver;
    }
    //生成模板引擎并为模板引擎注入模板解析器
    @Bean
    public SpringTemplateEngine templateEngine(ITemplateResolver
templateResolver) {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        return templateEngine;
    }
    //生成视图解析器并未解析器注入模板引擎
    @Bean
    public ViewResolver viewResolver(SpringTemplateEngine templateEngine) {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setCharacterEncoding("UTF-8");
        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }
}
```





## SpringMVC执行流程

### SpringMVC常用组件

- DispatcherServlet：前端控制器，不需要工程师开发，由框架提供。 作用：统一处理请求和响应，整个流程控制的中心，由它调用其它组件处理用户的请求。
- HandlerMapping：处理器映射器，不需要工程师开发，由框架提供。作用：根据请求的url、method等信息查找Handler，即控制器方法。
- Handler：处理器，需要工程师开发。作用：在DispatcherServlet的控制下Handler对具体的用户请求进行处理。
- HandlerAdapter：处理器适配器，不需要工程师开发，由框架提供。 作用：通过HandlerAdapter对处理器（控制器方法）进行执行。
- ViewResolver：视图解析器，不需要工程师开发，由框架提供。作用：进行视图解析，得到相应的视图，例如：ThymeleafView、InternalResourceView、 RedirectView。
- View：视图。作用：将模型数据通过页面展示给用户



### DispatcherServlet初始化过程

​	DispatcherServlet 本质上是一个 Servlet，所以天然的遵循 Servlet 的生命周期。所以宏观上是 Servlet 生命周期来进行调度。

![image-20220802150606621](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220802150606621.png)



①初始化WebApplicationContext：

所在类：org.springframework.web.servlet.FrameworkServlet

```java
protected WebApplicationContext initWebApplicationContext() {
    WebApplicationContext rootContext =
        WebApplicationContextUtils.getWebApplicationContext(getServletContext());
    WebApplicationContext wac = null;
    if (this.webApplicationContext != null) {
        // A context instance was injected at construction time -> use it
        wac = this.webApplicationContext;
        if (wac instanceof ConfigurableWebApplicationContext) {
            ConfigurableWebApplicationContext cwac =
                (ConfigurableWebApplicationContext) wac;
            if (!cwac.isActive()) {
                // The context has not yet been refreshed -> provide services such as
                    // setting the parent context, setting the application context
                    id, etc
                    if (cwac.getParent() == null) {
                        // The context instance was injected without an explicit parent -> set
                            // the root application context (if any; may be null) as the parent
                            cwac.setParent(rootContext);
                    }
                configureAndRefreshWebApplicationContext(cwac);
            }
        }
    }
    if (wac == null) {
        // No context instance was injected at construction time -> see if one
        // has been registered in the servlet context. If one exists, it is
        assumed
            // that the parent context (if any) has already been set and that the
            // user has performed any initialization such as setting the context id
            wac = findWebApplicationContext();
    }
    if (wac == null) {
        // No context instance is defined for this servlet -> create a local one
        // 创建WebApplicationContext
        wac = createWebApplicationContext(rootContext);
    }
    if (!this.refreshEventReceived) {
        // Either the context is not a ConfigurableApplicationContext with
        refresh
            // support or the context injected at construction time had already been
            // refreshed -> trigger initial onRefresh manually here.
            synchronized (this.onRefreshMonitor) {
            // 刷新WebApplicationContext
            onRefresh(wac);
        }
    }
    if (this.publishContext) {
        // Publish the context as a servlet context attribute.
        // 将IOC容器在应用域共享
        String attrName = getServletContextAttributeName();
        getServletContext().setAttribute(attrName, wac);
    }
    return wac;
}
```



②创建WebApplicationContext 所在类：

org.springframework.web.servlet.FrameworkServlet

```java
protected WebApplicationContext createWebApplicationContext(@Nullable
    ApplicationContext parent) {
    Class<?> contextClass = getContextClass();
    if (!ConfigurableWebApplicationContext.class.isAssignableFrom(contextClass))
    {
        throw new ApplicationContextException(
            "Fatal initialization error in servlet with name '" +
            getServletName() +
            "': custom WebApplicationContext class [" + contextClass.getName() +
            "] is not of type ConfigurableWebApplicationContext");
    }
    // 通过反射创建 IOC 容器对象
    ConfigurableWebApplicationContext wac =
        (ConfigurableWebApplicationContext)
        BeanUtils.instantiateClass(contextClass);
    wac.setEnvironment(getEnvironment());
    // 设置父容器
    wac.setParent(parent);
    String configLocation = getContextConfigLocation();
    if (configLocation != null) {
        wac.setConfigLocation(configLocation);
    }
    configureAndRefreshWebApplicationContext(wac);
    return wac;
}
```



③DispatcherServlet初始化策略 

FrameworkServlet创建WebApplicationContext后，刷新容器，调用onRefresh(wac)，此方法在 DispatcherServlet中进行了重写，调用了initStrategies(context)方法，初始化策略，即初始化 DispatcherServlet的各个组件 

所在类：org.springframework.web.servlet.DispatcherServlet

```java
protected void initStrategies(ApplicationContext context) {
    initMultipartResolver(context);
    initLocaleResolver(context);
    initThemeResolver(context);
    initHandlerMappings(context);
    initHandlerAdapters(context);
    initHandlerExceptionResolvers(context);
    initRequestToViewNameTranslator(context);
    initViewResolvers(context);
    initFlashMapManager(context);
}
```



### DispatcherServlet调用组件处理请求

①processRequest()

​	FrameworkServlet重写HttpServlet中的service()和doXxx()，这些方法中调用了 processRequest(request, response) 

​	所在类: org.springframework.web.servlet.FrameworkServlet

```java
protected final void processRequest(HttpServletRequest request,
                                    HttpServletResponse response)
    throws ServletException, IOException {
    long startTime = System.currentTimeMillis();
    Throwable failureCause = null;
    LocaleContext previousLocaleContext =
        LocaleContextHolder.getLocaleContext();
    LocaleContext localeContext = buildLocaleContext(request);
    RequestAttributes previousAttributes =
        RequestContextHolder.getRequestAttributes();
    ServletRequestAttributes requestAttributes = buildRequestAttributes(request,
                                                                        response, previousAttributes);
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);
    asyncManager.registerCallableInterceptor(FrameworkServlet.class.getName(),
                                             new RequestBindingInterceptor());
    initContextHolders(request, localeContext, requestAttributes);
    try {
        // 执行服务，doService()是一个抽象方法，在DispatcherServlet中进行了重写
        doService(request, response);
    }
    catch (ServletException | IOException ex) {
        failureCause = ex;
        throw ex;
    }
    catch (Throwable ex) {
        failureCause = ex;
        throw new NestedServletException("Request processing failed", ex);
    }
    finally {
        resetContextHolders(request, previousLocaleContext, previousAttributes);
        if (requestAttributes != null) {
            requestAttributes.requestCompleted();
        }
        logResult(request, response, failureCause, asyncManager);
        publishRequestHandledEvent(request, response, startTime, failureCause);
    }
}
```



②doService() 

​	所在类：org.springframework.web.servlet.DispatcherServlet

```java
@Override
protected void doService(HttpServletRequest request, HttpServletResponse
                         response) throws Exception {
    logRequest(request);
    // Keep a snapshot of the request attributes in case of an include,
    // to be able to restore the original attributes after the include.
    Map<String, Object> attributesSnapshot = null;
    if (WebUtils.isIncludeRequest(request)) {
        attributesSnapshot = new HashMap<>();
        Enumeration<?> attrNames = request.getAttributeNames();
        while (attrNames.hasMoreElements()) {
            String attrName = (String) attrNames.nextElement();
            if (this.cleanupAfterInclude ||
                attrName.startsWith(DEFAULT_STRATEGIES_PREFIX)) {
                attributesSnapshot.put(attrName,
                                       request.getAttribute(attrName));
            }
        }
    }
    // Make framework objects available to handlers and view objects.
    request.setAttribute(WEB_APPLICATION_CONTEXT_ATTRIBUTE,
                         getWebApplicationContext());
    request.setAttribute(LOCALE_RESOLVER_ATTRIBUTE, this.localeResolver);
    request.setAttribute(THEME_RESOLVER_ATTRIBUTE, this.themeResolver);
    request.setAttribute(THEME_SOURCE_ATTRIBUTE, getThemeSource());
    if (this.flashMapManager != null) {
        FlashMap inputFlashMap = this.flashMapManager.retrieveAndUpdate(request,
                                                                        response);
        if (inputFlashMap != null) {
            request.setAttribute(INPUT_FLASH_MAP_ATTRIBUTE,
                                 Collections.unmodifiableMap(inputFlashMap));
        }
        request.setAttribute(OUTPUT_FLASH_MAP_ATTRIBUTE, new FlashMap());
        request.setAttribute(FLASH_MAP_MANAGER_ATTRIBUTE, this.flashMapManager);
    }
    RequestPath requestPath = null;
    if (this.parseRequestPath &&
        !ServletRequestPathUtils.hasParsedRequestPath(request)) {
        requestPath = ServletRequestPathUtils.parseAndCache(request);
    }
    try {
        // 处理请求和响应
        doDispatch(request, response);
    }
    finally {
        if
            (!WebAsyncUtils.getAsyncManager(request).isConcurrentHandlingStarted()) {
            // Restore the original attribute snapshot, in case of an include.
            if (attributesSnapshot != null) {
                restoreAttributesAfterInclude(request, attributesSnapshot);
            }
        }
        if (requestPath != null) {
            ServletRequestPathUtils.clearParsedRequestPath(request);
        }
    }
}    
```



③doDispatch() 

​	所在类：org.springframework.web.servlet.DispatcherServlet

```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse
                          response) throws Exception {
    HttpServletRequest processedRequest = request;
    HandlerExecutionChain mappedHandler = null;
    boolean multipartRequestParsed = false;
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);
    try {
        ModelAndView mv = null;
        Exception dispatchException = null;
        try {
            processedRequest = checkMultipart(request);
            multipartRequestParsed = (processedRequest != request);
            // Determine handler for the current request.
            /*
			mappedHandler：调用链
			包含handler、interceptorList、interceptorIndex
			handler：浏览器发送的请求所匹配的控制器方法
			interceptorList：处理控制器方法的所有拦截器集合
			interceptorIndex：拦截器索引，控制拦截器afterCompletion()的执行
			*/
            mappedHandler = getHandler(processedRequest);
            if (mappedHandler == null) {
                noHandlerFound(processedRequest, response);
                return;
            }
            // Determine handler adapter for the current request.
            // 通过控制器方法创建相应的处理器适配器，调用所对应的控制器方法
            HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
            // Process last-modified header, if supported by the handler.
            String method = request.getMethod();
            boolean isGet = "GET".equals(method);
            if (isGet || "HEAD".equals(method)) {
                long lastModified = ha.getLastModified(request,
                                                       mappedHandler.getHandler());
                if (new ServletWebRequest(request, response).checkNotModified(lastModified) && isGet) {
                    return;
                }
            }
            // 调用拦截器的postHandle()
            mappedHandler.applyPostHandle(processedRequest, response, mv);
        }
        catch (Exception ex) {
            dispatchException = ex;
        }
        catch (Throwable err) {
            dispatchException = new NestedServletException("Handler dispatch failed", err);
        }
        // 后续处理：处理模型数据和渲染视图
        processDispatchResult(processedRequest, response, mappedHandler, mv,
                              dispatchException);
    }
    catch (Exception ex) {
        triggerAfterCompletion(processedRequest, response, mappedHandler, ex);
    }
    catch (Throwable err) {
        triggerAfterCompletion(processedRequest, response, mappedHandler,
                               new NestedServletException("Handler processing failed", err));
    }
    finally {
        if (asyncManager.isConcurrentHandlingStarted()) {
            // Instead of postHandle and afterCompletion
            if (mappedHandler != null) {
                mappedHandler.applyAfterConcurrentHandlingStarted(processedRequest, response);
            }
        }
        else {
            // Clean up any resources used by a multipart request.
            if (multipartRequestParsed) {
                cleanupMultipart(processedRequest);
            }
        }
    }
}
```



④processDispatchResult()

```java
private void processDispatchResult(HttpServletRequest request,
                                   HttpServletResponse response,@Nullable HandlerExecutionChain
                                   mappedHandler, @Nullable ModelAndView mv,
                                   @Nullable Exception exception) throws
    Exception {
    boolean errorView = false;
    if (exception != null) {
        if (exception instanceof ModelAndViewDefiningException) {
            logger.debug("ModelAndViewDefiningException encountered",
                         exception);
            mv = ((ModelAndViewDefiningException) exception).getModelAndView();
        }
        else {
            Object handler = (mappedHandler != null ? mappedHandler.getHandler()
                              : null);
            mv = processHandlerException(request, response, handler, exception);
            errorView = (mv != null);
        }
    }
    // Did the handler return a view to render?
    if (mv != null && !mv.wasCleared()) {
        // 处理模型数据和渲染视图
        render(mv, request, response);
        if (errorView) {
            WebUtils.clearErrorRequestAttributes(request);
        }
    }
    else {
        if (logger.isTraceEnabled()) {
            logger.trace("No view rendering, null ModelAndView returned.");
        }
    }
    if (WebAsyncUtils.getAsyncManager(request).isConcurrentHandlingStarted()) {
        // Concurrent handling started during a forward
        return;
    }
    if (mappedHandler != null) {
        // Exception (if any) is already handled..
        // 调用拦截器的afterCompletion()
        mappedHandler.triggerAfterCompletion(request, response, null);
    }
}

```



### ==SpringMVC的执行流程==

1) 用户向服务器发送请求，请求被SpringMVC 前端控制器 DispatcherServlet捕获。 

2) DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI），判断请求URI对应的映射：

   > a) 不存在 i. 再判断是否配置了mvc:default-servlet-handler ii. 如果没配置，则控制台报映射查找不到，客户端展示404错误
   >
   > b) 存在则执行下面的流程

3) 根据该URI，调用 HandlerMapping 获得该 Handler 配置的所有相关的对象（包括Handler对象以及 Handler对象对应的拦截器），最后以 HandlerExecutionChain 执行链对象的形式返回。

4) DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter 来执行对应的控制器方法。

5) 如果成功获得HandlerAdapter，此时将开始执行拦截器的preHandler(…)方法【正向】

6) 提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)方法，处理请求。 在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：

   > a) HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定 的响应信息 
   >
   > b) 数据转换：对请求消息进行数据转换。如String转换成Integer、Double等 
   >
   > c) 数据格式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等 
   >
   > d) 数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中

7) Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象。

8) 此时将开始执行拦截器的postHandle(...)方法【逆向】。

9)  根据返回的ModelAndView（此时会判断是否存在异常：如果存在异常，则执行 HandlerExceptionResolver进行异常处理）选择一个适合的ViewResolver进行视图解析，根据Model 和View，来渲染视图。

10) 渲染视图完毕执行拦截器的afterCompletion(…)方法【逆向】。

11) 将渲染结果返回给客户端。

---

# MyBatis

下载地址：[mybatis/mybatis-3: MyBatis SQL mapper framework for Java (github.com)](https://github.com/mybatis/mybatis-3)

**JDBC:** 

- SQL 夹杂在Java代码中耦合度高，导致硬编码内伤 

- 维护不易且实际开发需求中 SQL 有变化，频繁修改的情况多见 

- 代码冗长，开发效率低 

**Hibernate 和 JPA :**

- 操作简便，开发效率高 
- 程序中的长难复杂 SQL 需要绕过框架
- 内部自动生产的 SQL，不容易做特殊优化 
- 基于全映射的全自动框架，大量字段的 POJO 进行部分映射时比较困难。 
- 反射操作太多，导致数据库性能下降

**MyBatis 轻量级**:

- 性能出色 SQL 和 Java 编码分开，功能边界清晰
- Java代码专注业务、SQL语句专注数据 
- 开发效率稍逊于HIbernate，但是完全能够接受

---



## 搭建 MyBatis

### 开发环境

**IDE**：idea 2019.2 

**构建工具**：maven 3.5.4 

**MySQL版本**：MySQL 8 

**MyBatis版本**：MyBatis 3.5.7 

**MySQL不同版本的注意事项** ：

> 1、驱动类driver-class-name :
>
> MySQL 5版本使用jdbc5驱动，驱动类使用：com.mysql.jdbc.Driver 
>
> MySQL 8版本使用jdbc8驱动，驱动类使用：com.mysql.cj.jdbc.Driver 
>
> 2、连接地址url：
>
>  MySQL 5版本的url： jdbc:mysql://localhost:3306/ssm 
>
> MySQL 8版本的url： jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC 
>
> 否则运行测试用例报告如下错误：
>
>  java.sql.SQLException: The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more



### 创建 Mevan 工程准备

1. 打包方式：

   ```xml
   <packaging>jar</packaging>
   ```

2. 引入依赖

   ```xml
   <dependencies>
       <!-- Mybatis核心 -->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.7</version>
       </dependency>
       <!-- junit测试 -->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
           <scope>test</scope>
       </dependency>
       <!-- MySQL驱动 -->
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>8.0.16</version>
       </dependency>
   </dependencies>
   ```

3. 建一个测试样表

   ```sql
   create database ssm;
   use ssm;
   create table t_user(id int not null auto_increment primary key, username varchar(128), password varchar(128), age int, gender char, email varchar(128));
   ```

4. 创建对应的 bean 对象

   ```java
   public class User {
       private Integer id;
       private String username;
       private String password;
       private Integer age;
       private String gender;
       private String email;
   
       public User() {
       }
       
       ...
   }
   ```



### 创建 MyBatis  的核心配置文件

核心配置文件主要用于配置连接数据库的环境以及 MayBatis 的全局配置信息，存放位置是 src/main/resources 目录下。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--设置连接数据库的环境-->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://192.168.146.129:3306/ssm?
serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <!--引入映射文件-->
    <mappers>
        <mapper resource="mappers/UserMapper.xml"/>
    </mappers>
</configuration>
```



### 创建 mapper 接口

mybatis 中的 mapper 接口相当于以前的 dao，区别在于，mapper 仅仅是接口，我们不需要提供实现类。

```java
public interface UserMapper {
    int insertUser();
}
```



### 创建 MyBatis 映射文件

**ORM**：Object Relationship Mapping 对象映射关系

| java 概念 | 数据库概念 |
| --------- | ---------- |
| 类        | 表         |
| 属性      | 字段/列    |
| 对象      | 记录/行    |

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.taro.mybatis.mapper.UserMapper">
    <!--int insertUser();-->
    <insert id="insertUser">
        insert into t_user values(null,'admin','123456',23,'男','12345@qq.com')
    </insert>
</mapper>
```



### 测试

```java
public class MyBatisTest {
    @Test
    public void testInsert() throws IOException {
        //获取核心文件的输入流
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        //获取 SqlSessionFactoryBuilder 对象
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();//工厂模式
        //根据 mybatis 核心文件的输入流 获取 SqlSessionFactory
        SqlSessionFactory factory = sqlSessionFactoryBuilder.build(is);
        //获取 SqlSession sql 的会话对象，是 mybatis 提供的创建数据库的对象
        //可以设置参数为autoCommit: true 即可自动提交
        SqlSession sqlSession = factory.openSession();

        //获取 UserMapper 的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);//代理模式， mybatis 会根据我们编写的映射文件帮我们实现接口创建实例对象
        //调用 mapper 接口中的方法，实现添加用户信息的功能
        int ret = mapper.insertUser();
        //这种方式事务需要手动提交，回滚事务
        sqlSession.commit();
        System.out.println(ret);

        //使用完及时关闭会话
        sqlSession.close();
    }
}
```



### 添加日志功能

maven 的 pom.xml 中添加依赖

```xml
<!-- log4j日志 -->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

在 src/main.resources 中添加 log4j.xml 配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8" />
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS}
%m (%F:%L) \n" />
        </layout>
    </appender>
    <logger name="java.sql">
        <level value="debug" />
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info" />
    </logger>
    <root>
        <level value="debug" />
        <appender-ref ref="STDOUT" />
    </root>
</log4j:configuration>
```



### 抽取创建 SqlSession 的 Util 类

```java
public class SqlSessionUtil {

    public static SqlSession getSqlSession(){
        SqlSession sqlSession = null;
        try {
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
            SqlSessionFactory factory = sqlSessionFactoryBuilder.build(is);
            sqlSession = factory.openSession(true);
        } catch (IOException e) {
            e.printStackTrace();
        }

        return sqlSession;
    }
}
```



### 查询测试

```xml
<!-- User getUserById();-->
<!--	查询映射需要设置属性
        resultType：设置结果类型，即查询的数据要转换的 java 类型
        resultMap：自定义映射，处理一对一或一对多的映射关系
    -->
<select id="getUserById" resultType="com.taro.mybatis.pojo.User">
    select * from t_user where id = 2;
</select>

<!-- getAllUser -->
<select id="getAllUser" resultType="com.taro.mybatis.pojo.User">
    select * from t_user;
</select>
```





## 核心配置文件

**mybatis 核心配置文件中的标签必须按照指定的顺序去配置:** `properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,objectWrapperFactory?,reflectorFactory?,plugins?,environments?,databaseIdProvider?,mappers?`

### environments 标签

```xml
<!--设置连接数据库的环境 default 属性指定默认配置环境 -->
<environments default="development">
    <!--
    	environment：设置一个具体的连接数据库的环境
        属性：id：设置环境的唯一标识，不能重复
    -->
    <environment id="development">
        <!--
        	transactionManager：设置事务管理器
        	type有两个属性值: 1.JDBC原生的事务管理；2.MANAGED 被管理
         -->
        <transactionManager type="JDBC"/>
        <!--
        	dataSource：设置数据源
        	属性：type：POOLED|UNPOOLED|JNDI
             	POOLED 使用数据库连接池，UNPOOLED 不使用连接池，JNDI 使用上下文中的数据源
         -->
        <dataSource type="POOLED">
            <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql://192.168.146.129:3306/ssm?serverTimezone=UTC"/>
            <property name="username" value="root"/>
            <property name="password" value="1234"/>
        </dataSource>
    </environment>
</environments>
```



### properties 

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://192.168.146.129:3306/ssm?serverTimezone=UTC
jdbc.username=root
jdbc.password=1234
```

```xml
<configuration>
    <!-- 引入 properties 配置文件，以后可以使用 ${key} 的方式访问 value-->
    <properties resource="jdbc.properties"/>
   
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!-- 通过 ${key} 来配置 -->
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
  
    <mappers>
        <mapper resource="mappers/UserMapper.xml"/>
    </mappers>
</configuration>
```



### typeAliases

类型别名，注意核心配置中的标签顺序

```xml
<!-- typeAliases：设置类型别名，为某个具体的类型设置一个别名，在 mybatis 的范围内，就可以使用这个别名表示该类型 -->
<typeAliases>
    <!--
		1.type：设置需要起别名的类型；alias：指定设置的别名
		2.若不设置 alias 属性指定别名，当前类型默认拥有别名，即的类名且不区分大小写
	-->
    <typeAlias type="com.taro.mybatis.pojo.User" alias="User"></typeAlias>
    <!-- 3.通过包设置类型别名，指定包下所有的类型将全部拥有默认的别名 -->
    <package name="com.taro.mybatis.pojo"></typeAlias>
</typeAliases>
```



### mappers

```xml
<!-- 方式一：指定映射文件 -->
<mappers>
    <mapper resource="mappers/UserMapper.xml"/>
</mappers>

<!-- 方式二：以包的形式映射文件 -->
<mappers>
    <!-- 
		1.mapper 接口和映射文件所在的包必须一致
		2.mapper 接口的名字和映射文件的名字必须一致
 	-->
    <package name="com.taro.mybatis.mapper"/>
</mappers>
```

![image-20220723205959441](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220723205959441.png)![image-20220723210108338](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220723210108338.png)

注意在资源文件中 `/` 相隔才能创建层级目录



### idea 中核心配置文件，映射文件模板

![image-20220723214046453](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220723214046453.png)

---



## mybatis 获取参数的方式 ${} 和 #{}

${} 本质就是字符串拼接，#{} 的本质就是占位符赋值



### 单个字面量类型的参数

接口

```java
public interface UserMapper {
    User getUserByUsername(String username);
}
```

映射

```xml
<mapper namespace="com.taro.mybatis.mapper.UserMapper">

    <!-- User getUserByUsername(String username); -->
    <select id="getUserByUsername" resultType="User">
        <!-- select * from t_user where username = #{username}; -->
        <!-- 字符串拼接需要添加单引号 -->
        select * from t_user where username = '${username}'
    </select>

</mapper>
```

测试

```java
@Test
public void testGetUserByUsername(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User taro = mapper.getUserByUsername("taro");
    System.out.println(taro);
}
```



### 多个字面量

```java
User checkLogin(String username, String password);
```

```xml
<!-- 错误写法 -->
<!-- User checkLogin(String username, String password); -->
<select id="checkLogin" resultType="User">
    select * from t_user where username = #{username} and password = #{password}
</select>
```

![image-20220724174244879](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724174244879.png)

多个字面量时，mybatis 会将字面量存储在 map 中有两种键的形式 `arg0, arg1 [,...]`，`param1, param2 [,...]`，我们需要在 #{} 或 ${} 中填写键获取参数。

```xml
<!-- User checkLogin(String username, String password); -->
<select id="checkLogin" resultType="User">
    select * from t_user where username = #{arg0} and password = #{arg1}
</select>
```



### 多个字面量，自定义的 map

```java
User checkLoginByMap(Map<String, Object> map);
```

```xml
<!-- User checkLoginByMap(Map<String, Object> map); -->
<select id="checkLoginByMap" resultType="User">
    select * from t_user where username = #{username} and password = #{password}
</select>
```

```java
@Test
public void testCheckLoginByMap(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    Map<String, Object> map = new HashMap(){
        {
            put("username", "taro");
            put("password", "123456");
        }
    };
    User user = mapper.checkLoginByMap(map);
    System.out.println(user);
}
```



### 根据实体类对象获取参数（常用）

对象的属性就相当于键(属性的获取基于 get，set方法)

```java
void insertUser(User user);
```

```xml
<!-- void insertUser(User user);-->
<insert id="insertUser">
    insert into t_user values(null, #{username}, #{password}, #{age}, #{gender}, #{email})
</insert>
```



### 使用注解自定义默认 map 中的键（常用）

**命名参数**，使用`param1, param2 [,...]`做键仍可以取值

```java
User checkLoginByParam(@Param("username") String name, @Param("password") String password);
```

```xml
<!-- User checkLoginByParam(@Param("username") String name, @Param("password") String password); -->
<select id="checkLoginByParam" resultType="User">
    select * from t_user where username = #{username} and password = #{password}
</select>
```





## MyBatis 查询功能

### 查询一个实体类对象

```java
/**
* 根据 id 查询用户信息
* @param id
* @return
*/
User getUserById(@Param("id") Integer id);
```

```xml
<!-- User getUserById(@Param("id") Integer id);-->
<select id="getUserById" resultType="User">
    select * from t_user where id = #{id}
</select>
```

```java
@Test
public void test1(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    User userById = mapper.getUserById(2);
    System.out.println(userById);
}
```



### 查询一个 list 集合

```java
List<User> getAll();
```

```xml
<!-- List<User> getAll();-->
<select id="getAll" resultType="User">
    select * from t_user
</select>
```

```java
@Test
public void test2(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    List<User> all = mapper.getAll();
    System.out.println(all);
}
```



### 查询返回 java 中的常用类型

常用类型以及设置了默认别名

```java
Integer userCount();
```

```xml
<!-- Integer userCount();-->
<select id="userCount" resultType="Integer">
    select count(*) from t_user
</select>
```



### 查询返回 Map

返回 Map 中 属性名为 键，属性值为 值

```java
Map<String, Object> getUserByIdToMap(@Param("id") Integer id);
```

```xml
<!--Map<String, Object> getUserByIdToMap(@Param("id") Integer id);-->
<select id="getUserByIdToMap" resultType="map">
    select * from t_user where id = #{id}
</select>
```

```java
@Test
public void test4(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    Map<String, Object> userByIdToMap = mapper.getUserByIdToMap(2);
    System.out.println(userByIdToMap);
}
```

![image-20220724205938329](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724205938329.png)

多条数据返回多个 Map

方法一：返回 list

```java
List<Map<String, Object>> getAllToMap();
```

```xml
<!--List<Map<String, Object>> getAllToMap();-->
<select id="getAllToMap" resultType="map">
    select * from t_user
</select>
```

```java
@Test
public void test5(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    List<Map<String, Object>> allToMap = mapper.getAllToMap();
    System.out.println(allToMap);
}
```

![image-20220724211250708](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724211250708.png)

方法二：返回一个 Map key 需要我们使用注解 `@MapKey()`指定为某个查询值， value 为整个查询结果的 Map

```java
@MapKey("id")
Map<String, Object> getAllToMap();
```

```java
@Test
public void test5(){
    ...
    Map<String, Object> allToMap = mapper.getAllToMap();
    System.out.println(allToMap);
}
```

![image-20220724211502959](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724211502959.png)



## 特殊  sql 的执行

### 模糊查询

```java
/**
* 通过用户名模糊查询用户信息
* @param like
* @return
*/
List<User> getUserByLike(@Param("like") String like);
```

```java
@Test
public void test1(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    SpecialSQLMapper mapper = sqlSession.getMapper(SpecialSQLMapper.class);
    List<User> users = mapper.getUserByLike("t");
    users.forEach(System.out::println);
}
```

mapper 映射文件的错误写法模糊查询中使用 #{}

```xml
<!--List<User> getUserByLike(@Param("like") String like);-->
<select id="getUserByLike" resultType="User">
    select * from t_user where username like '%#{like}%'
</select>
```

![image-20220724213305461](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724213305461.png)

#{ } 会被 mybatis 解析为占位符，若在字符串中则该占位符并不能被识别，所以此处应该使用 ${ }  `'%${}%'`或者使用双引号包裹 % 去和 #{} 拼接 `"%"#{}"%"`

```xml
<select id="getUserByLike" resultType="User">
    select * from t_user where username like '%${like}%'
</select>
```

![image-20220724215310409](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724215310409.png)

```xml
<!-- 常用 -->
<select id="getUserByLike" resultType="User">
    select * from t_user where username like "%"#{like}"%"
</select>
```

![image-20220724215234086](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724215234086.png)



### 批量删除

```java
void deleteMoreUser(@Param("ids") String ids);
```

仍然要注意 #{} 会替换为占位符并自动添加单引号的问题

```xml
<!--void deleteMoreUser(@Param("ids") String ids);-->
<delete id="deleteMoreUser">
    delete from t_user where id in(${ids});
</delete>
```



### 动态设置表名

```java
List<User> getUserList(@Param("tableName") String tableName);
```

表名不能有单引号

```xml
<!--List<User> getUserList(@Param("tableName") String tableName);-->
<select id="getUserList" resultType="User">
    select * from ${tableName}
</select>
```



### 获取自增主键

```java
/**
* 增加用户信息，并获取自增主键
* @param user
*/
void insertUser(User user);
```

```xml
<!--void insertUser(User user);
        useGeneratedKeys 使用自增的主键
        keyProperty 接收主键值的属性参数，获取的主键值不能作为返回值接收因为增删改的返回值是受影响行数
-->
<insert id="insertUser" useGeneratedKeys="true" keyProperty="id">
    insert into t_user values(null, #{username}, #{password}, #{age}, #{gender}, #{email})
</insert>
```

```java
@Test
public void test4(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    SpecialSQLMapper mapper = sqlSession.getMapper(SpecialSQLMapper.class);
    User user = new User(null, "lzy", "123456", 24, "m", "123@.com");
    mapper.insertUser(user);
    System.out.println("user 获取的 id：" + user.getId());
}
```

![image-20220724222457696](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220724222457696.png)



## 自定义映射 resultMap

### resultMap 处理字段和属性的映射关系

若字段名和实体类中的属性名不一致，则可以通过 resultMap 设置自定义映射。

```mysql
-- 测试样表
use ssm;

create table t_dept(dept_id int not null auto_increment primary key, dept_name varchar(128));

create table t_emp(emp_id int not null auto_increment primary key, emp_name varchar(128), age int, gender char, dept_id int);
```

bean 

```java
//数据库表中的字段名与类中的属性名不一致，如何去获取数据
public class Emp {
    private Integer empId;
    private String empName;
    private Integer age;
    private String gender;
    private Integer deptId;
    ...
}
```

```java
public class Dept {
    private Integer deptId;
    private String deptName;
	...
}
```

mapper 映射

```xml
<!--Emp getEmpByEmpId(@Param("empId") Integer id);-->
<select id="getEmpByEmpId" resultType="Emp">
    select * from t_emp where emp_id = #{empId}
</select>
```

test

```java
@Test
public void test1(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    Emp empByEmpId = mapper.getEmpByEmpId(1);
    System.out.println(empByEmpId);
}
```

![image-20220726143928140](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726143928140.png)

可以看到，数据库表中的字段名与类中的属性名不一致，若不使用 resultMap 处理字段和属性的映射关系，就无法获取对应数据。



**1.朴素解决方法**：直接在 sql 语句中取别名与我们的属性名保持一致

```xml
<!--Emp getEmpByEmpId(@Param("empId") Integer id);-->
<select id="getEmpByEmpId" resultType="Emp">
    select emp_id empId, emp_name empName, dept_id deptId from t_emp where emp_id = #{empId}
</select>
```

![image-20220726144318352](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726144318352.png)



**2.当字段符合 masql 的下划线命名要求，而属性值符合 java 的驼峰命名规则**：可以在 mybatis 的核心配置文件中设置一个全局配置，可以自动将下划线命名映射为驼峰命名。

```xml
<!--Emp getEmpByEmpId(@Param("empId") Integer id);-->
<select id="getEmpByEmpId" resultType="Emp">
    select * from t_emp where emp_id = #{empId}
</select>
```

```xml
<settings>
    <!-- emp_id : empId-->
    <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```

![image-20220726144927509](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726144927509.png)



**自定义映射 resultMap**：

```xml
<resultMap id="empResultMap" type="Emp">
    <!-- id 标签用于设置主键映射 -->
    <id column="emp_id" property="empId"></id>
    <!-- result 标签用于设置普通字段 -->
    <result column="emp_name" property="empName"></result>
    <result column="age" property="age"></result>
    <result column="gender" property="gender"></result>
    <result column="dept_id" property="deptId"></result>
</resultMap>

<!--Emp getEmpByEmpId(@Param("empId") Integer id);-->
<!-- resultMap 属性设置一个对应的 resultMap 标签的 id -->
<select id="getEmpByEmpId" resultMap="empResultMap">
    select * from t_emp where emp_id = #{empId}
</select>
```



### 处理多对一映射关系

```java
//多个员工对应一个部门
public class Emp {
    private Integer empId;
    private String empName;
    private Integer age;
    private String gender;
    private Dept dept;
    ...
}
```

```java
Emp getEmpAndDept(@Param("empId") Integer id);
```

```xml
<!--Emp getEmpAndDept(@Param("empId") Integer id);-->
<select id="getEmpAndDept" resultType="Emp">
    select 
    t_emp.*, t_dept.* 
    from t_emp left join t_dept 
    on t_emp.dept_id = t_dept.dept_id 
    where t_emp.emp_id = #{empId}
</select>
```

![image-20220726151812481](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726151812481.png)

当我们使用 resultType 来接收多对一中的对象时，并不能接收其属性对应的字段。



**方法一：**级联方式处理

```xml
<resultMap id="empAndDeptResultMapper" type="Emp">
    <id column="emp_id" property="empId"></id>
    <result column="emp_name" property="empName"></result>
    <result column="age" property="age"></result>
    <result column="gender" property="gender"></result>

    <result column="dept_id" property="dept.deptId"></result>
    <result column="dept_name" property="dept.deptName"></result>
</resultMap>

<!--Emp getEmpAndDept(@Param("empId") Integer id);-->
<select id="getEmpAndDept" resultMap="empAndDeptResultMapper">
    select t_emp.*, t_dept.* from t_emp left join t_dept on t_emp.dept_id = t_dept.dept_id where t_emp.emp_id = #{empId}
</select>
```

![image-20220726152519081](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726152519081.png)



**方式二：** association 标签

```xml
<resultMap id="empAndDeptResultMapper" type="Emp">
    <id column="emp_id" property="empId"></id>
    <result column="emp_name" property="empName"></result>
    <result column="age" property="age"></result>
    <result column="gender" property="gender"></result>
    <!-- association 处理多对一映射(处理实体类类型的属性)
         javaType ：对应的实体类，已经在 config 中设置过别名
    -->
    <association property="dept" javaType="Dept">
        <id column="dept_id" property="deptId"></id>
        <result column="dept_name" property="deptName"></result>
    </association>
</resultMap>

<!--Emp getEmpAndDept(@Param("empId") Integer id);-->
<select id="getEmpAndDept" resultMap="empAndDeptResultMapper">
    select t_emp.*, t_dept.* from t_emp left join t_dept on t_emp.dept_id = t_dept.dept_id where t_emp.emp_id = #{empId}
</select>
```



**方式三：**分步查询

分步查询优势：可以实现延时加载（懒加载），需要在核心配置文件中设置全局配置信息。

```xml
<settings>
   ...
    <!-- 开启懒加载 -->
    <setting name="lazyLoadingEnable" value="true"/>
    <!-- 按需加载 -->
    <setting name="aggressiveLazyLoading" value="false"/>
</settings>
```

若开启全局延时加载后，某些分步查询需要一次性全部加载，可以在 association 标签中设置 fetchType 标签为 eager

```java
public interface EmpMapper {
    /**
     * 通过分步查询，查询员工以及所对应的部门信息的第一步
     * @param id
     * @return
     */
    Emp getEmpAndDeptStep1(@Param("empId") Integer id);
}
```

```java
//step 2
public interface DeptMapper {
    Dept getDeptByDeptId(@Param("deptId") Integer id);
}

```

dept mapper 映射

```xml
<!--Dept getDeptByDeptId(@Param("deptId") Integer id);-->
<select id="getDeptByDeptId" resultType="Dept">
    select * from t_dept where dept_id = #{deptId}
</select>
```

emp mapper 映射

```xml
    <resultMap id="getEmpAndDeptStepMapper" type="Emp">
        <id column="emp_id" property="empId"></id>
        <result column="emp_name" property="empName"></result>
        <result column="age" property="age"></result>
        <result column="gender" property="gender"></result>
        <!-- select 属性设置的是后续查询调用的接口方法，在由 mybatis 去根据它的 mapper 映射创建代理实现类来实现查询
			column 是我们根据第一次查询为后续查询传入的参数列
        -->
        <association property="dept" fetchType="eager"
                  select="com.taro.mybatis.mapper.DeptMapper.getDeptByDeptId"
                     column="dept_id"></association>
    </resultMap>

    <!--Emp getEmpAndDeptStep1(@Param("empId") Integer id);-->
    <select id="getEmpAndDeptStep1" resultMap="getEmpAndDeptStepMapper">
        select * from t_emp where emp_id = #{empId}
    </select>
```

![image-20220726154849754](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726154849754.png)



### 一对多

Dept 类

```java
public class Dept {
    private Integer deptId;
    private String deptName;
    private List<Emp> emps;
    ...
}
```

```java
/**
* 根据部门 id 查询部门以及部门员工
* @param id
* @return
*/
Dept getDeptAndEmpsByDeptId(@Param("deptId") Integer id);
```



**方式一：**多表联查

```xml
<resultMap id="deptAndEmpsResultMap" type="Dept">
    <id column="dept_id" property="deptId"></id>
    <result column="dept_name" property="deptName"></result>
    <!-- 处理一对多的映射关系，处理集合类型的属性
           ofType 设置集合中的属性类型
       -->
    <collection property="emps" ofType="Emp">
        <id column="emp_id" property="empId"></id>
        <result column="emp_name" property="empName"></result>
        <result column="age" property="age"></result>
        <result column="gender" property="gender"></result>
    </collection>
</resultMap>

<!--Dept getDeptAndEmpsByDeptId(@Param("deptId") Integer id);-->
<select id="getDeptAndEmpsByDeptId" resultMap="deptAndEmpsResultMap">
    select t_emp.*, t_dept.* from t_dept left join t_emp on t_dept.dept_id = t_emp.dept_id where t_dept.dept_id= #{deptId}
</select>
```

![image-20220726162553832](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726162553832.png)



**方式一：**分步查询

```java
public interface DeptMapper {
    /**
     * 分步查询第一步查询部门
     * @param id
     * @return
     */
    Dept getDeptAndEmpsByStep(@Param("deptId") Integer id);
}
```

```java
public interface EmpMapper {
	//step 2
    List<Emp> getEmpsByDeptId(@Param("deptId") Integer id);
}
```

dept mapper 

```xml
<resultMap id="deptAndEmpsByStepResultMap" type="Dept">
    <id column="dept_id" property="deptId"></id>
    <result column="dept_name" property="deptName"></result>
    <collection property="emps"
                select="com.taro.mybatis.mapper.EmpMapper.getEmpsByDeptId"
                column="dept_id"></collection>
</resultMap>

<!--Dept getDeptAndEmpsByStep(@Param("deptId") Integer id);-->
<select id="getDeptAndEmpsByStep"  resultMap="deptAndEmpsByStepResultMap">
    select * from t_dept where dept_id = #{deptId}
</select>
```

emp mapper

```xml
<!--List<Emp> getEmpsByDeptId(@Param("deptId") Integer id);-->
<select id="getEmpsByDeptId" resultType="Emp">
    select * from t_emp where dept_id = #{deptId}
</select>
```

![image-20220726164404399](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726164404399.png)



## 动态 sql

mybatis 动态 sql 技术是一种根据特定的条件动态拼接 sql 语句的功能。



### if  标签

```java
public interface DynamicSQLMapper {
    List<Emp> getEmpByCondition(@Param("emp") Emp emp);
}
```

```xml
<!--List<Emp> getEmpByCondition(@Param("emp") Emp emp);-->
<select id="getEmpByCondition"  resultType="Emp">
    select * from t_emp where 1=1
    <if test="empName != null and empName != '' ">and emp_name = #{empName}</if>
    <if test="age != null and age != '' ">and age = #{age}</if>
    <if test="gender != null and gender != '' ">and gender = #{gender}</if>
</select>
```

if 标签通过 test 属性中的表达式判断标签内容是否有效。



### where 标签

会动态生成 where 关键字，而且会自动去掉拼接语句**前面**多余的 and 关键字（标签内文本后面的 and 不能去除），且没有任何条件满足时，不会生成 where 关键字。

```xml
<!--List<Emp> getEmpByCondition(@Param("emp") Emp emp);-->
<select id="getEmpByCondition"  resultType="Emp">
    select * from t_emp
    <where>
        <if test="empName != null and empName != '' ">and emp_name = #{empName}</if>
        <if test="age != null and age != '' ">and age = #{age}</if>
        <if test="gender != null and gender != '' ">and gender = #{gender}</if>
    </where>
</select>
```



### trim 标签

![image-20220726210617186](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726210617186.png)

prefix:前添加；prefixOverrides:前去除；suffix:后添加；suffixOverrides:后去除。

```xml
<select id="getEmpByCondition"  resultType="Emp">
    select * from t_emp
    <trim prefix="where" suffixOverrides="and" >
        <if test="empName != null and empName != '' "> emp_name = #{empName} and</if>
        <if test="age != null and age != '' "> age = #{age} and</if>
        <if test="gender != null and gender != '' "> gender = #{gender} and</if>
    </trim>
</select>
```



### choose 标签

choose 相当于 switch ，子标签 when 相当于 case，otherwise 相当于 default

```xml
<select id="getEmpByCondition"  resultType="Emp">
    select * from t_emp
    <where>
        <choose>
            <when test="empName != null and empName != '' "> emp_name = #{empName}</when>
            <when test="age != null and age != '' "> age = #{age}</when>
            <when test="gender != null and gender != '' "> gender = #{gender}</when>
        </choose>
    </where>
</select>
```



### ==foreach 标签==

批量操作集合

```java
public interface DynamicSQLMapper {
    /**
     * 通过集合批量操作，List 默认键 list
     */
    void InsertMoreEmps(List<Emp> emnps);
}
```

```xml
<!--void insertMoreEmps(@Param("emps") List<Emp> emnps);-->
<insert id="insertMoreEmps" >
    insert into t_emp values
    <!-- collection：指定集合
             item：指定集合里的项
             separator：拼接分隔符
         -->
    <foreach collection="emps" item="emp" separator=",">
        (null, #{emp.empName}, #{emp.age}, #{emp.gender}, null)
    </foreach>
</insert>
```

![image-20220726213440333](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726213440333.png)

通过数组批量操作

```java
/**
* 使用数组批量操作，数组默认键 array
* @param empIds
*/
void deleteMoreEmps(@Param("empIds") Integer[] empIds);
```

delete 方式一：where  ...  in ( )

```xml
<!--void deleteMoreEmps(@Param("empIds") Integer[] empIds);-->
<delete id="deleteMoreEmps">
    delete from t_emp where emp_id in
    (
    <foreach collection="empIds" item="empId" separator=",">
        #{empId}
    </foreach>
    )
</delete>
```

=>

```xml
<!--void deleteMoreEmps(@Param("empIds") Integer[] empIds);-->
<delete id="deleteMoreEmps">
    delete from t_emp where emp_id in
    <!-- open 拼接语句以什么开始
		close 以什么结尾
		将这循环体包括起来
	-->
    <foreach collection="empIds" item="empId" separator="," open="(" close=")">
        #{empId}
    </foreach>
</delete>
```

方式二：where ... or ...[or ...]

```xml
<delete id="deleteMoreEmps">
    delete from t_emp where
    <foreach collection="empIds" item="empId" separator="or">
        emp_id = #{empId}
    </foreach>
</delete>
```



### sql 标签

通过在 sql 标签内书写 sql 片段，然后再拼接 sql 语句时可以通过 include 标签引入 sql 片段。

```xml
<sql id="empColumns">
    emp_id, emp_name, age, gender, dept_id
</sql>

<!--List<Emp> getEmpByCondition(@Param("emp") Emp emp);-->
<select id="getEmpByCondition"  resultType="Emp">
    select <include refid="empColumns"></include> from t_emp
    <trim prefix="where" suffixOverrides="and" >
        <if test="empName != null and empName != '' ">and emp_name = #{empName}</if>
        <if test="age != null and age != '' ">and age = #{age}</if>
        <if test="gender != null and gender != '' ">and gender = #{gender}</if>
    </trim>
</select>
```



## MyBatis 缓存

### MyBatis的一级缓存

​	一级缓存是 **SqlSession** 级别的，通过同一个 SqlSession 查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问，使一级缓存失效的四种情况： 

1. 不同的 SqlSession 对应不同的一级缓存 
2. 同一个 SqlSession 但是查询条件不同 
3.  同一个 SqlSession 两次查询期间执行了任何一次增删改操作 
4.  同一个 SqlSession 两次查询期间手动清空了缓存 `clearCache()`



### MyBatis的二级缓存

​	二级缓存是 **SqlSessionFactory** 级别，通过同一个 SqlSessionFactory 创建的 SqlSession查询的结果会被缓存；此后若再次执行相同的查询语句，结果就会从缓存中获取。

 二级缓存开启的条件： 

> 1. 在核心配置文件中，设置全局配置属性 cacheEnabled="true"，默认为true，不需要设置
>
> 2. 在映射文件中设置标签 
>
> 3. 二级缓存必须在 SqlSession 关闭或提交之后有效，一级缓存内容才会被保存到二级缓存
>
> 4. 查询的数据所转换的实体类类型必须实现**序列化**的接口 

使二级缓存失效的情况：

> **两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效**



### 二级缓存的相关配置

在 mapper 配置文件中添加的 cache 标签可以设置一些属性：

①eviction属性：缓存回收策略，默认的是 LRU。 

> LRU（Least Recently Used） – 最近最少使用的：移除最长时间不被使用的对象。
>
> FIFO（First in First out） – 先进先出：按对象进入缓存的顺序来移除它们。     
>
> SOFT – 软引用：移除基于垃圾回收器状态和软引用规则的对象。
>
> WEAK – 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象。

②flushInterval属性：刷新间隔，单位毫秒

> 默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用语句时刷新

③size属性：引用数目，正整数 

> 代表缓存最多可以存储多少个对象，太大容易导致内存溢出

④readOnly属性：只读， true/false 

> true：只读缓存；会给所有调用者返回缓存对象的相同实例。因此这些对象不能被修改。这提供了 很重 要的性能优势。 
>
> false：读写缓存；会返回缓存对象的拷贝（通过序列化）。这会慢一些，但是安全，因此默认是 false。



### MyBatis缓存查询的顺序

1. 先查询二级缓存，因为二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用。 
2. 如果二级缓存没有命中，再查询一级缓存 
3. 如果一级缓存也没有命中，则查询数据库 
4. SqlSession关闭之后，一级缓存中的数据会写入二级缓存



### 整合第三方缓存 EHCache

maven 的 pom 配置文件中添加依赖

```xml
<!-- Mybatis EHCache整合包 -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>
<!-- slf4j日志门面的一个具体实现 -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version>
</dependency>
```

创建EHCache的配置文件 ehcache.xml

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
    <!-- 磁盘保存路径 -->
    <diskStore path="D:\atguigu\ehcache"/>
    <defaultCache
                  maxElementsInMemory="1000"
                  maxElementsOnDisk="10000000"
                  eternal="false"
                  overflowToDisk="true"
                  timeToIdleSeconds="120"
                  timeToLiveSeconds="120"
                  diskExpiryThreadIntervalSeconds="120"
                  memoryStoreEvictionPolicy="LRU">
    </defaultCache>
</ehcache>
```

再 mapper 映射文件中设置二级缓存的类型

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

加入 logback 日志

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="true">
    <!-- 指定日志输出的位置 -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <!-- 日志输出的格式 -->
            <!-- 按照顺序分别是： 时间、日志级别、线程名称、打印日志的类、日志主体内容、换行
-->
            <pattern>[%d{HH:mm:ss.SSS}] [%-5level] [%thread] [%logger]
                [%msg]%n</pattern>
        </encoder>
    </appender>
    <!-- 设置全局日志级别。日志级别按顺序分别是： DEBUG、INFO、WARN、ERROR -->
    <!-- 指定任何一个日志级别都只打印当前级别和后面级别的日志。 -->
    <root level="DEBUG">
        <!-- 指定打印日志的appender，这里通过“STDOUT”引用了前面配置的appender -->
        <appender-ref ref="STDOUT" />
    </root>
    <!-- 根据特殊需求指定局部日志级别 -->
    <logger name="com.atguigu.crowd.mapper" level="DEBUG"/>
</configuration>
```



## 逆向工程

正向工程：先创建Java实体类，由框架负责根据实体类生成数据库表。 Hibernate是支持正向工程的。 

逆向工程：先创建数据库表，由框架负责根据数据库表，反向生成如下资源： 

> - Java实体类 
>
> - Mapper接口 
>
> - Mapper映射文件



### 添加依赖

pom.xml

```xml
<!-- 依赖MyBatis核心包 -->
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- log4j日志 -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>
</dependencies>
<!-- 控制Maven在构建过程中相关配置 -->
<build>
    <!-- 构建过程中用到的插件 -->
    <plugins>
        <!-- 具体插件，逆向工程的操作是以构建过程中插件形式出现的 -->
        <plugin>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-maven-plugin</artifactId>
            <version>1.3.0</version>
            <!-- 插件的依赖 -->
            <dependencies>
                <!-- 逆向工程的核心依赖 -->
                <dependency>
                    <groupId>org.mybatis.generator</groupId>
                    <artifactId>mybatis-generator-core</artifactId>
                    <version>1.3.2</version>
                </dependency>
                <!-- MySQL驱动 -->
                <dependency>
                    <groupId>mysql</groupId>
                    <artifactId>mysql-connector-java</artifactId>
                    <version>8.0.16</version>
                </dependency>
            </dependencies>
        </plugin>
    </plugins>
</build>
```



### 创建 mybatis 核心配置文件



### 创建逆向工程的配置文件

​	文件名必须是：generatorConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
"http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <!--
		targetRuntime: 执行生成的逆向工程的版本
		MyBatis3Simple: 生成基本的CRUD（清新简洁版）
		MyBatis3: 生成带条件的CRUD（奢华尊享版）
	-->
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <!-- 数据库的连接信息 -->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://192.168.146.129:3306/ssm?serverTimezone=UTC"
                        userId="root"
                        password="1234">
        </jdbcConnection>
        <!-- javaBean的生成策略-->
        <javaModelGenerator targetPackage="com.taro.mybatis.pojo"
                            targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true" />
            <property name="trimStrings" value="true" />
        </javaModelGenerator>
        <!-- SQL映射文件的生成策略 -->
        <sqlMapGenerator targetPackage="com.taro.mybatis.mapper"
                         targetProject=".\src\main\resources">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>
        <!-- Mapper接口的生成策略 -->
        <javaClientGenerator type="XMLMAPPER"
                             targetPackage="com.taro.mybatis.mapper" targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>
        <!-- 逆向分析的表 -->
        <!-- tableName设置为*号，可以对应所有表，此时不写domainObjectName -->
        <!-- domainObjectName属性指定生成出来的实体类的类名 -->
        <table tableName="t_emp" domainObjectName="Emp"/>
        <table tableName="t_dept" domainObjectName="Dept"/>
    </context>
</generatorConfiguration>
```



### 执行 maven 中 MBG 插件的generate目标

![image-20220726231056663](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220726231056663.png)



### 生成的 QBC 风格的查询

```java
@Test
public void testMBG(){
    try {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new
            SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
        //查询所有数据
        /*List<Emp> list = mapper.selectByExample(null);
list.forEach(emp -> System.out.println(emp));*/
        //根据条件查询
        /*EmpExample example = new EmpExample();
		example.createCriteria().andEmpNameEqualTo("张三").andAgeGreaterThanOrEqualTo(20);
		example.or().andDidIsNotNull();
		List<Emp> list = mapper.selectByExample(example);
		list.forEach(emp -> System.out.println(emp));*/
        											mapper.updateByPrimaryKeySelective(newEmp(1,"admin",22,null, "456@qq.com",
 3));
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```



## 分页插件

pom.xml 中添加依赖

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.2.0</version>
</dependency>
```

在 MyBatis 的核心配置文件中配置插件

```XML
<plugins>
    <!--设置分页插件-->
    <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
</plugins>
```

test

```java
@Test
public void test1(){
    SqlSession sqlSession = SqlSessionUtil.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    //开启分页功能 startPage(pageNum, pageSize );
    Page<Object> pages = PageHelper.startPage(1, 4);
    //无条件查询，相当于 select *
    List<Emp> list = mapper.selectByExample(null);
    //在查询之后，我们可以获取分页相关的所有数据
    PageInfo<Emp> empPageInfo = new PageInfo<>(list, 5);

    list.forEach(System.out::println);
    System.out.println("---------------------------------------------");
    System.out.println(pages);
    System.out.println("---------------------------------------------");
    System.out.println(empPageInfo);
}
```

![image-20220727154824865](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220727154824865.png)





# SSM 整合

## ContextLoaderListener

​	web 工程中 SpringMVC 的 Controller 的实现依赖与 Spring 管理的 Service ，所以 Spring 的 IOC 容器的创建需要在 SpringMVC 的 DispatchServlet 的创建之前实现。所以应该在 SpringMVC 的 listener 或者 filter 的方法中完成创建，filter 我们关注于它的 doFilter 方法，于我们的需求并不符，所以应该在 SpringMVC 的 listener 初始化方法中完成对 Spring 的 IOC 容器的获取，这样在初始化 DispatchServlet 时就能够完成 Controller 里的 Service 的自动装配。

​	Spring 提供了监听器 ContextLoaderListener，实现 ServletContextListener 接口，可监听 ServletContext 的状态，在web服务器的启动，读取 Spring 的配置文件，创建 Spring 的IOC容器。web 应用中必须在web.xml中配置

```xml
<listener>
    <!--
	配置Spring的监听器，在服务器启动时加载Spring的配置文件
	Spring配置文件默认位置和名称：/WEB-INF/applicationContext.xml
	可通过上下文参数自定义Spring配置文件的位置和名称
	-->
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
<!--自定义Spring配置文件的位置和名称-->
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring.xml</param-value>
</context-param>
```



## 准备工作

### 创建Maven Module

### 导入依赖

```xml
<packaging>war</packaging>
<properties>
    <spring.version>5.3.1</spring.version>
</properties>
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!--springmvc-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!-- Mybatis核心 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <!--mybatis和spring的整合包-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.6</version>
    </dependency>
    <!-- 连接池 -->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.0.9</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>
    <!-- log4j日志 -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper -->
    <dependency>
        <groupId>com.github.pagehelper</groupId>
        <artifactId>pagehelper</artifactId>
        <version>5.2.0</version>
    </dependency>
    <!-- 日志 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <!-- ServletAPI -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.12.1</version>
    </dependency>
    <dependency>
        <groupId>commons-fileupload</groupId>
        <artifactId>commons-fileupload</artifactId>
        <version>1.3.1</version>
    </dependency>
    <!-- Spring5和Thymeleaf整合包 -->
    <dependency>
        <groupId>org.thymeleaf</groupId>
        <artifactId>thymeleaf-spring5</artifactId>
        <version>3.0.12.RELEASE</version>
    </dependency>
</dependencies>
```



### 样表创建

```mysql
CREATE TABLE `t_emp` (
    `emp_id` int(11) NOT NULL AUTO_INCREMENT,
    `emp_name` varchar(20) DEFAULT NULL,
    `age` int(11) DEFAULT NULL,
    `sex` char(1) DEFAULT NULL,
    `email` varchar(50) DEFAULT NULL,
    PRIMARY KEY (`emp_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```



### web.xml 完整版配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- 配置 Spring 的编码过滤器 -->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- 配置处理请求方式的过滤器 -->
    <filter>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- SpringMVC 的前端控制器 -->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- SpringMVC 配置文件的自定义位置和名称 -->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!-- 将 DispathcServlet 的初始化时间提前至服务器启动时 -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!-- Spring 的监听器，服务器启动的时加载 Spring 的配置文件 -->
    <listener>
        <!-- 服务器启动时加载 Spring 的配置文件 -->
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!-- 设置 Spring 配置文件的自定义位置和名称 -->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring.xml</param-value>
    </context-param>

</web-app>
```



### SpringMVC 的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 自动扫描包 -->
    <context:component-scan base-package="com.taro.controller"/>
    <!-- 配置Thymeleaf视图解析器 -->
    <bean id="viewResolver"
          class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <property name="order" value="1"/>
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean
                            class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                        <!-- 视图前缀 -->
                        <property name="prefix" value="/WEB-INF/templates/"/>
                        <!-- 视图后缀 -->
                        <property name="suffix" value=".html"/>
                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8" />
                    </bean>
                </property>
            </bean>
        </property>
    </bean>

    <!-- 配置默认的 servlet 处理静态资源
        因为我们自己配置了 SpringMVC 处理自己工程中的所有请求，但是它并不能处理静态资源
        而当我们配置的路径与 tomcat 的 sevlet 默认处理路径冲突时，会以当前项目配置的处理器为准
        所以我们需要 tomcat 的 servlet 来帮我们处理静态资源时，需要为静态资源配置默认的 servlet
    -->
    <mvc:default-servlet-handler />

    <!-- 开启 MVC 的注解驱动 -->
    <mvc:annotation-driven />

    <!-- 配置视图控制器 -->
    <mvc:view-controller path="/" view-name="index" />

    <!--必须通过文件解析器的解析才能将文件转换为MultipartFile对象-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"/>
</beans>
```



### 整合 Spring 配置文件

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://192.168.146.129:3306/ssm?serverTimezone=UTC&rewriteBatchedStatements=true
jdbc.username=root
jdbc.password=1234
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 扫描组件，除了控制层 -->
    <context:component-scan base-package="com.taro">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!-- 引入配置文件 -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!-- 配置数据源 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

</beans>
```



### Spring  整合 MyBatis 配置

在 Spring 配置中完成 MyBatis 的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!-- 扫描组件，除了控制层 -->
    <context:component-scan base-package="com.taro">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!-- 引入配置文件 -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!-- 配置数据源 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <!-- 配置事务管理器 -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>
    <!-- 开启事务的注解驱动 -->
    <tx:annotation-driven transaction-manager="transactionManager"/>

    <!-- 配置 SqlSessionFactoryBean，可以直接在 Spring 的 IOC 中获取 SqlSessionFactory -->
    <bean class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 设置 MyBatis 核心配置文件的路径 -->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <!-- 配置数据源 -->
        <property name="dataSource" ref="dataSource"/>
        <!-- 配置类型别名所对应的包 -->
        <property name="typeAliasesPackage" value="com.taro.pojo"/>
        <!-- 配置映射文件, 一般只有在映射文件的包和 mapper 接口的包不一致时才需要设置 -->
        <!-- <property name="mapperLocations" value="classpath:mappers/*.xml"/> -->
    </bean>

    <!-- 配置 mapper 接口的扫描，可以指定包下所有的 mapper 接口，通过 sqlSession 创建代理实现类对象，并且将这些对象交给 IOC 容器管理，可以直接通过注解自动装配 Mapper 的代理对象 -->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.taro.mapper"/>
    </bean>
</beans>
```

MyBatis 配置文件中只需要完成一些在 Spring 中去配置比较繁琐的剩余部分

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <settings>
        <!-- 将下划线映射为驼峰 -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <!-- 开启懒加载 -->
        <setting name="lazyLoadingEnabled" value="true"/>
        <setting name="aggressiveLazyLoading" value="false"/>
    </settings>

    <plugins>
        <!-- 配置分页插件 -->
        <plugin interceptor="com.github.pagehelper.PageInterceptor"/>
    </plugins>

</configuration>
```



## 查询操作带分页功能

index.html

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8"/>
    <title>首页</title>
</head>
<body>

    <form th:action="@{/emp/page/1}" method="get">
        <input type="submit" value="查询所有员工信息"/>
    </form>
    <hr/>

</body>
</html>
```

employe_page.html

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>员工列表</title>
</head>
<body>
<table>
   <tr>
       <th colspan="6">员工列表</th>
   </tr>
   <tr>
       <th>序号</th>
       <th>员工姓名</th>
       <th>年龄</th>
       <th>性别</th>
       <th>邮箱</th>
       <th>操作</th>
   </tr>
   <tr th:each="emp,status : ${page.list}">
       <td th:text="${status.count}"></td>
       <td th:text="${emp.empName}"></td>
       <td th:text="${emp.age}"></td>
       <td th:text="${emp.sex}"></td>
       <td th:text="${emp.email}"></td>
       <td>
           <a href="">删除</a>
           <a href="">修改</a>
       </td>
   </tr>
</table>
<div style="text-align: center;">
    <a th:if="${page.hasPreviousPage}" th:href="@{/emp/page/1}">首页</a>
    <!-- @{} 里面的路径信息若需要拼接域对象中的数据，需要在地址上加单引号再去拼接 -->
    <a th:if="${page.hasPreviousPage}" th:href="@{'/emp/page/' + ${page.prePage}}">上一页</a>

    <span th:each="num : ${page.navigatepageNums}">
        <a th:if="${page.pageNum == num}" style="color: red" th:href="@{'/emp/page/' + ${num}}" th:text="'[' + ${num} + ']'"></a>
        <a th:if="${page.pageNum != num}" th:href="@{'/emp/page/' + ${num}}" th:text="${num}"></a>
    </span>

    <a th:if="${page.hasNextPage}" th:href="@{'/emp/page/' + ${page.nextPage}}">下一页</a>
    <a th:if="${page.hasNextPage}" th:href="@{'/emp/page/' + ${page.pages}}">末页</a>
</div>
</body>
</html>
```

Controller 

```java
@Controller
public class EmpController {
    @Autowired
    private EmpService empService;

    @RequestMapping(value = "/emp/page/{pageNum}", method = RequestMethod.GET)
    public String getEmpPage(@PathVariable("pageNum") Integer pageNum, Model model){
        //获取员工分页信息
        PageInfo<Emp> page = empService.getEmpPage(pageNum);
        //将分页数据共享到请求域中
        model.addAttribute("page", page);
        return "employee_page";
    }

    @RequestMapping(value = "/emp", method = RequestMethod.GET)
    public String getAllEmps(Model model){
        List<Emp> list = empService.getAllEmps();
        //将员工信息在请求域中共享
        model.addAttribute("list", list);
        //跳转页面
        return "employee_list";
    }
}
```

Service

```java
//接口
public interface EmpService {
    List<Emp> getAllEmps();
    PageInfo<Emp> getEmpPage(Integer pageNum);
}
```

```java
//实现类
@Service
@Transactional
public class EmpServiceImpl implements EmpService {

    @Autowired
    private EmpMapper empMapper;

    @Override
    public List<Emp> getAllEmps() {
        return empMapper.getAllEmps();
    }

    @Override
    public PageInfo<Emp> getEmpPage(Integer pageNum) {
        //开启分页功能
        PageHelper.startPage(pageNum, 4);
        List<Emp> allEmps = empMapper.getAllEmps();
        //分页处理查询结果
        PageInfo<Emp> page = new PageInfo<>(allEmps, 5);
        return page;
    }
}
```

Mapper 接口(dao)

```java
public interface EmpMapper {
    List<Emp> getAllEmps();
}
```

Mybatis 的 mapper 映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.taro.mapper.EmpMapper">
    <!--List<Emp> getAllEmps();-->
    <select id="getAllEmps" resultType="Emp">
        select * from t_emp
    </select>
</mapper>
```

















































