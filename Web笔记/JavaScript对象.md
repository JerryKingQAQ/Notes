

# JavaScript对象

## Array数组对象

### 数组对象的构建

#### 字面量方式

```javascript
var b = [1,true,2];
```

#### new方式

通过数组的构造函数**Array()**来创建一个数组对象。

```javascript
new Array();
new Array(size);
new Array(element0, element1, ..., elementN);
```

使用无参数构造函数创建数组时会返回一个空数组，数组长度为0。

**例子：**

```javascript
var goodsTypes = new Array();
goodsTypes[0]="男装";
window.alert(goodsTypes[0]);
```

**注意：**

当把构造函数当作函数调用，不使用new运算符时，其行为与使用new运算符调用时的行为完全一致。



### 数组对象的属性

Array对象的属性包括constructor、length和prototype。

| 属性        | 描述                             |
| ----------- | -------------------------------- |
| constructor | 返回对创建此对象的构造函数的引用 |
| length      | 数组的长度                       |
| prototype   | 对对象添加属性和方法             |

**例子：**

```javascript
var movies=new Array("分歧者2:绝地反击","疯狂的麦克斯：狂暴之路",
				"复仇者联盟2:奥创纪元","飓风营救4");
				
if(movies.constructor==String){
		alert("movies是个字符串对象");
}else if(movies.constructor==Array){
	   alert("movies是个数组对象，数组中元素的个数是："+movies.length
		+"\n------------------------\n"+movies.constructor);
}else if(movies.constructor==Date){
		alert("movies是个日期对象");
	}
```



### 数组对象的常用方法

| **方 法** | **描 述**                                                  |
| --------- | ---------------------------------------------------------- |
| concat()  | 用于连接两个或多个数组                                     |
| join()    | 用于把数组中的所有元素放入一个字符串，并用指定的分隔符隔开 |
| push()    | 可向数组的末尾添加一个或多个元素，并返回新的长度           |
| pop()     | 用于删除并返回数组的最后一个元素                           |
| shift()   | 用于删除并返回数组的第一个元素                             |
| reverse() | 在原有数组的基础上，颠倒数组中元素的顺序，不会创建新的数组 |
| slice()   | 可从已有的数组中返回选定的元素                             |
| sort()    | 用于对数组的元素进行排序                                   |
| splice()  | 向数组中添加或删除一个或多个元素，然后返回被删除的元素     |

 

#### 查找元素的位置

根据值查找元素的位置，有两个方法：`indexOf()`和`lastIndexOf()`，前者从索引小处往大搜索，后者相反。都返回第一次遇到该元素时的索引。

两者都有两个参数，第一个参数为要查找的元素，第二个参数可选，为搜索的起点索引。如：

```javascript
var search = ["a","b","a","b","c","d","a","a","b","a"]; console.log(search.indexOf("a"));//输出0  
console.log(search.lastIndexOf("a"));//输出9  
console.log(search.indexOf("a",2));//输出2，从索引为2处开始搜索  
```

第二个参数可以是负数，`-1`表示倒数第一个元素，`-2`表示倒数第二个元素，依次类推。如：

```
var search = ["a","b","a","b"];  
console.log(search.indexOf("a"，-3));//输出2  
console.log(search.lastIndexOf("a"，-3));//输出0
```

#### 数组的合并

`concat()`实现数组合并，其形式是`数组a.concat(数组b)`，合并之后返回新数组，新数组为数组`a`后面连接数组`b`，但是数组`a`和`b`不变。

```
var a = [1,2,3];  
var b = [4,5,6];  
var c = a.concat(b);//合并后返回新数组  
console.log(c);//输出[1,2,3,4,5,6]  
```

#### 数组倒置

`reverse()`实现数组倒置，无参数，返回倒置后的数组，同时调用该方法的数组也会被倒置。称为就地逆置。

```
var a = [1,2,3,4];  
var b = a.reverse();  
console.log(a);//输出[4,3,2,1]  
console.log(b);//输出[4,3,2,1]  
```

#### 元素合并

`join()`将数组的所有元素连接起来组成字符串，参数为元素之间的分隔符，默认逗号。

```
var sArray = ["June","July","August"];  
console.log(sArray.join());//输出June,July,August  
console.log(sArray.join("+"));//输出June+July+August  
```

#### 元素排序

`sort()`实现数据元素排序，不带该参数表示元素按照`ASCII`表从小到大排序（参考`JavaScript`学习手册三）。如：

```
var stringArray = ["a","ab","b","aa"];  
stringArray.sort();  
console.log(stringArray);//输出["a","aa","ab","b"]  
```

需要注意的是数字的排序，例子如下：

```
var arr = [1,2,10,5,12];  
arr.sort();  
console.log(arr);//输出[1,10,12,2,5];  
```

带参数的格式如下：  

```
arr.sort(function(a,b){  
            return a-b;  //升序排列  
})  
```

或者：

```
arr.sort(function(a,b){  
            return b-a;  //降序排列  
})  
```

说明：  

- `arr`是要排序的数组；
- `a`，`b`是两个参数，返回`a-b`，升序排列，返回`b-a`，降序排列。

对于数字的排序，`sort()`带参数和不带参数是不一样的，例子如下：

```
var arr = [1,2,10,5,12];  
arr.sort();  
console.log(arr);//输出[1,10,12,2,5]  
arr.sort(function(a,b){  
     return a-b;  
});  
console.log(arr);//输出[1,2,5,10,12]  
```

