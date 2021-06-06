# 接口
* 接口类使用interface修饰符修饰
``` java
public interface Ainterface<T>{}
```

## 接口的概念
* 接口不是类，而是希望符合这个借口的类的一组需求(就是定义一个接口类，里面有定义一些要用到的方法，不用具体实现，其他类实现这个接口，必须实现借口类的所有方法)
* 接口中的所有方法都是public方法，所以接口声明方法，不必提供关键字public
* 接口中绝对不会有实例字段
* 提供实例字段和方法实现的任务应该由实现接口的那个类来完成，可以将接口看成是没有实例字段的抽象类(有区别)

* 让类实现一个接口
  * 将类声明为实现给定的接口，关键字 **implements**
  * 对接口中的 **所有** 方法提供定义
  ``` java
  class Employee implements Comparable{
      public int compareTo(Object otherObject){
          statements;
      }
  }
  ```

* 可以为泛型Comparable接口提供一个类型参数
``` java
class Employee implements Comparable<Employee>{
    public int compareTo(Employee other){
        statements;
    }
}
```

## 接口的属性
* 接口不能创建实例(不能new出来)
* 但可以声明借口变量，该变量必须引用实现了这个接口的类对象，可以使用instanceof检查
``` java
if (anObject instanceof comparable)( statements );
```
* 只能继承一个超类，但是可以实现多个接口
``` java
class Employee implements Cloneable, Comparable
```

## 接口与抽象类
* java没有多重继承 只能继承一个超类，但是可以实现多个接口

## 静态和私有方法
* java8中允许在借口中增加静态方法
* java9中，接口的方法可以是private，private方法可以是静态方法或实例方法，但是私有方法只能在接口本身的方法中使用

## 默认方法
* 可以为接口方法提供一个默认实现，必须用default修饰符标记，实现类可以不重写这个方法
``` java {.line-numbers}
public interface CompareTo<T>{
    default int compareTo(T other){
        return 0;
    }
}
```
* 默认方法可以调用其他方法


## 解决默认方法冲突
* 接口和超类中定义了相同的方法
  * 超类优先
  * 接口冲突，多个接口相同默认方法，则必须覆盖(重写)这个方法

## 接口与回调


## Comparator接口
* Arrays.sort方法，参数是一个数组和比较器(comparator),比较器是实现了Comparator接口的类的实例
``` java {.line-comparator}
public interface Comparator<T>{
    int compare(T first, T second);
}

class lengthComparator implements Comparator<String>{
    public int compare(String first, String second){
        return first.length() - second.length();
    }
}

// Comparator<String> comp = new LengthComparator();
String[] friends = {"Peter", "paul", "Mary"};
Arrays.sort(friends, new LengthComparator);
```

## 对象克隆
* Cloneable接口,指示一个类提供一个安全的clone方法
* **=** 赋值是同一个对象引用，任何一个变量改变都会影响另一个变量(这里指的是对象，可变对象)
* clone方法是Object的一个protected方法,子类只能调用受保护的clone方法来克隆它自己的对象，必须重新定义clone为public才能允许所有方法克隆对象
* Cloneable接口，标记接口，对象请求克隆，必须实现这个接口，否则会生成检查型异常
* 默认的clone事浅拷贝
  * 浅拷贝不会拷贝引用字段，还是指向同一个引用
* 即使默认的clone能够满足要求，还是要实现Cloneable接口，将clone重新定义为public,在调用super.clone()
``` java {.line-numbers}
class Employee implements Cloneable{
    public Employee clone() throws CloneNotSupportedException{
        return (Employee) super.clone();
    }
}
```
* 要创建深拷贝需要在方法中对类里的可变字段进行处理
* 小心子类的克隆，超类如果定义了clone方法，子类可以引用，需要考虑子类的clone是否能完成工作

