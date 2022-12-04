# BOM与DOM编程

## BOM和DOM模型

### **BOM模型**

浏览器对象模型（BOM）中定义了JS操作浏览器的接口，提供了与浏览器窗口交互的功能。

BOM是用于描述浏览器中对象与对象之间层次关系的模型，提供了独立于页面内容并能够与浏览器窗口进行交互的对象结构。

![image-20220426192950207](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220426192950207.png)

浏览器会为每一个页面自动创建window、document、location、navigator和history对象：

- window对象是BOM模型中的最高一层，通过window对象的属性和方法来实现对浏览器窗口的操作
- document对象是BOM的核心对象，提供了访问HTML文档对象的属性、方法以及事件处理
- location对象包含当前页面的URL地址，如协议、主机名、端口号和路径等信息
- navigator对象包含与浏览器相关的信息，如浏览器类型、版本等
- history对象包含浏览器的历史访问记录，如访问过的URL、访问数量等信息

### **DOM模型**

文档对象模型属于BOM的一部分，用于对BOM中的核心对象document进行操作。

HTML文档中的DOM模型如下图所示，document对象是DOM模型的根节点。

![image-20220426193305098](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220426193305098.png)

### 事件机制

JS采用事件驱动的响应机制，用户在页面上进行交互操作时会触发相应的事件。当事件发生时，系统调用JS中指定的事件处理函数进行处理。

在JavaScript中，事件分为两大类：

- 操作事件：用户在浏览器中操作所产生的事件
- 文档事件：文档本身所产生的事件，如文件加载完毕、卸载文档和文档窗口改变等事件

**操作事件**包括**鼠标事件、键盘事件和表单事件**

- 常见的鼠标事件(Mouse Events)有鼠标点击、双击、按下、松开、移动、移出和悬停等事件
- 键盘事件事件(Keyboard Events)包括按下、松开、按下后又松开等事件；
- 表单及表单元素事件(Form & Element Events)包括表单提交、重置和表单元素的改变、选取、获得焦点、失去焦点等事件



## window对象

window对象与浏览器窗口相对应。

### window对象属性

| **属 性**     | **描 述**                                            |
| ------------- | ---------------------------------------------------- |
| closed        | 只读，返回窗口是否已被关闭                           |
| defaultStatus | 可返回或设置窗口状态栏中的缺省内容  （在浏览器下面） |
| innerWidth    | 只读，窗口的文档显示区的宽度（单位像素）             |
| innerHeight   | 只读，窗口的文档显示区的高度（单位像素）             |
| name          | 当前窗口的名称                                       |
| opener        | 可返回对创建该窗口的window对象的引用                 |
| parent        | 如果当前窗口有父窗口，表示当前窗口的父窗口对象       |
| self          | 只读，对窗口自身的引用                               |
| top           | 当前窗口的最顶层窗口对象                             |
| status        | 可返回或设置窗口状态栏中显示的内容                   |

**示例：**

```html
<script type="text/javascript">
window.defaultStatus="漫步时尚广场，休闲娱乐一体的综合性广场。";
function changeStatus(){
	window.status="漫步时尚广场，不一样的广场！";
}
function getWidthAndHeight(){
	alert("当前窗口的宽度："+window.innerWidth
		+",高度："+window.innerHeight);
}
</script>
```

### window对象的方法

| **方 法**                  | **描 述**                                        |
| -------------------------- | ------------------------------------------------ |
| open()                     | 打开一个新的浏览器窗口或查找一个已命名的窗口     |
| close()                    | 关闭浏览器窗口                                   |
| setTimeout(code,millisec)  | 在指定的毫秒数后调用函数或计算表达式，仅执行一次 |
| setInterval(code,millisec) | 按照指定的周期（以毫秒计）来调用函数或计算表达式 |
| clearTimeout()             | 取消由setTimeout()方法设置的计时器               |
| clearInterval()            | 取消由setInterval()设置的计时器                  |
| prompt()                   | 显示可提示用户输入的对话框                       |



#### open方法

open()方法用于打开一个新窗口。

```js
var targetWindow=window.open(url,name,features,replace)
```

参数features用于设置窗口在创建时所具有的特征，如标题栏、菜单栏、状态栏、是否全屏显示等特征。

