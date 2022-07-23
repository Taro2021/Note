

# html

**B/S 软件结构**：javaSE中 c/s结构 client/server ; javaEE项目 b/s browser（浏览器）, server

**网页的组成**：

- 内容(结构)，在页面中可以看到的数据。一般使用 html 技术实现
- 表现，指的是内容在页面上的展现形式。一般使用 css 技术实现
- 行为，指的是页面中的元素与输入设备的交互响应。一般使用 javascript 实现

**简介**：

**html**：Hyper Text Markup Language 超文本标记语言

通过在文本文件中添加标记符，可以告诉浏览器如何显示其中内容

---

## 创建

1. 创建一个 web 工程（静态的）
2. 在工程下创建 html 页面

## 书写规范

```html
<!DOCTYPE html><!-- 约束，声明 -->
<html lang="en"><!-- html标签表示html的开始， lang="en" 表示支持英文，html标签一般分为两部分：head 和 body -->
<head><!--表示头部信息，一般包含三部分内容，title标签，css样式，js代码 -->
    <meta charset="UTF-8"><!-- 表示当前页面使用 utf-8 字符集 -->
    <title>Title</title><!-- 表示标题 -->
</head><!-- 表示头部信息的结束-->
<body><!-- 主体内容的开始 -->
    hello
</body><!-- 主体内容的结束 -->
</html><!-- html标签表示html的结束-->
```

## 标签

1. 标签格式：`<标签名>封装的数据</标签名>`
2. 标签对大小写不敏感
3. 标签拥有自己的属性
   - 基本属性：例背景颜色：`bgcolor="red"`
   - 事件属性：例点击事件的响应：`onclick="alert('hello!');"`
4. 标签又分为单标签，双标签
   - 单标签：`<标签名/>`自结束，常用单标签: 换行 `<br/>`，水平线`<hr/>`
   - 双标签格式：`<标签名>封装的数据</标签名>`

**语法**

```html
<!DOCTYPE html>
<html lang="zh_CN">
<head>
    <meta charset="UTF-8">
    <title>标签语法</title>
</head>
<body>
    <!-- 标签不能交叉嵌套 -->
    正确：<div><span>hello,world</span></div>
    错误：<!-- <div><span>hello,world</div></span> -->
    <hr/>
    
    <!-- 标签必须正确关闭-->
    正确：<div>hello,world</div>
    错误：<!-- <div>hello,world -->
    <hr/>
    
    <!-- 单标签必须带上结束符-->
    正确：<br/>
    错误：<!-- <br> -->
    <hr/>
    
    <!-- 属性必须有值，属性值必须加双引号-->
    正确：<font color="blue">helloworld</font>
    错误：<!-- <font color=blue>helloworld</font> -->
    <hr/>
    <!-- 注释不能嵌套 -->
</body>
</html>
```



**font 标签**：字体标签，可以用来通过属性 face,color,size,来修改文本的字体，颜色，大小

**常用的特殊字符**：`<` => `&lt;`  ， `>`=> `&gt;`，空格 => `&nbsp`

**标题标签**

```html
<h1>标题1</h1>
<h2>标题2</h2>
<h3>标题3</h3>
<h4>标题4</h4>
<h5>标题5</h5>
<h6>标题6</h6>
```

==超链接==

```html
<a href="http://www.baidu.com">百度</a>
<a href="http://www.baidu.com" target="_self">当前窗口跳转至百度</a>
<a href="http://www.baidu.com" target="_blank">新窗口跳转至百度</a>
```

**列表标签**

```html
<!-- 无序列表，没有序号 type 能够修改列表项前面的符号-->
<ul type="none">
    <!-- li 是列表项 -->
    <li>tony</li>
    <li>mark</li>
    <li>lily</li>
    <li>tom</li>
</ul>
<!-- 有序列表 -->
<ol>
    <li>tony</li>
    <li>mark</li>
    <li>lily</li>
    <li>tom</li>
</ol>
```

**img标签**

```html
<!-- img标签是图片标签，用来显示图片，src 属性设置图片路径
	web 中路径分为相对路劲和绝对路径
	相对路径：
			.  表示当前文件所在的目录
			.. 表示当前文件所在的上一级目录
			文件名  表示当前文件所在目录的文件，相当于 ./文件名
	绝对路径：
			格式是：http://ip:port/工程名/资源路径
	属性 ：width，height， border边框，alt(设置当指定图片路径找不到时显示内容)
-->
<img src="../imgs/1.jpg" width="200" height="200" border="1" alt="图片未找到"/>
```

==表格标签==

```html
<!-- table 表格标签 
	border 设置表格边框
	width 设置表格宽度
	height 设置表格高度
	align 设置表格相对页面的对齐方式
	cellspacing 设置单元格间距
-->
<table border="1" width="100" heught=""10>
    <!-- 单元格 
	tr 是行标签
	th 是表头标签
	td 是单元格标签
		align 设置单元格文本的对齐方式
		colspan 设置跨列
		rowspan 设置跨行
	b 是加粗标签
	-->
    <tr>
        <td align="center" colspan="2" ><b>1.1</b></td>
        <td rowspan="2">1.2</td>
    </tr>
    <tr>
        <td>2.1</td>
        <td>2.2</td>
    </tr>
</table>
```

**ifame框架标签**

```html
<!-- iframe标签可以在页面上开辟一个小区域显示一个单独页面
	iframe 和 a 标签组合使用的步骤：
		1.在 iframe 标签中使用 name 属性定义一个名称
		2.在 a 标签的 target 属性上设置 iframe 的 name 的属性值
		可以将内容显示到 iframe 页面上
-->
<iframe src="test.html" width="500" height="400" name="abc"></iframe>
<br/>
<ul>
    <li><a href="http://www.baidu.com" target="abc">baidu</a></li>
</ul>
```

==表单标签==

```html
<!-- form 标签就是表单
		input type="text" 是文本输入框 value 设置默认显示内容
		input type="password" 密码输入框
		input tyoe="radio" 单选框 name 属性可以对其进行分组，组内只能单选checked="checked" 表示默认选中
		input type="checkbox" 多选框
		input type="reset" 重置按钮 value 可以更改按钮上文本
		input type="submit" 提交按钮 value 可以更改按钮上文本
		input type="file" 是文件上传域
		input type="hidden" 隐藏域，发送某些学习，不需要用户参与，可以使用隐藏域隐藏信息

		select 下拉列表框
			option 下拉列表的选项 select="selected" 设置默认选中
		textarea 表示多行文本输入框 rows 行数 cols 列数，起始标签和结束标签之间可以填入默认值	
-->
<form>
    用户名称：<input type="text" value="默认值"/><br/>
    用户密码：<input type="password"/><br/>
    性别：<input type="radio" name="sex">男<input type="radio" name="sex" checked="checked">女<br/>
    兴趣爱好：<input type="checkbox"/>Java<input type="checkbox"/>JavaScript<input type="checkbox"/>Golang<br/>
    国籍：<select>
    	<option>--请选择国籍--</option>
     	<option select="selected">中国</option>
    	<option>兔兔</option>
    	<option>神神</option>
    </select><br/>
    自我评价：<textarea rows="10" cols="20">默认值</textarea><br/>
    <input type="reset" value="重置"/>
    <input type="submit"/>
    <input type="file"/><br/>   
</form>
```

表单+表格

```html
<!--
	form 标签是表单标签
		action 属性设置提交的服务器地址
		method 属性设置提交的发送 get(默认值) 或 post

	表单提交时，数据没有发送给服务器的三种情况
		1. 表单没有 name 属性值
		2. 单选，复选，都需要添加 value 属性，以便发送给服务器
		3. 表单项不在提交的 form 标签中
	
	get 请求的特点是：
		1. 浏览器地址栏中的地址是：action属性+[?+请求参数...]
			请求参数的格式是：name=value[&name=value...]
		2.不安全
		3.有数据长度限制

	post 请求的特点：
		1.浏览器地址栏中只有 action 属性
		2.相对于 get 请求安全
		3.理论上没有数据长度限制
-->
<form action="http://www.baidu.com" method="get">
    <input type="hidden" name="action" value="login"/>
    <h1 align="center">用户登录</h1>
    <table align="center">
        <tr>
            <td>用户名称：</td>
        	<td><input type="text" value="默认值" name="usrname" /></td>
        </tr>
         <tr>
            <td>用户密码：</td>
        	<td><input type="password" name="usrpwd" value="abc"/></td>
        </tr>
         <tr>
            <td>性别：</td>
        	<td><input type="radio" name="sex" value="boy">男<input type="radio" name="sex" checked="checked" value="girl">女</td>
        </tr>
         <tr>
            <td>兴趣爱好：</td>
        	<td><input type="checkbox" name="hobby" value="java"/>Java<input type="checkbox" name="hobby" value="javascript"/>JavaScript<input type="checkbox" name="hobby" value="golang"/>Golang</td>
        </tr>
         <tr>
            <td>国籍：</td>
        	<td><select name="country">
                <option value="none">--请选择国籍--</option>
                <option select="selected" value="cn">中国</option>
                <option value="tt">兔兔</option>
                <option value="ss">神神</option>
    </select></td>
        </tr>
        <tr>
            <td><input type="reset" value="重置"/></td>
            <td><input type="submit"/></td>
        </tr>
    </table>
</form>
```

**其它标签**

```html
<!-- div, span, p 标签
	div 标签默认独占一行
	span 标签长度是封装数据的长度
	p 标签默认会在段落的上方和下方空出一行来
-->
<div>div标签1</div>
<div>div标签2</div>
<span>span标签1</span>
<span>span标签2</span>
<p>p段落标签1</p>
<p>p段落标签2</p>
```

---

# CSS

CSS 是 层叠样式表单。用于增强控制网页样式，并允许将样式信息与网页内容分离的一种标记性语言。

**语法规则**

```css
选择器{
    属性:值;
}
```



**css与html结合**

1. **方式一**

> 在标签的`style`属性上设置`key:value [value...];`修改样式
>
> 缺点：若标签太多了，样式多了，代码量非常大；可读性差；css 代码没有什么复用性可言

2. **方式二**

   > 在`head`标签中，使用`style`标签来定义各种自己需要的 css 样式
   >
   > 缺点：只能在一个页面内复用该 css 代码，维护起来不方便，实际项目中的页面会有很多

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- style标签专门用来定义css样式代码-->
    <style type="text/css" >
        /* 需求：分别定义两个 div span 标签，修改样式为：边框1像素，实线，天蓝色*/
        div{
            border: 1px solid skyblue;
        }
        span{
            border: 1px solid skyblue;
        }
    </style>
</head>
<body>
    <div>div标签1</div>
    <div>div标签2</div>
    <span>span标签1</span>
    <span>span标签2</span>
   
</body>
</html>
```

3. **方式三**

   > 把 css 样式写成一个单独的 css 文件，通过 `link`标签引入即可复用
   >
   > `<link rel="stylesheet" type="text/css" href="./styles.css">`

```css
/*styles.css*/
div{
    border: 1px solid skyblue;
    color: deepskyblue;
    font-size: 12px;/*字体大小*/
}
span{
    border: 1px solid skyblue;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- link标签专门用来引入 css 文件 -->
    <link rel="stylesheet" type="text/css" href="./styles.css">
</head>
<body>
    <div>div标签1</div>
    <div>div标签2</div>
    <span>span标签1</span>
    <span>span标签2</span>
</body>
</html>
```

**id选择器** :可以让我们通过 id 选择性的去修改属性值，id 唯一不能重复

```css
/* #id{} */
#101{
    border: 1px solid skyblue;
    color: deepskyblue;
    font-size: 12px;/*字体大小*/
}
#102{
    border: 1px solid red;
    color: red;
    font-size: 12px;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- link标签专门用来引入 css 文件 -->
    <link rel="stylesheet" type="text/css" href="./styles.css">
</head>
<body>
    <div id="101">div标签1</div>
    <div id="102">div标签2</div>
