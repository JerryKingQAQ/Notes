# JavaScript语言基础

## 1.使用形式

### 1.行内Javascript脚本

```html
<p onclick="alert('你点击了第一个自然段')">第一个自然段</p>
<a href="javascript:alert('你点击了超链接')" >超链接</a>
```

### 2.内部Javascript脚本

将这些JavaScript脚本提取出来统一放在**script**标签中。

```html
<body>
    <script type="text/javascript">
        alert("body中的JavaScript");
    </script>
</body>
```

### 3.外部Javascript脚本

从外部.js文件中导入。

```html
<script type="text/javascript" src="js/test.js"></script>
```



## 2.语法格式

### 变量

#### 定义

JavaScript中的变量是弱数据类型
在声明变量时不需要指明变量的数据类型，通过关键字var进行声明；

```javascript
var 变量1[, 变量2, ...];
```



#### 申明提前

JavaScript 局部变量有一个很重要的概念，叫**申明提前**，我们先来看一个例子。  

```javascript
var wholeVar = 1;    // 全局变量  
function myTest() {  
  console.log(wholeVar);  
  var wholeVar = 2;  
  console.log(wholeVar);  
}  
```

关于第三行的输出，你的第一反应一定是1吧，正确答案是undefined。这是因为在函数内部，**变量不论在何处申明，都应该看成是在最开始申明**（赋值不会看成是在最开始赋值，这就是不输出2的原因），这就是“申明提前”，所以，以上代码等价于：

```javascript
var wholeVar = 1;  
function myTest() {  
    var wholeVar;    // 申明提前了，覆盖了全局变量  
    console.log(wholeVar);    // 上面只申明，没赋值  
    wholeVar = 2;  
    console.log(wholeVar);  
}  
```



### 实参对象

JavaScript一切都是对象，实参也是一个对象，有一个专门的名字arguments，这个对象可以看成一个数组（类数组，不是真的数组），实参从左到右分别是arguments[0]、arguments[1]...，arguments.length表示实参的个数。

```javascript
//求参数的和  
function getSum() {  
    var aLength = arguments.length;  
    var sum = 0;  
    for(var i = 0;i < aLength;i++) {  
        sum += arguments[i];  
    }  
    return sum;  
}  
console.log(getSum(1,2,3,4,5))//输出15  
```



##### 函数对象作为另一个函数的参数

一个函数（为方便行文，称为a函数）可以作为另外一个函数（称为b函数）的参数，b函数最终可以返回一个具体的值。

从原理上来说，b函数在自己的函数体内调用了a函数，所以需要把a函数的名字作为实际参数传递给b函数。如下：

```javascript
function getMax(a,b) {  
    return a>b?a:b;  
}  
//求最小值  
function getMin(a,b) {  
    return a<b?a:b;  
}  
//下面这个函数以函数作为参数，并最终返回一个值  
function getM(func,num1,num2) {  
    return func(num1,num2);  
}  
getM(getMax,1,2);//返回2  
getM(getMin,1,2);//返回1  
```



## 3.函数

常用函数：

| **函数**     | **描 述**                                                    |
| ------------ | ------------------------------------------------------------ |
| parseInt()   | 将字符串转换成整型                                           |
| parseFloat() | 将字符串转换成浮点型                                         |
| isNaN()      | 测试是否不是一个数字（全称：is not a number）当参数是一个数字时，返回一个false；否则返回true |
| isFinite()   | 测试是否是一个无穷。如果是，返回一个false，否则返回true      |
| escape()     | 将字符转换成Unicode码                                        |
| unescape()   | 解码由escape函数编码的字符                                   |
| ev           | 将JavaScript中的字符串作为脚本代码来执行                     |
| alert()      | 显示一个提醒对话框，包括一个OK按钮                           |
| confirm()    | 显示一个确认对话框，包括OK和Cancel按钮                       |
| prompt()     | 显示一个输入对话框，提示等待用户输入                         |



### 1.命名函数的定义

计算各数位之和。

```html
<script type="text/javascript">
    function input(){
        return window.prompt("Please input a number:");
    }

    function count(data){
        var sum=0;
        for(var i in data){
            sum = sum + parseInt(data[i]);
        }
        return sum;
    }

    var data = input();
    var sum = count(data);
    alert(data+"中各位数字之和"+sum);
</script>
```





### 2.匿名函数的定义

匿名函数的定义格式与命名函数基本相同，只是没有提供函数的名称，且在函数结束位置以分号（；）结束。
由于没有函数名字，所以需要使用变量对匿名函数进行接收，方便后面函数的调用。

```html
<script type="text/javascript">	
    var f=function(user){
		alert("欢迎"+user+"来到漫步时尚广场");
    }
    var test=f;
    f("admin");
    test("admin");
</script>
```

test和f的效果完全一样。



### 3.对象函数的定义

JavaScript还提供Function类，用于定义函数。

```javascript
var funcName=new Function([parameters],statements;);
```

例如：

```html
<script type="text/javascript">	
	var showInfo=new Function("name","age","authority","address",
	   "alert('数据处理中……');"+
	   "return( '姓名：'+name+'，年龄：'+age+'，权限：'+authority+'，地址：'+address);");
	alert(showInfo("guoqy",30,"管理员","青岛"));
</script>
```



### 4.自调用函数

