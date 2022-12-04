# DOM  文档元素的操作

## 通过ID获取文档元素

##### 什么是DOM

`Document Object Module`，简称`DOM`，中文名文档对象模型。在网页上，组成页面（又叫文档）的一个个对象被组织在树形结构中，用这种结构表示它们之间的层次关系，表示文档中对象的标准模型就称为`DOM`。

`DOM`的作用是给`HTML`文档提供一个标准的树状模型，这样开发人员就能够通过`DOM`提供的接口去操作`HTML`里面的元素。

##### 文档元素

先看一段网页代码：

```html
<html>  
    <head>  
        <title>这里是标题</title>  
    </head>  
    <body>  
        <p>这是我学习JavaScript的网址：</p>  
        <a href="https://www.educoder.net/paths">JavaScript学习手册</a>  
    </body>  
</html> 
```

执行后效果如下：  

   ![img](https://data.educoder.net/api/attachments/194098)  

文档元素：指的就是`<html>`、`<head>`等等这样一个个的**标签和里面的内容**。

比如文档元素`<title>`就是这样：

```
<title>这里是标题</title>  
```

在`JavaScript`中，元素`<title>`**对应一个对象**，这个对象有一个属性的值是“这里是标题”。

所以，用`JS`操作这些文档元素，操作的就是它们对应的`JS`对象。

##### 节点树

从代码的缩进可以知道，文档元素之间有层次关系，如下：

   ![img](https://data.educoder.net/api/attachments/194100)  

上面的图和数据结构中树的概念类似，被称为**节点树**。`<html>`是根节点，网页的所有文档元素都在里面，`<head>`和`<body>`是两个子节点，分别存储网页**标题**有关内容和网页的**主体**部分。

`JavaScript`要操作这些元素，第一步自然是获得这些元素对应的`JavaScript`对象，那么，怎么获取呢？

##### 通过id获取文档元素

文档元素一般都有一个`id`属性，它的值在本文档中唯一，如下：

```
<p id="myId">这是我学习JavaScript的网址：</p>  
```

用这个`id`获取`<p>`元素的方法如下：

```
var pElement = document.getElementById("myId");  
```

其中`document`表示整个文档，`getElementById()`是`document`对象的一个方法，参数是`id`属性的值`myId`。

获取的`pElement`就代表了`<p>`标签以及里面的内容，接下来，可以通过`pElement`操作这个元素。比如可以用弹框展示一下`<p>`标签里面的内容：

```
window.alert(pElement.innerText);  
```

效果如下：

   ![img](https://data.educoder.net/api/attachments/206262)  



## 通过类名获取文档元素

除了`id`以外，文档元素另外一个常见的属性是类名。

###### 通过类名获取文档元素

文档元素的类名不唯一（存在多个文档元素的类名相同的情况），如下：

```
<p class="myName">段落</p>  <a class="myName" href="https://www.educoder.net">这是一个链接</a>  
```

`document`的**getElementsByClassName()**方法用来获取指定类名的文档元素数组（`NodeList`，一般叫节点列表），如下：

```
var myNodeList = document.getElementsByClassName("myName");  
```

这样，`myNodeList[0]`就是`<p>`元素，而`myNodeList[1]`就是`<a>`元素，通过这个方法的名字我们也可以知道获取的标签不唯一。

我们以弹框的形式查看一下`<p>`里面的内容：

```
window.alert(myNodeList[0].innerText);  
```

效果如下：

   ![img](https://data.educoder.net/api/attachments/206265)



## 通过标签名获取文档元素

通过前面的多个例子，我们可以看到，文档无非是由几个特定的标签组成，比如`<p>`、`<a>`、`<img>`等，由此可以想到，我们能不能通过标签的名字获取特定的文档元素呢？

###### 通过标签的名字获取文档元素

标签名指的是`<>`里面的字符串，`document`对象的`getElementsByTagName()`获取整个文档中指定名字的所有标签，显然，结果是一个文档元素数组（节点列表），方法的名字也暗示了这一点。

```
<div id="div1">  
    <p id="p1">文本1</p>  
    <p id="p2">文本2</p>  
    <a name="a1">链接</a>  
</div>  
<div id="div2">  
    <p id="p3" name="a1">文本3</p>  
</div>  
```

获取所有的`<div>`元素，如下：

```
var allDiv = document.getElementsByTagName("div");  
```

为了显示效果，我们以页面弹框的形式展示第一个`<div>`里面的内容：

```
window.alert(allDiv[0]);  
```

效果如下：

   ![img](https://data.educoder.net/api/attachments/206266)  

这个弹框表明，我们试图弹出的内容是一个`div`元素。

###### 获取标签内部的子元素

我们获取到的文档元素，也有`getElementsByTagName()`方法，作用是获取该元素**内部**指定名字的所有子元素。比如，要获取第一个`<div>`里面所有的`<a>`元素，代码如下：

```
//变量allDiv上面有，这里不再重复！  
var allLink = allDiv[0].getElementsByTagName("a");  
```

这样就获取了第一个`<div>`里面的所有超链接元素。



## 下拉列表级联

综合前面学习过的节点的各种操作，可以实现很复杂的功能。

##### 下拉列表的级联

相信大家都见过这样的下拉框：

   ![img](https://data.educoder.net/api/attachments/205243)  

它有三列，每一列都会根据前一列的结果动态的改变自己的可选项，称为下拉框的级联，那么如何实现呢？

第一步：静态的HTML的代码如下（简单起见，只考虑前两列）：

```html
<select id="province" onChange="changeCity()">  
    <option value="BeiJing" id="bj">北京</option>  
    <option value="AnHui" id="ah">安徽</option>  
</select>  
<select id="city">  
    <option value="BeiJingCity">北京市</option>  
</select>  
```

`select`表示选择框，`option`表示选择框里面的每一个选项，`onChange="changeCity()"`表示一旦改变当前的选项，就会触发`JavaScript`函数`changeCity()`的执行。

对于这个静态的`HTML`页面，不论你在第一列选择的是`北京`还是`安徽`，第二列的选项都只有`北京市`一项。

第二步：获取两个选择框对应的节点元素
（以下的所有代码都是`changeCity()`函数里面的内容）：

```js
var province = document.getElementById("province");  
var city = document.getElementById("city");  
```

`province`变量代表第一列的选择框，`city`变量代表第二列的选择框。

第三步：清空第二列中的所有内容；
根据第一列的选择结果改变第二列的内容，就是根据父节点的不同替换不同的子节点，我们采用先删除后新增的方法实现替换：

```js
var length = city.children.length;  
for(var i = length-1;i >= 0;i--) {  
    city.removeChild(city.children[i]);  
}  
```

在`for`循环里面，依次删除`city`节点下面的所有子节点。

需要注意的是，每删除一个子节点后，表示子节点个数的属性`city.children.length`都会自动减`1`，所以我们需要在`for`循环开始之前索取子节点的长度。

第四步：根据父节点的不同新增不同的子节点：

```js
if(province.value == "BeiJing") {  
    var child1 = document.createElement("option");  
    child1.value ="BeiJingCity";  
    child1.innerText="北京市"  
    city.appendChild(child1);  
} else {  
    var child1 = document.createElement("option");  
    child1.value="HuangShanCity";  
    child1.innerText="黄山市";  
    city.appendChild(child1);  
}  
```

`province.value`表示第一列选中的选项的值，即选中的`option`标签的`value`的值。

如果第一列选择的是`北京`，我们需要增加一个选项为`北京市`的`option`节点，这个节点将作为`city`的子节点。如果第一列选择的是`安徽`，我们需要增加一个选项为`黄山市`的`option`节点，这个节点将作为`city`的子节点。

`value`属性表示`option`标签的值，`innerText`表示`option`标签呈现出来的值。