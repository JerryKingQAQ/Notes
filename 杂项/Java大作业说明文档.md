# 说明文档

## 项目简介

项目名称：基于MySQL的学生信息管理系统

项目简介：本项目基于MySQL与Java实现了学生信息管理系统，其可以存储和管理学生信息，实现了数据录入、查询、删除、修改功能

完成人：8班金家瑞 20212005073

 

## 设计要点

### 登录界面

![image-20230103194327668](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103194327668.png)

开启程序后自动进入登录界面，输入SQL数据库的账户密码。

![image-20230103194437764](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103194437764.png)

如果账户密码输入错误，会提示链接失败。为了保证老师可以查看后续界面，这里不返回登录界面而直接进入主界面。



### 主界面

![image-20230103194541852](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103194541852.png)

成功登录后将进入主界面。主界面分为菜单区和文本提示区。

![image-20230103194607694](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103194607694.png)

菜单主要有以下功能：

- 添加学生数据
- 删除学生数据
- 修改学生数据
- 查询学生数据
- 所有学生信息



#### 添加学生数据

点击添加学生数据按钮后即可开始添加学生数据。

![image-20230103195112033](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195112033.png)

![image-20230103195126171](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195126171.png)

![image-20230103195133955](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195133955.png)

![image-20230103195140118](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195140118.png)

此时打开SQLyog，可以查看到数据已经添加至数据库中。

![image-20230103195229604](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195229604.png)



#### 删除学生数据

首先添加部分数据

![image-20230103195550764](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195550764.png)

点击删除数据按钮，开始输入信息

![image-20230103195557562](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195557562.png)

![image-20230103195635499](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195635499.png)

![image-20230103195743126](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195743126.png)

此时打开SQLyog查询数据库数据，删除成功

![image-20230103195749867](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195749867.png)



#### 修改学生数据

点击修改学生数据按钮，开始输入信息

![image-20230103195842732](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195842732.png)

![image-20230103195852777](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195852777.png)

![image-20230103195858100](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195858100.png)

![image-20230103195902018](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103195902018.png)

此时打开SQLyog查询数据库数据，修改成功

![image-20230103200014635](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103200014635.png)



#### 查询学生信息

点击修改学生数据按钮，开始输入信息

![image-20230103200042615](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103200042615.png)

如果存在数据，则弹窗提示相关信息

![image-20230103200322683](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103200322683.png)

![image-20230103200326719](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103200326719.png)

信息框中也有相关信息

![image-20230103200331150](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103200331150.png)



#### 所有学生信息

点击所有学生信息后，即可显示所有学生的信息。

![image-20230103200454515](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230103200454515.png)



## 总结

本次Java大作业主要使用了Swing、JDBC、多线程等相关技术，以此实现了基于MySQL数据库的学生信息管理系统。这是一次多技术间的共同协作，我在代码编写中提升了相关知识的认识，尤其是数据库操作的认识。这对我来说是一次很不错的能力提升机会，也感谢老师能提供这个机会让我有所练习与提升。