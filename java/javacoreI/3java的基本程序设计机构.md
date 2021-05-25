# 数据结构

* 8种基本类型
    * 4种整型
    * 2种浮点型
    * 1种字符类型char
    * 1种布尔类型

## 整型

* **int** 4字节
* **short** 2字节
* **long**  8字节 (有后缀L或l)
* **byte**  1字节

## 浮点类型

* **float** 4字节
* **double** 8字节

## char类型

* **char** 表示单个字符，使用单引号括起来

## 变量与常量

* 声明变量时必须先指定类型
* 不使用java保留字作为变量名
* 大小写敏感
* 必须赋值显式初始化才可以使用
* 常量使用**final**修饰，只能被赋值一次
* 类常量使用**final static**修饰
* 枚举类型

## 运算符

* +、-、*、/ 加减乘除
* % 求余

## 数值类型之间的转换

* **无信息丢失的转换**
  * byte->shot->int->long
  * int->double
  * char->int
  * float->double
* **有信息丢失的转换**
  * int->float
  * long->float
  * long->double
* **运算符连接转换**
  * 有一个double类型，另一个转为double
  * 有一个float，另一个转为float
  * 有一个long，另一个转为long
  * 两个都转为int

## 强制类型转换

* 圆括号加上要转换的类型, 强转直接截掉小数点
``` java
double x = 7.19;
int y = (int)x;
// y=7
```

## 结合赋值和运算符

* /=
* +=
* %=
* -=
* *=
* ...
``` java
x = x + 1;
x += 1;
```

## 自增与自减

* 表达式中会有区别
  * **前缀** 
    前缀会先完成加(减)1操作
    ```java
    int m = 7;
    int a = 2 * ++m; //a为16
  * **后缀**
  使用变量原来的值
  ``` java
  int n = 7;
  int b = 2 * n++; //b 为14
  ```

# 字符串

* 字符串是java标准列库中的一个预定义类
* 使用双引号括起来
* 字符串是不可变的，但是可以改变变量的引用对象

## 子串

* 使用substring截取
``` java
String a = "i love you";
String b = a.substring(0, 9); //截取0-8,不包含9
```
  
## 拼接

* 使用 **+** 号连接
  ``` java
  String a = "i ";
  String b = "love ";
  String c = "you";
  String x = a + b + c;
  ```
* 字符串与非字符串拼接，非字符串会自动转化为字符串，再拼接
* 连接多字符串，并用分割符分割
  ``` java 
  String a = String.join("/", "a", "b", "c", "d");
  // a = "a/b/c/d"
  ```

## 检查字符串是否相等
* 使用**equals**方法，**equalsIgnoreCase**方法(忽略大小写)
``` java
String a = "b";
a.equals("b"); //true
```
* 不使用 **==** 来检查是否相等，**==** 判断的是内存地址
  
## 空串与null
* 空串是长度为0的字符串，即""
* null 表示没有对象与变量关联

## 常用的String api

* int compareTo(String other) 
  对比，在前返回负数，在后返回正数，相等返回0
* boolean empty()
  是否为空
* boolean equals(Object other)
  是否相等
* boolean equalsIgnoreCase(String other)
  忽略大小写，是否相等
* boolean starsWith(String prefix)
  是否以字符串prefix开头
* boolean endsWith(String suffix)
  是否以字符串suffix结尾
* int indexOf(String str)
  返回匹配str的第一个子串开始的位置
* int indexOf(String str, int fromIndex)
  从fromIndex开始，返回匹配str的第一个子串开始的位置
* int lastIndexOf(String str)
  返回匹配str的最后一个子串开始的位置
* int lastIndexOf(String str, int fromIndex)
  从fromIndex开始，返回匹配str的最后一个子串开始的位置
* int length()
  返回长度
* String replace(CharSequence oldString, CharSequence newString)
  可用String或StringBuilder对象作为CharSequence参数，newString替换oldString
* String subString(int beginIndex)
* String subString(int beginIndex, int endIndex)
* String toLowerCase()
  字符串改为小写
* String toUpperCase()
  字符串改为大写
* String trim()
  去掉头部和尾部的空白符
* String join(CharSequence delimiter, CharSequence... elements)
  java8，用给定的分隔符连接所有元素

