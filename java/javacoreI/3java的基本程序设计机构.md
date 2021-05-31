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
  * 对比，在前返回负数，在后返回正数，相等返回0
* boolean empty()
  * 是否为空
* boolean equals(Object other)
  * 是否相等
* boolean equalsIgnoreCase(String other)
  * 忽略大小写，是否相等
* boolean starsWith(String prefix)
  * 是否以字符串prefix开头
* boolean endsWith(String suffix)
  * 是否以字符串suffix结尾
* int indexOf(String str)
  * 返回匹配str的第一个子串开始的位置
* int indexOf(String str, int fromIndex)
  * 从fromIndex开始，返回匹配str的第一个子串开始的位置
* int lastIndexOf(String str)
  * 返回匹配str的最后一个子串开始的位置
* int lastIndexOf(String str, int fromIndex)
  * 从fromIndex开始，返回匹配str的最后一个子串开始的位置
* int length()
  v返回长度
* String replace(CharSequence oldString, CharSequence newString)
  * 可用String或StringBuilder对象作为CharSequence参数，newString替换oldString
* String subString(int beginIndex)
* String subString(int beginIndex, int endIndex)
* String toLowerCase()
  * 字符串改为小写
* String toUpperCase()
  * 字符串改为大写
* String trim()
  * 去掉头部和尾部的空白符
* String join(CharSequence delimiter, CharSequence... elements)
  * java8，用给定的分隔符连接所有元素

## StringBuilder构建字符串
``` java
StringBuilder builder = new StringBuilder();
builder.append(ch);
builder.append(str);
String doneStr = builder.toString();
```

* **StringBuilder**中的重要方法
  * int length()
  * StringBuilder append(String str)
    追加一个字符串，并返回this
  * StringBuilder append(char c)
  * void setCharAt(int i, char c)
    将第I个代码单元设置为c
  * StringBuilder insert(int offset, String str)
    在offset位置插入一个字符串
  * StringBuilder insert(int offset, char c)
  * StringBuilder delete(int startIndex, int endIndex)
  * String toString()

## 格式化输出
``` java
String.format("hello, %s, next year, you will be %d", name, age);
```

* 转换符
  * **d** 十进制整数
  * **x** 十六进制整数
  * **o** 八进制整数
  * **f** 定点浮点数
  * **e** 指数浮点数
  * **g** 通用浮点数
  * **a** 十六进制浮点数
  * **s** 字符串
  * **c** 字符
  * **b** boolean
  * **h** 散列码
  * **%** 百分号
  * **n** 与平台有关的行分隔符
* 标志
  * **+** 打印正负数符号
  * **空格** 在正数之前添加空格
  * **0** 数字前面补0
  * **-** 左对齐
  * **（** 将负数括在括号内
  * **,** 添加分组分隔符
  * **#** 对于f格式，包含小数点， 对于x或0格式，添加前缀0x或0
* 日期时间转换符
  * **c** 完整日期时间 
  * **D** 美国格式日期  
  * **T** 24小时时间 
  * **r** 12小时时间 
  * **Y** 4位数字的年 
  * **y** 年的后两位数字 
  * **C** 年的前两位数字 
  * **B** 月的完整拼写(英文) 
  * **b或h** 月的缩写 
  * **m** 两位数字的月 
  * **d** 两位数字的日 补零 
  * **e** 两位数字的日 不补零
  * **A** 星期几的完整拼写(英文)
  * **a** 星期几的缩写 
  * **j** 三位数的年重第几天 补零
  * **H** 两位数的小时 前面补零 0~23
  * **k** 两位数的小时 前面不补零 0~23
  * **I** 两位数的小时 前面补零 01~12
  * **l** 两位数的小时 前面不补零 1~12
  * **M** 两位数的分钟 补零
  * **S** 两位数的秒 补零
  * **L** 三位数的毫秒 补零
  * **N** 九位数的毫秒 补零
  * **p** 上午或下午的标志
  * **Z** 时区
  * **s** 从格林尼治时间起得秒数
  * **Q** 从格林尼治时间起得毫秒数


# 控制流程

## 块作用域

* 块，使用 **{}** 括起来的若干，可嵌套
* 确定变量的作用域，嵌套块不能声明相同名的变量
  
## 条件语句
``` java
if (condition){
    statement;
}else if (condition){ //可选，可多个else if
    statement;
}else{ //可选，只能一个else
    statement;
}
```

## while循环
``` java
while (condition){
  statement;
}
```
为true执行循环体，第一次就为false，一次也不执行

```java
do {
  statement;
}while (condition)
```
先执行后判断，必定执行一次

## for循环
``` java
for (int i=1; i<=10; i++){
    statement;
}
```

## switch语句
``` java
int choice = ;
switch (choice){
    case 1:
        statement;
        break;
    case 2:
        statement;
        break;
    case 3:
        statement;
        break;
    case ...:
        statement;
        break;
    default: //没有匹配的case标签，执行default
        statement;
        break;
}
```
* 没有匹配的case标签，执行default
* 直到遇到break，或者执行到switch语句的结束处为止
* 有可能触发多个case分支
* case标签可以为：
  * char、byte、short、int
  * 枚举常量
  * java7开始，可以是字符串字面量


## 中断控制流程的语句
### goto语句
* 不建议使用