| **窗口特征** | **描 述**                                                    |
| ------------ | ------------------------------------------------------------ |
| channelmode  | 是否使用channel模式显示窗口，取值范围yes\|no\|1\|0，默认为no |
| directories  | 是否添加目录按钮，取值范围yes\|no\|1\|0，默认为yes           |
| fullscreen   | 是否使用全屏模式显示浏览器，取值范围yes\|no\|1\|0，默认为no  |
| location     | 是否显示地址栏，取值范围yes\|no\|1\|0，默认为yes             |
| menubar      | 是否显示菜单栏，取值范围yes\|no\|1\|0，默认为yes             |
| resizable    | 窗口是否可调节尺寸，取值范围yes\|no\|1\|0，默认为yes         |

| **窗口特征** | **描 述**                                                |
| ------------ | -------------------------------------------------------- |
| scrollbars   | 是否显示滚动条，取值范围yes\|no\|1\|0，默认为yes         |
| status       | 是否添加状态栏，取值范围yes\|no\|1\|0，默认为yes         |
| titlebar     | 是否显示标题栏，取值范围yes\|no\|1\|0，默认为yes         |
| toolbar      | 是否显示浏览器的工具栏，取值范围yes\|no\|1\|0，默认为yes |
| width        | 窗口显示区的宽度，单位是像素                             |
| height       | 窗口显示区的高度，单位是像素                             |
| left         | 窗口的y坐标，单位是像素                                  |
| top          | 窗口的x坐标，单位是像素                                  |

**示例：**

```html
<script type="text/javascript">
var newWindow=window.open("http://www.itshixun.com","弹出广告窗",
"width=400,height=300,toolbar=no,menubar=no,location=no,status=no,resizable=yes");
</script>
```



#### setTimeout()方法

setTimeout()方法用于设置一个计时器，在指定的时间间隔后调用函数或计算表达式，且仅执行一次。

```js
var id_Of_timeout=setTimeout(code,millisec)
```

- 参数code必需，表示被调用的函数或需要执行的JavaScript代码串
- 参数millisec必需，表示在执行代码前需等待的时间（以毫秒计）
- code代码仅被执行一次
- setTimeout()方法返回一个计时器的ID



#### clearTimeout()方法

clearTimeout()方法用于取消由setTimeout()方法所设置的计时器。

```js
function openWin(){
	myWindow=window.open('','','width=200,height=100');
	myWindow.document.write("This is 'myWindow'");
}
function moveWin(){
	x+=10;
	y+=10;
	myWindow.moveBy(x,y);
	timer=setTimeout("moveWin()",1000);
}
function stopMove(){
	clearTimeout(timer);
}
function closeWin(){
	myWindow.close();
}
```





## location对象

location对象是window对象的子对象，用于提供当前窗口或指定框架的URL地址。

### location对象的属性

location对象中包含当前页面的URL地址的各种信息，例如：协议、主机服务器和端口号等。

| **属性** | **描 述**                                            |
| -------- | ---------------------------------------------------- |
| protocol | 设置或返回当前URL的协议                              |
| host     | 设置或返回当前URL的主机名称和端口号                  |
| hostname | 设置或返回当前URL的主机名                            |
| port     | 设置或返回当前URL的端口部分                          |
| pathname | 设置或返回当前URL的路径部分                          |
| href     | 设置或返回当前显示的文档的完整URL                    |
| hash     | URL的锚部分（从#号开始的部分）                       |
| search   | 设置或返回当前URL的查询部分（从问号?开始的参数部分） |

**例如：**当URL为http://192.168.1.252:8080/test/locationProperty.html?name=guoqy#myAnchor时， location对象中的属性取值如图所示。

![image-20220426201643699](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220426201643699.png)

### location对象的方法

location对象提供了以下三个方法，用于加载或重新加载页面中的内容：

- assign(url)：可加载一个新的文档，与location.href实现的页面导航效果相同

- reload(force)：用于重新加载当前文档；

- replace(url)：使用一个新文档取代当前文档，且不会在history对象中生成新的记录。



## history对象

history对象用于保存用户在浏览网页时所访问过的URL地址

- length属性表示访问历史记录列表中URL的数量。

由于隐私方面的原因，JavaScript不允许通过history对象获取已经访问过的URL地址

history对象提供了back()、forward()和go()方法来实现针对历史访问的前进与后退功能

| **方法**     | **描 述**                          |
| ------------ | ---------------------------------- |
| back()       | 可加载历史列表中的前一个URL        |
| forward()    | 可加载历史列表中的后一个URL        |
| go(n \| url) | 可加载历史列表中的某个具体的页面； |



