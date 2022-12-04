# JavaScript事件处理

## 注册事件处理程序

页面上的每一个元素，会发生几种不同的事件，比如表单元素，可能会发生提交事件，也可能发生重置事件，我们需要为每一个事件绑定一个事件处理程序，也叫为事件注册事件处理程序。

下面是三种注册事件处理程序的方法。

##### 为JavaScript对象设置一个函数

页面上的元素对应一个`JavaScript`对象，元素的每一个事件对应对象的一个属性，比如：

```js
<form id="myForm"></form>  
var myForm = document.getElementById("myForm");  
```

`myForm`对应页面中`id`值为`myForm`的表单，`myForm.onsubmit`对应表单提交事件，`myForm.onreset`对应表单重置事件。通过为这些属性设置一个函数类型的值，实现事件处理程序的注册：

```js
//为表单提交事件注册处理程序  
myForm.onsubmit = function() {  
    console.log("表单提交的事件处理程序");  
}  
//为表单重置事件注册处理程序  
myForm.onreset = function() {  
    console.log("表单重置的事件处理程序");  
}  
```

##### 设置HTML标签属性的值为事件处理程序

比如，设置`form`标签的`onsubmit`属性的值为事件处理程序：

```js
<form onsubmit="submitForm()"></form>  
function submitForm() {  
    console.log("表单提交的事件处理程序");  
}  
```

这样提交表单时，就会触发`submitForm()`函数。

##### 调用addEventListener()函数

页面元素对应的`JS`对象，通过调用`addEventListener()`函数也可以注册事件处理程序，函数的第一个参数是事件的类型，第二个参数是事件处理程序：

```js
<form id="myForm"></form>  
var myForm = document.getElementById("myForm");  
myForm.addEventListener("submit",function() {  
    console.log("表单提交中");  
});  
```

`submit`表示这是一个表单提交事件，后面的匿名函数即表单提交的事件处理程序。



## 文档加载事件

文档，指的是网页上的所有元素构成的一种格式化文本。文档加载事件指浏览器从服务器下载并渲染完文档后发生的事件。

文档加载事件名字为`load`。

##### 文档加载事件

当文档加载完成后，就会触发文档加载事件监听程序（即上一关所说的事件处理程序），一般我们会在这个时候监测用户浏览器的类型、版本，从而加载不同的脚本。

在大多数情况下，文档记载事件绑定在`body`元素上，表示网页主体加载完成后触发该事件，也有少数情况下绑定在`image`等元素上，表示相关的元素加载完成后触发该事件。

文档加载完成后监测用户的浏览器类型并在控制台打印：

```js
<body onload="detectBrowser()"></body>  
function detectBrowser(){  
    var userAgent = navigator.userAgent; //取得浏览器的userAgent字符串  
    if (userAgent.indexOf("Opera") > -1) {//判断是否是Opera浏览器  
        console.log("Opera");  
    };  
    if (userAgent.indexOf("Firefox") > -1) { //判断是否是Firefox浏览器  
        console.log("Firefox");  
    }  
    if (userAgent.indexOf("Chrome") > -1) { //判断是否是Chrome浏览器  
        console.log("Chrome");  
    }  
    if (userAgent.indexOf("Safari") > -1) {//判断是否是Safari浏览器  
        console.log("Safari");  
    }  
    if (userAgent.indexOf("compatible") > -1 && userAgent.indexOf("MSIE") > -1) {  
        console.log("IE");  
    };  
}  
```



## 鼠标事件

鼠标是计算机最常见的外设之一，鼠标事件指用户操作鼠标的过程中触发的事件。

##### 常见的鼠标事件

说到鼠标事件，最常见的无非是鼠标单击事件`click`，很多按钮都会绑定一个`onclick()`函数，表示当用户单击鼠标后会执行的函数。其实还有很多鼠标事件，比如双击鼠标、按下鼠标等，下面是一个总结：

| 类型      | 事件处理函数 | 触发条件         |
| --------- | ------------ | ---------------- |
| click     | onclick      | 按下并且释放鼠标 |
| dbclick   | ondbclick    | 双击鼠标         |
| mousedown | onmousedown  | 按下鼠标按键     |
| mouseup   | onmouseup    | 释放鼠标按键     |
| mousemove | onmousemove  | 移动鼠标         |
| mouseover | onmouseover  | 鼠标进入元素     |
| mouseout  | onmouseout   | 鼠标离开元素     |

为页面上的某一个元素绑定一个鼠标事件，当用户在该元素上**用鼠标**执行了**指定的动作**后，就会触发指定的鼠标事件处理程序，开始执行函数。

##### 鼠标的按下和释放

`mousedowm`表示鼠标按下的事件，`onmousedown`是用户按下鼠标后会触发的事件处理程序；`mouseup`表示鼠标按键释放的事件，`onmouseup`表示用户释放鼠标按键后会触发的事件处理函数。

下面是一个例子，页面上有一行文字“点我”，用户在文字上按下鼠标按键后，文字会变成“鼠标已经按下”，而用户释放鼠标后，文字会变成“鼠标已经释放”。