#### 提取子数组

`slice()`返回切割出的子数组，不修改原来的数组。

它有两个整数参数`a`和`b`，`a`表示切割的起点，该点属于子数组；`b`可选，表示切割的终点，该点不属于子数组。

`a`和`b`都可以为负数，如`-1`表示倒数第一个位置，依次类推。

```javascript
var arr = ["a","b","c","d","e"]; console.log(arr.slice(0,3));//["a","b","c"] 
console.log(arr.slice(0,-2));//["a","b","c"] 
console.log(arr.slice(4)); //["e"]  
console.log(arr.slice(-4));//["b","c","d","e"]  
```



#### join()方法

join()方法用于把数组中的所有元素放入一个字符串中，并通过指定的分隔符隔开。

```javascript
arrayObject.join(separator);
```

- separator是可选的，作为数组元素之间的分隔符，默认为逗号。

- join()方法的返回形式是字符串。



#### splice()方法

splice()方法用于向数组中添加1~n个元素或从数组中删除元素。

```
arrayObject.splice(index,howmany,[item1,.....,itemX]);
```

- 参数index必须，规定添加或删除元素的位置。当为负数时从末尾计数；
- 参数howmany必需，表示要删除元素的数量，0代表不删除数据；
- 参数列表item1, ..., itemX可选，表示向数组中添加或替换的新元素；
- 该方法在原数组基础上实现，不会生成新的副本数组。



### 二维数组

在JavaScript中，没有二维或多维数组，不能通过new Array()()方式来创建二维数组。
通过在一维数组中存放另一个数组，来模拟实现二维数组。

数组中可以包含不同的数据类型。

```javascript
var array=new Array();
array[0]=new Array("科幻","《2012》",80);
array[1]=["爱情","《何以笙箫默》",6];
array[2]="从1992年到2012年这二十年是本次太阳纪的最后一个周期…";
array[3]=88;
```



## String字符串对象

### 字符串的创建

字符串对象的创建有以下两种方式：字面量方式和new方式

#### 字面量方式

在Javascript中，可以隐式地将一个字符串转换成字符串对象。

```javascript
var name="漫步时尚广场";		//类型为string类型
var address='中国·青岛·高新区';		//类型为string类型
```

使用单引号（'）或双引号（"）均可生成一个字符串。

#### new方式

new方式创建字符串对象是通过调用**String()**构造函数来完成，并返回一个String对象。

```javascript
var movieName=new String("何以笙箫默");	//类型为String对象
var director=String("刘俊杰");		//类型为string类型
```

在JavaScript中，string和String的区别如下：

- String是string的包装类；
- string是一种基本的数据类型，没有提供substring()等方法；
- String是构造函数用于创建字符串对象，使用new创建的对象具有substring()等方法；
- string没有提供prototype原型对象，而String对象具有prototype原型对象，通过浏览器的端点调试方式进行查看该区别；
- 使用typeof()函数查看类型时，string变量返回“string”，String对象返回“Object”，而String返回“function”；
- 使用= =比较时，string类型判断其值是否相等，而String对象则判断是否对同一对象进行引用；
- 二者的生命周期不同，使用new创建的对象一直存在，而string类型自动生成的会在代码执行后立即销毁。



### 字符串对象的方法

| **方法**                             | **描 述**                                                    |
| ------------------------------------ | ------------------------------------------------------------ |
| indexOf(searchValue,[fromIndex])     | 返回searchValue在字符串中首次出现的位置                      |
| lastIndexOf(searchValue,[fromIndex]) | 从后向前进行检索，返回searchValue在字符串中首次出现的位置    |
| slice(start,[end])                   | 抽取从start开始（包括start）到end结束（不包括end）为止的所有字符 |
| substring(start,[stop])              | 抽取从start处到stop-1处的所有字符                            |
| split()                              | 用于把一个字符串分割成字符串数组                             |



#### indexOf()方法

indexOf()方法用于检索子串在字符串中首次出现的位置。

```
stringObject.indexOf(searchValue,[fromIndex])
```

- 参数searchValue表示被检索的子串
- 参数fromIndex可选，表示字符串开始检索的位置，取值范围0~stringObject.length-1，默认值为0
- 当检索到子串时，返回子串在字符串中的位置；否则返回-1
- 字符串的开始下标是从0开始的



#### lastIndexOf()方法

lastIndexOf()方法用于**从后向前**对字符串进行检索，并返回子串在字符串中首次出现的位置。



#### slice()方法

slice()方法用于从字符串中抽取一部分内容。

```
stringObject.slice(start,[end])
```

- 抽取范围从start位置开始（包括start）到end结束（不包括end）
- 参数start必选，表示要抽取子串的起始下标
- 参数end可选，表示要抽取子串的结束下标；当参数end省略时，表示提取范围从start位置到字符串的结尾
- start和end允许取负数；-1表示字符串的最后一个字符，-2表示倒数第二个字符，其他以此类推



#### substring()方法

```
stringObject.substring(start,[stop])
```

- substring()方法与slice()方法相似，也是从字符串中抽取一部分
- 与slice()方法不同，substring()方法不接受负参数



#### split()方法

split()方法用于把一个字符串分割成一个字符串数组。

```
stringObject.split(separator,[howmany])
```

- 参数separator（必需）是一个字符串或正则表达式，使用该参数指定的规则对字符串进行分割；
- 参数howmany可选，用于指定返回的数组的最大长度；当参数howmany存在时，返回的子串个数不应大于howmany；当参数howmany省略时，对整个字符串进行分割，而不考虑结果的数量