### break
* 结束循环体

### continue
* 结束当前循环，进入下一次循环

# 大数
* java.math下的两个类:
  * BigInteger 整数运算
  * BigDecimal 浮点数运算
* 可以处理包含任意长度数字序列的数值

``` java
BigInteger a  = BigInteger.valueOf(1000);
//过长用这个 BigInteger a = new BigInteger("123343352345213452344352345");
//不能使用算数运算符
BigInteger b = new BigInteger("1111");
BigInteger c = a.add(b);
BigInteger d = c.multiply(b.add(BigInteger.valueOf(2)));
```

## 常见api
* java.math.BigInteger
  * BigInteger add(BigInteger other) 和
  * BigInteger subtract(BigInteger other) 差
  * BigInteger multiply(BigInteger other) 积
  * BigInteger divide(BigInteger other) 商
  * BigInteger mod(BigInteger other) 余数
  * BigInteger sqrt() java9 平方根
  * int compareTo(BigInteger other)
    * 对比，相等0，大于正数，小于负数
  * static BigInteger valueOf(long x)
    * 返回值等于x的大整数

* java.math.BigDecimal
  * BigDecimal add(BigDecimal other) 和
  * BigDecimal subtract(BigDecimal other) 差
  * BigDecimal multiply(BigDecimal other) 积
  * BigDecimal divide(BigDecimal other) 商
  * BigDecimal divide(BigDecimal other, RoundingMode mode) 
    * 如果商是无限循环小数，上一个方法抛出异常，使用该方法，第二个参数表示舍入方法
  * int compareTo(BigDecimal other)
    * 对比，相等0，大于正数，小于负数
  * static BigDecimal valueOf(long x)
  * static BigDecimal valueOf(long x, int scale)
    * 返回值等于x或10的大整数

# 数组

## 声明数组
* 需要指出数组类型(数据元素类型紧跟[])和数组变量的名字
* 一旦创建数组，就不能改变长度
``` java
//创建类型为int，长度100的数组
int[] a = new int[100];
```

* 创建数组对象，并同时初始化的简写
``` java
int[] smallPrimes = {2, 3, 5, 7, 11, 13};
```

* 匿名数组
``` java
new int[] {17, 19, 23, 29, 31};
//分配新数组并初始化，可以用这种语法重新初始化数组，而无须创建新变量
smallPrimes = new int[]{17, 19, 23, 29, 31, 37};
```

## 访问数组元素
* 数组的下标从0开始，使用 **变量[下标]** 访问
``` java
int[] a = new int[100];
for (int i = 0; i<100; i++){
    a[i] = i;
}
```
* 默认初始化
  * 数字数组，所有元素初始化为0
  * boolean，所有元素初始化为false
  * 对象数组，所有元素初始化为null,表示未存放对象

## for each循环
* 可用来依次处理数组(集合)中的每一个元素，而不用考虑下标值
``` java
// variable变量暂存集合中的每一个元素
// collection 数组或者是实现了Iterable接口的类对象
for (variable: collection){
    statement;
}
```

``` java
String[] s = {"1", "2", "3", "4"};
for (String word: s){
    System.out.println(word);
}
```

## 数组拷贝

* 使用Arrays类的copyOf方法(拷贝到新的数组中)
* 拷贝的数组，扩展的话
  * 如果是数值数组，额外元素初始化为0
  * 布尔类型数组，则赋值false
* 如果新数组小于原始数组，只拷贝前面的值
``` java
int[] luckyNumbers = {1,2,3,4,5,6,7};
//第二个参数为新数组的长度，通常用来增加数组的大小
int[] copyLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);
luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);
```

## 命令行参数
* main 带有String arg[]参数，可以命令行上指定参数
* 例如 java Message -g cruel world
* 调用Message程序，args数组将包含以下内容
  * args[0]: "-g"
  * args[1]: "cruel"
  * args[2]: "world"

## 数组排序
* 使用Arrays类中的sort方法
``` java
int[] a = {2,1,6,3,9};
//该方法使用优化的快速排序算法
Arrays.sort(a);
```

* 常用java.util.Arrays API
  * static String toString(xxx[] a)
    * 返回字符串,用中括号包围，逗号分隔
  * static xxx[] copyOf(xxx[] a, int length)
  * static xxx[] copyOfRange(xxx[] a, int start, int end)
    * 返回与a同类型，长度为length或end-start的数组
  * static void sort(xxx[], a)
  * static int binarySearch(xxx[] a, xxx v)
  * static int binarySearch(xxx[] a, int start, int end, xxx v)
    * 使用二分查找算法查找 **有序数组** a中的v,找到返回下标，否则返回负数，-r-1是v应该插入的位置
  * static void fill(xxx[] a, xxx v)
    * 将数组所有元素设置为v
  * static boolean equals(xxx[] a, xxx[] b)
    * 如果数组大小相同，对应下标元素相同，返回true


## 多维数组
* 其实是数组中的数组，即数组中的元素存储的是数组
``` java
double[][] balance = new double[NYEARS][NRATES];
```

## 不规则数组
* 数组中的每一行有不同的长度
``` java
int NMAX = 10;
int[] odds = new int[NMAX+1][];
for (int n=0; n<=NMAX; n++){
  odds[n] = new int[n+1];
}
```