## navigator对象

navigator对象中包含浏览器的相关信息，如浏览器名称、版本号和脱机状态等信息。

| **方法**      | **描 述**                                                    |
| ------------- | ------------------------------------------------------------ |
| appName       | 可返回浏览器的名称，如：Netscape、Microsoft  Internet Explorer等 |
| appVersion    | 可返回浏览器的平台和版本信息                                 |
| platform      | 声明了运行浏览器的操作系统和（或）硬件平台，如“Win32”、“MacPPC”等 |
| userAgent     | 声明了浏览器用于HTTP请求的用户代理头的值，由navigator.appCodeName的值之后加上斜线和navigator.appVersion的值构成的 |
| onLine        | 声明了系统是否处于脱机模式                                   |
| cookieEnabled | 浏览器启用了cookie时返回true，否则返回false                  |



## document对象

document对象是window对象的子对象，是指在浏览器窗口中显示的内容部分。

### document对象的属性

| **属 性**    | **描 述**                                                    |
| ------------ | ------------------------------------------------------------ |
| body         | 提供对body元素的直接访问                                     |
| cookie       | 设置或查询与当前文档相关的所有cookie                         |
| referrer     | 返回载入当前文档的文档URL                                    |
| URL          | 返回当前文档的URL                                            |
| lastModified | 返回文档最后被修改的日期和时间                               |
| domain       | 返回下载当前文档的服务器域名                                 |
| all[]        | 返回对文档中所有HTML元素的引用，all[]已经被documen对象的getElementById()等方法替代 |
| forms[]      | 返回对文档中所有的form对象集合                               |
| images[]     | 返回对文档中所有的image对象集合，但不包括由<object>标签内定义的图像 |

#### cookie属性

- cookie是浏览器在客户端保存的与服务器端的会话信息，该信息允许服务器端访问
- cookie本质上是一个字符串

```js
document.cookie=cookieStr;
```

- cookie本身有一定的大小限制，每个cookie所存放的数据不能超过4KB
- cookie是由一些键值对（cookieName-value）构成；根据cookieName来检索cookie中信息，包括expires、path和domain等信息
- 一般情况下，cookie信息都没有经过编码；当cookie中包含空格、分号、逗号等特殊符号时，需要使用escape()函数进行编码；当从cookie中取出数据时，需要使用unescape()函数进行解码



### document对象的方法

document对象的方法从整体上分为两大类：

- 对文档流的操作
- 对文档元素的操作

| **方 法**                | **描 述**                                                    |
| ------------------------ | ------------------------------------------------------------ |
| open()                   | 打开一个新文档，并擦除当前文档的内容                         |
| write()                  | 向文档写入HTML或JavaScript代码                               |
| writeln()                | write()方法作用基本相同，在每次内容输出后额外加一个换行符（\n），在使用\<pre>标签时比较有用 |
| close()                  | 关闭一个由document.open()方法打开的输出流，并显示选定的数据  |
| getElementById()         | 返回对拥有指定ID的第一个对象                                 |
| getElementsByName()      | 返回带有指定名称的对象的集合                                 |
| getElementsByTagName()   | 返回带有指定标签名的对象的集合                               |
| getElementsByClassName() | 返回带有指定class属性的对象集合，该方法属于HTML5 DOM         |
| querySelector()          | 返回满足条件的单个元素；当满足条件有多个时只返回第一个元素   |
| querySelectorAll()       | 返回满足条件的元素集合                                       |



#### write()和writeln()方法

- write()和writeln()方法都是用于向文档流中输出内容；
- 当输出内容为纯文本时，将在页面中直接显示；
- 当输出内容为HTML标签时，由浏览器解析后并进行显示。
- writeln()与write()基本相同，区别在于writeln()每次输出结果之后额外加一个换行符（\n）。页面中的换行通常使用\<br/>标签而非换行符（\n），换行符仅在\<pre>标签中起作用。

#### querySelectorAll()方法

是HTML 5中新引入的方法，返回指定CSS选择器的元素集合

```js
var span=document.querySelector("#menuDiv"); 
var span=document.querySelector(".filmClass");	
var span=document.querySelectorAll(".baseClass");
```



##  Form对象

- Form对象是document对象的子对象，通过Form对象可以实现表单验证等效果
- 通过Form对象可以访问表单对象的属性及方法