#### charAt()

`charAt()`作用是返回调用者指定位置的字符，位置从`0`计数：

```javascript
var str = "abcdefg";  console.log(str.charAt(0));//输出a  
console.log(str.charAt(str.length-1));//输出g  
```



#### 转义字符

| **转义字符** | **实现方式** | **转义字符** | **实现方式** |
| ------------ | ------------ | ------------ | ------------ |
| 双引号       | \"           | 换行         | \n           |
| 单引号       | \'           | 回车         | \r           |
| Tab          | \t           | 反斜杠       | \\           |
| 退格         | \b           | 换页符       | \f           |



## Date日期对象

JavaScript通过日期对象（Date）来操作日期和时间。通过日期对象的构造函数创建一个系统当前时间或指定时间的日期对象。

```javascript
var myDate1=new Date();
var myDate2=new Date(1218253167595);
var myDate3=new Date(2015,9,2);
	
var myDate4=new Date(2015,9,2,12,08,16);
var myDate5=new Date("9/25/2015 9:25:38");
var myDate6=new Date("April 25,2048");
var myDate7=new Date("Apr 25,2048 17:32:16");
```

| **方法**      | **描 述**                      |
| ------------- | ------------------------------ |
| getDate()     | 返回一个月中的某一天(1~31)     |
| getDay()      | 返回一周中的某一天(0~6)        |
| getMonth()    | 返回月份(0~11)                 |
| getFullYear() | 返回4位数字的年份              |
| getHours()    | 返回Date对象的小时(0~23)       |
| getMinutes()  | 返回Date对象的分钟(0~59)       |
| getSeconds()  | 返回Date对象的秒数(0~59)       |
| getTime()     | 返回1970年1月1日至今的毫秒数   |
| setXxx()      | 用于设置日期对象的年月日等信息 |

### 常用方法

#### setFullYear()

setFullYear()方法用于设置年份（包括月份和日期）。

```
dateObject.setFullYear(year[,month[,day]])
```

#### setHours()

setHours()方法用于设置指定时间的小时（包括分钟、秒、毫秒）。

```
dateObject.setHours(hour[,min,sec,millisec])
```



## Math数学对象

数学对象（Math）提供了一些数学运算中的常数及数学计算方法，在数学运算时非常有用。
与String、Date不同，Math对象**没有提供构造方法**，可以直接使用Math对象。
在Math对象中，提供了一些常用的数学常数，如圆周率、自然对数的底数等。

| **属性** | **描 述**                                      |
| -------- | ---------------------------------------------- |
| E        | 返回算术常量e，即自然对数的底数（约等于2.718） |
| LN2      | 返回2的自然对数（约等于0.693）                 |
| LN10     | 返回10的自然对数（约等于2.302）                |
| LOG2E    | 返回以2为底的e的对数（约等于1.442）            |
| LOG10E   | 返回以10为底的e的对数（约等于0.434）           |
| PI       | 返回圆周率（约等于3.14159）                    |
| SORT2    | 返回2的平方根（约等于1.414）                   |
| SQRT1_2  | 返回2的平方根的倒数（约等于0.7071）            |

**示例代码：**

```javascript
var num=10;
        document.write("随机生成"+num+"个整数：");
		var array=[];
		var maxNum=0;
		var minNum=0;
		for(var i=0;i<num;i++){
			var tmp=Math.random()*100
			array[i]=Math.floor(tmp);
			document.write(array[i]+"\t");	
			if(i==0){
				maxNum=array[0];
				minNum=array[0];	
			}else{
				maxNum=Math.max(maxNum,array[i]);
				minNum=Math.min(minNum,array[i]);
			}
		}
		document.write("<br/>随机数中的最大数为："+maxNum);
		document.write("<br/>随机数中的最小数为："+minNum);
		document.write("<hr/>");
		var randomNum=60+Math.random()*40;
		document.write("随机生成一个60~100之间的数："+randomNum);
		document.write("<br/>round()四舍五入的结果："+Math.round(randomNum));
		document.write("<br/>ceil()上取整的结果："+Math.ceil(randomNum));
		document.write("<br/>floor()下取整的结果："+Math.floor(randomNum));
		document.write("<hr/>");
		document.write("2的3次幂："+Math.pow(2,3));
		document.write("<br/>16的平方根："+Math.sqrt(16));
		document.write("<br/>90<sup>o</sup>的正弦值是："+Math.sin(90*Math.PI/180));
```

![image-20220418144918573](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220418144918573.png)



## RegExp正则表达式对象

正则表达式（Regular Expression）最早出现于20世纪40年代，在数学与计算机科学理论中用于反映“正则性”的数学表达式特征。直到70年代末，才真正在程序设计领域中得到应用。

正则表达式是一种**字符串匹配的模式**，通过单个字符串来描述和匹配一系列符合某个句法的规则。JavaScript提供了一个RegExp对象来完成有关正则表达式的匹配功能。

正则表达式类似于通配符，是计算机帮助人们去匹配指定规则的字符串。

### 对象创建

创建一个RegExp对象有两种方式：直接量方式和构造函数方式。

```javascript
var reg=/pattern/attributes;		                     //直接量方式
var regExp=new RegExp(pattern,attributes);		//构造函数方式
```