# lambda表达式
* lambda表达式是一个可传递的代码块, 以及必须传入代码的变量规范
``` java {.line-numbers}
(String first, String second) ->
    first.length() - second.length()
```
* 形式：参数，箭头(->)以及表达式，只有一个语句可以省略 **{}**
``` java {.line-numbers}
(String first, String second) ->
{
    if (first.length() < second.length()) return -1;
    else if (first.length() > second.length()) return 1;
    else return 0;
}
```
* 即使lambda表达式没有参数，要提供空括号
``` java {.line-numbers}
() -> {
    for (int i = 100; i >= 0; i++)
        System.out.println(i);
}
```
* 如果编译器可以推导出参数必定是某个类型，可以忽略类型
``` java {.line-numbers}
Comparator<String> comp = (first, second) -> first.length - second.length();
```
* 如果方法只有一个参数，且可以推导出，可以省略括号
``` java {.line-numbers}
ActionListener listener = event -> System.out.println("1");
```
* 无须指定lambda表达式的返回类型，总是由上下文推导得出

## 函数式接口
* 对于 **只有一个抽象方法的接口**，需要这种接口对象的时候，就可以提供一个lambda表达式，这种接口称为函数式接口
* 如Comparator接口
``` java 
Arrays.sort(words, (first, second)->first.length()-second.length());
```
* 可以把lambda表达式看做是一个函数，而不是一个对象，它传递到函数式接口，可以转换为借口
``` java {.line-numbers}
Comparator<String> comp = new Comparator(
    (first, second) -> {
        if (first.length() < second.length()) return -1;
        else if (first.length() > second.length()) return 1;
        else return 0;
    }
)
```

## 方法引用
* lambda表达式涉及一个方法，如
``` java 
var timer = new Timer(1000, event->System.out.println(event));
//可以直接把println方法传递到Timer构造器
var timer1 = new Timer(1000, System.out::println);
```
* System.out:println是一个方法引用，指示编译器生成一个函数式接口的实例，覆盖这个接口的抽象方法来调用给定的方法，如果想对字符串排序，不考虑字母的大小写，可以传递以下方法表达式
``` java
Arrays.sort(strings, String::compareToIgnoreCase);
```
* 语法 **::** 运算符分隔方法明与对象或类名,主要三种情况
  * object::instanceMethod
    * 等价与向方法传递参数的lambda表达式
    ``` java
    System.out::println;
    //等价于
    x->System.out.println(x);
    ```
  * Class::instanceMethod
    * 第一个参数会成为方法的隐式参数
    ``` java
    String::CompareToIgnoreCase;
    //等价于
    (x,y)->x.compareToIgnoreCase(y);
    ```
  * Class::staticMethod
    * 所有参数传递到静态方法
    ``` java
    Math::pow;
    //等价于
    (x, y) -> Math.pow(x, y);
    ```
* 只有当lambda表达式的体只调用一个方法而不做其他操作时，才能把lambad表达式重写为方法引用

## 构造器引用
* 构造器引用与方法引用类似，不过方法名为new
例如 Employee::new;

## 变量作用域
* 在lambda表达式中访问外围方法或类中的变量
``` java {.line-numbers}
public static void repeatMessage(String text, int delay){
    ActionListener listener = event -> {
        System.out.println(text);
        Toolkit.getDefaultToolkit().beep();
    };
    new Timer(delay, listener).start();
}
```
* lambda有三个部分：
  * 一个代码块
  * 参数
  * 自由变量的值，即非参数而且不在代码中定义的变量
* lambda表达式的数据结构会存储自由变量的值，如上的text,只能引用值不会改变的变量，且这个值不能在外部改变，即必须是 **事实最终变量**
* lambda中的this参数，即创建这个lambda表达式的方法的this参数


# 内部类
* 内部类是定义在另一个类钟的类
  * 内部类可以对同一个包中的其他类隐藏
  * 内部类方法可以访问定义这个类的作用域钟的数据，包括原本私有的数据