自己调用自己。

```javascript
(function([parameters]){
	statementes;
	[return 表达式];
}) ([params]);
```

parameters是形参，params是实参



## 4.数据类型转换

### 字符串转整数

#### parseInt()方法

使用parseInt()方法，参数为字符串，结果为该字符串转换而来的整数；
parseInt()还可以有第二个参数，表示**待转换字符串的进制**。

**规则：**

如果字符串的首字符不是一个数字，转换失败，返回 NaN ；否则，转换到字符串中第一个不是数字的字符为止，即，遇到字母、小数点下划线等字符立即停止转换。
需要注意的是，16 进制的符号**0x不会让转换停止**。



#### Number()方法

使用Number()转换一个字符串，这个字符串**必须是**只含有数字的字符串，即数字的字符串形式。

因为对于12a3这种含有字母等非数字字符的字符串，Number()会报错。



### 字符串转小数

与整数相同，字符串转小数也有两种方式parseFloat()和Number()。

#### parseFloat()方法

parseFloat()方法只转换到字符串中第一个不是数字的字符为止，当然这个字符不包括第一个小数点。

```javascript
parseFloat("12");    // 返回12  
parseFloat("12.2a");    // 返回12.2  
parseFloat("12.2.2");    // 返回12.2，第二个小数点会让转换停止  
parseFloat(null);    // 返回0  
```



### 数字转字符串

**toString()**实现一般的数字转字符串，**String()**则是强制类型转换。

toString()括号内有一个可选的参数，指以几进制的形式转换该字符串，如数字12调用toString(16)得到的结果就是 C ，即12的16进制表示方式。

String()可以转换 null 和 undefined，而toString()不可以。

```javascript
var myNum = 15;  
console.log(myNum.toString());    // 输出"15"  
console.log(myNum.toString(16));    // 输出"F"  
console.log(String(myNum));    // 输出"15"  
```



### 布尔型与其他类型的相互转换

布尔型的值只有两个 true 和 false。转换规则：  

- 布尔型转为字符串直接就是字符串 true 或者 false ；
- 布尔型中的 true 转换为数字 1，布尔型中的 false 转换为数字 0;
- 数字 0 、 null、 undefined、空字符串转换为布尔型的 false，其他所有都是转换为 true。

#### Boolean()方法

使用Boolean()方法可以实现其他类型转换成布尔型。

```javascript
var myBool = ture;  
myBool.toString();    // 返回"true"  
Number(true);    // 返回1  
Boolean("js");    // 返回true  
Boolean("");    // 返回false  
```

注意，上面讲的空字符串是""，而不是空格字符串" "，这两个不同，后者双引号之间有一个英文字符的大小的空位，他们转为布尔型的结果不同：  

```javascript
Boolean("");    // 返回false  
Boolean(" "); // 返回true  
```



### 隐式转换

JavaScript 是一种弱类型语言，不同类型的变量在运算符的作用下会发生类型转换。这个是编译环境下直接进行的，所以叫隐式类型转换。下面是一些转换规则：  

- +运算的两个操作数是**数字**和**字符串**，数字会被转换为字符串；
- +运算的两个操作数是**数字**和**布尔型**，布尔型会被转换为数字；
- +运算的两个操作数是**字符串**和**布尔型**，布尔型会被转换为字符串；
- 减、乘、除、取余运算会把**其他类型转换为数字**；
- if 括号中**单独的一个变量**会被转换为**布尔型**。



## JavaScript错误

`JavaScript`代码在运行过程中，可能会因为很多原因出现错误，如：语法错误、用户输入错误等。发生错误后不能置之不理，要进行处理。为可能的错误提前在代码中制定解决方案。

### try-catch捕获和处理错误

用法如下：

```
try {  
    //运行时可能出错的代码  
}catch(err) {  
    //处理出现的错误  
}  
```

`JavaScript`在运行时抛出的错误或者异常，会被`catch`语句捕捉到，其中的变量`err`包含了错误的有关信息。

```
try {  
    console.lo("JavaScript");  
}catch(err) {  
    window.alert("发生错误，错误信息："+err.message);  
}  
console.log("错误已处理完毕。");  
```

第二句有语法错误，被`catch`捕捉到，错误信息`console.lo is not a function`通过弹窗告知用户。用户点击弹窗上的确定后，程序继续往下运行。

如果没有进行错误处理，程序在第二句停止运行，这样后面的所有代码都不再执行。

##### 创建自定义错误

`console.lo is not a function`显然是一个系统内置的错误类型，如果用户觉得这样的错误类型不够具体，可以自定义错误类型：

```
throw exception;  
```

`exception`可以是字符串、数字、逻辑值或者对象，这样的错误也会被`catch`语句块捕获。

```
//求开方的值  
function mySqrt(a) {  
    try {  
        if(a < 0)  
            throw new Error("错误！负数不能开平方");  
        if(a > 10000)  
            throw new Error("错误！不支持大数开平方");  
        return Math.sqrt(a);  
    } catch(err) {  
        console.log("发生错误，错误信息："+err.message);  
    }  
    return "error";  
}  
```

`new Error()`是一个`Error`对象，括号内的参数是`err.message`属性的值。比如`a`是`-2`，抛出第一个自定义异常，并在`catch`块中输出异常的信息，函数最后返回`error`。