- 参数pattern是一个字符串或表达式，表示正则表达式的模式；
- 参数attributes是一个可选的字符串，取值包括"g"、"i"和"m"，分别用于指定**全局匹配**、**区分大小写的匹配**和**多行匹配**。



### 常用元字符

正则表达式中的pattern部分可以包括**元字符**、**括号表达式**以及**量词**等。

| **元字符** | **描 述**                                          |
| ---------- | -------------------------------------------------- |
| .          | 用于查找单个字符，除了换行和行结束符               |
| \w         | 匹配包括下划线的任何单词字符，  等价于[A-Za-z0-9_] |
| \W         | 匹配任何非单词字符，等价于[ ^A-Za-z0-9_]           |
| \d         | 查找数字                                           |
| \D         | 查找非数字字符                                     |
| \s         | 查找空白字符                                       |
| \S         | 查找非空白字符                                     |
| \n         | 查找换行符                                         |
| \r         | 查找回车符                                         |
| \xxx       | 查找以八进制数xxx规定的字符                        |
| \xdd       | 查找以十六进制数dd规定的字符                       |



| **表达式**        | **描 述**                    |
| ----------------- | ---------------------------- |
| [abc]             | 查找括号内的任意字符         |
| [ ^abc]           | 查找除了括号内的其他任意字符 |
| [0-9]             | 查找0-9之间的任意数字        |
| [a-z]             | 查找a-z之间的任意字符        |
| [A-Z]             | 查找A-Z之间的任意字符        |
| [A-z]             | 查找A-z之间的任意字符        |
| (boy\|girl\|baby) | 查找括号内的某一项（或关系） |



| **量词** | **描 述**                               |
| -------- | --------------------------------------- |
| n+       | 匹配任何包含至少一个n的字符串           |
| n*       | 匹配任何包含零个或多个n的字符串         |
| n?       | 匹配任何包含零个或一个n的字符串         |
| n{x}     | 匹配包含x个n的序列的字符串              |
| n{x,y}   | 匹配包含x或y个n的序列的字符串           |
| n{x,}    | 匹配包含至少x个n的序列的字符串          |
| n$       | 匹配任何结尾为n的字符串                 |
| ^n       | 匹配任何开头为n的字符串                 |
| ?=n      | 匹配任何其后紧接指定字符串n的字符串     |
| ?!n      | 匹配任何其后没有紧接指定字符串n的字符串 |



### 重复

通过前面的学习，我们可以编写一些简单正则表达式，比如两个连续的数字可以表示为`[0-9][0-9]`，但是，这种方法有一个问题：比如手机号码的正则表达式，用`11`个连续的`[0-9]`写起来容易错，且不具有可读性。正则表达式用重复解决了这个问题。

#### 重复

**重复**表示指定的字符或者字符串（本关可以简单理解为前面**紧邻**的字符）可以连续出现多次。比如匹配含有`100`个字母`a`的字符串，在这个字符串中，`a`连续出现`100`次，用正则表达式表示为：

```
var pattern = /a{100}/;//匹配100个连续的字母a组成的字符串  
```

有多种表示重复的方法：

- `{a,b}`中的`a`和`b`都是数字，表示前面的字符至少出现`a`次，最多出现`b`次；

```
var pattern = /at{1,2}/;//表示a后面最少一个t，最多两个t  pattern.test("at");//true  pattern.test("att");//true  pattern.test("am");//false  
```

- `{a,}`表示前面的字符至少出现`a`次，最多不限制；

```
var pattern = /[0-9]{4,}/;//匹配最少四个数字  pattern.test("1234");//true  pattern.test("1");//false  
```

- `{a}`表示前面的字符出现`a`次；

```
var pattern = /[a-z]{1}/;//匹配单个小写字母  pattern.test("r");//true  pattern.test("12R");//false  
```

- `?`，表示前面的字符出现一次或者不出现，等价于`{0,1}`；

```
var pattern = /A[0-9]?A/;//匹配两个A之间有0或1个数字  pattern.test("AA");//true  pattern.test("A0A");//true  pattern.test("A01A");//false  
```

- `+`，表示前面的字符至少出现一次，等价于`{1,}`；

```
var pattern = /js+/;//匹配j后面最少一个s  pattern.test("jsjs");//true  pattern.test("java");//false  
```

- `*`，表示前面的字符至少出现`0`次，等价于`{0,}`；

```
var pattern = /A[0-9]*B/;//匹配A和B之间为空或者只有数字  pattern.test("AB");//true  pattern.test("A1B");//true  pattern.test("AaB");//false  
```

需要特别注意的是，至少出现`0`次，就是说这个字符**可以不出现**，比如正则表达式`[0-9]{0,}`和字符串`hello`是匹配的，这里特别容易出错。

总结一下重复匹配的用法，如下：

| 表达式 | 匹配                     | 等价于 |
| ------ | ------------------------ | ------ |
| {a,b}  | 至少出现a次，最多出现b次 |        |
| {a,}   | 至少出现a次              |        |
| {a}    | 出现a次                  | {a,a}  |
| +      | 最少出现一次             | {1,}   |
| ?      | 出现一次或者不出现       | {0,1}  |
| *      | 至少出现0次              | {0,}   |

#### 转义

相信细心的读者已经发现了一个问题：对于`?`、`+`等表示特殊含义的字符，如何实现字面量匹配呢？就是说如何匹配他们本来的含义呢？

