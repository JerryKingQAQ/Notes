# 基本输入输出范例代码

```java
 Scanner sc=new Scanner(System.in);
 int n=sc.nextInt();
 String str1=sc.next();
 System.out.println("欢迎"+n+"号同学"+str1);
```



# 第四章 流程控制

## 循环语句

### foreach语句

```java
for(元素类型x:遍历对象obj){
    引用了x的java语句;
}
```

**例子：**遍历一维数组

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



# 第五章 数组

## 数组的基本操作

### 数组排序

* `Arrays.sort(arr);`
* `Arrays.parallelSort(arr);`多线程排序，数据量大于一百万

### 复制数组

#### copyof()方法

语法：`int a[]=Arrays.copyOf(arr,int newlength);`

* newlength：复制后新数组的长度

> ！注：不能直接`a=b`，数组名是指针常量（常指针）

# 第六章 类和对象

## 面向对象概述

### 封装

* 避免外部操作对内部数据的影响，提高程序的可维护性
* 提高工作效率，把无需调用者关心的内容隐藏，简化编程，知道面对外部的接口能调用即可

## 类

**对于人来说，**

public：学历、知识（别人抢不走的）

protected：身体等

public：很多

**protected同包其他类或子类(继承)可见，其他包的类或子类不可见；private都不可见，只有本类可见。**

### this 关键字

this关键字用于表示本类当前的对象，只能在本类中使用。

```java
public void setName(String name){//定义一个setName()的方法
    this.name=name;//将参数值赋予类中的成员变量
}
```



## 类的构造方法

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



## 静态

```java
public class Lab2_1{
    
    public static void main(String[] args){
        new Lab2_1().show();//临时无名对象
        //如果是show.()直接调用会报错，除非把show 声明为静态函数，说这是上面的方法，调用类内成员函数
    }
    void show(){
        System.out.println("Hello!")
    }
}
```

类内静态成员共用一份空间

如果函数



## 对象

### 对象的销毁

```java
public class Lab2_1{
    
    public static void main(String[] args){
        Lab2_1 l2=new Lab2_1();
        //l2=null; 销毁对象 之后如果是l2.show();那么会报错NullPointerException 
    }//超过作用域 对象l2销毁
    void show(){
        System.out.println("Hello!")
    }
}
```



# 第七章 继承、多态、抽象类与接口

## 类的继承

### extends 关键字

语法：`CHild extends Parents`

### super 关键字



## Object 类

**Object类是一切类的基类**，隐含的继承

* 如果没声明，toString()一定是调用自Object类，输出是字符编号。

* 输出字符串自动会调用toString()函数，应当重写以达到需要的输出目的。
* 重写只能保持或扩大访问权限，如原本是Public不能改成Private。

```java
public class Student{
    String name;
    int age;
    
    public Student(String name,int age){
        this.name=name;
        this.age=age;
    }
    
    @Override//加这个帮助检查重写的函数名是否正确
    public String toString(){
        return "我叫"+name+",今年"+age+"岁。";
    }
    public static void main(String[] args){
        Student s1=new Student("张三",16);
        System.out.println(s1);//就是System.out.println(s1.toString());
    }
}
```



## 对象的类型转换

**需要基类对象的任何地方，都可以用派生类对象替代**

### 向上转型



### 向下转型



## instanceof关键字判断对象类型

## 方法的重载

>  函数的返回值类型不属于重载的依据



## final 关键字

最终的、终态

## 多态



## 抽象类与接口

### 抽象类

* 只要类中有一个抽象方法，此类就是抽象类
* 抽象类不能实例化，抽象类存在的目的就是为了被继承
* c++中全是抽象方法就叫纯虚类

### 接口

* 只能声明，不能实现



# 第十章 字符串

String创建的字符串是不可变的，改变字符串对象会在内存中创建新的字符串对象。

# 第十一章 常用类库

## 数字处理

### Random类

```java
Random r=new Random();
```

### BigInteger类

```java
BigInteger twoLnstance=new BigInteger("2");
```

## Runtime类

```java
public class RuntimeExecDemo{
    public
}
```



# 十二章 集合类

```java
Collection<类名> list=new ArrayList<>();//尖括号只能呢是类，比如不能放int要放integer
```



遍历集合通过迭代器(Iterator)来实现，只读且向前。可以用foreach，可读可写，但是不能break，除非抛出异常。遍历修改迭代器(ListIterator)

```java
import java.util.*;
public class Muster{
    public static void main(String args[]){
        Collection<String> list=new ArrayList();
        list.add("《Java从入门到精通》");
        list.add("《java实战》");
        lterator<Sting> it=list.iterator();
        while(it.hasNext()){
            String str=(String)it.next();
            System.out.printLn(Str);
        }
    }
}
```