## 使用内部类访问对象状态
``` java {.line-numbers}
public class TestInnerClass{
    public void main(String[] args){
        Out out = new Out();
        out.start();
    }
}

public class Out{
    private String name;

    public void start(){
        Inner inner = new Inner();
        inner.start();
    }

    public class inner{
        public void start(){
            // 访问外部类数据
            System.out.println(name);
        }
    }
}
```
* 内部类方法可以访问自身的数据字段，也可以访问创建它的外围类对象的数据字段
* 内部类的对象总由一个隐式引用，指向创建它的外部类对象

## 局部内部类
* 局部类的作用域被限定在声明这个局部类的块中,如下，只有start方法可以访问局部类inner
``` java {.line-numbers}
public class TestInnerClass{
    public void main(String[] args){
        Out out = new Out();
        out.start();
    }
}

public class Out{
    private String name;

    public void start(){

        public class inner{
            public void start(){
                // 访问外部类数据
                System.out.println(name);
            }
        }

        Inner inner = new Inner();
        inner.start();
    }
}
```

## 由外部方法访问变量
``` java {.line-numbers}
public class TestInnerClass{
    public void main(String[] args){
        Out out = new Out();
        out.start("lllllll");
    }
}

public class Out{

    public void start(String name){

        public class inner{
            public void start(){
                // 访问外部类数据
                System.out.println(name);
            }
        }

        Inner inner = new Inner();
        inner.start();
    }
}
```
* 对局部变量的访问，会为每一个变量创建响应的实例字段

## 匿名内部类
* 创建类对象，实现接口，并实现接口的方法
``` java {.line-numbers}
interface HelloWorld {
    public void greet();
    public void greetSomeone();
}

public class HelloWorldAnonymousClasses{
    public void sayHello(){
        // 接口实现匿名内部类
        HelloWorld hw = new HelloWorld(){
            public void greet(){
                System.out.println("greet");
            }
            public void greetSomeone(){
                System.out.println("greetSomeone");
            }
        };
        hw.greet();
        hw.greetSomeone();
    }
}
```

## 静态内部类
* 不需要内部类有外围类对象的引用，可以将内部类声明为static

# 代理

##代理类
* 利用代理可以在运行时创建实现了一组给定接口的新类
* 代理类包含以下方法：
  * 指定接口所需要的全部方法
  * Object类中的全部方法
* 实现InvocationHandler接口：
  * 只有一个方法Object invoke(Object proxy, Method method, Object[] args):
    * args为方法参数

## 创建代理对象
* 需要使用Proxy类的newProxyInstance方法，有三个参数：
  * 一个类加载器
  * 一个Class对象数组，每个元素对应需要实现的各个接口
  * 一个调用处理器
* 调用代理对象方法时，会将方法传递给invoke方法，需要在invoke方法中完成方法的执行
``` java {.line-numbers}
package proxy;

import java.lang.reflect.*;
import java.util.*;

public class ProxyTest{
    Object[] elements = new Object[1000];
    for (int i = 0; i<elements.length; i++){
        Integer value = i + 1;
        TraceHandler handler = new TraceHandler(value);
        Object proxy = Proxy.newProxyInstance(ClassLoader.getSystemClassLoader(), new Class[]{Comparable.class}, handler);
        elements[i] = proxy;
    }

    Integer key = new Random().nextInt(elements.length) + 1;
    int result = Arrays.binarySearch(elements, key);
    if(result>=0) System.out.println(elements[result]);
}

class TraceHandler implements InvocationHandler{
    private Object target;
    public TraceHandler(Object target){
        this.target = target;
    }
    public Object invoke(Object proxy, Method m, Object[] args) throws Throwable{
        System.out.print(target);
        System.out.print("."+m.getName()+"(");
        if (args != null){
            for (int i=0; i<args.length; i++>){
                System.out.println(args[i]);
                if (i<args.length-1) System.out.println(",");
            }
        }
        System.out.println(")");
        return m.invoke(target, args);
    }
}
```