在`JavaScript`中，使用`\`实现特殊符号的普通化，又叫做转义：

```
var pattern1 = new RegExp("\?");//匹配一个问号  
var pattern2 = /\+{4}/;//匹配四个加号 
```



### 匹配

考虑这样一种情况，判断一个字符串是否为合法的`JavaScript`变量名，变量名必须以字母、`$`或者`_`开头，这个时候要用到正则表达式中指定匹配位置的功能。

#### 指定匹配位置

`^`用来匹配字符串的开头，比如:

```
var startPattern = /^[0-9]/;//匹配以数字开头的字符串  console.log(startPattern.test("1aa"));//true  console.log(startPattern.test("a11"));//false  
```

注意，`^`符号在中括号的**外面**！不要与`[^0-9]`混淆，后者匹配非数字字符。

`$`用来匹配字符串的结尾，比如：

```
var endPattern = /ing$/;//匹配以ing结尾的字符串  console.log(endPattern.test("playing"));//true  console.log(endPattern.test("going first"));//false  
```

`\b`用来匹配单词的边界，那么什么是单词的边界？

   ![img](https://data.educoder.net/api/attachments/189326)  

图片中蓝色的线指示了单词的边界，实际上就是英文字母和非英文字母（如空格符）之间的界限。

```
var boundaryPattern = /\bOK\b/;//匹配单词OK  console.log(boundaryPattern.test("OK"));//true  console.log(boundaryPattern.test("rewa OK de"));//true  console.log(boundaryPattern.test("sa,OK"));//true  console.log(boundaryPattern.test("OKNot"));//false  
```

简单来说，`\b`表示**英文字母**和**非英文字母**之间的界限，这个界限不占用字符的位置。

`\B`用来匹配非单词的边界，与上面的`\b`相反。

```
var pattern = /\Bed/;//ed左侧不能是单词的边界  console.log(pattern.test("played"));//true  console.log(pattern.test("edu"));//false  
```



### 修饰符

修饰符用来描述一些整体的匹配规则，有`i`、`g`、`m`三种。

修饰符需要放在`//`符号之后，如果通过新建`RegExp`对象定义正则表达式，则修饰符作为第二个参数。比如：

```
var pattern1 = /^java/m;  var pattern2 = new RegExp("^java","m");  
```

#### 不区分大小写

`i`表示整个的匹配过程中不考虑单词的大小写。如：

```
var pattern = /^edU/i;  console.log(pattern.test("edu"));//输出true  console.log(pattern.test("Edu"));//输出true  console.log(pattern.test("EDUCoder"));//输出true  
```

#### 全局匹配

`g`表示执行**全局匹配**，即找出所有满足匹配的子字符串。比如，已知`match()`函数返回由匹配结果组成的数组，如果没有匹配到返回`null`。

不用`g`修饰时：

```
var pattern = /[a-z]/;//匹配小写字母  console.log("a1b2c3".match(pattern));//输出["a", index: 0, input: "a1b2c3"]  
```

显然，只匹配到了第一个小写字母`a`。

##### 用`g`修饰时：

```
var pattern = /[a-z]/g;//全局匹配小写字母  console.log("a1b2c3".match(pattern));//输出["a", "b", "c"]  
```

三个小写字母都被匹配到了，这就是所谓的全局匹配。

#### 多行模式

有的时候，需要匹配的字符串很长，分为很多行（即中间有换行符号）。

`m`在多行模式中执行匹配，即：符号`^`不仅匹配整个字符串的开头，还匹配每一行的开头，`&`不仅匹配整个字符串的结尾，还匹配每一行的结尾。

```
var pattern = /[0-9]$/m;//多行匹配以数字结尾的字符串  var string = "1\nhello";//字符串在两行，中间的\n是换行符  console.log(pattern.test(string));//输出true  
```

如果没有`m`修饰，将会输出`false`，因为这种情况下`$`不会和换行符`\n`匹配。



## 自定义对象

用户还可以自定义对象，定义对象有五种方式：

- ​	原始方式
- ​	构造函数方式
- ​	原型方式
- ​	混合方式
- ​	JSON方式

### 原始方式

使用原始方式创建一个JavaScript对象，步骤如下：

```javascript
var object = new Object();
object.porpertyName = value;
object.methodName = functionName | function(){};
```

- 使用Object类创建一个对象object；
- propertyName表示为object对象添加属性名
- methodName表示为object对象添加方法名

**示例：**

```javascript
var goods=new Object();
goods.name="男士白领衬衣";
goods.type="男装";
goods.price="580";
goods.color="white";

goods.showInfo=function(){
	alert("商品名称："+goods.name+"\n商品类型："+goods.type+"\n商品价格："
		+goods.price+"\n商品颜色："+goods.color);
}

goods.showColor=showColor;
function showColor(){
	alert("商品颜色："+goods.color);
}
```



### 构造函数方式

通过构造函数创建一个JavaScript对象，步骤如下：

- 创建构造函数
- 用new运算符和构造函数来创建一个对象

```javascript
function ClassName([param1][,param2]...){
	this.propertyName=value;
	//其他属性...
	this.methodName=functionName | function (){...};
	//其他方法...
}
```

**示例：**

```javascript
//创建构造函数
function Goods(name,type,price,color){
}
Goods.name=name;
Goodstype=type;
Goods.price=price;
Goods.color=color;

Goods.showInfo=function(){
	alert("商品名称："+this.name+"\n商品类型："+this.type+"\n商品价格："
		+this.price+"\n商品颜色："+this.color);
};
//创建一个对象
var goods =new Goods("Nick","Shoes",1200,"White");
//方法的调用
goods.showInfo();
```