</body>
</html>
```

**类型选择器**：class 类型选择器，可以通过 class 属性有效的选择性的去使用这个样式，

```css
/* .class{} */
.class01{
    border: 1px solid skyblue;
    color: deepskyblue;
    font-size: 12px;/*字体大小*/
}
.class02{
    border: 1px solid red;
    color: red;
    font-size: 12px;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- link标签专门用来引入 css 文件 -->
    <link rel="stylesheet" type="text/css" href="./styles.css">
</head>
<body>
    <div class="class01">div标签1</div>
    <div class="class02">div标签2</div>
</body>
</html>
```

**组合选择器**：选择器1[,选择器2，...]{ }

---

# JavaScript

**js 是弱类型，java 是强类型**：

> 弱类型就是类型可变
>
> 强类型，就是定义变量的时候，类型已经确定，而且不可变

**js 特点**：交互性，安全性，跨平台性(通过浏览器实现)

## JavaScript结合html

方式一

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>hello</title>
    <!-- 第一种方式：在 head 或 body 标签中，使用 script 标签来写 javascript 代码-->
    <script type="text/javascript">
        //alert()是 javascript提供的一个警告框函数
        //它可以接收 任意类型的参数，这个参数就是警告框的提示信息
        alert("hello, javascript!");
    </script>
</head>
<body>

</body>
</html>
```

方式二

```javascript
//js01.js
alert("hello, javascript");
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>hello</title>
    <!--
        使用 script 标签引入外部的 js 文件来执行
			src 属性专门用来引入 js 文件，可以是相对路径也可以是绝对路径
		script 可以用来定义 js 代码，也可以引入 js 文件，一个标签只能实现一个功能
    -->
    <script type="text/javascript" src="js01.js"/>
</head>
<body>

</body>
</html>
```

## js 的变量

number(int, short, float,..)，string，object， boolean，function

**js 变量的特殊值**：

1. `undifined`未定义
2. `null`
3. `NAN` not  a number 非数字

```javascript
var i;
i = 1;
alert(typeof (i));
i = "adc";   
alert(typeof (i));
var a = 1;
alert(i * a);//NAN
```

## 关系运算符

等于 ：`==` 就是简单的字面值比较

全等于：`===`除了比较字面值外，还会比较两个数据的类型

## js 的数组

```javascript
var arrName = []; //定义一个空数组，底层会自动扩容，为赋值空间 undefined
var arrName1 = [1,"abc",true]
//数组遍历
for(var i = 0; i < arrName1.length; i ++){
    alert(arrName1[i]);
}
```

## 函数的定义

方式一

```javascript
//使用function 关键字
function func() {
    alert("无参函数被调用了")
}

//调用 才会执行
func();

//有参函数
function func1(a, b){
    alert("有参函数被调用 a="+ a +" b=" + b);
    return a + b;
}

var sum = func1(1, 2);
```

方式二

```go
var func = function (){ 
    alert("无参函数");
};

func();

var func1 = function(a, b){
    alert("有参函数");
    return a + b;
}

alert(func1(1, 2));
```

js 中没有函数的重载

**函数的 arguments 隐形参数**

```javascript
var func = function (){ 
    alert(arguments.length);//可以看隐藏参数数组的长度
    for(var i = 0; i < arguments.length; i++){
        alert(arguments[i]);
    }
    alert("无参函数");
};

func(1, 2);
```

## js 自定义对象

```javascript
var obj = new Object();//new 一个空对象
obj.name = "tony";//定义一个属性
obj.fun = function(){//定义一个函数
    alert("name:" + obj.name);
}

//花括号形式定义一个对象
var obj1 = {
    name: lzy,
    age: 18
};
```

## 事件

1. `onload`加载完成事件，页面自动执行，常用于页面 js 代码的初始化
2. `onclick`单击事件
3. `onblur`失去焦点事件，常用于输入框失去焦点后验证齐输入内容的合法性
4. `onchange`内容发生改变事件
5. `onsubmit`表单提交事件

**事件的注册**

1. **静态注册**

   > 通过 html 标签的事件属性直接赋于事件响应的代码

2. **动态注册**

   > 指先通过 js 代码得到标签的 dom 对象，然后通过 dom 对象.事件名 = function(){} 这种形式赋予事件响应代码
   >
   > 基本步骤：1.获取标签对象；2. 标签名.事件名 = function(){}

---

## document 对象

**DOM**:  document object model 文档对象模型，就是把文档中的标签，属性，文本转换成对象来管理。

1. Document 对象管理了所有的 html 文档内容
2. document 它是一种树形结构的文档。有层级关系
3. 它让我们把所有的标签都对象化
4. 我们可以通过 document 访问所有的标签对象

**docuement 对象的方法**：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        function onclickFun(){
            //当我们要操作一个标签时，一定要先获取该标签的对象
            
            //1.通过 id 获取 dom 对象,id 是唯一的返回唯一的 dom 对象
            var usrnameObj = document.getElementById("usrname");
            //alert(usrnameObj.id);
            //alert(usrnameObj.value);
            var usrnameText = usrnameObj.value;
            //正则验证
            var ragex = /^\w{5,12}$/;// ^文本开头，$文本结尾， \w 字母，数字，下划线 {n,m}, n~m个字符

            var usrnameSpanObj = document.getElementById("usrnameSpan");
            //test()方法用于测试某个字符串是否满足正则表达式
            if(ragex.test(usrnameText)){
                //dom.innerHTML 表示起始标签结束标签间的内容，这个属性可读可写
                usrnameSpanObj.innerHTML = "V";
            }else{
                usrnameSpanObj.innerHTML = "X";
            }
        }

        
        function checkAll(){
            //2.通过 name 获取多个标签对象集合
            //对该集合的操作和操作数组一样
            //集合中元素都是 dom 对象
            var hobbyObjs = document.getElementsByName("hobby");
            for(var i = 0; i < hobbyObjs.length; i++){
                hobbyObjs[i].checked = true;
            }
        }
        //同理
        function checkNo(){
            var hobbyObjs = document.getElementsByName("hobby");
            for(var i = 0; i < hobbyObjs.length; i++){
                hobbyObjs[i].checked = false;
            }
        }

        function checkReverse(){
            var hobbyObjs = document.getElementsByName("hobby");
            for(var i = 0; i < hobbyObjs.length; i++){
                hobbyObjs[i].checked = !hobbyObjs[i].checked;
            }
        }
        
        
        function checkAllByTag(){
            //3.通过 tagName 标签名获取标签对象
            var inputObjs = document.getElementsByTagName("input");
            for(var i = 0; i < inputObjs.length; i++){
                inputObjs[i].checked = true;
            }
        }
    </script>
</head>
<body>
    用户名：<input type="text" id="usrname"/>
    <span id="usrnameSpan" style="color:red"></span>
    <button onclick="onclickFun()">校验</button>
    <br/>
    兴趣爱好：
    <input type="checkbox" name="hobby" value="cpp">c++
    <input type="checkbox" name="hobby" value="java">java
    <input type="checkbox" name="hobby" value="javascript">javascript
    <br/>
    <button onclick="checkAll()">全选</button>
    <button onclick="checkNo()">全不选</button>
    <button onclick="checkReverse()">反选</button>

    <button onclick="checkAllByTag()">全选bytag</button>
</body>
</html>
```

**标签对象也称为节点**：

节点的方法：

> `getElementsTagName()`获取当前节点的指定标签名孩子节点
>
> `appendChild( oChildNode)`添加一个孩子节点

属性：

> `childNodes`获取当前节点的所有孩子节点
>
> `firstChild`获取当前节点的第一个子节点
>
> `lastChild`获取当前节点的最后一个节点
>
> `parentChild`获取当前节点的父节点
>
> `nextSibling`获取当前节点的下一个节点
>
> `previousSibling`获取当前节点的前一个节点
>
> `className`用于获取或设置标签的 class 属性值
>
> `innerHTML`起始，终止标签间的内容
>
> `innerText`起始，终止标签间的文本

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        ////页面完成加载，document 中才能完成 body 对象的创建，我们才能去修改 body 的 dom 对象
        window.onload = function () {

            //创建一个 div 标签的 dom 对象
            var divObj = document.createElement("div");

            //在起止标签内添加内容
            divObj.innerHTML = "hello,world!";

            //将该标签对象添加到 body 的 dom 对象的孩子中
            document.body.appendChild(divObj);
        }
    </script>
</head>
<body>

</body>
</html>
```

---

# jQuery

JavaScript 和 查询 Query，辅助 JavaScript 的 js 类库

## 配置：

[jQuery](https://jquery.com/)：download后复制网页代码，到自己的新建的 jquery.js 文件中

编写 html 时引入该库

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="../jquery.js"></script>
    <script type="text/javascript">
        //$()表示页面加载完成再执行，相当于 windows.onload = function() 事件
        //$(function(){}); 是 $(document).ready(function(){}); 的简写
        $(function () {
            var $btnObj = $("#btnId");//#表示按 id 查询标签对象
            $btnObj.click(function (){
                alert("jQuery 的单击事件")
            });
        });
    </script>
</head>
<body>
    <button id="btnId">SayHello</button>
</body>
</html>
```

**jQuery 的 `$()`是 jQuery 的核心函数**

1. 传入参数是函数时：表示页面加载完成自动调用。相当于 `windows.onload = function(){}`

2. 传入参数为 HTML 字符串时：会自动帮我们创建这些 html 标签对象

3. 传入参数是 选择器字符串时 ：

   > `$(#id属性值)`：id 选择器，根据 id 查询标签对象
   >
   > `$("标签名")`：标签名选择器，根据指定的标签名查询标签对象
   >
   > `$(".class属性值")`：类型选择器，可以根据 class 属性查询标签对象

4. 传入参数是 dom 对象时：会把这个 dom 对象转换为 jQuery 对象



## jQuery 对象

jQuery 对象是 dom 对象的数组 + jQuery 提供的一系列功能函数

**dom 对象转换为 jQuery 对象**：

> 1. 先有 dom 对象
> 2. `$( dom对象 )`就可以转换为 jQuery 对象

**jQuery对象转换为 dom 对象**

> 1. 先有 jQuery 对象
> 2. jQuery 对象[下标]取出对应的 dom 对象

## jQuery 的选择器

```javascript
$(...).css(...);//设置样式
//基本选择器
$("#id");//id选择器
$("标签名");//标签选择器
$("[标签].class属性值");//类选择器
$("*");//通配符

//组合选择器，将多个选择器匹配的元素一起返回
//例
$("div, span, p.myClass")//p.myClass, p标签，class = "myClass"

//层级选择器
$("ancestor descendant");//空格间隔 匹配 ancestor标签 中所有的 descendant标签
$("parent >child");//匹配 parent标签 中所有的子级 child标签
$("prev + next");//匹配跟在 prev标签 后面的第一个 next标签
$("prev ~ siblings");///匹配跟在 prev标签 后面的所有 next标签

//过滤器
$("...:first");//获取第一个匹配
$("...:last");//获取最后一个匹配
$("...:not(...)");//去除 not 里的过滤器匹配的元素
$("...:even");//匹配索引偶数的元素，从 0 开始
$("...:odd");
$("...:gt(idx)");//匹配指定索引处元素
$("...:lt(idx)");//匹配小于指定索引处元素
$("...:header");//匹配标记元素
$("...:animated");//匹配所有执行动画效果元素

//内容过滤器,起止标签间的文本内容
$("...:contains('text')");
$("...:empty");
$("...:parent");//文本非空
$("...:has(selector)");//匹配含有选择器所匹配的元素的元素

//属性过滤
$("...[attribute]");//匹配含有 attribute 属性的元素
$("...[attribute='value']");//匹配含有 attribute 属性 = 'value' 的元素
$("...[attribute!='value']");//匹配不含有 attribute 属性的元素，或者attribute 属性 != 'value' 的元素
$("...[attribute^='value']");//匹配含有 attribute 属性 以'value'打头 的元素
$("...[attribute$='value']");//匹配含有 attribute 属性 以'value'结尾 的元素
$("...[attribute*='value']");//匹配含有 attribute 属性 包含'value'结尾 的元素
$("...[selector][[selector1]...]");//同时满足多个过滤条件

//表单过滤
$("...:type_name");//匹配表单中 type="type_name" 的元素
//表单对象域过滤
$("...:disabled");//不可用
$("...:enabled");//可用
$("...:checked");//选中
$("...:");//
```

## jQuery筛选方法

```javascript
$("...").eql(idx);//获取给定索引元素
$("...").first();//获取第一个元素
$("...").last();//获取最后一个元素
$("...").filter("exp");//留下匹配表达式的元素
$("...").is("exp");//判断选择器结果是否有匹配表达式的元素，有返回true
$("...").has("exp");//获取含有表达式所匹配的元素的元素
$("...").not("exp");//去除匹配表达式的元素
$("...").children("exp");
$("...").find("exp");
$("...").next();
$("...").nextAll();
$("...").nextUntil();
$("...").parent();
$("...").prev("exp");
$("...").prevAll();
$("...").prevUnit("exp");
$("...").siblings("exp");
$("...").add("exp");
```

## 属性操作

```javascript
$("...").html();//可以设置和获取起止标签间的内容
$("...").test();//可以设置和获取起止标签间的文本内容
$("...").val();//可以设置和获取表单项的 value 属性值

//不传参是获取，传参是设置

//获取，设置属性
$("...").attr("name");//获取，
$("...").attr("name", "abc");//设置
//attr还可以操作自定义属性
$("...").prop("name");//忽略 undifined 的错误，获取
$("...").prop("name","abc");//设置

```

# xml

## 简介

是一种可扩展的标记语言：

1. 用来保存数据，而这些数据具有自我描述性
2. 它还可以用来作为项目或者模块的配置文件
3. 还可以做为网络传输数据的格式(现在以 json 为主)

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--注释和 html 一样，xml可以自定义标签
    xml 文件的声明，version 版本，encoding 字符集
-->
<books><!-- books 表示我们自定义的多个图书信息标签 -->
    <book sn="sn1546546"><!-- book 表示我们自定义的单个图书信息标签 sn自定义属性表示书的额序列号-->
        <name>时间简史</name>
        <author>霍金</author>
        <price>50</price>
    </book>
    <book sn="sn154654226">
        <name>java入门到送外卖</name>
        <author>tony</author>
        <price>0.1</price>
    </book>
</books>
```

- xml 文档对**大小写敏感**
- xml 文档**必须有根元素**(没有父标签且同级唯一)
- xml 文档文本区域的 `CDATA`格式：`<![CDATA[这里可以把你输入的字符原样显示，不会解析 xml]]>`

## dom4j 解析 xml

不管是 html 或者是 xml 文件它们都是标记型文档，都可以用 w3c 组织制定的 dom 技术来解析。

jdk 最早提供的两种解析技术 dom 和 sax 已经过时。

现在使用 **Dom4j** 第三方解析技术。

1. 引入 dom4j 的 jar 包到 lib 里，并添加到库中

```java
//book 类
public class Book {
    private  String sn;
    private  String name;
    private BigDecimal price;
    private String author;
    ...;
}
```

```java
public class Dom4jTest {
    @Test
    public void test1() throws DocumentException {
        //创建一个 SAXReader 输入流，去读取 xml 文件，生成 Document 对象
        SAXReader saxReader = new SAXReader();
        Document dom = null;
        try {
            dom = saxReader.read("src/books.xml");
            System.out.println(dom);
        } catch (DocumentException e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test02() throws DocumentException {
        //读取 books.xml 文件生成 book 类
        //1.读取 books.xml文件
        SAXReader saxReader = new SAXReader();
        Document dom = saxReader.read("src/books.xml");

        //在 Junit 测试中，相对路径是从模块名开始算
        //2.通过 Document 对象获得根元素
        Element rootElement = dom.getRootElement();
        System.out.println( rootElement );

        //3.通过根元素获得 book 标签对象
        // element() 和 elements() 都是通过标签名查找子元素，单个或多个(多个返回 List)
        List<Element> books = rootElement.elements();

        //4.遍历，处理每个 book 标签转化为 book 对象
        for(Element book : books){
            //asXML() 把标签对象，转化为标签字符串
            //System.out.println( book.asXML() );

            Element nameElement = book.element("name");
            //getText() 获取起止标签间的文本内容
            String nameText = nameElement.getText();

            //elementText() 等效于 element() + getText()
            String authorName = book.elementText("author");
            String priceText = book.elementText("price");
            // attributeValue() 获取属性值
            String snText = book.attributeValue("sn");

            System.out.println(new Book(snText, nameText, BigDecimal.valueOf(Double.parseDouble(priceText)), authorName));
        }
    }
}
```

---

# Tomcat

javaWeb：所有通过 java 语言编写可以通过浏览器访问的程序总称，是基于请求和响应开发的。

tomcat：是 apache 组织提供的一种 web 服务器，提供对 jsp 和 servlet 支持。是一种轻量级的 javaWeb 容器(服务器) 免费

jboss：遵守 javaEE 规范的，开源，纯 java 的  EJB 服务器，支持所有的 JavaEE 规范

GlassFish：由 Oracle 公司开发的一款 JavaWeb 服务器，商业服务器，轻量级

Resin，WebLogic



**tomcat 企业常用版本 7.\*/8.\* **

| tomcat | Servlet/JSP | JavaEE | 运行环境 |
| ------ | ----------- | ------ | -------- |
| 7.0    | 3.0/2.2     | 6.0    | JDK6.0   |
| 8.0    | 3.1/2.3     | 7.0    | JDK7.0   |

**tomcat 默认端口 8080**，mysql 3306：更改 tomcat 的默认端口

> 找到 toomcat 目录下的 conf 目录，找到 server.xml 配置文件，找到 connector 标签修改其 port 属性(1~65535)

---

## 如何部署 web 项目到 tomcat

**方式一：**

> 只要把 web 工程的目录拷贝到 tomcat 的 Webapps 目录下即可。
>
> 访问：`http://127.0.0.1:8080/book_staticweb/index.html`
>
> `http://127.0.0.1:8080`就是访问到 tomcat 的 Webapps 目录为止

**方式二：**

> 在 conf 目录,下的 Catalina\localhost\ 下，创建如下配置文件：xxx.xml
>
> 部署示例：`<Context path="/abc" docBase="F:\java\code\bookshop\book_staticweb" />`
>
> Context 表示工程上下文， path 自定义访问路径， docBase 工程文件目录

**手拖 html 文件到浏览器**：这个时候浏览器地址如下 `file:///F:/java/code/bookshop/book_staticweb/index.html` 使用的协议是 `file://`协议，`file`协议表示告诉浏览器直接读取 file 协议后面的本地文件路径，直接显示在浏览器上即可。

**在浏览器输入访问地址**：`http://localhost:8080/abc/index.html`,所用的协议是 `http`

localhost ip地址，8080 端口， /abc 工程路径，index.html 具体文件

**root 工程的访问**：当我们输入的地址为 `http://ip:port/`时，没有工程名，默认访问的是 root 工程，tomcat 的 root 工程默认就是 初始的猫猫页面，可以更改 root 文件夹下的 index.html

 文件。访问任何一个工程若未输入访问的文件`http://ip:port/abc/`时默认访问该工程下的 index.html。

---

## IDEA 整合 Tomcat

设置->应用程序服务器->添加tomcat->选择对应路径

新建模块->Java Enterprice->选择对应服务器，项目模板选择 web应用程序

**文件结构**：

![](F:\java\javaweb\photo\snipaste_20220702_165844.jpg)

---

# Maven



自动化构建工具

![](F:\java\javaweb\photo\snipaste_20220702_185306.jpg)

目前的技术在开发中存在的问题：

- 一个项目就是一个工程
- 项目中的 jar 包必须手动 cv 到 WEB-INF/lib 目录下
- jar 包需要别人替我们准备好，或到官网下载
- 一个 jar 包依赖其它 jar 包需要主机手动加入到项目中

# Servlet

JavaEE 的规范之一，是 JavaWeb 的三大组件之一（三大组件 Servlet 程序，Filter 过滤器， Listener 监听器）。Servlet 是一个运行在服务器上的小程序，可以接受客户端发送过来的请求，并相应数据给客户端。

## 实现一个 Servlet 程序

1. 编写一个类去实现 Servlet 接口
2. 实现其 service 方法，处理请求，并响应数据
3. 到 web.xml 中去配置 Servlet 程序的访问地址

```java
package com.example.project73;

import java.io.*;
import javax.servlet.*;

public class HelloServlet implements Servlet {

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }
    //service 方法是专门用来处理请求和响应的
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hello,world!");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- servlet标签给tomcat配置servlet程序-->
    <servlet>
        <!--servlet-name标签 Servlet 程序起的一个别名-->
        <servlet-name>HelloServlet</servlet-name>
        <!--servlet-class标签 Servlet 程序的全类名-->
        <servlet-class>com.example.project73.HelloServlet</servlet-class>

    </servlet>
    <!--servlet-mapping 标签给 servlet 程序配置访问地址-->
    <servlet-mapping>
        <!--servlet-name 标签的作用就是告诉服务器，我当前配置的地址给哪个 Servlet 程序使用 -->
        <servlet-name>HelloServlet</servlet-name>
        <!--url-pattern配置访问地址
            / 斜杠在服务解析的时候，表示地址为 http://ip:port/工程路径
            /hello 就表示 http://ip:port/工程路径/hello
        -->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```

---

## Servlet 生命周期

1. 执行 Servlet 构造器方法

2. 执行 init 初始化方法

   1,2 在创建 servlet 程序时会调用

3. 执行 service 方法，每次访问都会调用
4. 执行 destroy 方法，web工程停止的时候执行

**请求的方法处理**

```java
//以 get，post 的区别处理为例   
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hello,world!");
        //类型转换，因为 HttpServletRequest 有 getMethod() 方法
        HttpServletRequest httpServletRequest = (HttpServletRequest)servletRequest;
        String method = httpServletRequest.getMethod();
        //请求的分发处理
        if("GET".equals(method)){
            doGet();
        }else if("POST".equals(method)){
            doPost();
        }

    }

    public void doGet(){
        System.out.println("get请求");
    }

    public void doPost(){
        System.out.println("post请求");
    }
```



## HttpServlet 

实际开发中通常通过继承 HttpServlet 实现 Servlet 程序

1. 编写一个类去继承 HettpServlet 类
2. 根据业务重写  doGet 或 doPost 方法
3. 到 web.xml 中配置 Servlet 程序的访问地址

```java
public class HelloServlet1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("HelloServlet1 的 doGet 方法");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("HelloServlet1 的 doPost 方法");
    }
}
```

HttpServlet 实现了 Servlet 的方法，并完成的请求的分发处理

---

## ServletConfig

Servlet 程序的配置信息类

1. 可以获取 Servlet 程序的别名 servlet-name 的值
2. 获取初始化参数 **init-param**
3. 获取 ServletContext 对象

```xml
...
<servlet>
    ...
<!-- init-param 初始化参数-->
        <init-param>
            <!-- 参数名 -->
            <param-name>username</param-name>
            <!-- 参数值 -->
            <param-value>lzy</param-value>
        </init-param>
    ...
</servlet>
...
```

```java
public class HelloServlet implements Servlet {

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("HelloServlet 程序别名：" + servletConfig.getServletName());
        System.out.println("HelloServlet 初始化参数" + servletConfig.getInitParameter("username"));
	   System.out.println(servletConfig.getServletContext());
    }
...
}
```

Servlet 程序和 ServletConfig 对象都是由 tomcat 服务器负责创建，Servlet 程序默认第一次访问的时候创建，ServletConfig 是每个Servlet 程序创建时就创建对应的对象，对应自己的 Servlet 程序。

也可以使用 `getServletConfig() `获取 ServletConfig 类的对象

**tip:**

```java
public class HelloServlet1 extends HttpServlet {

    @Override
    public void init(ServletConfig config) throws ServletException {
        super.init(config);//父类初始化方法中会保存 config 信息，所以我们重写后必须调用父类的 init 方法,不然 ServletConfig 类的对象得不到保存
        System.out.println("重写 init 初始化方法");
    }

    ...
}

```

---

## ServletContext 类

1. ServletContext 是一个接口，表示 Servlet 上下文对象
2. 一个 web 工程只有一个 ServletContext 对象实例
3. ServletContext 对象是一个 域 对象(域对象，是可以像 Map 一样存取数据的对象，域是存取数据的操作范围)
4. ServletContext 的域即整个 web 工程内，开启工程时创建，关闭工程时销毁

|        | 存数据         | 取数据         | 删除数据          |
| ------ | -------------- | -------------- | ----------------- |
| Map    | put()          | get()          | remove()          |
| 域对象 | setAttribute() | getAttribute() | removeAttribute() |

**作用**：

- 获取 web.xml 中配置的上下文参数 **context-param**
- 获取当前的工程路径，格式：/工程路径
- 获取工程部署后在服务器磁盘上的绝对路径
- 像 Map 一样存取数据

```xml
<web-app> 
    ...
	<!-- context-param 是上下文参数(它属于整个 web 工程)-->
    <!-- 注意 context-param 和 init-param 的区别-->
    <context-param>
        <param-name>username</param-name>
        <param-value>root</param-value>
    </context-param>
	...
    <!-- 配置访问路径 -->
    <servlet-mapping>
        <servlet-name>ContextServlet</servlet-name>
        <url-pattern>/contextServlet</url-pattern>
    </servlet-mapping>
    ...
</web-app>
```

```java
public class ContextServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取 web.xml 中配置的上下文对象 context-param
        //通过 ServletConfig 对象获取 ServletContext 对象
        //或者直接 getServletContext(),因为 GenericServlet 里重写了该方法也是通过 getServletConfig().getServletContext() 实现的
        ServletContext context = getServletConfig().getServletContext();
        String username = context.getInitParameter("username");
        System.out.println("context-param 中 username value: " + username);

        //2.获取当前的工程路径
        System.out.println("当前工程路径：" + context.getContextPath());

        //3.获取工程部署后在服务器磁盘上的绝对路径
        // "/ " 斜杆被服务器解析为 http://ip:port/工程名/ 实际映射到 idea 代码的 web 目录
        System.out.println("工程部署后在服务器磁盘上的绝对路径：" + context.getRealPath("/"));

        //4.像 Map 一样存取数据
        System.out.println("保存前 Context 中获取域数据 key1 的值是 ： " + context.getAttribute("key1"));
        context.setAttribute("key1","value1");
        System.out.println("Context 中获取域数据 key1 的值是 ：" + context.getAttribute("key1"));
    }

}
```

![](F:\java\javaweb\photo\snipaste_20220703_212455.jpg)

---

## http协议

### **GET请求**：

1. 请求行

   > (1)请求方式									GET
   >
   > (2)请求资源路径[ + ? + 请求参数]
   >
   > (3)请求协议的版本号					  HTTP/1.1

2. 请求头

   > key:value 组成，不同键值对表示不同的含义

![](F:\java\javaweb\photo\snipaste_20220703_215559.jpg)

---

### **POST请求**：

1. 请求行

   > (1)请求方式									POST
   >
   > (2)请求资源路径[ + ? + 请求参数]
   >
   > (3)请求协议的版本号					  HTTP/1.1

2. 请求头

   > key:value 组成，不同键值对表示不同的含义

3. **空行**

4. 请求体：发送给服务器的数据

![](F:\java\javaweb\photo\snipaste_20220703_215508.jpg)

---

**GET请求有哪些**：

1. form 标签 method="get"
2. a 标签
3. link 标签引入 css
4.  script 标签引入 js 文件
5.  img 标签引入图片
6. ifame 引入 html 页面
7. 在浏览器地址栏中输入地址后回车

**POST请求有哪些**：

1. form 标签 method="post"

### 响应 http 协议格式

1. 响应行

   > (1)响应的协议和版本号 		HTTP/1.1
   >
   > (2)响应状态码						
   >
   > (3)响应状态描述符

2. 响应头

   > (1)key:value

3. **空行**

4. 响应体：回传给客户端的数据

![](F:\java\javaweb\photo\snipaste_20220703_220804.jpg)

**常见的响应码**：200 请求成功，302 表示请求重定向，404 表示请求服务器已经收到，但是要求的数据不存在(请求地址错误)，500 表示服务器已经收到请求，但是服务器内部错误(一般是代码错误)

### MME 数据类型

是 http 协议中的数据类型，多功能 internet 邮件阔绰服务。格式是 "大类型/小类型"，并与某种文件的扩展名对应。

![](F:\java\javaweb\photo\snipaste_20220704_152115.jpg)

## HttpServletRequest

每次请求进入 tomcat 服务器，tomcat 就会把请求过来的 Http 协议信息解析号封装到 Request 对象中，然后传递到 service 方法(doGet， doPost)中给我们使用。我们可以通过 HttpServletRequest 对象，获取所有请求的信息。

![](F:\java\javaweb\photo\snipaste_20220704_153100.jpg)

```java
public class HttpServletRequest01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //getRequestURI() 获取请求的资源路径
        System.out.println("URI: " + request.getRequestURI());
        //getRequestURL() 获取请求的统一资源定位符(绝对路径)
        System.out.println("URL: " + request.getRequestURL());
        //getRemoteHost() 获取客户端的 ip 地址
        System.out.println("客户端 IP：" + request.getRemoteHost());
        //getHeader() 获取请求头
        System.out.println("请求头：" + request.getHeader("User-Agent"));
        //getMethod() 获取请求的方式 GET 或 POST
        System.out.println("请求方式：" + request.getMethod());


    }
}
```

![](F:\java\javaweb\photo\snipaste_20220704_153953.jpg)

**获取请求参数值**

```xml
...    
	<servlet>
        <servlet-name>ParameterServlet</servlet-name>
        <servlet-class>com.example.project73.ParameterServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>ParameterServlet</servlet-name>
        <url-pattern>/parameterServlet</url-pattern>
    </servlet-mapping>
...
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="http://localhost:8080/project73/parameterServlet" method="get">
        用户名：<input type="text" name="username"/><br/>
        密码：<input type="password" name="password"/><br/>
        兴趣爱好：<input type="checkbox" name="hobby" value="java"/>java<input type="checkbox" name="hobby" value="c++"/>c++
        <input type="checkbox" name="hobby" value="c">c<br/>
        <input type="submit"/>
    </form>
</body>
</html>
```

```java
public class ParameterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
	    //防止乱码，设置字符集为 UTF-8，要在获取请求参数前设置
        req.setCharacterEncoding("UTF-8");
        
        //获取请求参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("username: "  + username + " password: " + password);

        //获取多个参数
        String[] hobbies = req.getParameterValues("hobby");
        System.out.print("兴趣爱好：" + Arrays.asList(hobbies));


    }
}
```

---

## 请求转发

多个 servlet 程序间的通信

**Servlet1**

```java
public class Servlet1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求的参数(办事的材料)查看
        String username = req.getParameter("username");
        System.out.println("在 servlet1 柜台1 中查看材料， username："  + username);


        //通过域数据给数据标记，并传递至柜台2 去查看
        req.setAttribute("key1","柜台 1 的标记");

        //问路：servlet2 怎么走
        /*
        *请求转发必须以斜杆打头，/ 表示地址为 http://ip:port/工程名/
        * 映射到 idea 代码的 web 目录
        */
        RequestDispatcher requestDispatcher = req.getRequestDispatcher("/servlet2");

        //去到 servlet2
        requestDispatcher.forward(req, resp);
    }
}

```

**Servlet2**

```java
public class Servlet2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求的参数(办事的材料)查看
        String username = req.getParameter("username");
        System.out.println("在 servlet2 柜台2 中查看材料， username："  + username);

        //查看 servlet1 是否有标记
        Object key1 = req.getAttribute("key1");
        System.out.println("柜台一是否右标记：" + key1);

        //处理自己的业务
        System.out.println("servlet2 处理自己业务");

    }
}
```

访问 Servlet1， ？后面传入参数

`http://localhost:8080/project73/servlet1?username=lzy`

![](F:\java\javaweb\photo\snipaste_20220704_212606.jpg)

**请求转发特点：**

- 虽然访问了两个 servlet 程序，但是浏览器地址没有变化
- 它们是一次请求
- 它们共享 Request 域中的数据
- 可以转发到 WEB-INF 目录下资源
- 不能访问工程外资源

## base 标签

所有的**相对路径**在工作的时候都会参照当前浏览器地址栏中的路径来进行跳转，而当我们使用请求转发的模式跳转到一个页面中去，而这个页面中恰好有一个 a 标签中是相对路径的跳转，而**请求转发的模式下浏览器地址并不会变化**，仍然在开启页面的 servlet 的地址下，这样就会导致页面的相对路径错误，不能找到资源。使用相对路径时，使用**base**标签来确定相对路径的寻址路径。

存在 base 标签就会忽略浏览器地址值，而参考 base 标签内地址值

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- base 标签设置页面相对路径工作时参照的地址
            href就是参照地址值
    -->
    <base href="http:localhost:8080/project73/a/b/c.html">
</head>
<body>
    这是a下的b下的c<br/>
    <a href="../../index.html">跳回首页</a>
</body>
</html>
```

`/`的不同含义：

- 若被浏览器解析，得到的地址是 ：`http://ip:port/`
- 若被服务器解析，得到的地址是：`http://ip:port/工程路径`
- 特殊情况：`response.sendRediect("/")`，把斜杆发送给浏览器解析。得到`http://ip:port/`

## HttpServletResponse

HttpServletResponse 和 HttpServletRequest 一样，每次请求进入 tomcat 服务器，tomcat 就会创建一个 Response 对象，然后传递到 servlet 程序中给我们使用。HttpServletResponse 表示所有响应的信息。

**两个输出流**

| 字节流     | getOutputStream() | 常用于下载(传递二进制数据) |
| ---------- | ----------------- | -------------------------- |
| **字符流** | **getWriter()**   | **常用于回传字符串**       |

两个流同时只能使用一个。

```java
public class ResponseIO extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置服务器字符集为 UTF-8
        resp.setCharacterEncoding("UTF-8");

        //通过响应头，设置浏览器也使用 UTF-8 字符集
        resp.setHeader("Content-Type", "text/html; charset=UTF-8");
	   
        /* 一条指令同时设定服务器和客户端的字符集，
           此方法一定要在获取输出流对象前执行
	   *  resp.setContentType("text/html; charset=UTF-8");
	   */
        
        //往客户端回传数据
        PrintWriter writer = resp.getWriter();
        writer.write("response's content!");
    }
}

```

**请求重定向**：

```java
public class Response01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Response01");
        //设置响应状态码 302，表示重定向（表示该 servlet 程序已搬迁）
        resp.setStatus(302);
        //设置响应头，告知重定向地址
        resp.setHeader("Location", "http://localhost:8080/project73/response02");
    }
}
```

```java
public class Response02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("response02");
    }
}
```

- 请求重定向后，浏览器地址跳转至重定向的 servlet 程序
- 一次原请求，一次重定向后的请求，一共两次请求
- 重定向后的 servlet 程序和原 servlet 程序域数据不共享

# JavaEE三层结构

![](F:\java\javaweb\photo\snipaste_20220704_230908.jpg)

---

# 书城项目

## 1.创建书城所需的数据库和表

```mysql
drop database if exists book;
create database book;
use book;

create table t_user(
		`id` int primary key auto_increment,
		`username` varchar(128) not null unique,
		`password` varchar(32) not null,
		`email` varchar(128)
);

insert into t_user(`username`,`password`,`email`) values('lzy','1234','11@qq.com');

select * from t_user;
```



## 2.创建数据库表对应的 JavaBean 对象



```java
package com.example.book.project;

/**
 * ClassName User
 * Author taro
 * Date 2022/7/5 10:10
 * Version 1.0
 */

public class User {

    private Integer id;
    private  String username;
    private  String password;
    private  String email;

    public User(){

    }

    public User(Integer id, String username, String password, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.email = email;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                '}';
    }

    public Integer getId() {
        return id;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    public String getEmail() {
        return email;
    }
}

```

## 3.编写工具类 JdbcUtils

```java
package com.example.book.utils;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.pool.DruidDataSourceFactory;

import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;

/**
 * ClassName JdbcUtils
 * Author taro
 * Date 2022/7/5 10:14
 * Version 1.0
 */

public class JdbcUtils {

    private static DruidDataSource dataSource;
    //静态代码块初始化连接池
    static {

        Properties properties = new Properties();

        try {
            //读取 jdbc.properties 属性配置文件
            InputStream inputStream = JdbcUtils.class.getClassLoader().getResourceAsStream("jdbc.properties");
            //从流中加载数据
            properties.load(inputStream);
            //创建数据库连接池
            dataSource = (DruidDataSource) DruidDataSourceFactory.createDataSource(properties);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //获取数据库连接池中的连接
    //若返回 null 说明获取连接失败
    public static Connection getConnection(){
        Connection conn = null;
        try {
            conn = dataSource.getConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }

        return conn;
    }

    //关闭连接，返回数据库连接池
    public static void close(Connection conn){
        if (conn != null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 4.编写 BaseDao 

```java
package com.example.book.dao.impl;

import com.example.book.utils.JdbcUtils;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.ResultSetHandler;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;

import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;

/**
 * ClassName BaseDao
 * Author taro
 * Date 2022/7/5 11:09
 * Version 1.0
 */

public abstract class BaseDao {

    //使用 Dbutils 操作数据库
    private QueryRunner queryRunner = new QueryRunner();

    /**
     * update 方法用来执行 insert/update/delete 语句
     *
     * @return
     */
    public int update(String sql, Object... args) {
        Connection conn = JdbcUtils.getConnection();
        try {
            return queryRunner.update(conn, sql, args);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(conn);
        }

        return -1;
    }

    /**
     * 查询返回一个 javaBean 的 sql 语句
     *
     * @param type 返回的对象类型
     * @param sql  执行的 sql 语句
     * @param args sql 对应的参数
     * @param <T>  返回的类型的泛型
     * @return
     * @throws SQLException
     */
    public <T> T queryForOne(Class<T> type, String sql, Object... args) throws SQLException {
        Connection conn = JdbcUtils.getConnection();
        try {
            return queryRunner.query(conn, sql, new BeanHandler<T>(type), args);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(conn);
        }

        return null;
    }

    //返回多行
    public <T> List<T> queryForList(Class<T> type, String sql, Object... args) throws SQLException {
        Connection conn = JdbcUtils.getConnection();
        try {
            return queryRunner.query(conn, sql, new BeanListHandler<T>(type), args);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(conn);
        }

        return null;
    }

    //返回一行一列数据
    public Object queryForSingleValue(String sql, Object... args) {
        Connection conn = JdbcUtils.getConnection();
        try {
            return queryRunner.query(conn, sql, new ScalarHandler(), args);
        } catch (SQLException e) {
            e.printStackTrace();
        }

        return null;
    }
}
```

## 5.编写 UserDao 和测试

###  UserDao  接口

```java
package com.example.book.dao;

import com.example.book.project.User;

/**
 * ClassName UserDao
 * Author taro
 * Date 2022/7/5 11:57
 * Version 1.0
 */

public interface UserDao {

    /**
     * 根据用户名查询用户信息
     * @param username 用户名
     * @return 若返回 null 则不存在此用户
     */
    public User queryUserByUsername(String username);

    /**
     * 根据用户名和密码查询用户信息
     * @param username 用户名
     * @param password 密码
     * @return 返回 null 用户名或密码错误
     */
    public User queryUserByUsernameAndPassword(String username, String password);

    /**
     * 保存用户信息
     * @param user
     * @return
     */
    public int saveUser(User user);


}
```

​      

### 实现 UserDao

```java
package com.example.book.dao.impl;

import com.example.book.dao.UserDao;
import com.example.book.project.User;

import java.sql.SQLException;

/**
 * ClassName UserDaoImpl
 * Author taro
 * Date 2022/7/5 12:04
 * Version 1.0
 */

public class UserDaoImpl extends BaseDao implements UserDao {
    @Override
    public User queryUserByUsername(String username) {
        String sql = "select `id`, `username`,`password`, `email` from t_user where username = ?";
        try {
            return queryForOne(User.class, sql, username);
        } catch (SQLException e) {
            e.printStackTrace();
        }

        return null;
    }

    @Override
    public User queryUserByUsernameAndPassword(String username, String password) {
        String sql = "select `id`, `username`, `password`,`email` from t_user where username = ? and password = ?";
        try {
            return queryForOne(User.class, sql, username, password);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }

    @Override
    public int saveUser(User user) {
        String sql = "insert into t_user(`username`, `password`, `email`) values(?, ?, ?)";
        return update(sql, user.getUsername(), user.getPassword(),user.getEmail());
    }
}

```



## 6. UserService

UserService 接口

```java
package com.example.book.service;

import com.example.book.project.User;

public interface UserService {
    //一个业务一个方法

    /**
     * 注册用户
     * @param user
     */
    public void registerUser(User user);

    /**
     * 登录
     * @param user
     * @return 返回 null 登录失败，返回有值，登陆成功
     */
    public User login(User user);

    /**
     * 检查用户是否可用
     * @param username
     * @return 返回 true 表示已经存在，返回 false 表示可用
     */
    public boolean existsUsername(String username);
}

```

UserService 接口的实现类 UserServiceImpl

```java
package com.example.book.service.impl;

import com.example.book.dao.UserDao;
import com.example.book.dao.impl.UserDaoImpl;
import com.example.book.project.User;
import com.example.book.service.UserService;

/**
 * ClassName UserServiceImpl
 * Author taro
 * Date 2022/7/5 12:38
 * Version 1.0
 */

public class UserServiceImpl implements UserService {

    private UserDao userDao = new UserDaoImpl();

    @Override
    public void registerUser(User user) {
        userDao.saveUser(user);
    }

    @Override
    public User login(User user) {
        return userDao.queryUserByUsernameAndPassword(user.getUsername(), user.getPassword());
    }

    @Override
    public boolean existsUsername(String username) {
        if(userDao.queryUserByUsername(username) != null){
            return true;
        }else{
            return false;
        }
    }
}

```

## 7.web层

```java
package com.example.book.web;

import com.example.book.project.User;
import com.example.book.service.UserService;
import com.example.book.service.impl.UserServiceImpl;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * ClassName RegisterServlet
 * Author taro
 * Date 2022/7/5 12:59
 * Version 1.0
 */

public class RegisterServlet extends HttpServlet {

    private UserService userService = new UserServiceImpl();

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //1.获取请求的参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String repwd = req.getParameter("repwd");
        String email = req.getParameter("email");
        String code = req.getParameter("code");

        //2.检验验证码是否正确。 此处写死，要求验证码为：abcde
        if("abcde".equalsIgnoreCase(code)){//正确

            //3.检查用户名是否正确
            if(userService.existsUsername(username)){
                //不可用跳回注册页面
                System.out.println("用户名[" + username + "]已存在");
                req.getRequestDispatcher("/pages/user/regist.html").forward(req,resp);
            }else{
                //可用
                //调用 servise 保存到数据库
                userService.registerUser(new User(null, username, password, email));
                //跳转到注册成功页面
                req.getRequestDispatcher("/pages/user/regist_success.html").forward(req,resp);
            }

        }else{//不正确
            //请求转发跳回注册页面
            System.out.println("验证码[" + code + "]错误");
            req.getRequestDispatcher("/pages/user/regist.html").forward(req, resp);
        }
    }
}

```

```java
package com.example.book.web;

import com.example.book.project.User;
import com.example.book.service.UserService;
import com.example.book.service.impl.UserServiceImpl;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * ClassName LoginServlet
 * Author taro
 * Date 2022/7/5 14:38
 * Version 1.0
 */

public class LoginServlet extends HttpServlet {

    private UserService userService = new UserServiceImpl();

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取请求的参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");


        if(userService.login(new User(null, username, password, null)) != null){
            //验证成功
            System.out.println("用户[" + username + "]登录成功");
            //跳转至登录成功页面
            req.getRequestDispatcher("/pages/user/login_success.html").forward(req, resp);
        }else{
            //验证失败
            System.out.println("用户[" + username + "]登录失败");
            //跳转回登录页面
            req.getRequestDispatcher("/pages/user/login.html").forward(req, resp);
        }

    }
}
```

# jsp

全称 java server page。 java 的服务器页面

jsp 的作用主要是代替 servlet 程序回传 html 页面的数据

**jsp页面的本质**：本质是一个 servlet 程序，当我们第一次访问 jsp 页面时。tomcat 服务器会帮我门把 jsp 页面翻译成一个 java 源文件，并将它编译为 .class 字节码程序

# Listener

1. 监听器是 JavaEE 的三大组件之一
2. Listener 它是 JavaEE 规范，就是接口
3. 监听器的作用就是监听某种事务的变化，然后通过回调函数，反馈给客户

**`ServletContextListener`**：可以监听 ServletContext 对象的创建和销毁，ServletContext 对象在web 工程启动时创建，在 web 工程停止时销毁，监听到创建和销毁都会分别调用 ServletContextListener 监听器的方法反馈。

`contextInitialized` 和 `contextDestroyed`

使用 **`ServletContextListener`**监听`ServletContext`对象步骤：

1. 编写一个类去实现  **`ServletContextListener`**
2. 实现这两个回调方法
3. 到 web.xml 中去配置监听器

---

# 文件的上传下载



## 文件的上传

1. 要有一个 `form` 标签：`method="post"`请求
2. `form`标签的`encType`属性值必须为`multipart/form-data`
3. 在`form`标签中使用`input type="file"`添加上传文件
4. 编写服务器代码接收，处理上传的数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <!--
		enctype="multipart/form-data" 表示提交的数据，以多段的形式进行拼接，然	  后以二进制流的形式发送给服务器。
	-->
    <form action="http://localhost:8080/project73/uploadServlet" method="post" enctype="multipart/form-data">
      用户名：<input type="text" name="username"/><br/>
      头像：<input type="file" name="photo"/><br/>
      <input type="submit" value="上传"/>
    </form>
</body>
</html>
```

```java
package com.example.project73;

import javax.servlet.ServletException;
import javax.servlet.ServletInputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * ClassName uploadServlet
 * Author taro
 * Date 2022/7/9 14:26
 * Version 1.0
 */

public class UploadServlet extends HttpServlet {
    /**
     * 用来处理文件上传
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("文件上传过来了");
        //以什么方式发送，只能以什么方式接收
        //客户端以流的形式发送，也应以流的形式接收
        ServletInputStream inputStream = req.getInputStream();

        byte[] buffer = new byte[1024000];
        int read = inputStream.read(buffer);
        System.out.println(new String(buffer, 0, read));
    }
}
```

![](F:\java\javaweb\photo\snipaste_20220709_144443.jpg)

## 文件解析

jar 包：`commons-fileupload.jar` `commons-io-1.4.jar`

**常用类**：

`ServletFileUpload`类用于解析上传数据

![](F:\java\javaweb\photo\snipaste_20220709_145601.jpg)

```java
package com.example.project73;

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileItemFactory;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.ServletException;
import javax.servlet.ServletInputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.IOException;
import java.util.List;

/**
 * ClassName uploadServlet
 * Author taro
 * Date 2022/7/9 14:26
 * Version 1.0
 */

public class UploadServlet extends HttpServlet {
    /**
     * 用来处理文件上传
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.先判断文件是否是多端数据(只有多段数据才是文件上传的，需要解析)
        if(ServletFileUpload.isMultipartContent(req)){
            //创建 FileItemFactory 工厂实现类
            FileItemFactory fileItemFactory = new DiskFileItemFactory();
            //创建用于解析上传数据的工具类 ServletFileUpload
            ServletFileUpload servletFileUpload = new ServletFileUpload(fileItemFactory);

            try {
                //解析上传的数据，得到每一个表单项 FileItem
                List<FileItem> list = servletFileUpload.parseRequest(req);
                //循环判断，每一个表单项，是普通类型，还是上传文件
                for(FileItem fileItem : list){
                    if(fileItem.isFormField()){
                        //普通表单项
                        System.out.println("表单项的 name 属性值：" + fileItem.getFieldName());
                        //参数指定字符集 UTF-8 解决乱码
                        System.out.println("表单项的 value 属性值：" + fileItem.getString("UTF-8"));
                    }else{
                        //上传的文件
                        System.out.println("表单项的 name 属性值：" + fileItem.getFieldName());
                        System.out.println("上传的文件名：" + fileItem.getName());

                        fileItem.write(new File("f:\\" + fileItem.getName()));
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            }

        }
    }
}

```

![](F:\java\javaweb\photo\snipaste_20220709_150853.jpg)

## 文件下载

```java
package com.example.project73;

import org.apache.commons.io.IOUtils;

import javax.servlet.Servlet;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.InputStream;

/**
 * ClassName DownloadServlet
 * Author taro
 * Date 2022/7/9 15:13
 * Version 1.0
 */

public class DownloadServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取要下载的文件名，这里直接写死
        String downloadFilename = "1.jpg";

        //2.读取要下载的文件内容，通过 ServletContext 对象可以读取
        ServletContext servletContext = getServletContext();

        //3.在回传前，通过响应头告诉客户端返回的数据类型
        //获取要下载的文件类型
        String mimeType = servletContext.getMimeType("/file/" + downloadFilename);
        //设置类型
        resp.setContentType(mimeType);

        //4.还要告诉客户端收到的数据是用于下载的，还是使用响应头
        //Content-Disposition 响应头，表示收到的数据怎么处理
        //attachment 表示附件
        //filename= 表示指定下载的文件名,下载文件名可以自定义
        //URL 编码是把汉字转化为 %xx%xx 两个十六进制的格式
        resp.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode("汉字.jpg", "UTF-8"));

        //5.把下载的文件内容回传给客户端
        InputStream resourceAsStream = servletContext.getResourceAsStream("/file/" + downloadFilename);
        //获取响应的输出流
        ServletOutputStream outputStream = resp.getOutputStream();
        //读取输入流中的全部数据到输出流，输出给客户端
        IOUtils.copy(resourceAsStream, outputStream);
        
    }
}

```

---

# 代码优化

## BaseServlet 的抽取

在实际开发中，一般只有一个 servlet 程序

```html
<!-- 添加隐藏域，来区分不同的表单提交 -->
<form action="userServlet" method="post">
	<input type="hidden" name="action" value="regist">
    ...
</form>
```

```html
<form action="userServlet" method="post">
	<input type="hidden" name="action" value="login">
    ...
</form>
```

```java
//使用一个 servlet 实现登录/注册

/**
 * ClassName UserServlet
 * Author taro
 * Date 2022/7/9 20:07
 * Version 1.0
 */

public class UserServlet extends HttpServlet {

    private UserService userService = new UserServiceImpl();

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String action = req.getParameter("action");

        if("login".equals(action)){
            login(req, resp);
        }else if("regist".equals(action)){
            regist(req, resp);
        }
    }
    
  /*----------------------------------------------------------------------*/  

    protected void login(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("登录业务");
        //1.获取请求的参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");

        if(userService.login(new User(null, username, password, null)) != null){
            //验证成功
            System.out.println("用户[" + username + "]登录成功");
            //跳转至登录成功页面
            req.getRequestDispatcher("/pages/user/login_success.html").forward(req, resp);
        }else{
            //验证失败
            System.out.println("用户[" + username + "]登录失败");
            //跳转回登录页面
            req.getRequestDispatcher("/pages/user/login.html").forward(req, resp);
        }
    }

    protected void regist(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("注册业务");
        //1.获取请求的参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String repwd = req.getParameter("repwd");
        String email = req.getParameter("email");
        String code = req.getParameter("code");

        //2.检验验证码是否正确。 此处写死，要求验证码为：abcde
        if("abcde".equalsIgnoreCase(code)){//正确

            //3.检查用户名是否正确
            if(userService.existsUsername(username)){
                //不可用跳回注册页面
                System.out.println("用户名[" + username + "]已存在");
                req.getRequestDispatcher("/pages/user/regist.html").forward(req,resp);
            }else{
                //可用
                //调用 servise 保存到数据库
                userService.registerUser(new User(null, username, password, email));
                //跳转到注册成功页面
                req.getRequestDispatcher("/pages/user/regist_success.html").forward(req,resp);
            }

        }else{//不正确
            //请求转发跳回注册页面
            System.out.println("验证码[" + code + "]错误");
            req.getRequestDispatcher("/pages/user/regist.html").forward(req, resp);
        }
    }
}
}

        }else{//不正确
            //请求转发跳回注册页面
            System.out.println("验证码[" + code + "]错误");
            req.getRequestDispatcher("/pages/user/regist.html").forward(req, resp);
        }
    }
}

```

## 使用反射优化大量的 if else 代码



```java
package com.example.book.test;

import com.example.book.project.User;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

/**
 * ClassName UserServletTest
 * Author taro
 * Date 2022/7/9 20:34
 * Version 1.0
 */

public class UserServletTest {
    public void login(){
        System.out.println("login");
    }

    public void regist(){
        System.out.println("regist");
    }

    public void updateUser(){
        System.out.println("updateUser");
    }

    public void updateUserPassword(){
        System.out.println("updateUserPassword");
    }
    //...

    public static void main(String[] args) {
        //以为 login 为例
        String action = "login";

        try {
            //通过 action 业务鉴别字符串，获取相应业务方法的反射对象
            Method method = UserServletTest.class.getDeclaredMethod(action);
            System.out.println(method);
            //调用目标方法
            method.invoke(new UserServletTest());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

![](F:\java\javaweb\photo\snipaste_20220709_204141.jpg)

**使用反射机制替换 BaseServlet 中的 if else**

```java
public class UserServlet extends HttpServlet {

    private UserService userService = new UserServiceImpl();

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String action = req.getParameter("action");

        try {
            //通过 action 业务鉴别字符串，获取相应业务方法的反射对象
            Method method = this.getClass().getMethod(action, HttpServletRequest.class, HttpServletResponse.class);
            System.out.println(method);
            //通过反射调用目标方法
            method.invoke(this, req, resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    
/*--------------------------------------------------------------------------*/
    protected void login(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ...
    }

    protected void regist(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       ...
    }
}
```

## BaseServlet 抽取 + 反射

1. 获取 action 参数值
2. 通过反射获取 action 对应的业务方法
3. 通过反射调用业务方法

```java
//BaseServlet
package com.example.book.web;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.Method;

/**
 * ClassName BaseServlet
 * Author taro
 * Date 2022/7/9 20:55
 * Version 1.0
 */

public abstract class BaseServlet extends HttpServlet {

    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String action = req.getParameter("action");

        try {
            //通过 action 业务鉴别字符串，获取相应业务方法的反射对象
            Method method = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);
            System.out.println(method);
            //通过反射调用目标方法
            method.invoke(this, req, resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```java
//UserServlet
public class UserServlet extends BaseServlet {

    private UserService userService = new UserServiceImpl();

    protected void login(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ...
    }

    protected void regist(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     ...
}

```

![](F:\java\javaweb\photo\snipaste_20220709_210202.jpg)

---

# 数据封装和抽取 BeanUtils

BeanUtils 工具类，它可以一次性把所有的请求参数注入到 JavaBean 中

BeanUtils 是第三方的需要导包 `commons-logging-1.1.1.jar`,`commons-beanutils-1.8.0.jar`

```java
//WebUtils 来完成数据注入
package com.example.book.utils;

import org.apache.commons.beanutils.BeanUtils;

import javax.servlet.http.HttpServletRequest;
import java.util.Map;

/**
 * ClassName WebUtils
 * Author taro
 * Date 2022/7/9 21:18
 * Version 1.0
 */

public class WebUtils {

    public static<T> T copyParamToBean(Map value, T bean){
        try {
            System.out.println("注入之前：" + bean);
            /**
             * 把所有请求的参数都注入到 user 对象中
             */
            BeanUtils.populate(bean, value);
            System.out.println("注入之后：" + bean);

        } catch (Exception e) {
            e.printStackTrace();
        }

        return bean;
    }
}
```

```java
package com.example.book.web;

import com.example.book.project.User;
import com.example.book.service.UserService;
import com.example.book.service.impl.UserServiceImpl;
import com.example.book.utils.WebUtils;
import org.apache.commons.beanutils.BeanUtils;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

/**
 * ClassName UserServlet
 * Author taro
 * Date 2022/7/9 20:07
 * Version 1.0
 */

public class UserServlet extends BaseServlet {

    private UserService userService = new UserServiceImpl();

    protected void login(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("登录业务");
	   
        //调用 webUtils 工具类注入数据
        User user = WebUtils.copyParamToBean(req.getParameterMap(), new User());

        if(userService.login(user) != null){
            //验证成功
            System.out.println("用户[" + user.getUsername() + "]登录成功");
            //跳转至登录成功页面
            req.getRequestDispatcher("/pages/user/login_success.html").forward(req, resp);
        }else{
            //验证失败
            System.out.println("用户[" + user.getUsername() + "]登录失败");
            //跳转回登录页面
            req.getRequestDispatcher("/pages/user/login.html").forward(req, resp);
        }
    }

    protected void regist(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("注册业务");
        String code = req.getParameter("code");

        //调用 webUtils 工具类注入数据
        User user = WebUtils.copyParamToBean(req.getParameterMap(), new User());


        if("abcde".equalsIgnoreCase(code)){

            if(userService.existsUsername(user.getUsername() )){
                System.out.println("用户名[" + user.getUsername() + "]已存在");
                req.getRequestDispatcher("/pages/user/regist.html").forward(req,resp);
            }else{
                userService.registerUser(user);
                req.getRequestDispatcher("/pages/user/regist_success.html").forward(req,resp);
            }

        }else{
            System.out.println("验证码[" + code + "]错误");
            req.getRequestDispatcher("/pages/user/regist.html").forward(req, resp);
        }
    }
}

```

# MVC

Model 模型， View 视图，  Controller 控制器

**Model 模型：**将于业务逻辑相关的数据封装为具体的 JavaBean 类，其中不掺杂任何与数据处理相关的代码——JavaBean/domaln/entity

**View 视图：**只负责接数据和界面的显示，不接受任何与显示数据无关的代码，便于程序员和美工分工合作——JSP/HTML

**Controller 控制器：**只负责接收请求，调用业务层的代码处理请求，然后派发页面，是一个调度者——Servlet



# 书城图书模块

## 1.建表

```mysql
create table t_book(
	`id` int primary key auto_increment,
	`name` varchar(128),
	`price` decimal(11,2),
	`author` varchar(128),
	`sales` int,
	`stock` int,
	`img_path` varchar(256)
);
```

## 2.编写 JavaBean 类 Book

```java
package com.example.book.project;

import java.math.BigDecimal;

/**
 * ClassName Book
 * Author taro
 * Date 2022/7/10 15:41
 * Version 1.0
 */

public class Book {

    private Integer id;
    private String name;
    private String author;
    private BigDecimal price;
    private Integer sales;
    private Integer stock;
    private String imgPath = "static/img/default.jpg";

    public Book(){};

    public Book(Integer id, String name, String author, BigDecimal price, Integer sales, Integer stock, String imgPath) {
        this.id = id;
        this.name = name;
        this.author = author;
        this.price = price;
        this.sales = sales;
        this.stock = stock;
        if(imgPath != null && !"".equals(imgPath)){
            this.imgPath = imgPath;
        }
    }

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", author='" + author + '\'' +
                ", price=" + price +
                ", sales=" + sales +
                ", stock=" + stock +
                ", imgPath='" + imgPath + '\'' +
                '}';
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public BigDecimal getPrice() {
        return price;
    }

    public void setPrice(BigDecimal price) {
        this.price = price;
    }

    public Integer getSales() {
        return sales;
    }

    public void setSales(Integer sales) {
        this.sales = sales;
    }

    public Integer getStock() {
        return stock;
    }

    public void setStock(Integer stock) {
        this.stock = stock;
    }

    public String getImgPath() {
        return imgPath;
    }

    public void setImgPath(String imgPath) {
        this.imgPath = imgPath;
    }
}
```

## 1.3 编写 Dao 和 测试 Dao

```java
package com.example.book.dao;

import com.example.book.project.Book;

import java.util.List;

public interface BookDao {

    public int addBook(Book book);
    public int deleteBookById(Integer id);
    public int updateBook(Book book);

    public Book queryBookById(Integer id);
    public List<Book> queryBooks();
}
```

```java
package com.example.book.dao.impl;

import com.example.book.dao.BookDao;
import com.example.book.project.Book;

import java.sql.SQLException;
import java.util.List;

/**
 * ClassName BookDaoImpl
 * Author taro
 * Date 2022/7/10 15:53
 * Version 1.0
 */

public class BookDaoImpl extends BaseDao implements BookDao {

    @Override
    public int addBook(Book book) {
        String sql = "insert into t_book(`name` , `author` , `price` , `sales` , `stock` , `img_path`) " +
                "values( ?, ?, ?, ?, ?, ?);";
        return update(sql, book.getName(), book.getAuthor(), book.getPrice(), book.getSales(), book.getStock(), book.getImgPath());
    }

    @Override
    public int deleteBookById(Integer id) {
        String sql = "delete from t_book where id = ?";
        return update(sql, id);
    }

    @Override
    public int updateBook(Book book) {
        String sql = "update t_book set `name`=? , `author`=?, `price`=?, `sales`=?, `stock`=?, `img_path`=? where id = ?";
        return update(sql, book.getName(), book.getAuthor(), book.getPrice(), book.getSales(), book.getStock(), book.getImgPath(), book.getId());
    }

    @Override
    public Book queryBookById(Integer id) {
        String sql = "select `id`, `name` , `author` , `price` , `sales` , `stock` , `img_path` imgPath from t_book where id = ?";
        try {
            return queryForOne(Book.class, sql, id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }

    @Override
    public List<Book> queryBooks() {
        String sql = "select `id`, `name` , `author` , `price` , `sales` , `stock` , `img_path` imgPath from t_book";
        try {
            return queryForList(Book.class, sql);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

## 1.3 Service

```java
package com.example.book.service;

import com.example.book.project.Book;

import java.util.List;

public interface BookService {

    public void addBook(Book book);
    public void deleteBookById(Integer id);
    public void updateBook(Book book);

    public Book queryBookById(Integer id);
    public List<Book> queryBooks();
}
```

```java
package com.example.book.service.impl;

import com.example.book.dao.BookDao;
import com.example.book.dao.impl.BookDaoImpl;
import com.example.book.project.Book;
import com.example.book.service.BookService;

import java.util.List;

/**
 * ClassName BookServiceImpl
 * Author taro
 * Date 2022/7/10 16:31
 * Version 1.0
 */

public class BookServiceImpl implements BookService {

    private BookDao bookDao = new BookDaoImpl();

    @Override
    public void addBook(Book book) {
        bookDao.addBook(book);
    }

    @Override
    public void deleteBookById(Integer id) {
        bookDao.deleteBookById(id);
    }

    @Override
    public void updateBook(Book book) {
        bookDao.updateBook(book);
    }

    @Override
    public Book queryBookById(Integer id) {
        return bookDao.queryBookById(id);
    }

    @Override
    public List<Book> queryBooks() {
        return bookDao.queryBooks();
    }
}
```



# cookie

==Cookie保存在客户端浏览器上==

1. cookie 是服务器通知客户端保存键值对的一种技术
2. 客户端有了 cookie 后，每次请求都发给服务器
3. 每个 cookie 的大小不超过 4kb

## cookie 的创建与接收

```html
...
	<li><a href="cookieServlet?action=createCookie" target="target">Cookie创建</a></li>
	<li><a href="cookieServlet?action=getCookie" target="target">Cookie获取</a></li>
...			
```

```java
package com.lzy.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * ClassName CookieServlet
 * Author taro
 * Date 2022/7/10 19:54
 * Version 1.0
 */

public class CookieServlet extends BaseServlet{

    protected void createCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.创建 cookie 对象
        Cookie cookie1 = new Cookie("key1", "value1");
        Cookie cookie2 = new Cookie("key2", "value2");
        //2.通知客户端保存 cookie
        resp.addCookie(cookie1);
        resp.addCookie(cookie2);

        resp.getWriter().write("Cookie 创建成功");
    }

    protected void getCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //服务器端接收 cookie
        Cookie[] cookies = req.getCookies();
        Cookie iWantCookie = null;
        for(Cookie cookie : cookies){
            //cookie.getName() 返回 cookie 的键
            //cookie.getValue() 返回 cookie 的值
            resp.getWriter().write("Cookie[" + cookie.getName() + " = " +  cookie.getValue() + "]<br/>" );

            //获取 cookie 只能通过 getCookies() 获取所有的 cookie
            //所以我们只能自己去判断获取想要的 cookie
            if("key2".equals(cookie.getName())){
                iWantCookie = cookie;
            }
        }

        if(iWantCookie != null){
            resp.getWriter().write("iWantCookie[" + iWantCookie.getName() + " = " +  iWantCookie.getValue() + "]<br/>" );
        }

    }
}
```

**获取对应 key 的 cookie 的方法抽取**

```java
package com.lzy.utils;

import javax.servlet.http.Cookie;

/**
 * ClassName CookieUtils
 * Author taro
 * Date 2022/7/10 20:30
 * Version 1.0
 */

public class CookieUtils {
    /**
     * 查找指定名称的 cookie 对象
     * @param name
     * @param cookies
     * @return
     */
    public static Cookie findCookie(String name, Cookie[] cookies){
        if(name == null || cookies == null || cookies.length == 0){
            return null;
        }else{
            Cookie iWantCookie =  null;
            for(Cookie cookie : cookies){
                if(name.equals(cookie.getName())) iWantCookie = cookie;
            }

            return iWantCookie;
        }
    }
}
```

## cookie 值的修改

方案一：

1. 先创建一个要修改的同名 cookie 对象
2. 在构造器，同时赋于新的 cookie 值
3. 调用 `response.addCookie(Cookie)`

```html
...	
	<li><a href="cookieServlet?action=updateCookie" target="target">Cookie值修改</a></li>
...
```

```java
protected void updateCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //先创建一个要修改的同名 cookie 对象
    //在构造器，同时赋于新的 cookie 值
    Cookie cookie = new Cookie("key1", "newValue");

    //调用 response.addCookie(Cookie)
    resp.addCookie(cookie);

    resp.getWriter().write("key1 的 value 值已修改");
}
```

方案二：

1. 先查找到需要修改的 cookie 对象
2. 调用 setValue() 方法赋于新的 cookie 值
3. 调用 `response.addCookie(Cookie)`

```java
protected void updateCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //先查找到需要修改的 cookie 对象
    Cookie cookie1 = CookieUtils.findCookie("key1", req.getCookies());

    //调用 setValue() 方法赋于新的 cookie 值
    if(cookie1 != null) {
        cookie1.setValue("newValue");

        //调用 response.addCookie(Cookie) 通知客户端
        resp.addCookie(cookie1);
        resp.getWriter().write("key1 的 value 值已修改");
    }
}
```

tip: cookie 的 value 不支持中文,...

<img src="F:\java\javaweb\photo\snipaste_20220710_205310.jpg" style="zoom:200%;" />

---

## **设置 cookie 的最大生存时间**

`setMaxAge(int expiry)`以秒为单位，负值意味着不会长久存储，浏览器退出时即删除



---

## Cookie 的有效路径 Path 的设置

cookie 的 path 属性可以有效的过滤哪些 cookie 可以发送给服务器，哪些不发。

path 属性是通过请求的地址来进行有效的过滤。

**例：**

> **CookieA    path=/工程路径**
>
> **CookieB	path=/工程路径/abc**
>
> 请求 cookie 的地址如下：
>
>  1. **`http://ip:port/工程路径/a.html`**
>
>     > CookieA 发送；CookieB 不发送
>
>  2. **`http://ip:port/工程路径/abc/a.html`**
>
>     > CookieA 发送；CookieB 发送

```java
protected void testPath(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie cookie = new Cookie("path1", "path1");
    //getContextPath() 得到工程路径
    cookie.setPath(req.getContextPath() + "/abc");//工程路径/abc
    resp.addCookie(cookie);
    resp.getWriter().write("创建了一个带有路径的cookie");
}
```

![](F:\java\javaweb\photo\snipaste_20220710_213757.jpg)

## 通过 cookie 实现免用户名登录

![](F:\java\javaweb\photo\snipaste_20220710_213939.jpg)



# Session

==Session保存在服务器上==

1.  Session 是一个接口 `HttpSession`
2. Session 就是一个会话。它是用来维护一个客户端和服务器之间关联的一种技术
3. 每个客户端都有自己的一个 Session 会话
4. Session 会话中，我们经常用来保存用户登录之后的信息

## Session 的创建和获取

创建和获取 Session 的 api 都是一样的

`request.getSession()`:第一次调用是创建 Session 会话，之后调用的都是获取。

`isNew()`：可以判断一个 Session 是不是刚创建出来的。

`getId()`：获取 Session 的id 值，每个 Session 都有一个唯一的 id ，对应一个客户端

```html
...
	<base href="http://localhost:8080/project710/"/>
...
	<li><a href="sessionServlet?action=createOrGetSession" target="target">Session的创建和获取（id号、是否为新创建）</a></li>
...
```

```java
public class SessionServlet extends BaseServlet {

    protected void createOrGetSession(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //创建和获取 Session 会话
        HttpSession session = req.getSession();
        //判断当前 Session 会话是否是刚创建出来的
        boolean isNew = session.isNew();
        //获取当前 Session 会话的唯一标识 id
        String id = session.getId();

        resp.getWriter().write("得到的 Session，它的 id 是：" + id + "<br/>");
        resp.getWriter().write("得到的 Session，是否是新创建的：" + isNew + "<br/>");
    }
}
```

![](F:\java\javaweb\photo\snipaste_20220711_152653.jpg)

---

## Session 域数据的存取

```html
...
	<li><a href="sessionServlet?action=setAttribute" target="target">Session域数据的存储</a></li>
	<li><a href="sessionServlet?action=getAttribute" target="target">Session域数据的获取</a></li>
...
```

```java
   /**
     * 往 Session 中保存数据
     * @param req
     * @param resp
     */
    protected void setAttribute(HttpServletRequest req, HttpServletResponse resp){
        req.getSession().setAttribute("key1", "value1");
    }

    /**
     * 获取 Session 域中的数据
     * @param req
     * @param resp
     */
    protected void getAttribute(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        Object attribute = req.getSession().getAttribute("key1");
        resp.getWriter().write("从 Session 中获取的 key1 的数据是：" + attribute);
    }
```

![](F:\java\javaweb\photo\snipaste_20220711_153141.jpg)

---

## Session 生命周期的控制

==Session的超时指的是，客户端两次请求的最大间隔==

`setMaxInactiveInterval(int interval)`:设置 Session 的超时时间，超时销毁，以秒为单位

`getMaxInactiveInterval()`：获取

​		在 tomcat 的服务器的配置文件 web.xml 中有以下默认配置，表示配置了当前 tomcat 服务器下的所有 Session 默认的超时时长为 30 分钟。

```xml
<!-- 在 xml 中配置单位为 分钟-->
<session-config>
    <session-timeout>30</session-timeout>
</session-config>
```

​		可以在自己的 web.xml 配置文件中做以上配置，修改 web 工程的所有 Session 的默认超时时长。

​		单独设置，调用 api `setMaxInactiveInterval(int interval)`

---

## 浏览器和 Session 之间的关联技术

![](F:\java\javaweb\photo\snipaste_20220711_161249.jpg)

Session 技术，底层是基于 Cookie 技术实现的。

---

# 验证码防止表单重复提交

![](F:\java\javaweb\photo\snipaste_20220711_170807.jpg)

**谷歌 kaptcha 图片验证码的使用**

1. 导入谷歌验证码的 jar 包

2. 在 web.xml 中去配置用于生成验证码的 servlet 程序

   ```xml
       <servlet>
           <servlet-name>KaptchaServlet</servlet-name>
           <servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>KaptchaServlet</servlet-name>
           <url-pattern>/kaptcha.jpg</url-pattern>
       </servlet-mapping>
   ```

3. 在表单中使用 img 标签去显示验证码图片并使用它

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   <form action="http://localhost:8080/project710/registerServlet" method="get">
       用户名：<input type="text" name="username"><br/>
       验证码：<input type="text" style="width: 80px;" name="code">
       <img src="http://localhost:8080/project710/kaptcha.jpg" alt="" style="width: 80px;height: 25px;"><br/>
       <input type="submit" value="登录">
   </form>
   </body>
   </html>
   ```

4. 在服务器获取谷歌生成的验证码和客户端发过来的验证码比较使用

   ```java
   package com.lzy.servlet;
   
   import javax.servlet.ServletException;
   import javax.servlet.http.HttpServlet;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   import java.io.IOException;
   
   import static com.google.code.kaptcha.Constants.KAPTCHA_SESSION_KEY;
   
   /**
    * ClassName RegisterServlet
    * Author taro
    * Date 2022/7/11 17:26
    * Version 1.0
    */
   
   public class RegisterServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           resp.setCharacterEncoding("UTF-8");
   
           //1.获取 Session 中的验证码
           String token = (String)req.getSession().getAttribute(KAPTCHA_SESSION_KEY);
           //获取验证码值后立即删除 Session 域中的验证码 key，防止重复获取，来避免表单的重复提交
           req.getSession().removeAttribute(KAPTCHA_SESSION_KEY);
   
           //2.获取客户端提交的表单的验证码
           String code = req.getParameter("code");
           String username = req.getParameter("username");
   
           //用户数据在放入数据库前需要先验证验证码
           if(token != null && token.equals(code)){
               System.out.println("保存到数据库：" + username);
           }else{
               resp.getWriter().write("default");
           }
       }
   }
   ```

5. ==验证码刷新，跳过缓存==

   ```html
   <!-- 绑定单击事件 -->
   <script type="text/javascript">			
       $(function () {
   
           $("#code_img").click(function (){
   <!-- 存在问题：浏览器为了请求速度更快，就会将每次请求的内容缓存到了浏览器上，这时同一连接的请求，浏览器会在缓存中找，导致验证码不刷新 -->
               this.src = this.src;
           });
           ...
       });
   </script>
   ...
   	<img id="code_img" alt="" src="kaptcha.jpg" style="width: 80px;height: 25px;"/>
   ...
   ```

   **解决缓存导致的验证码不更新**：跳过浏览器的缓存，而发起请求给服务器获取新验证码

   ```javascript
   $("#code_img").click(function (){
       //在请求验证码的链接后面添加时间戳
   	this.src = this.src + "?d=" + new Date().getTime();
   });

# 书城购物车模块

![](F:\java\javaweb\photo\snipaste_20220712_133640.jpg)

## 1.购物车模型

```java
package com.example.book.project;

import java.math.BigDecimal;
import java.util.*;

/**
 * ClassName Cart 购物车对象
 * Author taro
 * Date 2022/7/12 13:39
 * Version 1.0
 */

public class Cart {

    private Map<Integer, CartItem> items = new HashMap<>();

    /**
     * 添加商品项
     * @param cartItem
     */
    public void addItem(CartItem cartItem){
        //商品已经存在，增加数量，更新总价
        if(items.containsKey(cartItem.getId())){
            CartItem item = items.get(cartItem.getId());
            item.setCount(item.getCount() + cartItem.getCount());
            item.setTotalPrice(item.getPrice().multiply(new BigDecimal(item.getCount())));
        }else{
            items.put(cartItem.getId(), cartItem);

        }
    }

    /**
     * 删除商品项
     * @param id
     */
    public void deleteItem(Integer id){
        items.remove(id);
    }

    /**
     * 清空购物车
     */
    public void clean(){
        items.clear();
    }

    /**
     * 更新数量
     * @param id
     * @param count
     */
    public void updateCount(Integer id, Integer count){
        if(items.containsKey(id)){
            CartItem cartItem = items.get(id);
            cartItem.setCount(count);
            cartItem.setTotalPrice(cartItem.getPrice().multiply(new BigDecimal(count)));
        }
    }




    @Override
    public String toString() {
        return "Cart{" +
                "totalCount=" + getTotalCount() +
                ", totalPrice=" + getTotalPrice() +
                ", items=" + items +
                '}';
    }
	//购物车内的总数量和总价格不应该存在 set 方法可以去修改
    //而应该是有购物车的商品项目决定的
    public Integer getTotalCount() {
        Integer totalCount = 0;
        for(Integer id : items.keySet()){
            totalCount += items.get(id).getCount();
        }
        return totalCount;
    }



    public BigDecimal getTotalPrice() {
        BigDecimal totalPrice = new BigDecimal(0);
        for(Integer id : items.keySet()){
            totalPrice = totalPrice.add(items.get(id).getTotalPrice());
        }
        return totalPrice;
    }


    public Map<Integer, CartItem> getItems() {
        return items;
    }

    public void setItems(Map<Integer, CartItem> items) {
        this.items = items;
    }
}
```

```java
package com.example.book.project;

import java.math.BigDecimal;

/**
 * ClassName CartItem 购物车的商品项
 * Author taro
 * Date 2022/7/12 13:37
 * Version 1.0
 */

public class CartItem {

    private  Integer id;
    private  String name;
    private  Integer count;
    private BigDecimal price;
    private BigDecimal totalPrice;

    public CartItem(){}

    public CartItem(Integer id, String name, Integer count, BigDecimal price, BigDecimal totalPrice) {
        this.id = id;
        this.name = name;
        this.count = count;
        this.price = price;
        this.totalPrice = totalPrice;
    }

    @Override
    public String toString() {
        return "CartItem{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", count=" + count +
                ", price=" + price +
                ", totalPrice=" + totalPrice +
                '}';
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getCount() {
        return count;
    }

    public void setCount(Integer count) {
        this.count = count;
    }

    public BigDecimal getPrice() {
        return price;
    }

    public void setPrice(BigDecimal price) {
        this.price = price;
    }

    public BigDecimal getTotalPrice() {
        return totalPrice;
    }

    public void setTotalPrice(BigDecimal totalPrice) {
        this.totalPrice = totalPrice;
    }
}

```

## 2.给加入购物车绑定功能

```html
<script type="text/javascript">
    $(function(){
        //给加入购物车绑定单击事件
        $("botton.addToCart").click(function (){

            location.href="cartServlet?action=addItem";

        });
    });
</script>
```

## 3.CartServlet 编写

```java
package com.example.book.web;

import com.example.book.project.Book;
import com.example.book.project.Cart;
import com.example.book.project.CartItem;
import com.example.book.service.BookService;
import com.example.book.service.impl.BookServiceImpl;
import com.example.book.utils.WebUtils;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * ClassName CartServlet
 * Author taro
 * Date 2022/7/12 14:31
 * Version 1.0
 */

public class CartServlet extends BaseServlet{

    private BookService bookService = new BookServiceImpl();
    /**
     * 加入购物车
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    protected void addItem(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //System.out.println("addItem");
        //1.获取请求参数，商品编号
        if(req.getParameter("id") == null) return;
        int id = Integer.parseInt(req.getParameter("id"));

        //2.调用 BookService.queryBookById(id) 得到图书信息
        Book book = bookService.queryBookById(id);

        //3.把图书信息转换为 CartItem 页面
        CartItem item = new CartItem(id, book.getName(), 1, book.getPrice(), book.getPrice());

        //4.调用 Cart.addItem(cartItem) 添加商品项
        Cart cart = (Cart)req.getSession().getAttribute("Cart");
        //将 Cart 放在 Session 域中
        if(cart == null){
            cart = new Cart();
            req.getSession().setAttribute("cart", cart);
        }

        cart.addItem(item);
        System.out.println(cart);

        //5.通过请求头，重定向回到商品原来所在页面
        resp.sendRedirect(req.getHeader("Referer"));

    }
}

```



# 书城订单模块

![](F:\java\javaweb\photo\snipaste_20220712_171537.jpg)

## 1. 建表

```mysql
use book;

create table t_order(
	`order_id` varchar(50) primary key not null,
	`create_time` datetime,
	`price` decimal(11,2),
	`status` int,
	`user_id` int,
	foreign key(`user_id`) references t_user(`id`)
	
);

create table t_order_item(
	`id` int primary key not null auto_increment,
	`name` varchar(100),
	`count` int,
	`price` decimal(11,2),
	`total_price` decimal(11,2),
	`order_id` varchar(50), 
	foreign key(`order_id`) references t_order(`order_id`)
);
```

## 2.创建订单 bean

```java
public class Order {

    private String orderId;
    private Date createTime;
    private BigDecimal price;
    //0 表示未发货，1 表示已发货， 2 表示已签收
    private Integer status = 0;
    private Integer userId;
	...
}
```



```java
public class OrderItem {

    private Integer id;
    private String name;
    private Integer count;
    private BigDecimal price;
    private BigDecimal totalPrice;
    private String orderId;
    ...
}
```

## 3.Dao 层

以创建订单为例

```java
public interface OrderDao {
    public int saveOrder(Order order);
}
```

```java
public interface OrderItemDao {
    public int savaOrderItem(OrderItem orderItem);
}
```

**implements**

```java
public class OrderDaoImpl extends BaseDao implements OrderDao {
    @Override
    public int saveOrder(Order order) {
        String sql = "insert into t_order(`order_id`, `create_time`, `price` , `status`, `user_id`) values(?,?,?,?,?)";
        return update(sql, order.getOrderId(), order.getCreateTime(), order.getPrice(), order.getStatus(), order.getUserId());
    }
}
```

```java
public class OrderItemDaoImpl extends BaseDao implements OrderItemDao {
    @Override
    public int savaOrderItem(OrderItem orderItem) {
        String sql = "insert into t_order_item(`name`, `count`, `price` , `total_price`, `order_id`) values(?,?,?,?,?)";
        return update(sql, orderItem.getName(), orderItem.getCount(), orderItem.getPrice(), orderItem.getTotalPrice(), orderItem.getOrderId());
    }
}

```

## 4.service 层

```java
public interface OrderService {
    public String createOrder(Cart cart, Integer userId);
}
```

**implements**

```java
public class OrderServiceImpl implements OrderService {

    private OrderDao orderDao = new OrderDaoImpl();
    private OrderItemDao orderItemDao = new OrderItemDaoImpl();

    @Override
    public String createOrder(Cart cart, Integer userId) {
        //订单号要保证唯一
        String orderId = System.currentTimeMillis() + "" + userId;
        Order order = new Order(orderId, new Date(), cart.getTotalPrice(), 0, userId);
        //调用 dao 层，保存订单
        orderDao.saveOrder(order);

        //遍历购物车的每一个商品项转换成订单保存到数据库
        for(Map.Entry<Integer, CartItem>entry : cart.getItems().entrySet()){
            CartItem cartItem = entry.getValue();
            OrderItem orderItem = new OrderItem(null, cartItem.getName(), cartItem.getCount(), cartItem.getPrice(), cartItem.getTotalPrice(), orderId);
            orderItemDao.savaOrderItem(orderItem);
        }
        //清空购物车
        cart.clean();

        return orderId;
    }
}
```

## 5.web层

```java
public class OrderServlet extends HttpServlet {

    private OrderService orderService = new OrderServiceImpl();

    /**
     * 生成订单
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    protected void createOrder(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //先获取 Cart 购物车对象
        Cart cart = (Cart)req.getSession().getAttribute("cart");
        //获取 UserId
        User loginUser = (User)req.getSession().getAttribute("user");
        if(loginUser == null){//若未登录，则跳转到登陆页面
            req.getRequestDispatcher("/pages/user/login.html").forward(req,resp);
            return;
        }
        Integer id = loginUser.getId();

        //调用 orderService.createOrder(Cart, UserId) 生成订单
        String order = orderService.createOrder(cart, id);
        
        //订单号写入应该写入 Session 域中重定向后也可以访问订单号，写在request 域中重定向后不能共享
        //req.setAttribute("orderId", order); 写入 request 域中
        req.getSession().setAttribute("orderId", order);

        //订单提交后应该重定向，防止表单的重复提交
        /* 请求转发会存在表单重复提交的问题
        req.getRequestDispatcher("/pages/cart/checkout.html").forward(req, resp);
        */
        resp.sendRedirect(req.getContextPath() + "/pages/cart/checkout.html");

    }
}
```

---

# Filter过滤器

1. Filter javaWeb 的三大组件之一

2. 是 JavaEE 的规范，也就是接口

3. 作用：拦截请求，过滤响应

   > 拦截请求的常见应用场景：权限检查，日记操作，事务管理，...

使用步骤：编写一个类去实现 Filter 接口 -> 实现过滤方法 doFilter() -> 到 web.xml 中去配置 Filter 的拦截路径

**Filter 在 web.xml 中的配置方式类似 Servlet**

```xml
<filter>
    <!-- 别名 -->
    <filter-name>AdminFilter</filter-name>
    <filter-class>com.example.project712.AdminFilter</filter-class>
</filter>
<!-- 配置 filter 过滤器的拦截路径 -->
<filter-mapping>
    <!-- filter-name 表示当前拦截路径给哪个 filter 使用 -->
    <filter-name>AdminFilter</filter-name>
    <!-- 配置拦截路径 
            /admin/* 表示 web 目录下 admin 文件夹的所有文件
        -->
    <url-pattern>/admin/*</url-pattern>
</filter-mapping>
```

```java
package com.example.project712;

import javax.servlet.*;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

/**
 * ClassName AdminFilter
 * Author taro
 * Date 2022/7/12 19:28
 * Version 1.0
 */

public class AdminFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    /**
     * doFilter方法，专门用于拦截请求。可以做权限检查
     * @param servletRequest
     * @param servletResponse
     * @param filterChain
     * @throws IOException
     * @throws ServletException
     */
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
        Object user = httpServletRequest.getSession().getAttribute("user");
        //如果为 null，则表示还没有登录
        if(user == null){
            servletRequest.getRequestDispatcher("/login.html").forward(servletRequest, servletResponse);
        }else{
            //放行：让程序继续往下访问用户的目标资源
            filterChain.doFilter(servletRequest, servletResponse);
        }
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

---

## Filter 的生命周期

1. 构造器方法

2. init 初始化方法

   第 1，2步，在 web 工程启动的时候执行( Filter 创建 )

3. doFilter 过滤方法

   每次拦截到请求，就会执行

4. destroy 销毁

   停止 web 工程的时候，就会执行( 停止 web 工程，也会销毁 Filter 过滤器 )

---

## FilterConfig 类

是 Filter 过滤器的配置文件类， tomcat 创建 Filter 的时候，也会同时创建一个 FilterConfig类

FilterConfig类的作用：

> 1. 获取 Filter 的名称 filter-name 的内容
> 2. 获取 Filter 中配置的 init-param 初始化参数
> 3. 获取 SeverletContext 对象

---

## FilterChain 过滤器链

![](F:\java\javaweb\photo\snipaste_20220712_204615.jpg)

## Filter 拦截路径

1. 精确匹配：`<url-pattern>/target.html</url-pattern>` 具体到某个文件
2. 目录匹配：`<url-pattern>/dir/*</url-pattern>`
3. 后缀名匹配：`<url-pattern>/dir/*.html</url-pattern>`

Filter 过滤器它只关心请求的地址是否与拦截地址匹配，不关心请求资源是否存在。

---

# ThreadLocal

ThreadLocal 作用：可以解决多线程的数据安全问题。

ThreadLocal 它可以给当前线程关联一个数据（可以是普通变量，对象，...）

ThreadLocal 的特点：

1. ThreadLocal 可以为当线程关联一个数据(它可以像 map 一样存取数据， key 为当前线程)
2. 每一个 ThreadLocal 对象，只能为当前线程关联一个数据，若要关联多个数据，就需要创建多个 ThreadLocal 对象实例
3. 每个 ThreadLocal 对象实例定义的时候，一般都是 static 类型
4. ThreadLocal 对象中的数据，再线程销毁后，会有 jvm 自动释放

演示：

```java
package com.example.book.filter;

import java.util.Random;

/**
 * ClassName ThreadLocalTest
 * Author taro
 * Date 2022/7/13 15:51
 * Version 1.0
 */

public class ThreadLocalTest {

    public static ThreadLocal<Object> threadLocal = new ThreadLocal<>();

    public class Task implements Runnable{

        @Override
        public void run() {
            Random random = new Random();
            Integer i = random.nextInt(1000);

            String name = Thread.currentThread().getName();
            System.out.println("线程[" + name + "]生成的随机数是：" + i);

            threadLocal.set(i);//ThreadLocal 中 key 为当前线程名

            try {
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            new Test().method1();

            Object o = threadLocal.get();
            System.out.println("线程[" + name + "]结束时取出的随机数是：" + o);
        }
    }

    public static void main(String[] args) {
        for(int i = 0; i < 3; ++i){
            new Thread(new ThreadLocalTest().new Task()).start();
        }
    }
}
```

```java
package com.example.book.filter;

/**
 * ClassName Test
 * Author taro
 * Date 2022/7/13 15:57
 * Version 1.0
 */

public class Test {

    public void method1(){
        String name = Thread.currentThread().getName();
        System.out.println("Test 当前线程[" + name + "]保存的数据是：" + ThreadLocalTest.threadLocal.get());
    }
}
```

![](F:\java\javaweb\photo\snipaste_20220713_160803.jpg)

## 使用ThreadLocal

![](F:\java\javaweb\photo\snipaste_20220713_163623.jpg)

使用ThreadLocal 确保同一线程的所有操作使用同一个 Connection。

## JDBCUtils 的更改

```java
package com.example.book.utils;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.pool.DruidDataSourceFactory;

import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;

/**
 * ClassName JdbcUtils
 * Author taro
 * Date 2022/7/5 10:14
 * Version 1.0
 */

public class JdbcUtils {

    private static DruidDataSource dataSource;
    private static ThreadLocal<Connection> conns = new ThreadLocal<>();
    //静态代码块初始化连接池
    static {

        Properties properties = new Properties();

        try {
            InputStream inputStream = JdbcUtils.class.getClassLoader().getResourceAsStream("jdbc.properties");
            properties.load(inputStream);
            dataSource = (DruidDataSource) DruidDataSourceFactory.createDataSource(properties);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //获取数据库连接池中的连接
    //若返回 null 说明获取连接失败
    public static Connection getConnection(){
        Connection conn = conns.get();

        if(conn == null){//该线程连接还未获得，需要去连接池中获取连接
            try {
                conn = dataSource.getConnection();
                //放入 ThreadLocal 供该线程后面的 jdbc 操作使用
                conns.set(conn);
                //设置为手动提交事务
                conn.setAutoCommit(false);
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        return conn;
    }

    /**
     * 提交事务，并关闭释放连接
     */
    public static void commitAndClose(){
        Connection conn = conns.get();
        if(conn != null){//若不为空，说明之前使用过连接，操作数据库

            try {
                conn.commit();//提交事务
            } catch (SQLException e) {
                e.printStackTrace();
            }finally {
                try {
                    conn.close();//关闭连接
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        //一定要执行 remove 操作（以为连接已经关闭，若不把 ThreadLocal 中的连接删除，线程还能取到该连接，但是无法连接）
        conns.remove();
    }

    /**
     * 回滚事务，并关闭释放连接
     */
    public static void rollBack(){
        Connection conn = conns.get();
        if(conn != null){//若不为空，说明之前使用过连接，操作数据库

            try {
                conn.rollback();//回滚事务
            } catch (SQLException e) {
                e.printStackTrace();
            }finally {
                try {
                    conn.close();//关闭连接
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        conns.remove();
    }
}
```

## Dao 层更改

```java
public abstract class BaseDao {

    private QueryRunner queryRunner = new QueryRunner();
	//例
    public int update(String sql, Object... args) {
        Connection conn = JdbcUtils.getConnection();
        try {
            return queryRunner.update(conn, sql, args);
        } catch (SQLException e) {
            e.printStackTrace();
            throw new RuntimeException(e);//Dao 层抛出异常让 Service 去捕获执行回滚操作
        }
    }

    ...
}
```

## 对 Servlet 调用 Service 进行 try-catch

```java
public class OrderServlet extends HttpServlet {

    private OrderService orderService = new OrderServiceImpl();

    protected void createOrder(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Cart cart = (Cart)req.getSession().getAttribute("cart");
        User loginUser = (User)req.getSession().getAttribute("user");
        if(loginUser == null){ req.getRequestDispatcher("/pages/user/login.html").forward(req,resp);
            return;
        }
        Integer id = loginUser.getId();

        //调用 orderService.createOrder(Cart, UserId) 生成订单
        String order = null;
        try {
            order = orderService.createOrder(cart, id);
            //没有异常，提交事务
            JdbcUtils.commitAndClose();
        } catch (Exception e) {
            //异常，回滚
            JdbcUtils.rollBack();
            e.printStackTrace();
        }
      
        req.getSession().setAttribute("orderId", order);
        resp.sendRedirect(req.getContextPath() + "/pages/cart/checkout.html");

    }
}
```

## Filter + ThreadLocal

使用 Filter 过滤器统一给所有的 Service 方法都加上 try-catch 方法，来进行管理。

所有调用被 Filter 拦截资源的 Servlet 若被放行则一定会执行`filterChain.doFilter();` 间接调用了 Servlet 中的方法，当然包括 Servlet 对 Service 层的调用，所以我们可以在 Filter 的 doFilter() 方法里进行 try-catch 完成对所有 Servlet 事务的提交与回滚

![](F:\java\javaweb\photo\snipaste_20220713_170721.jpg)

```xml
<filter>
    <filter-name>TransactionFilter</filter-name>
    <filter-class>com.example.book.filter.TransactionFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>TransactionFilter</filter-name>
    <!-- 管理所有事务 -->
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

```java
public class TransactionFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        try {
            filterChain.doFilter(servletRequest, servletResponse);
            //提交事务
            JdbcUtils.commitAndClose();
        } catch (Exception e) {
            //回滚事务
            JdbcUtils.rollBack();
            e.printStackTrace();
            //继续抛出异常，给 tomcat 服务器捕获处理
            throw new RuntimeException(e);
        }
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

## tomcat 管理异常

使用 tomcat 统一管理异常，展示友好的错误界面

1. Filter 中拦截异常处理完回滚事务，继续将异常抛出，让 tomcat 做后续处理，提示用户
2. 在 web.xml 中配置相应的错误跳转的错误提示页面

```xml
<!-- 错误标签配置，服务器捕获错误后，自动跳转的页面-->
<error-page>
    <!-- 错误类型 -->
    <error-code>500</error-code>
    <!-- 错误跳转页面 -->
    <location>/pages/error/error500.html</location>
</error-page>
```

---

# JSON

JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式

json 是由键值对构成的，由花括号`{}`括起来，每个键由引号`""`引起来，键与值之间使用冒号`:`进行分隔，多组键值对间使用`,`分隔。

## JSON的定义

```javascript
var jsonObj = {
    "key1":1,
    "key2":"abc",
    "key3":true,
    "key4":[11,"abcd", false],
    "key5":{
        "key5_1":12,
        "key5_2":"abc"
    },
    "key6":[{
        "key6_1_1":12,
        "key6_1_2":"abc"
    },{
        "key6_2_1":12,
        "key6_2_2":"abc"
    }]
};
```

## JSON 的访问

JSON 本身是一个对象，JSON 中的 key 访问就跟访问对象的属性一样

## JSON 的两个常用方法

json 的两种存在形式：

1. 对象的形式存在，json 对象
2. 字符串的形式存在，json 字符串

`JSON.stringify()`：将 json 对象转换为 json 字符串

`JSON.parse()`：把 json 字符串转换为 json 对象

## JSON 在 Java 中的使用

导入 JSON jar 包

1. JavaBean 和 JSON 的转换

   ```java
   public void test1(){
       Person person = new Person(1, "tony");
       //Google 提供的 jar 包 gson-2.2.4.jar
       //创建一个 Gson 实例
       Gson gson = new Gson();
       //toJson 方法可以把 Java 对象转换成 json 字符串
       String personJson = gson.toJson(person);
       System.out.println(personJson);
   
       //fromJson 吧 json 字符串转换回 java 对象
       //第一个参数是 json 字符串
       //第二参数是转换回去的 java 对象类型
       Person person1 = gson.fromJson(personJson, Person.class);
       System.out.println(person1);
   }
   ```

   ![](F:\java\javaweb\photo\snipaste_20220713_194828.jpg)

2. List 和 JSON 的转换

   法一：具体写一个类去继承 `TypeToken<T>`，帮助确认泛型

   ```java
   //Json 转换回 List 需要编写一个类去继承 Gson 包里的 TypeToken<T>，通过它的 getType() 方法来帮助确认集合内元素的类型
   public class PersonListType extends TypeToken<List<Person>> {
       //不需要任何实现
   }
   ```

   ```java
   public void test2(){
       List<Person> personList = new ArrayList<>();
       personList.add(new Person(1, "tony"));
       personList.add(new Person(2, "tom"));
   
       Gson gson = new Gson();
       //List 转换为字符串
       String personListJson = gson.toJson(personList);
       System.out.println(personListJson);
   
       //Json 转换回 List
       List<Person> list = gson.fromJson(personListJson, new PersonListType().getType());
       System.out.println(list);
       System.out.println(list.get(0));
   }
   ```

   法二：匿名内部类

   ```java
   	//匿名内部类 Json 转换回 List
   	List<Person> list = gson.fromJson(personListJson, new TypeToken<List<Person>>(){}.getType());
   ```

   ![](F:\java\javaweb\photo\snipaste_20220713_195859.jpg)

3. Map 和 JSON 的转换

   法一：

   ```java
   public class PersonMapType extends TypeToken<Map<Integer, Person>> {
   }
   ```

   ```java
   public void test3(){
       Map<Integer, Person> personMap = new HashMap<>();
       personMap.put(1, new Person(1, "tony"));
       personMap.put(2, new Person(2, "tom"));
   
       Gson gson = new Gson();
       // map 转换为 json
       String personMapJson = gson.toJson(personMap);
       System.out.println(personMapJson);
   
       // json 转换回 map
       Map<Integer, Person> map = gson.fromJson(personMapJson, new PersonMapType().getType());
       System.out.println(map);
   }
   ```

   法二：

   ```java
   	//匿名内部类 Json 转换回 Map
   	Map<Integer, Person> map = gson.fromJson(personMapJson, new TypeToken<Map<Integer, Person>>(){}.getType());
   ```

   ![](F:\java\javaweb\photo\snipaste_20220713_201923.jpg)

# AJAX

Asynchronous Javascript And Xml ：异步 Javascript  和 xml，一种创建交互式网页应用开发的网页开发技术。**是一种浏览器通过 js 异步发起的请求。==局部==更新页面的技术**

AJAX的局部更新特点

- 地址栏的地址不会改变
- 局部更新不会舍弃原来页面的内容
- 异步请求，程序不会等待请求的执行完毕再继续执行

## 原生 JavaScript 的 AJAX 请求

Servlet 端

```java
public class AJAXServlet extends BaseServlet{

    protected void javaScriptAjax(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("收到AJAX请求");
        Person person = new Person(1, "tony");
        //数据转换为 json 格式字符串
        Gson gson = new Gson();
        String personJson = gson.toJson(person);
        //设置响应头
        resp.setHeader("Access-Control-Allow-Origin", "*");
        //回送请求
        resp.getWriter().write(personJson);
    }
}
```

web

```html
<script type="text/javascript">
    function ajaxRequest() {
        //在这里实现 JavaScript 语言发起 AJAX 请求，访问服务器 AJAXServlet程序中 javaScriptAjax 方法
        //1、我们首先要创建XMLHttpRequest
        var xmlHttpRequest = new XMLHttpRequest();

        //2、调用open方法设置请求参数 (method, 地址， 是否异步)
        xmlHttpRequest.open("GET", "http://localhost:8080/project712/ajaxServlet?action=javaScriptAjax", true);

        //3、在send方法前绑定onreadystatechange事件，处理请求完成后的操作。
        xmlHttpRequest.onreadystatechange = function (){
            if(xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200){
                //JavaScript 将 json 转换回对象
                var jsonObj = JSON.parse(xmlHttpRequest.responseText);
                //把响应的数据显示在页面上
                document.getElementById("div01").innerHTML = "编号:" + jsonObj.id + "，姓名：" + jsonObj.name;
            }
        }

        //4、调用send方法发送请求
        xmlHttpRequest.send();
    }
</script>
```

## jQuery 中的 AJAX 请求

`$.ajax 方法`

![](F:\java\javaweb\photo\snipaste_20220713_220215.jpg)

```html
<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
<script type="text/javascript">
    $(function(){
        // ajax请求
        $("#ajaxBtn").click(function(){

            $.ajax({
                url:"http://localhost:8080/project712/ajaxServlet",
                //data:{action:"jQueryAjax"} 两种方式都可以
                data:"action=jQueryAjax",
                type:"GET",
                success:function (data) {
                    //指定 dataType:"text"，需要自己转换 var jsonObj = JSON.parse(data);
                    //dataType:"json" jQuery 自动转换数据
                    $("#msg").html("编号：" + data.id + "，姓名：" + data.name);
                },
                dataType:"json"
            })

        });
</script>
```

`$.get `和 `$.post`方法 两个方法的使用方式一样

```html
<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
<script type="text/javascript">
    $(function(){
        // ajax--get请求
        $("#getBtn").click(function(){

            //$.get(url, data, callback, type);
            $.get("http://localhost:8080/project712/ajaxServlet", "action=jQueryAjax", function (data){
            	$("#msg").html("$.get()方法 编号：" + data.id + "，姓名：" + data.name);
  			}, "json");

        });

        // ajax--post请求
        $("#postBtn").click(function(){
            //$.get(url, data, callback, type);
            $.post("http://localhost:8080/project712/ajaxServlet", "action=jQueryAjax", function (data){
            	$("#msg").html("$.post()方法 编号：" + data.id + "，姓名：" + data.name);
            }, "json");

        });					
    });
</script>
```

`$.getJSON`方法

```html
<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
<script type="text/javascript">
    $(function(){
        // ajax--getJson请求
        $("#getJSONBtn").click(function(){
            //$getJSON(url, data, callback);
            $.getJSON("http://localhost:8080/project712/ajaxServlet", "action=jQueryAjax", function (data){
           	 	$("#msg").html("$.getJSON()方法 编号：" + data.id + "，姓名：" + data.name);
            });
        });
</script>
```

`serialize()`表单序列化：可以把表单中所有表单项的内容都获取到，并以 `name=value&name=value`的形式进行拼接。

```html
<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
<script type="text/javascript">
    $(function(){

        $("#submit").click(function(){
            //找到我们要提交的表单，序列化
            $("#form01").serialize();
            $.getJSON("http://localhost:8080/project712/ajaxServlet", "action=jQuerySerialize&" + $("#form01").serialize(), function (data){
                $("#msg").html("$.getJSON()方法 编号：" + data.id + "，姓名：" + data.name);
            });
        });

    });
</script>
```

```html
<form id="form01" >
    用户名：<input name="username" type="text" /><br/>
    密码：<input name="password" type="password" /><br/>
</form>	
<button id="submit">提交--serialize()</button>
```

```java
protected void jQuerySerialize(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("jQuerySerialize 方法调用了");
    System.out.println("用户名：" + req.getParameter("username"));
    System.out.println("密码：" + req.getParameter("password"));

    Person person = new Person(1, "tony");
    //数据转换为 json 格式字符串
    Gson gson = new Gson();
    String personJson = gson.toJson(person);

    resp.setHeader("Access-Control-Allow-Origin", "*");
    resp.getWriter().write(personJson);
}
```

![](F:\java\javaweb\photo\snipaste_20220713_223521.jpg)



2022-7-13 完成

























