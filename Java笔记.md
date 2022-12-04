# Java笔记

## 流程控制

### 循环语句

#### foreach

```
for(元素类型x:遍历对象obj){
    引用了x的java语句;
}
```

```java
public class Repetition{
    public static void main(String args[]){
        int arr[]={5,13,96};
        System.out.println("一维数组中的元素分别为：");
        //x的类型与arr元素的类型相同 。for循环依次取出arr中的值并赋给x
        for(int x:arr){
            System.out.println(x);
        }
    }
}

/*输出结果：
一维数组中的元素分别为：
5
13
96
*/
```



## 数组

### 基本操作

#### 数组排序

- `Arrays.sort(arr);`
- `Arrays.parallelSort(arr);`多线程排序，数据量大于一百万

#### 数组复制

- `int a[]=Arrays.copyOf(arr,int newlength);`

> newlength：复制后新数组的长度

> 注意不能直接a = b， 数组名是指针常量



## 类与对象

### 封装

- protected**同包其他类或子类(继承)**可见，其他包的类不可见；
- private都不可见，只有本类可见。

### 包访问权限

当声明类时不使用public等关键字修饰类的权限的时候，则这个类预设为包存取范围，即只有一个包中的类可以访问这个类的成员变量或成员方法。

- 包访问权限介于private与protected之间
- 包外派生类可以调用基类protected成员，包访问权限不行



### 类的构造方法

> Java类内的属性值不支持默认值，不能直接定义 `int count=0` 
>
> 应使用默认构造函数初始化

```java
public class eggCake{
    int eggCount;
    public EggCake(int eggCount){//有参构造
        this.eggCount=eggCount;
    }
    public EggCake(){
        //设置鸡蛋灌饼里蛋的个数为1
        this(1);
    }
}
```

##### this关键字

this关键字用于表示本类当前的对象，只能在本类中使用。

```java
public void setName(String name){//定义一个setName()的方法
    this.name=name;//将参数值赋予类中的成员变量
}
```



## 继承

### 类的继承

#### extends 关键字

语法：`CHild extends Parents`

#### super 关键字

super可以看作是**父类的**，存在类与类的继承关系会存在。主要功能有如下：

- 用**super.属性、super.方法**的方式，来表明调用的是父类的属性、方法
- 在重写了父类的方法时，如果**子类需要调用父类被重写的方法**，需要加super关键字，显示了调用了父类的方法
- 可以在子类的构造器中使用super(形参列表)，来调用父类的构造器但是必须要在代码的首行。
- this（形参列表）和super（形参列表）只能用一个，因为这两个都要求放在首行。

#### instanceof关键字

`instanceof` 是 Java 的保留关键字，它的作用是测试它**左边的对象是否是它右边的类的实例**，返回 boolean 的数据类型。

#### final关键字

final关键字代表最终、不可改变的。



### Object 类

**Object类是一切类的基类**，隐含的继承

* 如果没声明，toString()一定是调用自Object类，输出是字符编号。

* 输出字符串自动会调用toString()函数，应当重写以达到需要的输出目的。
* 重写只能**保持或扩大**访问权限，如原本是Public不能改成Private。



### 对象的类型转换

- 需要基类对象的任何地方，都可以用**派生类对象替代**
- 定义为基类对象，**只能使用基类的方法**，对于派生类新增的方法是无法使用的



## 抽象类与接口

### 抽象类

* 只要类中有一个抽象方法，此类就是抽象类
* 抽象类不能实例化，抽象类存在的目的就是**为了被继承**
* C++中全是抽象方法就叫纯虚类



### 接口

接口是抽象类的延伸，可以将它看作纯粹的抽象类，接口中的方法都没有方法体。

- 接口使用`interface`关键字定义
- 使用接口使用`implements`关键字

```JAva
public interface Paintable{
	...
}
```

```java
public class className implements Paintable{
	...
}
```



## 字符串

**注意：**字符串不能使用 **==** 进行对比，需要使用**equals**关键字。

String创建的字符串是不可变的，改变字符串对象会在内存中创建新的字符串对象。



## 常用库类

### Random类

```java
Random r=new Random();
```

### BigInteger类

```java
BigInteger twoLnstance=new BigInteger("2");
```

### Runtime类

```java
public class RuntimeExecDemo{
    public
}
```



## 集合类

注意：

- ```java
  Collection<类名> list=new ArrayList<>();//尖括号只能呢是类，比如不能放int要放integer
  ```

  