### 原型方式

当我们创建一个函数时，函数就会自动拥有一个`prototype`属性，这个属性的值是一个对象，这个对象被称为该函数的原型对象。也可以叫做`原型`。

这种方法是对使用构造函数创建对象的改进，使用构造函数创建一个对象时，会把构造函数中的方法（上面的构造函数只有属性的键值对，没有方法）都创建一遍，浪费内存，使用原型不存在这个问题。

```
object.prototype.name = value;
```

**示例：**

```javascript
//创建构造函数
function Goods(){
}
Goods.prototype.name="耐克运动鞋";
Goods.prototype.type="鞋类";
Goods.prototype.price=1200;
Goods.prototype.color="白色";

Goods.prototype.showInfo=function(){
	alert("商品名称："+this.name+"\n商品类型："+this.type+"\n商品价格："
		+this.price+"\n商品颜色："+this.color);
};
//创建一个对象
var goods=new Goods();
//方法的调用
goods.showInfo();
```



### 混合方法

使用原型方式创建对象时，对象属性值采用默认值，在对象创建完成后再去改变属性的值。而构造方式在创建对象时，会重复生成方法所引用的函数。在实际应用中，将两者混合使用。

```javascript
//创建构造函数
function Goods(name,type,price,color){
	this.name=name;
	this.type=type;
	this.price=price;
	this.color=color;
}
//原型方式添加方法
Goods.prototype.showInfo=function(){
	alert("商品名称："+this.name+"\n商品类型："+this.type+"\n商品价格："
		+this.price+"\n商品颜色："+this.color);
};
//创建对象实例
var goods1=new Goods("男士衬衣","男装",200,"白色");
var goods2=new Goods("女士花裙","女装",700,"红色");
//方法的调用
goods1.showInfo();
goods2.showInfo();
```



### JSON方式

- JSON（JavaScript Object Notation）是一种基于ECMAScript的轻量级数据交换格式，采用完全独立于语言的文本格式，能够以更加简单的方式来创建对象
- 使用JSON方式无需构造函数和new关键字，直接创建所需的JavaScript对象即可
- JSON对象是以“{”开始，以“}”结束，且属性与属性值成对出现

```javascript
{
    //对象的属性部分
    propertyName:value,
    //对象的方法部分
    methodName:function(){...}
};
```

**示例：**

```javascript
//创建对象实例
var goods={
	name:"男士衬衣",
	type:"男装",
	price:200,
	color:"白色",
	showInfo:function(){
		alert("商品名称："+this.name+"\n商品类型："+this.type+"\n商品价格："
			+this.price+"\n商品颜色："+this.color);
	},
	showColor:function(){
		alert("商品颜色："+this.color);
	}
};
//方法的调用
goods.showInfo();
```

在数据传输过程中，JSON数据往往以字符串的形式进行传输，所以在页面中需要通过

- 1.将JSON字符串转成JSON对象前，需在JSON字符串两侧添加一对括号“（）”
- 2.使用eval()方法将该字符串强制转换成JSON对象

```javascript
//JSON字符串
var movieStr='{'
	+'name:"小时代",'
	+'type:"爱情",'
	+'price:80,'
	+'showInfo:function(){'
	       +'document.write("影片名称："+this.name+",影片类型："+this.type+",票价："+this.price);'
	+'}'
+'}';
//eval()转换
var movie=eval("("+movieStr+")");
//对象方法的调用
movie.showInfo();
```

**Function对象方式**

```JavaScript
//JSON字符串
var movieStr='{'
	+'name:"小时代",'
	+'type:"爱情",'
	+'price:80,'
	+'showInfo:function(){'
	           +'document.write("影片名称："+this.name+",影片类型："+this.type+",票价："+this.price);'
	+'}'
+'}';
//1.Function对象方式，自调用函数的方式
var movie=(new Function("","return "+movieStr))();
movie.showInfo();
//2.分解写法，与上面写法完全等价
var movieFunction=new Function("","return "+movieStr);
var otherMovie=movieFunction();
otherMovie.showInfo();
```



## 属性的增删查改

在`Java`中，当实体类建立以后，类的属性只能获取与修改，不能增加与删除。但是因为`JavaScript`是动态类型的语言，`JavaScript`中对象的属性具有增删改查所有的操作。

### 属性的获取

#### 方式一

属性的获取有两种方式，一种是使用`.`符号，符号左侧是对象的名字，符号右侧是属性的名字，如下：

```
var student = {name:"Alice",gender:"girl"};  console.log(student.name);//输出Alice  
```

这种情况下属性名必须是静态的字符串，即不能是通过计算或者字符串的拼接形成的字符串。

#### 方式二

另外一种是使用`[""]`符号，符号的左边是对象的名字，双引号中间是属性的名字，这种情况下属性名可以是一个表达式，只要表达式的值是一个字符串即可。如下：

```
var student = {name:"Alice",gender:"girl"};  console.log(student["name"]);//输出Alice  
```

有两种情况必须使用第二种方式：

- 属性名含有空格字符，如`student["first name"]`，这时不能用`student.first name`代替，编译器无法解释后者；
- 属性名动态生成，比如用`for`循环获取前端连续`id`的值，这种`id`名之间一般有特定关系。如下面的例子：

```
for(int i = 0;i < 5;i ++) {      console.log(student["id"+i]);  }  
```



## 属性的检测和枚举

### 属性的检测