`html`代码如下：

```html
<body>  
    <p id="p" onmousedown="downfunc()" onmouseup="upfunc()">  
	 点我  
    </p>  
</body>  
```

页面的效果如下：

   ![img](https://data.educoder.net/api/attachments/207158)  

事件处理函数的代码如下：

```js
function downfunc() {  
    document.getElementById("p").innerText = "鼠标已经按下";  
}  
function upfunc() {  
    document.getElementById("p").innerText = "鼠标已经释放";  
}  
```

用户在文字上面先按下鼠标，再释放鼠标，效果如下：

   ![img](https://data.educoder.net/api/attachments/209397)****



键盘事件，是指用户敲击键盘上的按键所代表的事件。

键盘事件有三种：

- 按键按下：`keydown`，用户按下键盘上的键；
- 按键释放：`keyup`，用户释放按键；
- 点击按键：`keypress`，用户按下并且释放了按键。

##### 点击按键

`keypress`表示用户点击某个按键的事件，该事件会触发`onkeypress()`事件处理程序，`onkeypress()`有一个`event`参数，其中`event.which`表示点击的按键的编码。这个编码是该按键的`unicode`编码。

需要注意的是，按下键盘上的`A`时，`keyCode`值是`a`的编码，只有同时按下`shift`和`A`，`keyCode`的值才是`A`的编码。

下面是一个例子，当用户点击键盘上的按键时，会打印出该按键的编码值：

```html
<body onkeypress="keyEvent(event)">  
    <p>  
        keypress event  
    </p>  
</body>  
<script>  
    function keyEvent(event) {  
        console.log("编码是:"+event.which);  
    }  
</script>  
```

比如我们按下`B`时，控制台如下：

   ![img](https://data.educoder.net/api/attachments/207343)  

同时按下`B`和`shift`，控制台如下：

   ![img](https://data.educoder.net/api/attachments/207344)  

##### 按下按键

`keydown`表示用户按下按键，同上面一样，它也有一个`event.which`表示按下的按键的编码。

```html
<body onkeydown="downEvent(event)">  
</body>  
<script>  
    function downEvent(event) {  
        console.log("编码是:"+event.which);  
    }  
</script>  
```

如果你按下按键后没有释放，控制台将会一直进行打印，比如按下的是`1`，控制台的打印结果如下：

   ![img](https://data.educoder.net/api/attachments/208872)  

灰色的数字`20`表示这条信息已经打印了`20`次。

##### 释放按键

`keyup`表示用户释放按键，可以有一个参数`event`，`event.which`表示释放的按键的编码。

```html
<body onkeyup="upEvent(event)">  
</body>  
<script>  
    function upEvent(event) {  
        console.log("编码是:"+event.which);  
    }  
</script>  
```

比如，当用户按下`1`时，控制台没有输出，释放`1`后，控制台输出如下：

   ![img](https://data.educoder.net/api/attachments/208873)



## 表单事件

表单，即`form`，是页面最基本的元素之一，通常，用户的输入会放置在表单里面，然后提交给后台。

`form`有很多子元素，分别表示不同类型的用户输入：例如`input`表示文本等类型；`select`表示下拉列表；`button`表示按钮。

这些子元素可以被绑定一些事件，比如`change`表示用户的输入发生了改变。这些事件是表单元素特有的。

##### change事件

`change`事件表示当前元素**失去焦点**并且元素的**内容发生了改变**。失去焦点，指光标不在该元素上，比如光标本来在文本输入框里面，当用户在页面的其他地方点击了鼠标，文本框就会失去焦点。

下面是一个例子：当用户输入文本，并且鼠标点击页面上的其他地方后，我们将在控制台打印出用户的输入。

```html
<body>  
    <form>  
        <input id="t1" type="text" onchange="changeEve()"/>  
    </form>  
    <script>  
        function changeEve() {  
            var e = document.getElementById("t1");  
            console.log(e.value);  
        }  
    </script>  
</body>  
```

比如当用户输入`I changed`后，在页面的其他地方点击鼠标，控制台如下：

   ![img](https://data.educoder.net/api/attachments/207359)  

##### select事件

`select`事件：文本框中的文本被用户选中时发生。

只能作用在`<input type="text">`的文本框里面，可以用`window.getSelection().toString()`获取选择的文本。

下面的例子：当用户选择了一段文本后，我们在控制台打印出用户选择的文本：

```html
<body>  
    <input type="text" value="赵钱孙李，周吴郑王" onselect="selectEve()"/>  
    <script>  
        function selectEve() {   
            console.log(window.getSelection().toString());  
        }  
    </script>  
</body>  
```

比如我们选择了`郑王`，然后松开鼠标，控制台的输出如下：

   ![img](https://data.educoder.net/api/attachments/208547)  

##### submit事件

表单的提交事件。

表单里面包含了用户输入的信息，最终要传到后台的服务器进行处理，这样就有一个表单的提交过程，`submit`即表单提交事件。

通常情况下，在`submit`的事件处理函数中，校验用户的输入是否符合要求，比如密码的长度够不够。

下面的例子，用户提交表单时，用`js`校验用户输入的密码长度是否达到`6`位。

```html
<body>  
    <form onsubmit="subEve()">  
        <input type="password" id="pw"/>  
        <input type="submit" value="提交" />  
    </form>  
    <script>  
    function subEve() {  
        var content = document.getElementById("pw").value;  
        if (content.length < 6) {  
            window.alert("密码不可以小于6位");  
        }  
    }  
    </script>  
</body>  
```

这时，用户在密码输入框输入`123`，点击提交，页面会弹出一个警告框如下：

   ![img](https://data.educoder.net/api/attachments/208549)

## 拖动事件

##### 元素的拖放

鼠标指向元素，按下鼠标，然后移动鼠标到另一个地方释放，即拖动元素。

相比`html4`以及之前的版本，`html5`增加了一个全新的属性`draggable`，表示元素是否支持拖动，默认的情况下，图片和超链接元素是支持拖动的，其他元素不支持。

将元素的`draggable`属性设置为`true`，即表示元素支持拖动。如：下面设置了`p`元素支持拖动：

```html
<p id="p1" draggable="true">  
    元素支持鼠标的拖动  
</p>  
```

也可以用下面的`JavaScript`代码设置`p`为可拖动的：

```js
document.getElementById("p1").draggable = true;  
```

##### ondrag

`ondrag()`是元素正在拖动时触发的事件处理程序。如果元素一直在拖动的过程中，`ondrag()`会每隔`350ms`被触发一次，比如，在下面的例子中，我们一直在拖动`p`元素，控制台会一直打印拖动的信息：

```html
<body>  
    <div>  
        <p ondrag="dragging(event)" draggable="true">拖动我!</p>  
    </div>  
    <script>  
    function dragging(event) {  
        console.log("正在拖动");  
    }  
    </script>  
</body> 
```

拖动不放下，控制台如下：

   ![img](https://data.educoder.net/api/attachments/208647)  

`111`表示这条信息已经打印了`111`次。

##### ondragstart

用户开始拖动元素时触发，可以带有一个`event`参数，其中的`event.target`表示拖动的元素，比如，下面的例子中，用户开始拖动元素时，触发了`ondragstart`程序，我们尝试打印一下`event.target`的内容：

```html
<body>  
    <p ondragstart="dragStart(event)"  draggable="true">拖动我!</p>  
    <script>  
        function dragStart(event) {  
            console.log(event.target);  
            console.log("你要拖动的文本的内容是："+event.target.innerText);  
        }  
    </script>  
</body>  
```

拖动文本，效果如下：

   ![img](https://data.educoder.net/api/attachments/208652)  

第一行是要拖动的文本元素，第二行显示了文本里面的内容。



## 事件冒泡

##### 文档树

在前面的学习中，我们说过，文档元素之间有层次关系，比如：  

```html
<body>  
    <div onclick="clickParent()">  
        <p onclick="clickChild()">点我</p>  
        <p id="p">content</p>  
    </div>  
    <script>  
        function clickChild() {  
               console.log("子");  
        }  
        function clickParent() {  
               console.log("父");  
        }  
</script>  
</body>  
```

对应这样一个模型：

   ![img](https://data.educoder.net/api/attachments/208773)  

其中，箭头的方向是子节点的方向，而反过来则是父节点的方向。比如，两个`p`元素的父节点（父元素）都是`div`元素。

##### 事件冒泡

在上面的例子中，点击`p`元素里面的内容，显然会触发`p`元素的事件处理程序`clickChild`。然后，因为`p`元素是放在`div`里面的，点击`p`元素相当于点击了`div`元素，会触发`div`的事件处理程序`clickParent`，这个过程被称为**事件冒泡**。

事件冒泡是指，某个事件触发了某个元素的事件处理程序，接下来，就会自动沿着节点树往**根节点**的方向依次触发**经过的路径**上的所有元素的某个事件的处理程序。

比如上面的例子中，用鼠标点击`p`标签里面的文字`点我`，控制台的打印结果如下：

   ![img](https://data.educoder.net/api/attachments/208774)  

第一行是子元素的`click`事件的事件处理程序的输出，第二行是父元素的，这里有一个先后的顺序，即从子元素一直到根节点。

##### 事件冒泡的控制

事件冒泡不是所有的时候都受到欢迎，有的时候需要控制它的发生，使用`event.stopPropagation()`即可。

比如，对于上面的例子，我们在子元素的事件处理程序`clickChild()`的最后一行添加一行代码：

```js
function clickChild() {  
   console.log("子");  
   window.event?window.event.cancelBubble=true:event.stopPropagation();   
}  
```

这个时候再次点击`p`里面的内容，控制台的输出如下：

   ![img](https://data.educoder.net/api/attachments/208775)  

可以看出，事件没有冒泡到父元素上面。所以，想要在哪里停止事件的冒泡，就在它的子元素的事件处理程序的最后调用`event.stopPropagation()`即可。