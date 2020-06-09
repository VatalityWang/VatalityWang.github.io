---
layout: post
title: windows 下Qt 连接本地mysql
categories: 学习
description: mysql性能测试
keywords: trick

---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>
# windows 下Qt 连接本地mysql

1、安装mysql8.0

2、安装Qt5.11.1

3、安装vs2019

4、在vs2019上安装扩展Qt-vs-Tools



本地测试代码如下：

## QtGuiMysqlTest.h

```c++
#pragma once

#include <QtWidgets/QMainWindow>
#include "ui_QtGuiMysqlTest.h"

class QtGuiMysqlTest : public QMainWindow
{
	Q_OBJECT

public:
	QtGuiMysqlTest(QWidget *parent = Q_NULLPTR);

private:
	Ui::QtGuiMysqlTestClass ui;
};
```
## main.cpp

```c++
#include "QtGuiMysqlTest.h"
#include <QtWidgets/QApplication>

//#include "QtMysql.h"
#include <QtSql>
#include <QtSql/QSqlDatabase>
#include <QtSql/QSqlTableModel>
#include <QtSql/QSqlError>
#include <QMessageBox>

int main(int argc, char *argv[])
{
	QApplication a(argc, argv);
	QtGuiMysqlTest w;


//addDatabase（）来创建一个连接，调用这个函数时，我们可以传递我们要访问哪种类型的数据库
QSqlDatabase db = QSqlDatabase::addDatabase("QMYSQL");     //驱动 

db.setHostName("localhost");          //数据库地址，一般都是本地，就填localhost就可以 
db.setDatabaseName("world");           //数据库名，根据你Mysql里面的数据库名称来填写，比如我Mysql里面有个数据库叫test，可以用Navicat软件看自己的数据库名字
db.setUserName("root");               //用户名，一般是本地用户，就填root就可以
db.setPassword("*****");             //密码，填写你自己的Mysql登陆密码，为了保密我这里用*代替我的密码
db.setPort(3306);                   //端口默认的是3306，可以不用写 
if (db.open())
{
	QMessageBox::warning(NULL, QStringLiteral("提示"), "open ok", QMessageBox::Yes);

}
else
{
	QMessageBox::warning(NULL, QStringLiteral("提示"), "open failed", QMessageBox::Yes);
}
db.close();

w.show();
return a.exec();

}
```
5、F5 编译

![image-20200525103956935](/images/blog/image-20200525103956935.png)

6、查找问题：

（1）开启mysql root 用户远程访问权限。虽然是本地访问，做一个尝试。未解决。

（2）新建一个非系统初始化数据库，并建立表格。再次链接，未解决。

（3）在一个博客中发现需要将’C:\Program Files\MySQL\MySQL Server 8.0\lib下的libmysql.dll 拷贝至‘D:\Qt\Qt5.11.1\5.11.1\msvc2017_64\bin’下。

7、成功解决：

![image-20200525104618592](/images/blog/image-20200525104618592.png)