属性的检测指检查对象是否有某个属性或者方法，需要使用运算符`in`，`in`的左侧是属性或者方法名，右侧是检查对象，对象有该属性或者方法则返回`true`，否则返回`false`，如下：

```JavaScript
var school = {  
    name:"SJTU",  
    location:"ShangHai",  
    studentNum:40000,  
    display:function() {  
          console.log(this.name);  
    }  
};  
//检测属性  
console.log("name" in school);//输出true  
console.log("sales" in school);//输出false  
//检测方法  
console.log("display" in school);//输出true  
console.log("print" in school);//输出false  
```

这里的属性名是**字符串**，**必须用双引号包含在内**。

还可以用`hasOwnProperty()`检测对象是否具有某个自有属性或方法。括号内的参数是属性或者方法的名字。

所谓自有属性或者方法，是指对象自己定义的属性或者方法，而不是从原型链上继承来的。

### 属性的枚举

定义：属性的枚举指按顺序逐个的列出属性的名字。如下面的例子：

```JavaScript
var person = {  
    name:"Ye",  
    gender:"Gril",  
    age:23,  
    salary:23000,  
    height:1.78  
}  
```

根据前面的知识，我们知道对象`person`有五个属性，所谓枚举，就是依次列出这五个属性的名字，即：`name、gender、age、salary、height`，至于它们排列的顺序，在不同的浏览器中的结果不同，这里不讨论。

在继续下面的知识点之前，首先要知道一个概念：可枚举性（`enumerable`），这是对象的属性的一个性质，用户自己定义的属性默认为可枚举，系统内置的对象的属性默认为不可枚举。

枚举属性有三种方法：

- `for...in...`循环；可以枚举所有**可枚举**的属性，包括继承的属性。如下：

  ```JavaScript
  //首先定义一个school对象，它从原型链上继承的属性都是不可枚举的，而下面自定义的四个属性或者方法都是可枚举的  
  var school = {  
    name:"SJTU",  
    location:"ShangHai",  
    studentNum:40000,  
    display:function() {  
          console.log(this.name);  
    }  
  };  
  //枚举school的属性  
  //下面的圆括号中的att表示对象的属性，school表示对象  
  for(var att in school) {  
    //依次输出name,location,studentNum,display  
    console.log(att);  
  }  
  ```

  圆括号里面的表达式中，`att`表示对象的属性`school`表示该对象，这个循环将依次遍历对象的所有可枚举属性，每次输出一个属性的值。

- `Object.getOwnPropertyNames()`；   括号中有一个参数，是要枚举的对象。该表达式将返回对象的所有自有属性的名字，**不区分是否可枚举**，结果以字符串数组的形式呈现，如下：  

  ```JavaScript
  //定义一个school对象  
  var school = {  
    name:"SJTU",  
    location:"ShangHai",  
    studentNum:40000,  
    display:function() {  
          console.log(this.name);  
    }  
  };  
  //为school对象增加一个不可枚举的属性range  
  Object.defineProperty(school, "range", {  
    value: 4,//设置range属性的值  
    enumerable: false//设置range属性为不可枚举  
  });  
  //输出["name","location","studentNum","display","range"]  
  console.log(Object.getOwnPropertyNames(school));  
  ```

  如果用上面的`for...in...`循环，`range`属性是不能够枚举到的。

- `Object.keys()`；   括号中有一个参数，是要枚举的对象。该表达式返回可枚举的自有属性，以字符串数组的形式。所以这里对属性的要求更加严格，既要求是自有属性，又要求可枚举。  

  ```JavaScript
  var school = {  
    name:"SJTU",  
    location:"ShangHai",  
    studentNum:40000,  
    display:function() {  
          console.log(this.name);  
    }  
  };  
  //为school对象增加一个不可枚举的属性range  
  Object.defineProperty(school, "range", {  
    value: 4,//设置range属性的值  
    enumerable: false//设置range属性为不可枚举  
  });  
  //输出["name","location","studentNum","display"]  
  console.log(Object.keys(school));  
  ```

总结一下上面三个方法对属性是否自有，是否可枚举的要求：

| 方法名                       | 是否要求可枚举 | 是否要求自有 |
| ---------------------------- | -------------- | ------------ |
| for...in...                  | 是             | 否           |
| Object.getOwnPropertyNames() | 否             | 是           |
| Object.keys()                | 是             | 是           |



## JSON对象

`JSON`既然是用来传递数据的，必然要先存储数据，存储数据需要采用一定的数据格式，`JSON`常用的数据格式有`JSON`对象、`JSON`数组和`JSON`字符串。

##### 什么是JSON对象

`JSON`对象（通常叫`JSON`）是一种文本数据的交换格式，用于存储和传输数据。示例如下：

```
{"name":"Jerry", "age":15}
```

这就是一个简单的`json`对象，它的规则是：

- 数据以**键/值对**的形式存在；
- 数据之间用逗号间隔；
- 大括号表示保存对象；
- 方括号表示保存数组。

##### JSON对象与Javascript对象的区别

在实训四里面，我们讲过`JavaScript`中的自定义对象。而`JSON`是基于`JavaScript`语法的，所以`JSON`中也有对象的概念，但是和`JavaScript`中的对象有一些小的区别。

定义一个`JavaScript`对象：

```js
var myObject = {  
    id:1,  
    name:"Peter Bruce",  
    "first name":"Bruce",  
    display:function() {  
                console.log(this.name);  
            }  
}  
```

定义一个`JSON`对象：

```
{"id":1,"name":"Peter Bruce","first name":"Bruce"}  
```

三点区别：

- `JSON`对象的属性名（`key`）必须被包含在双引号之中，而`JavaScript`对象除了有空格的属性名、中间有连字符`-`的属性名必须在双引号之中外，其它随意；
- 不能在`JSON`对象中定义方法，而在`JavaScript`对象中可以；
- `JSON`对象可以被很多语言操作，而`JavaScript`对象只有`JS`自己可以识别。

**定义JSON对象**的方法如下：用一个`{}`包含在内，内部是若干个属性名和属性值构成的键值对，键值对之间用`,`隔开，属性名和属性值之间用`:`隔开，属性值可以是以下任意一种数据类型的数据：数字、字符串、`JSON`数组、`JSON`对象、`null`。如：

```
 {"a":1,"b":2.12,"c":true,"d":"string","e":null};  
```

属性值是`JSON`数组或者`JSON`对象的情况稍复杂，后面的关卡将介绍。

##### 在JavaScript中使用JSON对象

支持`JSON`的语言都能够使用`JSON`对象，这里仅介绍在`JavaScript`中如何使用`JSON`对象。

- 在`JavaScript`中定义一个`JSON`对象：

```
var jsonObject = {"name":"js","number":2};  
```

- 操作属性，使用`.`或者`[]`：  

  ```
  console.log(jsonObject.name);//读属性，输出js  console.log(jsonObject["name"]);//读属性，输出js  jsonObject.name = "javascript";//写属性，给name属性赋值javascript  
  ```

- 删除属性，使用`delete`：  

  ```
  var jsonObject = {"name":"js","number":2};  
  delete jsonObject.name;//删除name属性  
  ```

- 遍历属性，使用`for-in`循环：  

  ```
  var jsonObject = {"name":"js","number":2};  
  for(att in jsonObject) {  
    console.log(jsonObject[att]);//依次输出js、2  
  } 
  ```



### JSON字符串

在前端和后台之间传递数据可以使用`JSON`，但是实际上传递的是`JSON`字符串，而`JSON`对象是不可以直接进行传递的。

##### JSON字符串

`JSON`字符串就是在`JSON`对象两边套上`'`形成的字符串，如：

```
var JSONString1 = '{"k1":"v1","k2":"v2"}';  
console.log(JSON.parse(JSONString1));//输出Object {k1: "v1", k2: "v2"}  
```

上面的`JSONSring1`就是`JSON`字符串，可以直接从前端传到后台或者后台传到前端。

当`JavaScript`收到从后台传来的`JSON`字符串后，怎么把它变成`JSON`对象方便处理呢？

##### JSON字符串到JavaScript对象

`JSON.parse(a,b)`方法将`JSON`字符串`a`转换为`JavaScript`对象。`b`是一个可选的函数参数。

```
var JSONString1 = '{"k1":"v1","k2":"v2"}';  console.log(JSON.parse(JSONString1));//输出Object {k1: "v1", k2: "v2"}  
```

函数参数`b`按从里到外的顺序作用在对象的所有属性上，最后一个作用的是对象本身：

```js
//对象的每一个属性的值加1  
var text = '{ "key1":1, "key2":2, "key3":2.2}';  
var obj = JSON.parse(text, function (key, value) {  
    if(key === '')//当遇到对象本身时，不进行加1操作  
        return value;  
    return value+1;//对属性值加1  
});  
console.log(obj);//输出Object {key1: 2, key2: 3, key3: 3.2}  
```

如上面所示，函数的参数有两个，其中`key`表示属性的名字，`value`表示属性的值，当遇到对象本身时，`key`的值为`''`，即空字符串。

##### JSON对象转换为JSON字符串

`JSON.stringify(a,b,c)`，`a`是待转换的`JSON`对象，`b`和`c`为可选参数。

```
var JSONObject = {"k1":"v1","k2":"v2"};  JSON.stringify(JSONObject);//JSON对象转换为JSON字符串  
```

参数`b`为函数时，该函数按照从里到外的顺序处理`JSON`对象的每一个属性，最后一个处理的是`JSON`对象本身，处理完后再转为`JSON`字符串：

```js
//对象的所有属性值加1，再转为字符串  
var JSONObject = {"k1":1,"k2":2.2};  
var JSONString = JSON.stringify(JSONObject,function(k,v){  
    if(k === '')//处理到了JSON对象本身  
        return v;  
    return v+1;//所有的属性的值加1  
});  
console.log(JSONString);//输出{"k1":2,"k2":3.2}  
```

参数`b`还可以是数组，数组存储的是属性的名字，用来指定只转换哪些属性：

```js
//转换对象中特定的属性  
var JSONObject = {"k1":1,"k2":2.2,"k3":3};  
var JSONString = JSON.stringify(JSONObject,["k1","k2"]);  
console.log(JSONString);//输出{"k1":1,"k2":2.2} 
```

这里简单介绍一下`c`：

```js
var str = ["name":"Tom","age":16];  
var obj1 = JSON.stringify(str);  
var obj2 = JSON.stringify(str,null,4);
console.log(obj1);  //输出{"name":"Tom","age":16}
console.log(obj2); //输出  
//{  
//    "name": "Tom",  
//    "age": 16  
//}  
```

参数`c`：文本添加缩进、空格和换行符，如果 `c` 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 `c` 大于 `10`，则文本缩进 `10` 个空格。
