# Java基础学习笔记一 Java介绍

## **java 语言概述**

Java是sun公司开发的一门编程语言,目前被Oracle公司收购，编程语言就是用来编写软件的。

###  Java的应用

- 开发QQ、迅雷程序(桌面应用软件)
- 淘宝、京东(互联网应用软件)
- 安卓应用程序

###  Java的擅长

- 互联网：电商、P2P等等
- 企业级应用：ERP、CRM、BOS、OA等等

### Java语言平台

- JavaSE（标准版）部分,JavaSE并不能开发大型项目。
- JavaEE（企业版）部分,学习完JavaEE部分就可以开发各种大型项目了。

## **java**语言开发环境

JDK是Java开发环境，官网 http://www.oracle.com/cn/index.html

### JDK的安装

傻瓜式安装，双击安装程序，然后一路next即可，安装的推荐方式：

- 安装路径不要有中文或者特殊符号如空格等。
- 所有和开发相关的软件最好安装目录统一。
- 当提示安装JRE时，可以选择不安装。建议还是安装上。

 验证安装是否成功，通过DOS命令，切换到JDK安装的bin目录下。比如 D:\develop\Java\jdk1.7.0_72\bin，然后分别输入javac和java，如果正常显示一些内容，说明安装成功。

### 配置环境变量

环境变量的作用：由于javac和java命令只能在固定的目录下才能执行，而我们写的代码如果都和javac及java命令放在相同的目录中的话，会显得很乱”，为了让Java的bin目录下的javac命令可以在任意目录下执行，就得配置环境变量。

具体安装参考：[JAVA开发环境的搭建（配置JAVA开发环境）](http://www.cnblogs.com/Belieflee/p/4778315.html)

**JDK****和****JRE以及****跨平台**

JDK与JRE的关系

- JDK：Java Development Kit ，Java语言的开发工具包，提供了Java语言的开发工具，它里面包含了JRE，同时也就包含了JVM（Java虚拟机）。
- JRE：Java Runtime Environment，它是Java运行环境，如果你不需要开发只需要运行Java程序，那么你可以安装JRE。例如程序员开发出的程序最终卖给了用户，用户不用开发，只需要运行程序，所以用户在电脑上安装JRE即可。它包含了Java虚拟机，也就是JVM，同时还包含了Java语言运行需要的核心类库。

跨平台特性：平台指的是操作系统 （Windows，Linux，Mac）。只需在相应的平台上安装Java虚拟机，就可以运行Java程序。

## 使用IntelliJ IDEA打印Hello World

### 第一步：创建新项目

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170701211232211-2109811476.png)

### 第二步：选择jdk，然后next

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170701211457883-150724723.png)

### 第三步：选择Hello World模板，然后Next

 ![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170701211626743-101552981.png)

### 第四步：输入项目名称，然后Finish

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170701211759305-689114650.png)

### 第五步：运行

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170701211901883-623625448.png)

### 第六步：查看结果

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170701211940899-68699482.png)

## Java代码的编写执行过程

源文件：编写Java源文件（我们也称之为源代码文件），它的扩展名为.java；

编译：然后通过编译器把源文件编译成字节码文件，字节码文件扩展名为.class；

运行：最后使用解释器来运行字节码文件。

## CentOS7下Java8安装

1、到https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html找到jdk-8u221-linux-x64.tar.gz的下载地址，需要登录。

2、打开终端，使用 wget命令下载。比如：wget https://download.oracle.com/otn/java/jdk/8u221-b11/230deb18db3e4014bb8e3e8324f81b43/jdk-8u221-linux-x64.tar.gz?AuthParam=1569641530_05c699a00ac2afe0c0dde7cc5784e4d5

3、解压，tar -xzvf jdk-8u221-linux-x64.tar.gz?AuthParam=1569641530_05c699a00ac2afe0c0dde7cc5784e4d5

4、移动到/usr/local目录下，mv jdk-8u221-linux-x64.tar.gz?AuthParam=1569641530_05c699a00ac2afe0c0dde7cc5784e4d5 /opt/usr

5、切换到opt目录下，cd /opt/usr

6、改名为java8，mv jdk-8u221-linux-x64.tar.gz?AuthParam=1569641530_05c699a00ac2afe0c0dde7cc5784e4d5 java8

7、配置环境变量，vi /etc/profile,在文件后面追加以下代码：

JAVA_HOME=/usr/local/java8
JRE_HOME=/usr/local/java8/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH

8、执行source /etc/profile命令使配置生效，到这一步就算安装完成了，使用java -version查看安装是否成功。

# [Java基础学习笔记二 Java基础语法](https://www.cnblogs.com/ginb/p/7103664.html)

## 注释

注释用来解释和说明程序的文字，注释是不会被执行的.

单行注释

```
//这是一条单行注释 
public int i;
```

多行注释



```
/* 这是
* 一段注释，
* 它跨越了多个行
*/ 
public void f() {}
}
```



文档注释 



```
/** The first Thinking in Java example program.
* Lists system information on current machine.
* @author Bruce Eckel
* @author http://www.BruceEckel.com
* @version 1.0
*/
public class Property {
/** Sole entry point to class & application
* @param args array of string arguments
* @return No return value
* @exception exceptions No exceptions thrown
*/
public static void main(String[] args) {
System.out.println(new Date());
Properties p = System.getProperties();
p.list(System.out);
System.out.println("--- Memory Usage:");
Runtime rt = Runtime.getRuntime();
System.out.println("Total Memory = "
+ rt.totalMemory()
+ " Free Memory = "
+ rt.freeMemory());
}59
}
```



对于单行和多行注释，被注释的文字，不会被JVM解释执行；对于文档注释，可以被JDK提供的工具javadoc 所解析，生成一套以网页文件形式体现的该程序的说明文档；单行注释可以嵌套使用，多行注释不能嵌套使用。

## **关键字**

是被Java语言赋予特殊含义，具有专门用途的单词，比如class，int，double均为Java已经预设好的;

组成关键字的字母全部小写 ,注意String不是关键字;

goto与const是Java中的保留字，即没有赋予特殊含义却仍被Java占用的单词;

## **标识符**

就是给类,接口,方法,变量等起名字时使用的字符序列,组成规则只能包含下面的内容,不能有其它内容:

-  英文大小写字母
- 数字字符
-  $和_

### 注意事项

- 数字不能开头
- 不可以使用关键字
- 严格区分大小写，不限制长度
- 起名时，尽量见名知意

### 标识符中常见的命名规则

- 包名：多单词组成时所有字母均小写，使用.连接.比如：aaa.bbb.ccc
- 类名&接口名：大驼峰式。比如：AaaBbbCcc
- 变量名&方法名：小驼峰式。比如：aaaBbbCcc
- 常量名：多单词组成是所有字母均大写，使用_连接。比如：AAA_BBB_CCC

## 数据类型

为什么有数据类型？

Java是强类型语言，对于每一种数据都定义了明确的具体数据类型，变量必须要有明确的类型，什么类型的变量装载什么类型的数据。

### 数据类型的分类

基本数据类型

基本数据类型是Java语言中内置的类型，分别是整数类型、小数类型、字符类型、布尔类型。

这四类基本类型是最简单、最基础的类型。

- 整数(byte、short、int、long)，默认的整数类型是int类型，long类型需添加"L"后缀。
- 小数(float、double)、字符类型(char)，默认的浮点类型是double类型。在Java中所有没有后缀以及使用“D”后缀（小写也可以，但建议使用大写）的小数都是double类型；float类型常量必须添加“F”后缀
- 字符类型（char）
- 布尔类型(boolean)

引用数据类型

引用数据类型是强大的数据类型，它是基于基本数据类型创建的。JavaSE中提供了一个超级类库，类库中包含了近万种引用数据类型。比如：数组、类、接口。

## **常量**

常量就是不变的数据量, 在程序执行的过程中其值不可以发生改变

### 常量分类

整数类型

- 十进制表示方式：正常数字，如 13、25等
- 二进制表示方式：以0b(0B)开头，如0b1011 、0B1001
- 十六进制表示方式：以0x(0X)开头，数字以0-9及A-F组成  如0x23A2、0xa、0x10
- 八进制表示方式：以0开头，如01、07、0721

小数类型，如1.0、-3.15、3.168等

布尔类型， true、false

字符类型，字符必须使用’’ 包裹，并且其中只能且仅能包含一个字符。如'a'，'A', '0', '家'

字符串类型，一种引用类型，字符串必须使用""包裹，其中可以包含0~N个字符。如"我爱Java"，"0123"，""，"null"

### **在程序中输出Java中的常量**



```
public class Main {
    public static void main(String[] args) {
        //输出整数 十进制
        System.out.println(50);//50
        //输出整数，二进制, 数字开头0B
        System.out.println(0B11);//3
        //输出整数，八进制，数字开头0
        System.out.println(051);//41
        //输出整数，十六进制，数组开头0X  0-9 A-F
        System.out.println(0XE);//14
        //输出浮点数据
        System.out.println(5.0);//5.0
        //输出布尔数据，只有2个值，true，false 关键字
        System.out.println(true);//true
        System.out.println(false);//false
        //输出字符常量，单引号包裹，只能写1个字符
        System.out.println('a');//a
        //输出字符串常量，双引号包裹，可以写0-n个字符
        System.out.println("HelloWorld");//HelloWorld
    }
}
```



## **变量**

### **什么是变量?**

变量是一个内存中的小盒子（小容器），容器是什么？生活中也有很多容器，例如水杯是容器，用来装载水；你家里的大衣柜是容器，用来装载衣裤；饭盒是容器，用来装载饭菜。

那么变量是装载什么的呢？答案是数据！结论：变量是内存中装载数据的小盒子，你只能用它来存数据和取数据。

### 定义变量

```
数据类型  变量名  =  数据值；
int         a    =  100;
```

### **变量使用的注意事项**

变量定义后可以不赋值，使用时再赋值。不赋值不能使用。

```
int x;
x = 20; //为x赋值20
```

变量使用时有作用域的限制。



```
public static void main(String[] args) {
    int x = 20;
    {
        int y = 20;
    }
    System.out.println(x);//读取x变量中的值，再打印
    System.out.println(y);//读取y变量中的值失败，失败原因，找不到y变量，因为超出了y变量作用范围，所以不能使用y变量
}
```



变量不可以重复定义。

```
public static void main(String[] args){
      int x = 10;
      double x = 5.5;//编译失败，变量重复定义
}
```

## 数据类型转换

不同类型的变量可以在一起运算，但要先进行类型转换再运算。

- 范围小的数据类型值（如byte），可以直接转换为范围大的数据类型值（如int）；
- 范围大的数据类型值（如int），不可以直接转换为范围小的数据类型值（如byte）

数据范围从小到大依次列出：byte -> short -> int -> long -> float -> double

两种方式的数据类型转换

自动类型转换：表示范围小的数据类型转换成范围大的数据类型。格式：

```
范围大的数据类型 变量 = 范围小的数据类型值；
比如：double d = 1000; 
```

强制类型转换：表示范围大的数据类型转换成范围小的数据类型

```
范围小的数据类型  变量 = (范围小的数据类型) 范围大的数据类型值;
比如：int  i = (int)6.718;   //i的值为6
```

## 运算符

### 算数运算符

加号（ +）、减号和负号（ -）、乘号（ *）、除号（ /）、取模（%）、自增（++）、自减（--）以及等号（ =）的用法与其他所有编程语言都是类似的 。

++,--运算符后置时，先使用变量a原有值参与运算操作，运算操作完成后，变量a的值自增1或者自减1。

l ++，--运算符前置时，先将变量a的值自增1或者自减1，然后使用更新后的新值参与运算操作。

### 赋值运算符

赋值（=）、加后赋值（+=）、减后赋值（-=）、乘后赋值（*=）、整除后赋值（/=）取模后赋值（%=）的用法与其他所有编程语言都是类似的 。

### 关系运算符

等于（==）  不等于（!=） 小于（<） 大于（>）  小于等于（<=） 大于等于（>=）的用法与其他所有编程语言都是类似的 。

### **逻辑运算符**

与（&&）、或（||）、非（!）的用法与其他所有编程语言都是类似的 。

短路：当使用与或者或时，只要能判断出结果则后边的部分就不再判断。

### **三元运算符**

(条件表达式)？表达式1：表达式2；

```
int n = (3>2 && 4>6) ? 100 : 200;
//逻辑运算后的结果为false，运算结果为表达式2的值200,然后将结果200赋值给了变量n
```

## 商场库存清单案例

案例输出结果如下：

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702005415883-632304767.png)

### **案例需求分析**

观察清单后，可将清单分解为三个部分（清单顶部、清单中部、清单底部）

清单顶部为固定的数据，直接打印即可
清单中部为商品，为变化的数据，需要记录商品信息后，打印，经过观察，我们确定一项商品应该有如下几个属性：

- 品牌型号: 即商品名称，String型
- 尺寸：物品大小，double型
- 价格：物品单价，double型
- 配置：这一项为每种商品的配置信息，String型
- 库存数：这一项为每种商品的库存个数，int型

清单底部包含了统计操作，需经过计算后，打印，我们发现两个单独的可变化量：

- 总库存数：所有商品总个数，int型
- 库存商品总金额：所有商品金额，double型



```
public class Main {
    public static void main(String[] args) {
        //苹果笔记本电脑
        String macBrand = "MacBookAir";
        double macSize = 13.3;
        double macPrice = 6988.88;
        int macCount = 5;

        //联想Thinkpad笔记本电脑
        String thinkpadBrand = "ThinkpadT450";
        double thinkpadSize = 14.0;
        double thinkpadPrice = 5999.99;
        int thinkpadCount = 10;

        //华硕ASUS笔记本电脑
        String ASUSBrand = "ASUS-FL5800";
        double ASUSSize = 15.6;
        double ASUSPrice = 4999.50;
        int ASUSCount = 18;
        //统计所有库存商品数量与金额
        //统计库存总个数、库存总金额
        int totalCount = macCount + thinkpadCount + ASUSCount;
        double totalMoney = (macCount * macPrice) + (thinkpadCount * thinkpadPrice) + (ASUSCount * ASUSPrice);
        //打印库存清单顶部信息
        System.out.println("------------------------------商城库存清单-----------------------------");
        System.out.println("品牌型号    尺寸    价格    库存数");
        //打印库存清单中部信息
        System.out.println(macBrand + "    " + macSize + "    " + macPrice + "    " + macCount);
        System.out.println(thinkpadBrand + "    " + thinkpadSize + "    " + thinkpadPrice + "    " + thinkpadCount);
        System.out.println(ASUSBrand + "    " + ASUSSize + "    " + ASUSPrice + "    "+ASUSCount);
        //打印库存清单底部信息
        System.out.println("-----------------------------------------------------------------------");
        System.out.println("总库存数：" + totalCount);
        System.out.println("库存商品总金额：" + totalMoney);
    }
}
```

# [Java基础学习笔记三 Java基础语法](https://www.cnblogs.com/ginb/p/7105719.html)

## Scanner类

Scanner类属于引用数据类型，先了解下引用数据类型。

### 引用数据类型的使用

与定义基本数据类型变量不同，引用数据类型的变量定义及赋值有一个相对固定的步骤或格式。

```
数据类型  变量名  =  new 数据类型();
```

每种引用数据类型都有其功能，我们可以调用该类型实例使用其功能。

```
变量名.方法名();
```

## Scanner类

Scanner类可以完成用户键盘录入，获取到录入的数据。

Scanner使用步骤：

导包： import java.util.Scanner; 

创建对象实例：Scanner sc = new Scanner(System.in); 

调用方法：

```
int  i = sc.nextInt(); 用来接收控制台录入的数字

String s = sc.next(); 用来接收控制台录入的字符串
```

了解完Scanner类，我们编写代码来使用下它：ScannerDemo01.java



```
import java.util.Scanner;
public class ScannerDemo01 {
    public static void main(String[] args) {
        //创建Scanner引用类型的变量
        Scanner sc = new Scanner(System.in);
        //获取数字
        System.out.println("请输入一个数字");
        int n = sc.nextInt();
        System.out.println("n的值为" + n);
        //获取字符串
        String str = sc.next();
        System.out.println("str的值为" + str);

    }
}
```



运行结果如下图所示:

 ![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702115309524-1586429438.png)

##  **随机数类Random**

用来产生随机数的类Random，它也属于引用数据类型。

这个Random类，它可以产生多种数据类型的随机数，在这里主要介绍生成整数与小数的方式。

方法简介

```
public int nextInt(int maxValue) 产生[0,maxValue)范围的随机整数，包含0，不包含maxValue；

public double nextDouble()  产生[0,1)范围的随机小数，包含0.0，不包含1.0。
```

 Random使用方式:

import导包： java.util.Random 

创建实例格式 ：Random 变量名 = new Random(); 

接下来，通过一段代码，学习下Random类的使用，RandomDemo.java



```
import java.util.Random;
public class RandomDemo {
    public static void main(String[] args) {
        // 创建Random类的实例
        Random r = new Random();
        // 得到0-100范围内的随机整数，将产生的随机整数赋值给i变量
        int i = r.nextInt(100);
        //得到0.0-1.0范围内的随机小数，将产生的随机小数赋值给d变量
        double d = r.nextDouble();
        System.out.println(i);
        System.out.println(d);
    }
}
```



运行结果如下图所示：

 ![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702120054883-1319785629.png)

## 流程控制语句

### 选择结构if

 **if语句**

if语句是指如果满足某种条件，就进行某种处理。

在Java中，if语句的具体语法格式如下：



```
if (条件语句){

执行语句;

……

}
```



上述格式中，判断条件是一个布尔值，当判断条件为true时，{}中的执行语句才会执行。

接下来通过一段代码，学习一下if语句的具体用法，IfDemo01.java 



```
//定义了一个变量x，其初始值为5。在if语句的判断条件中判断x的值是否小于10，很明显条件成立，{}中的语句会被执行，变量x的值将进行自增。从运行结果可以看出，x的值已由原来的5变成了6。public class IfDemo01 {
    public static void main(String[] args) {
        int x = 5;
        if (x < 10) {
            x++;
        }
        System.out.println("x=" + x);//x=6
    }
}
```



### **if…****else语句**

if…else语句是指如果满足某种条件，就进行某种处理，否则就进行另一种处理。if…else语句具体语法格式如下：



```
if (判断条件){
    执行语句1
    ……
}else{
    执行语句2
    ……
}
```



上述格式中，判断条件是一个布尔值。当判断条件为true时，if后面{}中的执行语句1会执行。当判断条件为false时，else后面{}中的执行语句2会执行。

接下来通过一段代码，来实现判断奇偶数的程序，IfDemo02.java



```
public class IfDemo02 {
    public static void main(String[] args) {
        int num = 19;
        if (num % 2 == 0) {
        // 判断条件成立，num被2整除
            System.out.println("num是一个偶数");
        } else {
            System.out.println("num是一个奇数");
        }
    }
}
//num是一个奇数
```



上述代码中，变量num的值为19，模以2的结果为1，不等于0，判断条件不成立。因此会执行else后面{}中的语句，打印“num是一个奇数”。

### **if…****else if****…****else语句**

if…else if…else语句用于对多个条件进行判断，进行多种不同的处理。if…else if…else语句具体语法格式如下：



```
if (判断条件1) {
　　执行语句1
} else if (判断条件2) {
　　执行语句2
}
...
else if (判断条件n) {
　　执行语句n
} else {
　　执行语句n+1
}
```



上述格式中，判断条件是一个布尔值。当判断条件1为true时，if后面{}中的执行语句1会执行。当判断条件1为false时，会继续执行判断条件2，如果为true则执行语句2，以此类推，如果所有的判断条件都为false，则意味着所有条件均未满足，else后面{}中的执行语句n+1会执行。

接下来通过一段代码，来实现对学生考试成绩进行等级划分的程序，IfDemo03.java



```
public class IfDemo03 {
    public static void main(String[] args) {
        int grade = 75; // 定义学生成绩
        if (grade > 80) {
        // 满足条件 grade > 80
            System.out.println("该成绩的等级为优");
        } else if (grade > 70) {
        // 不满足条件 grade > 80 ，但满足条件 grade > 70
            System.out.println("该成绩的等级为良");
        } else if (grade > 60) {
        // 不满足条件 grade > 70 ，但满足条件 grade > 60
            System.out.println("该成绩的等级为中");
        } else {
        // 不满足条件 grade > 60
            System.out.println("该成绩的等级为差");
        }
    }
}
//该成绩的等级为良
```



上述代码中，定义了学生成绩grade为75。它不满足第一个判断条件grade>80，会执行第二个判断条件grade>70，条件成立，因此会打印“该成绩的等级为良”。

### **选择结构if语句与三元运算转换**

三元运算符，它和if-else语句类似，语法如下：

```
判断条件 ? 表达式1 : 表达式2
```

三元运算符会得到一个结果，通常用于对某个变量进行赋值，当判断条件成立时，运算结果为表达式1的值，否则结果为表达式2的值。

例如求两个数x、y中的较大者，如果用if…else语句来实现，具体代码如下：



```
int x = 0;
int y = 1;
int max;
if (x > y) {
　　max = x;
} else {
　　max = y;
}
```



可以替换为

```
int x=0;
int y=1;
int max = x > y ? x : y;
```

## **switch语句**

根据一个整数表达式的值， switch 语句可从一系列代码选出一段执行。它的格式如下：



```
switch(整数选择因子或者字符串或者枚举) {
　　case 整数值 1 : 语句; break;
　　case 整数值 2 : 语句; break;
　　case 整数值 3 : 语句; break;
　　case 整数值 4 : 语句; break;
　　case 整数值 5 : 语句; break;
　　//..
　　default:语句;92
}
```



switch 能将整数选择因子的结果与每个整数值比较。若发现相符的，就执行对应的语句（简单或复合语句）。若没有发现相符的，就执行default 语句。 示例：VowelsAndConsonants.java



```
public class VowelsAndConsonants {
    public static void main(String[] args) {
        char c = (char) (Math.random() * 26 + 'a');
        System.out.print(c + ": ");
        switch (c) {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                System.out.println("vowel");
                break;
            case 'y':
            case 'w':
                System.out.println(
                        "Sometimes a vowel");
                break;
            default:
                System.out.println("consonant");
        }
    }
}
```



### switch语句接受的数据类型

switch语句中的表达式的数据类型,是有要求的

- JDK1.0 - 1.4 数据类型接受 byte short int char
- JDK1.5 数据类型接受 byte short int char enum(枚举)
- JDK1.7 数据类型接受 byte short int char enum(枚举), String

### case穿透

在使用switch语句的过程中，如果多个case条件后面的执行语句是一样的，则该执行语句只需书写一次即可，这是一种简写的方式。
例如，要判断一周中的某一天是否为工作日，同样使用数字1~7来表示星期一到星期天，当输入的数字为1、2、3、4、5时就视为工作日，否则就视为休息日。如下所示。SwitchDemo02.java



```
public class SwitchDemo02 {
    public static void main(String[] args) {
        int week = 2;
        switch (week) {
            case 1:
            case 2:
            case 3:
            case 4:
            case 5:
                // 当 week 满足值 1、2、3、4、5 中任意一个时，处理方式相同
                System.out.println("今天是工作日");
                break;
            case 6:
            case 7:
                // 当 week 满足值 6、7 中任意一个时，处理方式相同
                System.out.println("今天是休息日");
                break;
        }
    }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702135211633-941232882.png)

上述代码中，当变量week值为1、2、3、4、5中任意一个值时，处理方式相同，都会打印“今天是工作日”。同理，当变量week值为6、7中任意一个值时，打印“今天是休息日”。

## 循环语句

### while语句

while循环语句和选择结构if语句有些相似，都是根据条件判断来决定是否执行大括号内的执行语句。区别在于，while语句会反复地进行条件判断，只要条件成立，{}内的执行语句就会执行，直到条件不成立，while循环结束。while循环语句的语法结构如下：

```
while(循环条件){
    执行语句
    ………
}
```

在上面的语法结构中，{}中的执行语句被称作循环体，循环体是否执行取决于循环条件。当循环条件为true时，循环体就会执行。循环体执行完毕时会继续判断循环条件，如条件仍为true则会继续执行，直到循环条件为false时，整个循环过程才会结束。

接下来通过一段代码，来实现打印1~4之间的自然数，WhileDemo.java



```
public class WhileDemo {
    public static void main(String[] args) {
        int x = 1; // 定义变量x，初始值为1
        while (x <= 4) { // 循环条件
            System.out.println("x = " + x); // 条件成立，打印x的值
            x++; // x进行自增
        }
    }
}

//x = 1
//x = 2
//x = 3
//x = 4
```



在上述代码中，x初始值为1，在满足循环条件x <= 4的情况下，循环体会重复执行，打印x的值并让x进行自增。因此打印结果中x的值分别为1、2、3、4。

值得注意的是，代码x++用于在每次循环时改变变量x的值，从而达到最终改变循环条件的目的。如果没有这行代码，整个循环会进入无限循环的状态，永远不会结束。

## **循环语句for**

for循环语句是最常用的循环语句，一般用在循环次数已知的情况下。for循环语句的语法格式如下：

```
for（初始化表达式; 循环条件; 操作表达式）{

    执行语句
    ………
}
```

在上面的语法结构中，for关键字后面()中包括了三部分内容：初始化表达式、循环条件和操作表达式，它们之间用“;”分隔，{}中的执行语句为循环体。

接下来分别用①表示初始化表达式、②表示循环条件、③表示操作表达式、④表示循环体，通过序号来具体分析for循环的执行流程。具体如下：

```
for（① ; ② ; ③）{
　　④
}
```

- 第一步，执行①
- 第二步，执行②，如果判断结果为true，执行第三步，如果判断结果为false，执行第五步
- 第三步，执行④
- 第四步，执行③，然后重复执行第二步
- 第五步，退出循环

接下来通过一个案例对自然数1~4进行求和，如下所示。ForDemo01.java



```
public class ForDemo01 {
    public static void main(String[] args) {
        int sum = 0; // 定义变量sum，用于记住累加的和
        for (int i = 1; i <= 4; i++) { // i的值会在1~4之间变化
            sum += i; // 实现sum与i的累加
        }
        System.out.println("sum = " + sum); // 打印累加的和
    }
}
```



上述代码中，变量i的初始值为1，在判断条件i<=4为true的情况下，会执行循环体sum+=i，执行完毕后，会执行操作表达式i++，i的值变为2，然后继续进行条件判断，开始下一次循环，直到i=5时，条件i<=4为false，结束循环，执行for循环后面的代码，打印“sum=10”。

## do…while语句

do…while循环语句和while循环语句功能类似，其语法结构如下：

```
do {

    执行语句
    ………
} while(循环条件);
```

在上面的语法结构中，关键字do后面{}中的执行语句是循环体。do…while循环语句将循环条件放在了循环体的后面。这也就意味着，循环体会无条件执行一次，然后再根据循环条件来决定是否继续执行。

接下来使用do…while循环语句来实现打印1~4之间的自然数DoWhileDemo.java。



```
public class DoWhileDemo {
    public static void main(String[] args) {
        int x = 1; // 定义变量x，初始值为1
        do {
            System.out.println("x = " + x); // 打印x的值
            x++; // 将x的值自增
        } while (x <= 4); // 循环条件
    }
}
```



do …while循环和while循环能实现同样的功能。然而在程序运行过程中，这两种语句还是有差别的。如果循环条件在循环语句开始时就不成立，那么while循环的循环体一次都不会执行，而do…while循环的循环体还是会执行一次。若将DoWhileDemo.java中的循环条件x<=4改为x < 1，DoWhileDemo.java运行结果会打印x=1，而WhileDemo.java运行结果什么也不会打印。

### **无限循环**

最简单无限循环格式：

```
while(true){}

或

for(;;){}
```

无限循环存在的原因是并不知道循环多少次，而是根据某些条件，来控制循环。

### 循环嵌套

嵌套循环是指在一个循环语句的循环体中再定义一个循环语句的语法结构。while、do…while、for循环语句都可以进行嵌套，并且它们之间也可以互相嵌套，如最常见的在for循环中嵌套for循环，格式如下：



```
for(初始化表达式; 循环条件; 操作表达式) {
    ………
    for(初始化表达式; 循环条件; 操作表达式) {
        执行语句
        ………
     }
    ………
}
```



接下来实现使用“*”打印直角三角形，如下所示。ForForDemo.java



```
public class ForForDemo {
    public static void main(String[] args) {
        int i, j; // 定义两个循环变量
        for (i = 1; i <= 9; i++) { // 外层循环
            for (j = 1; j <= i; j++) { // 内层循环
                System.out.print("*"); // 打印*
            }
            System.out.print("\n"); // 换行
        }
    }
}
```



运行结果如下所示：

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702122412493-715167864.png)

在上述代码中定义了两层for循环，分别为外层循环和内层循环，外层循环用于控制打印的行数，内层循环用于打印“*”，每一行的“*”个数逐行增加，最后输出一个直角三角形。由于嵌套循环程序比较复杂，下面分步骤进行详细地讲解，具体如下：

- 第一步，在第3行代码定义了两个循环变量i和j，其中i为外层循环变量，j为内层循环变量。
- 第二步，在第4行代码将i初始化为1，条件i <= 9为true，首次进入外层循环的循环体。
- 第三步，在第5行代码将j初始化为1，由于此时i的值为1，条件j <= i为true，首次进入内层循环的循环体，打印一个“*”。
- 第四步，执行第5行代码中内层循环的操作表达式j++，将j的值自增为2。
- 第五步，执行第5行代码中的判断条件j<=i，判断结果为false，内层循环结束。执行后面的代码，打印换行符。
- 第六步，执行第4行代码中外层循环的操作表达式i++，将i的值自增为2。
- 第七步，执行第4行代码中的判断条件i<=9，判断结果为true，进入外层循环的循环体，继续执行内层循环。
- 第八步，由于i的值为2，内层循环会执行两次，即在第2行打印两个“*”。在内层循环结束时会打印换行符。
- 第九步，以此类推，在第3行会打印3个“*”，逐行递增，直到i的值为10时，外层循环的判断条件i <= 9结果为false，外层循环结束，整个程序也就结束了。

## 跳转语句（break、continue）

跳转语句用于实现循环执行过程中程序流程的跳转，在Java中的跳转语句有break语句和continue语句。接下来分别进行详细地讲解。

### **break语句**

在switch条件语句和循环语句中都可以使用break语句。当它出现在switch条件语句中时，作用是终止某个case并跳出switch结构。当它出现在循环语句中，作用是跳出循环语句，执行后面的代码。

接下来通过下面一段代码，实现将当变量x的值为3时，使用break语句跳出循环，代码如下所示。BreakDemo.java



```
public class BreakDemo {
    public static void main(String[] args) {
        int x = 1; // 定义变量x，初始值为1
        while (x <= 4) { // 循环条件
            System.out.println("x = " + x); // 条件成立，打印x的值
            if (x == 3) {
                break;
            }
            x++; // x进行自增
        }
    }
}
```



```
在上述带代码中，通过while循环打印x的值，当x的值为3时使用break语句跳出循环。因此打印结果中并没有出现“x=4”。
```

### **标记**

当break语句出现在嵌套循环中的内层循环时，它只能跳出内层循环，如果想使用break语句跳出外层循环则需要对外层循环添加标记。接下来将ForForDemo.java稍作修改，控制程序只打印4行“*”，如下所示。BreakDemo02.java



```
public class BreakDemo02 {
    public static void main(String[] args) {
        int i, j; // 定义两个循环变量
        AA: for (i = 1; i <= 9; i++) { // 外层循环
            for (j = 1; j <= i; j++) { // 内层循环
                if (i > 4) { // 判断i的值是否大于4
                    break AA; // 跳出外层循环
                }
                System.out.print("*"); // 打印*
            }
            System.out.print("\n"); // 换行
        }
    }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702124101680-38623529.png)

BreakDemo02.java与ForForDemo.java实现原理类似，只是在外层for循环前面增加了标记“AA”。当i>4时，使用break AA;语句跳出外层循环。因此程序只打印了4行“*”。

### **continue语句**

continue语句用在循环语句中，它的作用是终止本次循环，执行下一次循环。接下来通过一个练习对1~100之内的奇数求和，ContinueDemo.java



```
public class ContinueDemo {
    public static void main(String[] args) {
        int sum = 0; // 定义变量sum，用于记住和
        for (int i = 1; i <= 100; i++) {
            if (i % 2 == 0) { // i是一个偶数，不累加
                continue; // 结束本次循环
            }
            sum += i; // 实现sum和i的累加
        }
        System.out.println("sum = " + sum);
    }
}
//sum = 2500
```



上述代码中，使用for循环让变量i的值在1~100之间循环，在循环过程中，当i的值为偶数时，将执行continue语句结束本次循环，进入下一次循环。当i的值为奇数时，sum和i进行累加，最终得到1~100之间所有奇数的和，打印“sum = 2500”。

在嵌套循环语句中，continue语句后面也可以通过使用标记的方式结束本次外层循环，用法与break语句相似，在此不再举例说明。

## 猜数字案例

### **案例介绍**

猜数字案例是要完成什么样的功能呢？顾名思义，这个游戏就是你出个数字、我来猜。

游戏操作如下：

后台预先生成一个1-100之间的随机数，用户键盘录入猜数字

如果猜对了，打印“恭喜您，答对了”

如果猜错了

- 猜大了：打印“sorry，您猜大了!”
- 猜小了：打印“sorry，您猜小了!”
- 直到数字猜到为止

### 思路

1.通过Random类中方法nextInt（），生成一个1-100之间的随机数

2.输入猜的数字

3.通过while循环，进行猜数字对错判断

猜对，跳出循环，游戏结束

猜错了，根据结果，给出提示，接着猜数字，游戏继续

如果猜大了，打印sorry，您猜大了!继续下一次循环

如果猜小了，打印sorry，您猜小了!继续下一次循环

### **实现代码步骤**

分析完毕之后，完成代码的编写：GuessNumber.java



```
import java.util.Random;
import java.util.Scanner;

public class GuessNumber {
    public static void main(String[] args) {
//1.通过Random类中方法nextInt（），生成一个1-100之间的随机数
        int randomNumber = new Random().nextInt(100);
        System.out.println("随机数已生成！");
//2.输入猜的数字
        System.out.println("----请输入您猜的数字：----");
        Scanner sc = new Scanner(System.in);
        int enterNumber = sc.nextInt();
//3.通过while循环，进行猜数字对错判断
//猜对，跳出循环，游戏结束
        while (enterNumber != randomNumber) {
//猜错了，根据结果，给出提示，接着猜数字，游戏继续
            if (enterNumber > randomNumber) {
//如果猜大了，打印sorry，您猜大了!继续下一次循环
                System.out.println("sorry，您猜大了!继续下一次循环");
            } else {
//如果猜小了，打印sorry，您猜小了!继续下一次循环
                System.out.println("sorry，您猜小了!继续下一次循环");
            }
//输入猜的数字
            System.out.println("----请输入您猜的数字：----");
            enterNumber = sc.nextInt();
        }
        System.out.println("恭喜您，答对了！");
    }

}
```



运行结果：

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702124615571-1341936766.png)

# [Java基础学习笔记四 Java基础语法](https://www.cnblogs.com/ginb/p/7106177.html)

## 数组

### 数组的需求

现在需要统计某公司员工的工资情况，例如计算平均工资、最高工资等。假设该公司有50名员工，用前面所学的知识完成，那么程序首先需要声明50个变量来分别记住每位员工的工资，这样做会显得很麻烦.

### 数组的概述

数组是指一组数据的集合，数组中的每个数据被称作元素。在数组中可以存放任意类型的元素，但同一个数组里存放的元素类型必须一致。

### 数组的定义

格式:

```
数据类型[] 数组名 = new 数据类型[元素个数或数组长度];

举例:int[] x = new int[100];
```

要点说明

- 数据类型: 数组中存储元素的数据类型
-  [] 表示数组的意思
- 变量名 自定义标识符
- new 创建容器关键字
- 元素个数,就是数组中,可以存储多少个数据 (恒定, 定长)
- 数组是一个容器: 存储到数组中的每个元素,都有自己的自动编号(索引(index), 下标, 角标)
- 访问数组存储的元素,必须依赖于索引, 数组名[索引]
- 数组中最小的索引是0，最大的索引是“数组的长度-1”。

在程序中可以通过“数组名.length”的方式来获得数组的长度，即元素的个数。

接下来，通过一个案例来演示如何定义数组以及访问数组中的元素，如下所示。ArrayDemo01.java



```
 public class ArrayDemo01 {
    public static void main(String[] args) {
               int[] arr; // 声明变量
               arr = new int[3]; // 创建数组对象
               System.out.println("arr[0]=" + arr[0]); // 访问数组中的第一个元素
               System.out.println("arr[1]=" + arr[1]); // 访问数组中的第二个元素
               System.out.println("arr[2]=" + arr[2]); // 访问数组中的第三个元素
               System.out.println("数组的长度是：" + arr.length); // 打印数组长度
           }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702140516336-1098531363.png)

如果在使用数组时，不想使用这些默认初始值，也可以显式地为这些元素赋值。接下来通过一个程序来学习如何为数组的元素赋值，如下所示。ArrayDemo02.java



```
 public class ArrayDemo02 {
     public static void main(String[] args) {
                int[] arr = new int[4]; // 定义可以存储4个整数的数组
                arr[0] = 1; // 为第1个元素赋值1
                arr[1] = 2; // 为第2个元素赋值2
                // 下面的代码是打印数组中每个元素的值
                System.out.println("arr[0]=" + arr[0]);
                System.out.println("arr[1]=" + arr[1]);
                System.out.println("arr[2]=" + arr[2]);
                System.out.println("arr[3]=" + arr[3]);
            }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702140700743-1600859845.png)

在定义数组时只指定数组的长度，由系统自动为元素赋初值的方式称作动态初始化。

在初始化数组时还有一种方式叫做静态初始化，就是在定义数组的同时就为数组的每个元素赋值。数组的静态初始化有两种方式，具体格式如下：

```
方式1  　　类型[] 数组名 = new 类型[]{元素，元素，……};
方式2 　　 类型[] 数组名 = {元素，元素，元素，……};
```

上面的两种方式都可以实现数组的静态初始化，但是为了简便，建议采用第二种方式。接下来通过一段代码来演示数组静态初始化的效果，如下所示。ArrayDemo03.java



```
 public class ArrayDemo03 {
    public static void main(String[] args) {
                int[] arr = { 1, 2, 3, 4 }; // 静态初始化
                // 下面的代码是依次访问数组中的元素
                System.out.println("arr[0] = " + arr[0]);
                System.out.println("arr[1] = " + arr[1]);
                System.out.println("arr[2] = " + arr[2]);
                System.out.println("arr[3] = " + arr[3]);
            }
 }
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702140924914-682488071.png)

在操作数组时，经常需要依次访问数组中的每个元素，这种操作称作数组的遍历。接下来通过一个案例来学习如何使用for循环来遍历数组，如下所示。ArrayDemo04.java



```
public class ArrayDemo04 {
    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5 }; // 定义数组
        // 使用for循环遍历数组的元素
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]); // 通过索引访问元素
        }
    }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702141041539-1659043722.png)

数组在编写程序时应用非常广泛，灵活地使用数组对实际开发很重要。接下来，本节将针对数组的常见操作进行详细地讲解，如数组的遍历、最值的获取、数组的排序等。

在操作数组时，经常需要获取数组中元素的最值。接下来通过一个案例来演示如何获取数组中元素的最大值，如下所示。ArrayDemo05.java



```
public class ArrayDemo05 {
    public static void main(String[] args) {
        int[] arr = { 4, 1, 6, 3, 9, 8 }; // 定义一个数组
        int max = arr[0]; // 定义变量max用于记住最大数，首先假设第一个元素为最大值
        // 下面通过一个for循环遍历数组中的元素
        for (int x = 1; x < arr.length; x++) {
            if (arr[x] > max) { // 比较 arr[x]的值是否大于max
                max = arr[x]; // 条件成立，将arr[x]的值赋给max
            }
        }
        System.out.println("max=" + max); // 打印最大值
    }
}
//max=9
```



每个数组的索引都有一个范围，即0~length-1。在访问数组的元素时，索引不能超出这个范围，否则程序会报错

在使用变量引用一个数组时，变量必须指向一个有效的数组对象，如果该变量的值为null，则意味着没有指向任何数组，此时通过该变量访问数组的元素会出现空指针异常，接下来通过一个案例来演示这种异常，如下所示。ArrayDemo07.java



```
 public class ArrayDemo07 {
     public static void main(String[] args) {
                int[] arr = new int[3]; // 定义一个长度为3的数组
                arr[0] = 5; // 为数组的第一个元素赋值
                System.out.println("arr[0]=" + arr[0]); // 访问数组的元素
                arr = null; // 将变量arr置为null
                System.out.println("arr[0]=" + arr[0]); // 访问数组的元素
            }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702141339930-904244546.png)

## 二维数组

二维数组的定义有很多方式，接下来针对几种常见的方式进行详细地讲解，具体如下：

第一种方式： int[][] arr = new int[3][4]; 

第二种方式： int[][] arr = new int[3][]; 

第三种方式： int[][] arr = {{1,2},{3,4,5,6},{7,8,9}}; 

对二维数组中元素的访问也是通过角标的方式，如需访问二维数组中第一个元素数组的第二个元素，具体代码如下：

```
arr[0][1];
```

操作二维数组时，经常需要获取数组中元素的值。接下来通过一个案例来演示如何获取数组中元素值，如下所示。ArrayDemo08.java



```
class ArrayDemo08 {
    public static void main(String[] args){
        //定义二维数组的方式
        int[][] arr = new int[3][4];

        System.out.println( arr );
        System.out.println("二维数组的长度: " + arr.length);
        //获取二维数组的3个元素
        System.out.println( arr[0] );
        System.out.println( arr[1] );
        System.out.println( arr[2] );

        System.out.println("打印第一个一维数组的元素值");
        System.out.println( arr[0][0] );
        System.out.println( arr[0][1] );//访问的为二维数组中第1个一维数组的第2个元素
        System.out.println( arr[0][2] );
        System.out.println( arr[0][3] );

        System.out.println("打印第二个一维数组的元素值");
        System.out.println( arr[1][0] );
        System.out.println( arr[1][1] );
        System.out.println( arr[1][2] );
        System.out.println( arr[1][3] );

        System.out.println("打印第三个一维数组的元素值");
        System.out.println( arr[2][0] );
        System.out.println( arr[2][1] );
        System.out.println( arr[2][2] );
        System.out.println( arr[2][3] );
    }
}
```



运行结果：



```
[[I@1540e19d
二维数组的长度: 3
[I@677327b6
[I@14ae5a5
[I@7f31245a
打印第一个一维数组的元素值
0
0
0
0
打印第二个一维数组的元素值
0
0
0
0
打印第三个一维数组的元素值
0
0
0
0
```



学习完了数组元素的访问，我们来学习下数组的遍历及数组的元素累加和操作。



```
public class ArrayDemo09 {
    public static void main(String[] args){
        //一维数组的求累加和并遍历
        int[] arr = {10,20,30,40,50};
        int sum = 0;
        for (int i=0; i<arr.length; i++) {
            //System.out.println(arr[i]);
            sum += arr[i];
        }
        System.out.println("sum= " + sum);
        System.out.println("---------------------");

//二维数组的求累加和并遍历
        int[][] arr2 = { {1,2},{3,4,5},{6,7,8,9,10} };
        int sum2 = 0;
        for (int i=0; i<arr2.length; i++) {
            for (int j=0; j<arr2[i].length; j++) {
                //System.out.println(arr2[i][j])
                sum2 += arr2[i][j];
            }
        }
        System.out.println("sum2= "+ sum2);
    }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702141843946-2081583668.png)

接下来通过一个案例来熟悉二维数组的使用。例如要统计一个公司三个销售小组中每个小组的总销售额以及整个公司的销售额。如下所示

- 第一小组销售额为{11, 12}万元
- 第二小组销售额为{21, 22, 23}万元
- 第三小组销售额为{31, 32, 33, 34}万元。



```
/**
 * Created by yang on 2017/7/2.
 */
public class ArrayDemo10 {
    public static void main(String[] args) {
        int[][] arr = new int[3][]; // 定义一个长度为3的二维数组
        arr[0] = new int[]{11, 12}; // 为数组的元素赋值
        arr[1] = new int[]{21, 22, 23};
        arr[2] = new int[]{31, 32, 33, 34};

        int sum = 0; // 定义变量记录总销售额
        for (int i = 0; i < arr.length; i++) { // 遍历数组元素
            int groupSum = 0; // 定义变量记录小组销售总额
            for (int j = 0; j < arr[i].length; j++) { // 遍历小组内每个人的销售额
                groupSum = groupSum + arr[i][j];
            }
            sum = sum + groupSum; // 累加小组销售额
            System.out.println("第" + (i + 1) + "小组销售额为：" + groupSum + " 万元");
        }
        System.out.println("总销售额为: " + sum + " 万元");
    }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702142106868-34781443.png)

### JVM内存划分 

 JVM对自己的内存划分为5个区域

- 寄存器:内存和CUP之间
- 本地方法栈: JVM调用了系统中的功能
- 方法和数据共享: 运行时期class文件进入的地方
- 方法栈:所有的方法运行的时候进入内存
- 堆:存储的是容器和对象

### 数组的内存

int[] x; // 声明一个int[]类型的变量
x = new int[100]; // 创建一个长度为100的数组
接下来，通过两张内存图来详细地说明数组在创建过程中内存的分配情况。
第一行代码 int[] x; 声明了一个变量x，该变量的类型为int[]，即一个int类型的数组。变量x会占用一块内存单元，它没有被分配初始值
第二行代码 x = new int[100]; 创建了一个数组，将数组的地址赋值给变量x。在程序运行期间可以使用变量x来引用数组，这时内存中的状态会发生变化

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702142732039-1063723182.png)![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702142742836-849345736.png)

### 数组中常见的异常

数组操作中,常见的两个异常
数组的索引越界异常
空指针异常

### 二维数组内存图

举例:int[][] arr = new int[3][4];
外层数组长在内存开辟连续的3个大的内存空间,每一个内存空间都对应的有地址值
每一个大内存空间里又开辟连续的四个小的内存空间.

 ![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702143034743-578977863.png)

## 方法

在java中，方法就是用来完成解决某件事情或实现某个功能的办法。

### **方法的语法格式**

在Java中，声明一个方法的具体语法格式如下：

```
修饰符 返回值类型 方法名(参数类型 参数名1,参数类型 参数名2,．．．．．．){ 
    执行语句
    ……… 
    return 返回值;
}
```

对于上面的语法格式中具体说明如下：

- 修饰符：方法的修饰符比较多，有对访问权限进行限定的，有静态修饰符static，还有最终修饰符final等，这些修饰符在后面的学习过程中会逐步介绍
- 返回值类型：用于限定方法返回值的数据类型
- 参数类型：用于限定调用方法时传入参数的数据类型
- 参数名：是一个变量，用于接收调用方法时传入的数据
- return关键字：用于结束方法以及返回方法指定类型的值
- 返回值：被return语句返回的值，该值会返回给调用者

### 方法使用的注意事项

- 方法不调用，自己不执行
- 方法中不能定义方法， 但是，方法中可以调用方法
- 方法定义的位置在类中，其他方法的外面
- 方法中的“参数类型 参数名1，参数类型 参数名2”被称作参数列表，它用于描述方法在被调用时需要接收的参数，如果方法不需要接收任何参数，则参数列表为空，即()内不写任何内容。
- 如果方法没有明确的返回值类型，使用'空'类型， void表示
- void只能在方法返回值类型位置使用，不能作为普通的数据类型使用
- 如果方法返回值类型为void类型，可以省略 return ;

接下来通过一个案例来演示方法的定义与使用，如下图所示。MethodDemo01.java



```
public class MethodDemo01 {
    public static void main(String[] args) {
        int area = getArea(3, 5); // 调用 getArea方法
        System.out.println(" The area is " + area);
    }

    // 下面定义了一个求矩形面积的方法，接收两个参数，其中x为高，y为宽
    public static int getArea(int x, int y) {
        int temp = x * y; // 使用变量temp记住运算结果
        return temp; // 将变量temp的值返回
    }
}
```



###  方法的重载

Java允许在一个类中定义多个名称相同的方法，但是参数的类型或个数必须不同，这就是方法的重载。

比如，下面的三个方法互为重载关系

```
public static int add(int x,int y) {逻辑} //两个整数加法

public static int add(int x,int y,int z) {逻辑} //三个整数加法

public static int add(double x,double y) {逻辑} //两个小数加法
```

接下来演示方法重载的方式如下所示。MethodDemo03.java



```
public class MethodDemo03 {
    public static void main(String[] args) {
        // 下面是针对求和方法的调用
        int sum1 = add(1, 2);
        int sum2 = add(1, 2, 3);
        double sum3 = add(1.2, 2.3);
        // 下面的代码是打印求和的结果
        System.out.println("sum1=" + sum1);
        System.out.println("sum2=" + sum2);
        System.out.println("sum3=" + sum3);
    }

    // 下面的方法实现了两个整数相加
    public static int add(int x, int y) {
        return x + y;
    }
    // 下面的方法实现了三个整数相加
    public static int add(int x, int y, int z) {
        return x + y + z;
    }
    // 下面的方法实现了两个小数相加
    public static double add(double x, double y) {
        return x + y;
    }
}
```



![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702160449571-810856488.png)

### 重载的注意事项

重载方法参数必须不同：

- 参数个数不同，如method(int x)与method(int x,int y)不同
- 参数类型不同，如method(int x)与method(double x)不同
- 参数顺序不同，如method(int x,double y)与method(double x,int y)不同

重载只与方法名与参数类型相关，与返回值无关。如void method(int x)与int method(int y)不是方法重载，不能同时存在

重载与具体的变量标识符无关。如method(int x)与method(int y)不是方法重载，不能同时存在

###  **参数传递**

定义方法时，参数列表中的变量，我们称为形式参数

调用方法时，传入给方法的数值，我们称为实际参数

### 参数传递图解与结论

 ![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170702160802977-2042370146.png)

通过上面的两段程序可以得出如下结论：

- 当调用方法时，如果传入的数值为基本数据类型（包含String类型），形式参数的改变对实际参数不影响
- 当调用方法时，如果传入的数值为引用数据类型（String类型除外），形式参数的改变对实际参数有影响

##  库存管理案例

现在，我们将原有的库存管理案例，进行业务逻辑的封装。

将对下列功能进行方法封装：

- 打印库存清单功能
- 库存商品数量修改功能
- 退出程序功能

编写代码，StockMamager.java



```
import java.util.Scanner;

/**
 * Created by yang on 2017/7/2.
 */
public class StockMamager {
    /**
     * 库存管理功能菜单
     * @return 管理员键盘输入的功能操作序号
     */
    public static int chooseFunction() {
        System.out.println("-------------库存管理------------");
        System.out.println("1.查看库存清单");
        System.out.println("2.修改商品库存数量");
        System.out.println("3.退出");
        System.out.println("请输入要执行的操作序号：");
        //接收键盘输入的功能选项序号
        Scanner sc = new Scanner(System.in);
        int choose = sc.nextInt();
        return choose;
    }
    /**
     * 查看库存清单
     * @param brands 商品品牌型号
     * @param sizes 商品尺寸大小
     * @param prices 商品价格
     * @param counts 商品库存个数
     */
    public static void printStore(String[] brands, double[] sizes, double[] prices, int[] counts) {
        //统计总库存个数、统计库存总金额
        int totalCount = 0;
        double totalMoney = 0.0;
        for (int i = 0; i < brands.length; i++) {
            totalCount += counts[i];
            totalMoney += counts[i] * prices[i];
        }
        //列表顶部
        System.out.println("---------------------------查看库存清单--------------------------");
        System.out.println("品牌型号        尺寸    价格    库存数");
        //列表中部
        for (int i = 0; i < brands.length; i++) {
            System.out.println(brands[i]+"    "+sizes[i]+"    "+prices[i]+"    "+counts[i]);
        }
        //列表底部
        System.out.println("-------------------------------------------------------------");
        System.out.println("总库存数："+totalCount);
        System.out.println("库存商品总金额："+totalMoney);
    }

    /**
     * 修改商品库存数量
     * @param brands 商品品牌型号
     * @param counts 商品库存个数
     */
    public static void update(String[] brands, int[] counts){
        System.out.println("------------修改商品库存数量-----------");
        for (int i = 0; i < brands.length; i++) {
            System.out.println("请输入"+ brands[i] +"商品库存数");
            counts[i] = new Scanner(System.in).nextInt();
        }
    }

    /**
     * 退出
     */
    public static void exit(){
        System.out.println("----------------退出---------------");
        System.out.println("您已退出系统");
    }

    public static void main(String[] args) {
        //记录库存商品信息
        //品牌型号
        String[] brands = new String[]{"MacBookAir", "ThinkpadT450"};
        //尺寸大小
        double[] sizes = new double[]{13.3, 14.0};
        //价格
        double[] prices = new double[]{6988.88, 5999.99};
        //库存个数
        int[] counts = new int[]{0, 0};

        //通过while循环模拟管理员进行功能重复选择操作
        while (true) {
            //打印功能菜单操作,接收键盘输入的功能选项序号
            int choose = chooseFunction();
            //执行序号对应的功能
            switch (choose) {
                case 1://查看库存清单
                    printStore(brands, sizes, prices, counts);
                    break;
                case 2://修改商品库存数量
                    update(brands, counts);
                    break;
                case 3://退出
                    exit();
                    return;
                default:
                    System.out.println("----------------------------------");
                    System.out.println("功能选择有误，请输入正确的功能序号!");
                    break;
            }
        }
    }
}
```



 运行结果如下：



```
-------------库存管理------------
1.查看库存清单
2.修改商品库存数量
3.退出
请输入要执行的操作序号：
1
---------------------------查看库存清单--------------------------
品牌型号        尺寸    价格    库存数
MacBookAir    13.3    6988.88    0
ThinkpadT450    14.0    5999.99    0
-------------------------------------------------------------
总库存数：0
库存商品总金额：0.0
-------------库存管理------------
1.查看库存清单
2.修改商品库存数量
3.退出
请输入要执行的操作序号：
2
------------修改商品库存数量-----------
请输入MacBookAir商品库存数
222
请输入ThinkpadT450商品库存数
15454
-------------库存管理------------
1.查看库存清单
2.修改商品库存数量
3.退出
请输入要执行的操作序号：
1
---------------------------查看库存清单--------------------------
品牌型号        尺寸    价格    库存数
MacBookAir    13.3    6988.88    222
ThinkpadT450    14.0    5999.99    15454
-------------------------------------------------------------
总库存数：15676
库存商品总金额：9.427537682E7
-------------库存管理------------
1.查看库存清单
2.修改商品库存数量
3.退出
请输入要执行的操作序号：
3
----------------退出---------------
您已退出系统

Process finished with exit code 0
```

# [Java基础学习笔记五 Java基础语法之面向对象](https://www.cnblogs.com/ginb/p/7124041.html)

## 面向对象

### 理解什么是面向过程、面向对象

面向过程与面向对象都是我们编程中，编写程序的一种思维方式。
面向过程的程序设计方式，是遇到一件事时，思考“我该怎么做”，然后一步步实现的过程。
例如：公司打扫卫生（擦玻璃、扫地、拖地、倒垃圾等），按照面向过程的程序设计方式会思考“打扫卫生我该怎么做，然后一件件的完成”，最后把公司卫生打扫干净了。
面向对象的程序设计方式，是遇到一件事时，思考“我该让谁来做”，然后那个“谁”就是对象，他要怎么做这件事是他自己的事，反正最后一群对象合力能把事就好就行了。
例如，公司打扫卫生（擦玻璃、扫地、拖地、倒垃圾等），按照面向对象的程序设计方式会思考“我该让谁来做，如小明擦玻璃、让小丽扫地、让小郭拖地、让小强倒垃圾等”,这里的“小明、小丽、小郭、小强”就是对象，他们要打扫卫生，怎么打扫是他们自己的事，反正最后一群对象合力把公司卫生打扫干净了。

### 面向对象举例

买电脑（组装机）
使用面向过程说明买电脑这件事：上网查询参数和报价、电脑城询价、现场安装和监督、抱电脑回家。在整个过程中我们参与了每一个细节，并且会感觉相当累。
使用面向对象说明买电脑这件事：假如我们需要买组装机，这时应该找一个懂电脑硬件的人，让他帮我们查看参数和报价，并进行询价和杀价，以及现场组装监督。而我们自己并不需要亲历亲为具体怎么做，只要告诉这个人我们想要的具体需求即可。分析上述整个过程，发现瞬间变的十分轻松，只要找到懂电脑硬件的这个人，我们的问题都可以解决。并且在这个过程中我们不用那么辛苦。

面向对象思维方式的好处

通过生活中的真实场景使用面向对象分析完之后，我们开始分析面向过程和面向对象的差异做出总结：

- 面向对象思维方式是一种更符合人们思考习惯的思想
- 面向过程思维方式中更多的体现的是执行者（自己做事情），面向对象中更多的体现是指挥者（指挥对象做事情）。
- 面向对象思维方式将复杂的问题简单化。

## 类与对象

### 对象在需求中的使用

对面向对象有了了解之后，我们来说说在具体问题中如何使用面向对象去分析问题，和如何使用面向对象。
我们把大象装冰箱为例进行分析。在针对具体的需求，可以使用名词提炼的办法进行分析，寻找具体的对象。
需求：把大象装冰箱里
对象：大象、冰箱
分三步：

- 1、打开冰箱门
- 2、将大象装进去
- 3、关闭冰箱门

分析发现打开、装、关闭都是冰箱的功能。即冰箱对象具备如下功能：
冰箱打开
冰箱存储
冰箱关闭
用伪代码描述，上述需求中有两个具体的事物 大象 和 冰箱
描述大象：

```
class 大象
{
}
```

描述冰箱



```
class冰箱
{
    void 打开(){}
    void 存储(大象){}
    void 关闭(){}
}
```



当把具体的事物描述清楚之后，需要使用这些具体的事物，Java使用具体的事物，需要通过new关键字来创建这个事物的具体实例。

使用对象：
1、创建冰箱的对象

```
冰箱 bx = new 冰箱(); 
```

2、调用冰箱的功能

```
对象.功能()；
bx.打开();
bx.存储(new 大象());
bx.关闭();
```

总结：

1、先按照名词提炼问题领域中的对象
2、对对象进行描述，其实就是在明确对象中应该具备的属性和功能
3、通过new的方式就可以创建该事物的具体对象
4、通过该对象调用它以后的功能。

### 对象在代码中的体现

在分析现实生活中的事物时发现，这些事物都有其具体的特点和功能，这些特点和功能就组成了这个特殊的事物。
比如描述小汽车：

- 分析：
- 事物的特点（属性）：
- 颜色。
- 轮胎个数。
- 事物的(功能)：
- 运行。

可以发现：事物其实就是由特点（属性）和行为（功能）组成的。
可以简单理解：属性就是数值，其实就是变量；行为就是功能，就是方法。

```
小汽车 {
    颜色；
    轮胎个数；
    运行() {    }
}
```

通过计算机语言Java来描述这个事物。

定义类的格式



```
public class 类名 {
    //可编写0至n个属性
    数据类型 变量名1；
    数据类型 变量名2；

    //可编写0至n个方法
    修饰符 返回值类型 方法名(参数){
        执行语句;
    }
}
```



汽车类



```
public class Car {
    String color;
    int number;

    void run() {
        System.out.println(color + ":" + number);
    }
}
```



通过代码的描述，知道类的真正意义就是在描述事物。属性和功能统称为事物中的成员。

事物的成员分为两种：成员属性和成员功能。
成员属性在代码中的体现就是成员变量；成员功能在代码中的体现就是成员方法
把写好的代码测试一下。需要一个可以独立运行类。
创建对象的格式： 类名 对象名 = new 类名(); 
测试类



```
public class CarDemo {
    public static void main(String[] args) { 
/*
* 测试：Car类中的run方法。
*/
// 1,创建Car的对象。给对象起个名字。
        Car c = new Car();// c是类类型的变量。c指向了一个具体的Car类型的对象。
// 2,通过已有的对象调用该对象的功能。格式：对象.对象成员;
// 3,可以该对象的属性赋值。
        c.color = "red";
        c.number = 4;
        c.run();
    }
}
```



对象的内存图解

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705230504956-8743412.png)

 

### 类和对象的区别

面向对象的编程思想力图在程序中对事物的描述与该事物在现实中的形态保持一致。为了做到这一点，面向对象的思想中提出两个概念，即类和对象。其中，类是对某一类事物的抽象描述，而对象用于表示现实中该类事物的个体。接下来通过一个图例来抽象描述类与对象的关系，如下图所示。

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705230558597-773944790.png)

 

在上图中，可以将玩具模型看作是一个类，将一个个玩具看作对象，从玩具模型和玩具之间的关系便可以看出类与对象之间的关系。类用于描述多个对象的共同特征，它是对象的模板。对象用于描述现实中的个体，它是类的实例。从上图中可以明显看出对象是根据类创建的，并且一个类可以对应多个对象，接下来分别讲解什么是类和对象。
经过前面几个知识点的学习，基本上掌握了类是用于描述事物的，类中可以定义事物的属性和行为。而对象是通过描述的这个类，使用new关键字创建出来，通过对象就可以调用该对象具体的属性和功能了。

### 局部变量和成员变量区别

类中定义的变量，和在方法定义的变量有啥差别呢？
区别一：定义的位置不同
定义在类中的变量是成员变量；定义在方法中或者{}语句里面的变量是局部变量
区别二：在内存中的位置不同
成员变量存储在对内存的对象中；局部变量存储在栈内存的方法中
区别三：声明周期不同
成员变量随着对象的出现而出现在堆中，随着对象的消失而从堆中消失；局部变量随着方法的运行而出现在栈中，随着方法的弹栈而消失
区别四：初始化不同
成员变量因为在堆内存中，所以有默认的初始化值；局部变量没有默认的初始化值，必须手动的给其赋值才可以使用。

### 基本类型和引用类型作为参数传递

引用类型数据和基本类型数据作为参数传递有没有差别呢？我们用如下代码进行说明：



```
class Demo
{
    public static void main(String[] args)
    {
        int x = 4;
        show(x);
        System.out.println("x="+x);
    }
    public static void show(int x)
    {
        x = 5;

    }
}    
```



基本类型作为参数传递时，其实就是将基本类型变量x空间中的值复制了一份传递给调用的方法show()，当在show()方法中x接受到了复制的值，再在show()方法中对x变量进行操作，这时只会影响到show中的x。当show方法执行完成，弹栈后，程序又回到main方法执行，main方法中的x值还是原来的值。



```
class Demo
{
    int x ;
    public static void main(String[] args)
    {

        Demo d = new Demo();
        d.x = 5;
        show(d);
        System.out.println("x="+d.x);
    }
    public static void show(Demo d)
    {
        d.x = 6;
    }
}    
```



当引用变量作为参数传递时，这时其实是将引用变量空间中的内存地址(引用)复制了一份传递给了show方法的d引用变量。这时会有两个引用同时指向堆中的同一个对象。当执行show方法中的d.x=6时，会根据d所持有的引用找到堆中的对象，并将其x属性的值改为6.show方法弹栈。由于是两个引用指向同一个对象，不管是哪一个引用改变了引用的所指向的对象的中的值，其他引用再次使用都是改变后的值。

 

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705231549112-1883192988.png)                                       ![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705231619347-1817697695.png)

 

 

## 封装

### 封装概述

封装，它也是面向对象思想的特征之一。面向对象共有三个特征：封装，继承，多态。
封装表现：

- 方法就是一个最基本封装体。
- 类其实也是一个封装体。

从以上两点得出结论，封装的好处：

- 提高了代码的复用性。
- 隐藏了实现细节，还要对外提供可以访问的方式。便于调用者的使用。这是核心之一，也可以理解为就是封装的概念。
- 提高了安全性。

封装举例
一台电脑，它是由CPU、主板、显卡、内存、硬盘、电源等部件组长，其实我们将这些部件组装在一起就可以使用电脑了，但是发现这些部件都散落在外面，很容造成不安全因素，于是，使用机箱壳子，把这些部件都装在里面，并在机箱壳上留下一些插口等，若不留插口，大家想想会是什么情况。总结：机箱其实就是隐藏了办卡设备的细节，对外提供了插口以及开关等访问内部细节的方式。

### 私有private

了解到封装在生活的体现之后，又要回到Java中，细说封装的在Java代码中的体现，先从描述Person说起。



```
class Person {
    int age;
    String name;

    public void show() {
        System.out.println("age=" + age + ",name" + name);
    }
}

public class PersonDemo {
    public static void main(String[] args) {
// 创建Person对象
        Person p = new Person();
        p.age = -20; // 给Person对象赋值
        p.name = "秀吉";
        p.show(); // 调用Person的show方法
    }
}
```



通过上述代码发现，虽然我们用Java代码把Person描述清楚了，但有个严重的问题，就是Person中的属性的行为可以任意访问和使用。这明显不符合实际需求。

可是怎么才能不让访问呢？需要使用一个Java中的关键字也是一个修饰符 private(私有，权限修饰符)。只要将Person的属性和行为私有起来，这样就无法直接访问。



```
class Person {
    private int age;
    private String name;

    public void show() {
        System.out.println("age=" + age + ",name" + name);
    }
}
```



年龄已被私有，错误的值无法赋值，可是正确的值也赋值不了，这样还是不行，那肿么办呢？按照之前所学习的封装的原理，隐藏后，还需要提供访问方式。只要对外提供可以访问的方法，让其他程序访问这些方法。同时在方法中可以对数据进行验证。

一般对成员属性的访问动作：赋值(设置 set)，取值(获取 get)，因此对私有的变量访问的方式可以提供对应的 setXxx或者getXxx的方法。



```
class Person {
    // 私有成员变量
    private int age;
    private String name;

    // 对外提供设置成员变量的方法
    public void setAge(int a) {
// 由于是设置成员变量的值，这里可以加入数据的验证
        if (a < 0 || a > 130) {
            System.out.println(a + "不符合年龄的数据范围");
            return;
        }
        age = a;
    }

    // 对外提供访问成员变量的方法
    public void getAge() {
        return age;
    }
}
```



总结：类中不需要对外提供的内容都私有化，包括属性和方法。以后再描述事物，属性都私有化，并提供setXxx getXxx方法对其进行访问。注意：私有仅仅是封装的体现形式而已。

### this关键字

成员变量和局部变量同名问题，当在方法中出现了局部变量和成员变量同名的时候，那么在方法中怎么区别局部变量成员变量呢？可以在成员变量名前面加上this，来区别成员变量和局部变量。



```
class Person {
    private int age;
    private String name;

    public void speak() {
        this.name = "小强";
        this.age = 18;
        System.out.println("name=" + this.name + ",age=" + this.age);
    }
}
class PersonDemo {
    public static void main(String[] args) {
        Person p = new Person();
        p.speak();
    }
}
```



### 对象的内存解释

我们已经学习了如何把生活中的事物使用Java代码描述，接下来我们分析对象在内存中的分配情况。这里需要画图一步一步演示，严格按照画图流程讲解内存对象创建使用过程。



```
class Person {
    private int age;
    public int getAge() {
        return this.age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
public class PersonDemo {
    public static void main(String[] args) {
        Person p = new Person();
        p.setAge(30);
        System.out.println("大家好，今年我" + p.getAge() + "岁");
    }
}
```



下图为程序中内存对象的创建使用过程。

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705232447940-669918149.png)

程序执行流程说明：

- 1、先执行main方法（压栈），执行其中的 Person p = new Person()；
- 2、在堆内存中开辟空间，并为其分配内存地址0x1234，紧接着成员变量默认初始化(age = 0)；将内存地址0x1234赋值给栈内中的Person p 变量
- 3、继续执行p.setAge(30)语句，这时会调用setAge(int age)方法，将30赋值为setAge方法中的“age”变量；执行this.age = age语句，将age变量值30 赋值给成员变量this.age为30；
- 4、setAge()方法执行完毕后（弹栈），回到main()方法，执行输出语句System.out.println()，控制台打印p对象中的age年龄值。

注意：
this到底代表什么呢？**this代表的是对象**，具体代表哪个对象呢？哪个对象调用了this所在的方法，this就代表哪个对象。
上述代码中的 p.setAge(30)语句中，**setAge(int age)方法中的this代表的就是p对象。**
this的应用
学习this的用法之后，现在做个小小的练习。需求：在Person类中定义功能，判断两个人是否是同龄人。



```
class Person {
    private int age;
    private String name;

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void speak() {
        System.out.println("name=" + this.name + ",age=" + this.age);
    }

    // 判断是否为同龄人
    public boolean equalsAge(Person p) {
// 使用当前调用该equalsAge方法对象的age和传递进来p的age进行比较
// 由于无法确定具体是哪一个对象调用equalsAge方法，这里就可以使用this来代替
/*
* if(this.age == p.age) { return true; } return false;
*/
        return this.age == p.age;
    }	
}
```

# [Java基础学习笔记六 Java基础语法之类和ArrayList](https://www.cnblogs.com/ginb/p/7123912.html)

## 引用数据类型

引用数据类型分类，提到引用数据类型（类），其实我们对它并不陌生，如使用过的Scanner类、Random类。
我们可以把类的类型为两种：

- 第一种，Java为我们提供好的类，如Scanner类，Random类等，这些已存在的类中包含了很多的方法与属性，可供我们使用。

- 第二种，我们自己创建的类，按照类的定义标准，可以在类中包含多个方法与属性，来供我们使用。

  这里我们主要介绍第二种情况的简单使用。

## 自定义数据类型概述

在Java中，将现实生活中的事物抽象成了代码。这时，我们可以使用自定义的数据类型（类）来描述（映射）现实生活中的事物。
类，它是引用数据类型，与之前学习的所有引用数据类型相同，自定义类也是一种数据类型。只是自定义类型并非Java为我们预先提供好的类型，而是我们自己定义的一种引用数据类型用来描述一个事物。

### 类的定义与使用

java代码映射成现实事物的过程就是定义类的过程。
我们就拿一部手机进行分析，它能用来做什么呢？它可以打电话，上网，聊微信等，这些就是手机所提供的功能，也就是方法；手机也有它的特征，如颜色、尺寸大小、品牌型号等，这些就是手机的特征，也就是属性。
目前，我们只关注类中的属性，类中的方法在面向对象部分再进行学习。

### 类的定义格式

创建java文件，与类名相同

```
public class 类名{
    数据类型 属性名称1；
    数据类型 属性名称2；
    …
}
```

通过类的定义格式，来进行手机类的描述，如下所示



```
public class Phone {
    /*
    * 属性
    */
    String brand;// 品牌型号
    String color;// 颜色
    double size; // 尺寸大小
}
```



上述代码，就是创建一个类的的过程，类的名称我们给起名为Phone，类中包含了三个属性（brand品牌型号、color颜色、size尺寸大小）。注意，类中定义的属性没有个数要求。

### 类的使用格式

Phone类定义好后，我们就可以使用这个类了，使用方式和使用引用数据类型Scanner类相似。格式如下：

- 导包：我们将所有的类放到同一个文件夹下，可以避免导包;
- 创建对象：数据类型 变量名 = new 数据类型();
- 调用方法：目前我们定义的自定义类不涉及方法，只是属性;
- 访问属性：变量名.属性 (这是当前的方式，后期会采取调用方法的方式替代掉直接访问的方式来完成对属性的访问。)

当有了Phone数据类型的变量后，我们就可以使用Phone类中的属性了。对属性的访问我们来演示一下，如下所示：



```
package arraylist;

public class Test {
    public static void main(String[] args) {
//定义了一个Phone类型的变量p
        Phone p = new Phone();
/*
* 通过p,使用Phone中的属性
*/
//访问p中的brand品牌属性
        p.brand = "苹果6s";//为p中brand属性赋值为 苹果6s
//访问p中的color颜色属性
        p.color = "白色";//为p中color属性赋值为”白色”
//访问p中的size尺寸大小属性
        p.size = 5.5;//为p中size属性赋值为5.5
        System.out.println("手机品牌为" + p.brand);
        System.out.println("手机颜色为" + p.color);
        System.out.println("手机尺寸大小为" + p.size);
    }
}
//手机品牌为苹果6s
//手机颜色为白色
//手机尺寸大小为5.5
```



### 自定义类型注意事项与内存图

上述代码中，通过类Phone创建出来的变量p，它相当于我们生活中的盒子，里面包含了它能够使用的属性。
通过 p.属性名 就可以对属性进行操作
与引用类型数组类似，引用类型的自定义类型的变量，直接变量时，结果为对象地址值，这里可以通过内存图简单解释。

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705222928315-1670375875.jpg)

下面再来看看某个类创建两个对象的内存图：

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705223054769-268035620.jpg)

 

## ArrayList集合

在前面我们学习了数组，数组可以保存多个元素，但在某些情况下无法确定到底要保存多少个元素，此时数组将不再适用，因为数组的长度不可变。为了保存这些数目不确定的元素，JDK中提供了一系列特殊的类，这些类可以存储任意类型的元素，并且长度可变，统称为集合。在这里，我们先介绍ArrayList集合，其他集合在后续课程中学习。
ArrayList集合是程序中最常见的一种集合，它属于引用数据类型（类）。在ArrayList内部封装了一个长度可变的数组，当存入的元素超过数组长度时，ArrayList会在内存中分配一个更大的数组来存储这些元素，因此可以将ArrayList集合看作一个长度可变的数组。

### 集合的创建

创建集合的常用格式在此说明一下：
1、导包：import java.util.ArrayList;
2、创建对象：与其他普通的引用数据类型创建方式完全相同，但是要指定容器中存储的数据类型：
3、ArrayList<要存储元素的数据类型> 变量名 = new ArrayList<要存储元素的数据类型>();

- 集合中存储的元素，只能为< >括号中指定的数据类型元素；
- “<要存储元素的数据类型>”中的数据类型必须是引用数据类型，不能是基本数据类型；

下面给出8种基本数据类型所对应的引用数据类型表示形式:
基本数据类型 对应的引用数据类型表示形式



```
byte　　——> 　　Byte
short    ——>　　Short
Int　　——>    Integer
long    ——>　　Long
float    ——>　　Float
double    ——>　　Double
char    ——>　　Character
boolean    ——>　　Boolean
```



我们通过举几个例子，来明确集合的创建方式：



```
//存储String类型的元素
ArrayList<String> list = new ArrayList<String>();
//存储int类型的数据
ArrayList<Integer> list = new ArrayList<Integer>(); 
//存储Phone类型的数据
ArrayList<Phone> list = new ArrayList<Phone>();
```



### 集合中常用方法

接下来，我们来学习下ArrayList集合提供的一些常用方法，如下：

```
boolean add（Object obj）    //将指定元素obj追加到集合的末尾
Object get（int index）      //返回集合中指定位置上的元素
int size（）    　　　　　　   //返回集合中的元素个数
```

下面通过代码演示上述方法的使用。ArrayListDemo01.java



```
package arraylist;
import java.util.ArrayList;
public class ArrayListDemo01 {
    public static void main(String[] args) {
// 创建ArrayList集合
        ArrayList<String> list = new ArrayList<String>();
// 向集合中添加元素
        list.add("stu1");
        list.add("stu2");
        list.add("stu3");
        list.add("stu4");
// 获取集合中元素的个数
        System.out.println("集合的长度：" + list.size());
// 取出并打印指定位置的元素
        System.out.println("第1个元素是：" + list.get(0));
        System.out.println("第2个元素是：" + list.get(1));
        System.out.println("第3个元素是：" + list.get(2));
        System.out.println("第4个元素是：" + list.get(3));
    }
}
//集合的长度：4
//第1个元素是：stu1
//第2个元素是：stu2
//第3个元素是：stu3
//第4个元素是：stu4
```



强调一点，ArrayList集合相当于是一个长度可变的数组，所以访问集合中的元素也是采用索引方式访问，第一个元素存储在索引0的位置，第二个元素存储在索引1的位置，依次类推。

### 集合的遍历

通过集合遍历，得到集合中每个元素，这是集合中最常见的操作。集合的遍历与数组的遍历很像，都是通过索引的方式，集合遍历方式如下：ArrayListDemo02.java



```
package arraylist;
import java.util.ArrayList;
public class ArrayListDemo02 {
    public static void main(String[] args) {
        //创建ArrayList集合
        ArrayList<Integer> list = new ArrayList<Integer>();
        //添加元素到集合
        list.add(13);
        list.add(15);
        list.add(22);
        list.add(29);
        //遍历集合
        for (int i = 0; i < list.size(); i++) {//[获取集合中元素的个数]
            //通过索引，获取到集合中每个元素
            int n = list.get(i);//[获取集合中指定位置上的元素值];
            System.out.println(n);
        }
    }
}
//13
//15
//22
//29
```



上述代码中，定义了一个可以存储int元素的集合；接着实现将int类型数值存储到集合中；接着实现遍历集合元素。这里要强调一点，get方法返回值的类型为集合中元素的类型。

### 集合中的常用方法补充

ArrayList集合提供的一些常用方法，如下：

```
boolean add（int index, Object obj）      //将指定元素obj插入到集合中指定的位置
Object remove（int index）    　　　　　 　//从集合中删除指定index处的元素，返回该元素
void clear（）    　　　　　　　　　　　　   //清空集合中所有元素
Object set（int index, Object obj）      //用指定元素obj替代集合中指定位置上的元素
```

 

 

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170705223218878-1549729373.jpg)

## ASCII编码表

ASCII编码表， 英文全称 American Standard Code for Information Interchange，美国标准信息交换代码。

### ASCII编码表由来

计算机中，所有的数据在存储和运算时都要使用二进制数表示
a、b、c、d这样的52个字母（包括大写）、以及0、1等数字还有一些常用的符号, 在计算机中存储时也要使用二进制数来表示， 具体用哪些二进制数字表示哪个符号，当然每个人都可以约定自己的一套（这就叫编码）。
大家如果要想互相通信而不造成混乱，那么大家就必须使用相同的编码规则，于是美国有关的标准化组织就出台了ASCII编码，统一规定了上述常用符号用哪些二进制数来表示。

中文编码表

- GB2312
- UNICODE

字符中重要的ASCII码对应关系

- a : 97
- A : 65
- 0 : 48

### char类型的存储

short:占两个字节,是有符号数据,取值范围-32768-32767，char: 占两个字节,是无符号数据,取值范围0-65536。char类型的数据参加运算时要先转换为int数据类型。

案例代码



```
package arraylist;

/*
    ASCII编码表演示
    字符Java 数据类型,char
    整数Java 数据类型,int
    
    int 类型和 char 数据类型转换
    char  两个字节, int 四个字节
    
    char转成int类型的时候,类型自动提示,char数据类型,会查询编码表,得到整数
    int转成char类型的时候,强制转换,会查询编码表
    
    char存储汉字,查询Unicode编码表
    
    char可以和int计算,提示为int类型, 内存中两个字节
    char取值范围是0-65535, 无符号的数据类型
*/
public class ASCIIDemo {
    public static void main(String[] args){
        char c = 'a';
        int i = c + 1;
        System.out.println(i);

        int j = 90;
        char h = (char)j;
        System.out.println(h);

        System.out.println( (char)6 );

        char k = '你';
        System.out.println(k);


        //char m = -1;
    }
}
//98
//Z
//
//你
```

# [Java基础学习笔记七 Java基础语法之继承和抽象类](https://www.cnblogs.com/ginb/p/7128615.html)

## 继承

### 继承的概念

在现实生活中，继承一般指的是子女继承父辈的财产。在程序中，继承描述的是事物之间的所属关系，通过继承可以使多种事物之间形成一种关系体系。

例如公司中的研发部员工和维护部员工都属于员工，程序中便可以描述为研发部员工和维护部员工继承自员工，同理，JavaEE工程师和Android工程师继承自研发部员工，而维网络维护工程师和硬件维护工程师继承自维护部员工。这些员工之间会形成一个继承体系，具体如下图所示。

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170706213116800-1078655550.png)

在Java中，类的继承是指在一个现有类的基础上去构建一个新的类，构建出来的新类被称作子类，现有类被称作父类，子类会自动拥有父类所有可继承的属性和方法。

### 继承的格式&使用

在程序中，如果想声明一个类继承另一个类，需要使用extends关键字。
格式：class 子类 extends 父类 {}
接下来通过一个案例来学习子类是如何继承父类的，如下所示。Employee .java



```
/*
* 定义员工类Employee
*/
public class Employee {
    String name; // 定义name属性
    // 定义员工的工作方法
    public void work() {
        System.out.println("尽心尽力地工作");
    }
}
```





```
/*
* 定义研发部员工类Developer 继承 员工类Employee
*/
class Developer extends Employee {
    // 定义一个打印name的方法
    public void printName() {
        System.out.println("name=" + name);
    }
}
```





```
* 定义测试类
*/
public class Example01 {
    public static void main(String[] args) {
        Developer d = new Developer(); // 创建一个研发部员工类对象
        d.name = "小明"; // 为该员工类的name属性进行赋值
        d.printName(); // 调用该员工的printName()方法
        d.work(); // 调用Developer类继承来的work()方法
    }
}
```



运行结果如下图所示。

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170706214329706-1834019079.png)

在上述代码中，Developer类通过extends关键字继承了Employee类，这样Developer类便是Employee类的子类。从运行结果不难看出，子类虽然没有定义name属性和work()方法，但是却能访问这两个成员。这就说明，子类在继承父类的时候，会自动拥有父类的成员。

### 继承的好处&注意事项

继承的好处：

- 继承的出现提高了代码的复用性，提高软件开发效率。
- 继承的出现让类与类之间产生了关系，提供了多态的前提。

在类的继承中，需要注意一些问题，具体如下：
1、在Java中，类只支持单继承，不允许多继承，也就是说一个类只能有一个直接父类，例如下面这种情况是不合法的。

```
class A{} 
class B{}
class C extends A,B{} // C类不可以同时继承A类和B类
```

2、多个类可以继承一个父类，例如下面这种情况是允许的。

```
class A{}
class B extends A{}
class C extends A{} // 类B和类C都可以继承类A
```

3、在Java中，多层继承是可以的，即一个类的父类可以再去继承另外的父类，例如C类继承自B类，而B类又可以去继承A类，这时，C类也可称作A类的子类。下面这种情况是允许的。

```
class A{}
class B extends A{} // 类B继承类A，类B是类A的子类
class C extends B{} // 类C继承类B，类C是类B的子类，同时也是类A的子类
```

4、在Java中，子类和父类是一种相对概念，也就是说一个类是某个类父类的同时，也可以是另一个类的子类。例如上面的这种情况中，B类是A类的子类，同时又是C类的父类。

### 继承-子父类中成员变量的特点

了解了继承给我们带来的好处，提高了代码的复用性。继承让类与类或者说对象与对象之间产生了关系。那么，当继承出现后，类的成员之间产生了那些变化呢？
成员变量：如果子类父类中出现不同名的成员变量，这时的访问是没有任何问题。
看如下代码：



```
class Fu
{
    //Fu中的成员变量。
    int num = 5;
}
class Zi extends Fu
{
    //Zi中的成员变量
    int num2 = 6;
    //Zi中的成员方法
    public void show()
    {
//访问父类中的num
        System.out.println("Fu num="+num);
//访问子类中的num2
        System.out.println("Zi num2="+num2);
    }
}
class Demo
{
    public static void main(String[] args)
    {
        Zi z = new Zi(); //创建子类对象
        z.show(); //调用子类中的show方法
    }
}
```



代码说明：Fu类中的成员变量是非私有的，子类中可以直接访问，若Fu类中的成员变量私有了，子类是不能直接访问的。

当子父类中出现了同名成员变量时，在子类中若要访问父类中的成员变量，必须使用关键字super来完成。super用来表示当前对象中包含的父类对象空间的引用。
在子类中，访问父类中的成员变量格式： super.父类中的成员变量 
看如下代码：



```
class Fu
{
    //Fu中的成员变量。
    int num = 5;
}
class Zi extends Fu
{
    //Zi中的成员变量
    int num = 6;
    void show()
    {
//子父类中出现了同名的成员变量时
//在子类中需要访问父类中非私有成员变量时，需要使用super关键字
//访问父类中的num
        System.out.println("Fu num="+super.num);
//访问子类中的num2
        System.out.println("Zi num2="+this.num);
    }
}
class Demo5
{
    public static void main(String[] args)
    {
        Zi z = new Zi(); //创建子类对象
        z.show(); //调用子类中的show方法
    }
}
```



### 继承-子父类中成员方法特点-重写&应用

子父类中成员方法的特点
当在程序中通过对象调用方法时，会先在子类中查找有没有对应的方法，若子类中存在就会执行子类中的方法，若子类中不存在就会执行父类中相应的方法。
看如下代码：



```
class Fu{
    public void show(){
        System.out.println("Fu类中的show方法执行");
    }
}
class Zi extends Fu{
    public void show2(){
        System.out.println("Zi类中的show2方法执行");
    }
}
public class Test{
    public static void main(String[] args) {
        Zi z = new Zi();
        z.show(); //子类中没有show方法，但是可以找到父类方法去执行
        z.show2();
    }
}
```



### 成员方法特殊情况——覆盖

子类中出现与父类一模一样的方法时，会出现覆盖操作，也称为override重写、复写或者覆盖。



```
class Fu
{
    public void show()
    {
        System.out.println("Fu show");
    }
}
class Zi extends Fu
{
    //子类复写了父类的show方法
    public void show()
    {
        System.out.println("Zi show");
    }
}
```



### 方法重写（覆盖）的应用

当子类需要父类的功能，而功能主体子类有自己特有内容时，可以重写父类中的方法，这样，即沿袭了父类的功能，又定义了子类特有的内容。
举例：比如手机，当描述一个手机时，它具有发短信，打电话，显示来电号码功能，后期由于手机需要在来电显示功能中增加显示姓名和头像，这时可以重新定义一个类描述智能手机，并继承原有描述手机的类。并在新定义的类中覆盖来电显示功能，在其中增加显示姓名和头像功能。
在子类中，访问父类中的成员方法格式： super.父类中的成员方法(); 
看如下代码：



```
//手机类
class Phone{
    public void sendMessage(){
        System.out.println("发短信");
    }
    public void call(){
        System.out.println("打电话");
    }
    public void showNum(){
        System.out.println("来电显示号码");
    }
}

//智能手机类
class NewPhone extends Phone{

    //覆盖父类的来电显示号码功能，并增加自己的显示姓名和图片功能
    public void showNum(){
//调用父类已经存在的功能使用super
        super.showNum();
//增加自己特有显示姓名和图片功能
        System.out.println("显示来电姓名");
        System.out.println("显示头像");
    }
}
```



### 方法重写的注意事项

重写需要注意的细节问题：子类方法覆盖父类方法，必须要保证权限大于等于父类权限。



```
class Fu(){
    void show(){}
    public void method(){}
}
class Zi() extends Fu{
    public void show(){} //编译运行没问题
        void method(){} //编译错误
}
```



写法上稍微注意:必须一模一样:方法的返回值类型 方法名 参数列表都要一样。

总结：当一个类是另一个类中的一种时，可以通过继承，来继承属性与功能。如果父类具备的功能内容需要子类特殊定义时，进行方法重写。

不能为了继承某个功能而随意进行继承操作， 必须要符合 is a 的关系

- 苹果 is a 水果
- 男人 is a 人
- 狗 is a 人 ， 这种情况就不能继承了

## 重载与重写对比

### 重载

权限修饰符(public private 默认):无关
方法名:重载的两个方法的方法名必须相同
形参列表:

- 形参类型的顺序不同
- 形参的个数不同
- 形参的类型不同

三者至少满足一个
返回值类型:重载与返回值类型无关

### 重写

权限修饰符(public private 默认): 子类方法的权限>=父类的方法的权限
方法名: 子类方法和父类方法必须相同
形参列表: 子类方法和父类方法的形参列表必须相同
返回值类型:基本类数据类型:必须相同
引用数据类型:子类方法的返回值类型和父类方法的返回值类型相同，或者子类方法的返回值类型是父类方法的返回值类型的 子类

## 抽象类

### 抽象类-产生

当编写一个类时，我们往往会为该类定义一些方法，这些方法是用来描述该类的功能具体实现方式，那么这些方法都有具体的方法体。但是有的时候，某个父类只是知道子类应该包含怎么样的方法，但是无法准确知道子类如何实现这些方法。比如一个图形类应该有一个求周长的方法，但是不同的图形求周长的算法不一样。那该怎么办呢？
分析事物时，发现了共性内容，就出现向上抽取。会有这样一种特殊情况，就是方法功能声明相同，但方法功能主体不同。那么这时也可以抽取，但只抽取方法声明，不抽取方法主体。那么此方法就是一个抽象方法。
描述JavaEE工程师：行为：工作。
描述Android工程师：行为：工作。
JavaEE工程师和Android工程师之间有共性，可以进行向上抽取。抽取它们的所属共性类型：研发部员工。由于JavaEE工程师和Android工程师都具有工作功能，但是他们具体工作内容却不一样。这时在描述研发部员工时，发现了有些功能（工作）不具体，这些不具体的功能，需要在类中标识出来，通过java中的关键字abstract(抽象)。
当定义了抽象函数的类也必须被abstract关键字修饰，被abstract关键字修饰的类是抽象类。

### 抽象类&抽象方法的定义

抽象方法定义的格式：

```
public abstract 返回值类型 方法名(参数);
    抽象类定义的格式：
    abstract class 类名 {
}
```

看如下代码：



```
//研发部员工 
abstract class Developer {
    public abstract void work();//抽象函数。需要abstract修饰，并分号;结束
}

//JavaEE工程师
class JavaEE extends Developer{
    public void work() {
        System.out.println("正在研发淘宝网站");
    }
}
```





```
//Android工程师

class Android extends Developer {
    public void work() {
        System.out.println("正在研发淘宝手机客户端软件");
    }
}
```



### 抽象类的特点

- 1、抽象类和抽象方法都需要被abstract修饰。抽象方法一定要定义在抽象类中。
- 2、抽象类不可以直接创建对象，原因：调用抽象方法没有意义。
- 3、只有覆盖了抽象类中所有的抽象方法后，其子类才可以创建对象。否则该子类还是一个抽象类。

之所以继承抽象类，更多的是在思想，是面对共性类型操作会更简单。

抽象类的细节问题：
1、抽象类一定是个父类？ 是的，因为不断抽取而来的。
2、抽象类中是否可以不定义抽象方法。是可以的，那这个抽象类的存在到底有什么意义呢？不让该类创建对象,方法可以直接让子类去使用
3、抽象关键字abstract不可以和哪些关键字共存？

- private：私有的方法子类是无法继承到的，也不存在覆盖，而abstract和private一起使用修饰方法，abstract既要子类去实现这个方法，而private修饰子类根本无法得到父类这个方法。互相矛盾。
- final，暂时不关注，后面学
- static，暂时不关注，后面学

## 综合案例---员工类系列定义

### 案例介绍

某IT公司有多名员工，按照员工负责的工作不同，进行了部门的划分（研发部员工、维护部员工）。研发部根据所需研发的内容不同，又分为JavaEE工程师、Android工程师；维护部根据所需维护的内容不同，又分为网络维护工程师、硬件维护工程师。
公司的每名员工都有他们自己的员工编号、姓名，并要做它们所负责的工作。

工作内容

JavaEE工程师：员工号为xxx的 xxx员工，正在研发淘宝网站
Android工程师：员工号为xxx的 xxx员工，正在研发淘宝手机客户端软件
网络维护工程师：员工号为xxx的 xxx员工，正在检查网络是否畅通
硬件维护工程师：员工号为xxx的 xxx员工，正在修复打印机
请根据描述，完成员工体系中所有类的定义，并指定类之间的继承关系。进行XX工程师类的对象创建，完成工作方法的调用。

### 案例分析

根据上述部门的描述，得出如下的员工体系图

![img](https://images2015.cnblogs.com/blog/612774/201707/612774-20170706220540690-1955238272.png)

根据员工信息的描述，确定每个员工都有员工编号、姓名、要进行工作。则，把这些共同的属性与功能抽取到父类中（员工类），关于工作的内容由具体的工程师来进行指定。

### 案例代码实现

根据员工体系图，完成类的定义
定义员工类(抽象类)



```
public abstract class Employee {
    private String id;// 员工编号
    private String name; // 员工姓名

    public String getId() {
        return id;
    }
    public void setId(String id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }

    //工作方法（抽象方法）
    public abstract void work();
}
```



定义研发部员工类Developer 继承 员工类Employee

```
public abstract class Developer extends Employee {
}
```

定义维护部员工类Maintainer 继承 员工类Employee

```
public abstract class Maintainer extends Employee {
}
```

定义JavaEE工程师 继承 研发部员工类，重写工作方法



```
public class JavaEE extends Developer {
    @Override
    public void work() {
        System.out.println("员工号为 " + getId() + " 的 " + getName() + " 员工，正在研发淘宝网站");
    }
}
```



定义Android工程师 继承 研发部员工类，重写工作方法



```
public class Android extends Developer {
    @Override
    public void work() {
        System.out.println("员工号为 " + getId() + " 的 " + getName() + " 员工，正在研发淘宝手机客户端软件");
    }
}
```



定义Network网络维护工程师 继承 维护部员工类，重写工作方法



```
public class Network extends Maintainer {
    @Override
    public void work() {
        System.out.println("员工号为 " + getId() + " 的 " + getName() + " 员工，正在检查网络是否畅通");
    }
}
```



定义Hardware硬件维护工程师 继承 维护部员工类，重写工作方法



```
public class Hardware extends Maintainer {
    @Override
    public void work() {
        System.out.println("员工号为 " + getId() + " 的 " + getName() + " 员工，正在修复打印机");
    }
}
```



在测试类中，创建JavaEE工程师对象，完成工作方法的调用



```
public class Test {
    public static void main(String[] args) {
//创建JavaEE工程师员工对象
        JavaEE ee = new JavaEE();
//设置该员工的编号
        ee.setId("000015");
//设置该员工的姓名
        ee.setName("小明");
//调用该员工的工作方法
        ee.work();
    }
}
```

# [Java基础学习笔记八 Java基础语法之接口和多态](https://www.cnblogs.com/ginb/p/7128649.html)

## 接口

### 接口概念

接口是功能的集合，同样可看做是一种数据类型，是比抽象类更为抽象的”类”。
接口只描述所应该具备的方法，并没有具体实现，具体的实现由接口的实现类(相当于接口的子类)来完成。这样将功能的定义与实现分离，优化了程序设计。
请记住：一切事物均有功能，即一切事物均有接口。

### 接口的定义

与定义类的class不同，接口定义时需要使用interface关键字。
定义接口所在的仍为.java文件，虽然声明时使用的为interface关键字的编译后仍然会产生.class文件。这点可以让我们将接口看做是一种只包含了功能声明的特殊类。
定义格式：

```
public interface 接口名 {
    抽象方法1;
    抽象方法2;
    抽象方法3;
}
```

使用interface代替了原来的class，其他步骤与定义类相同：

- 接口中的方法均为公共访问的抽象方法
- 接口中无法定义普通的成员变量

### 类实现接口

类与接口的关系为实现关系，即类实现接口。实现的动作类似继承，只是关键字不同，实现使用implements。
其他类(实现类)实现接口后，就相当于声明：”我应该具备这个接口中的功能”。实现类仍然需要重写方法以实现具体的功能。
格式：

```
class 类 implements 接口 {
    重写接口中方法
} 
```

在类实现接口后，该类就会将接口中的抽象方法继承过来，此时该类需要重写该抽象方法，完成具体的逻辑。

接口中定义功能，当需要具有该功能时，可以让类实现该接口，只声明了应该具备该方法，是功能的声明。在具体实现类中重写方法，实现功能，是方法的具体实现。于是，通过以上两个动作将功能的声明与实现便分开了。

### 接口中成员的特点

- **接口中可以定义变量**，但是变量必须有固定的修饰符修饰，public static final，所以接口中的变量也称之为常量，其值不能改变。后面我们会讲解static与final关键字
- **接口中可以定义方法**
- **接口不可以创建对象**
- **子类必须覆盖掉接口中所有的方法**后，子类才可以实例化。否则子类是一个抽象类。

```
class DemoImpl implements Demo { //子类实现Demo接口。
    //重写接口中的方法。
    public void show1(){}
    public void show2(){}
}
```

### 接口的多实现

了解了接口的特点后，那么想想为什么要定义接口，使用抽象类描述也没有问题，接口到底有啥用呢？接口最重要的体现：解决多继承的弊端。将多继承这种机制在java中通过多实现完成了。



```
interface Fu1
{
    void show1();
}
interface Fu2
{
    void show2();
}
class Zi implements Fu1,Fu2// 多实现。同时实现多个接口。
{
    public void show1(){}
    public void show2(){}
}
```



怎么解决多继承的弊端呢？

弊端：多继承时，当多个父类中有相同功能时，子类调用会产生不确定性。其实核心原因就是在于多继承父类中功能有主体，而导致调用运行时，不确定运行哪个主体内容。为什么多实现能解决了呢？因为接口中的功能都没有方法体，由子类来明确。

### 类继承类同时实现接口

接口和类之间可以通过实现产生关系，同时也学习了类与类之间可以通过继承产生关系。当一个类已经继承了一个父类，它又需要扩展额外的功能，这时接口就派上用场了。
子类通过继承父类扩展功能，通过继承扩展的功能都是子类应该具备的基础功能。如果子类想要继续扩展其他类中的功能呢？这时通过实现接口来完成。



```
class Fu {
    public void show(){}
}
interface Inter {
    pulbic abstract void show1();
}
class Zi extends Fu implements Inter {
    public void show1() {
    }
}
```



接口的出现避免了单继承的局限性。父类中定义的事物的基本功能。接口中定义的事物的扩展功能。

### 接口的多继承

多个接口之间可以使用extends进行继承。



```
interface Fu1{
    void show();
}
interface Fu2{
    void show1();
}
interface Fu3{
    void show2();
}
interface Zi extends Fu1,Fu2,Fu3{
    void show3();
}
```



在开发中如果多个接口中存在相同方法，这时若有个类实现了这些接口，那么就要实现接口中的方法，由于接口中的方法是抽象方法，子类实现后也不会发生调用的不确定性。

### 接口的思想

前面学习了接口的代码体现，现在来学习接口的思想，接下里从生活中的例子进行说明。
举例：我们都知道电脑上留有很多个插口，而这些插口可以插入相应的设备，这些设备为什么能插在上面呢？主要原因是这些设备在生产的时候符合了这个插口的使用规则，否则将无法插入接口中，更无法使用。发现这个插口的出现让我们使用更多的设备。
总结：接口在开发中的它好处

- 1、接口的出现扩展了功能。
- 2、接口其实就是暴漏出来的规则。
- 3、接口的出现降低了耦合性，即设备与设备之间实现了解耦。

接口的出现方便后期使用和维护，一方是在使用接口（如电脑），一方在实现接口（插在插口上的设备）。例如：笔记本使用这个规则（接口），电脑外围设备实现这个规则（接口）。

### 接口和抽象的区别

犬分为很多种类，他们吼叫和吃饭的方式不一样，在描述的时候不能具体化，也就是吼叫和吃饭的行为不能明确。当描述行为时，行为的具体动作不能明确，这时，可以将这个行为写为抽象行为，那么这个类也就是抽象类。

可是当缉毒犬有其他额外功能时，而这个功能并不在这个事物的体系中。这时可以让缉毒犬具备犬科自身特点的同时也有其他额外功能，可以将这个额外功能定义接口中。
如下代码演示：



```
interface 缉毒{
    public abstract void 缉毒();
}
//定义犬科的这个提醒的共性功能
abstract class 犬科{
    public abstract void 吃饭();
    public abstract void 吼叫();
}
// 缉毒犬属于犬科一种，让其继承犬科，获取的犬科的特性，

//由于缉毒犬具有缉毒功能，那么它只要实现缉毒接口即可，这样即保证缉毒犬具备犬科的特性，也拥有了缉毒的功能
class 缉毒犬 extends 犬科 implements 缉毒{

    public void 缉毒() {
    }
    void 吃饭() {
    }
    void 吼叫() {
    }
}
class 缉毒猪 implements 缉毒{
    public void 缉毒() {
    }
}
```



通过上面的例子总结接口和抽象类的区别：

相同点:

- 都位于继承的顶端,用于被其他类实现或继承;
- 都不能直接实例化对象;
- 都包含抽象方法,其子类都必须覆写这些抽象方法;

区别:

- 抽象类为部分方法提供实现,避免子类重复实现这些方法,提高代码重用性;接口只能包含抽象方法;
- 一个类只能继承一个直接父类(可能是抽象类),却可以实现多个接口;(接口弥补了Java的单继承)
- 抽象类是这个事物中应该具备的内容, 继承体系是一种 is..a关系
- 接口是这个事物中的额外内容,继承体系是一种 like..a关系

二者的选用:
优先选用接口,尽量少用抽象类;
需要定义子类的行为,又要为子类提供共性功能时才选用抽象类;

## 多态

多态是继封装、继承之后，面向对象的第三大特性。现实事物经常会体现出多种形态，如学生，学生是人的一种，则一个具体的同学张三既是学生也是人，即出现两种形态。
Java作为面向对象的语言，同样可以描述一个事物的多种形态。如Student类继承了Person类，一个Student的对象便既是Student，又是Person。
Java中多态的代码体现在一个子类对象(实现类对象)既可以给这个子类(实现类对象)引用变量赋值，又可以给这个子类(实现类对象)的父类(接口)变量赋值。
如Student类可以为Person类的子类。那么一个Student对象既可以赋值给一个Student类型的引用，也可以赋值给一个Person类型的引用。

- 最终多态体现为父类引用变量可以指向子类对象。
- 多态的前提是必须有子父类关系或者类实现接口关系，否则无法完成多态。
- 在使用多态后的父类引用变量调用方法时，会调用子类重写后的方法。

### 多态的定义与使用格式

多态的定义格式：就是父类的引用变量指向子类对象

```
父类类型 变量名 = new 子类类型();
变量名.方法名();
```

普通类多态定义的格式

```
父类 变量名 = new 子类();
如：    class Fu {}
class Zi extends Fu {}
//类的多态使用
Fu f = new Zi();
```

抽象类多态定义的格式

抽象类 变量名 = new 抽象类子类();
比如：



```
abstract class Fu {
    public abstract void method();
}
class Zi extends Fu {
    public void method(){
        System.out.println("重写父类抽象方法");
    }
}
//类的多态使用
Fu fu= new Zi();
```



接口多态定义的格式

接口 变量名 = new 接口实现类();
比如：



```
interface Fu {
    public abstract void method();
}
class Zi implements Fu {
    public void method(){
        System.out.println("重写接口抽象方法");
    }
}
//接口的多态使用
Fu fu = new Zi();
```



### 注意事项

同一个父类的方法会被不同的子类重写。在调用方法时，调用的为各个子类重写后的方法。

```
Person p1 = new Student();
Person p2 = new Teacher();
p1.work(); //p1会调用Student类中重写的work方法
p2.work(); //p2会调用Teacher类中重写的work方法
```

当变量名指向不同的子类对象时，由于每个子类重写父类方法的内容不同，所以会调用不同的方法。

### 多态-成员的特点

多态出现后会导致子父类中的成员变量有微弱的变化。看如下代码



```
class Fu {
    int num = 4;
}
class Zi extends Fu {
    int num = 5;
}
class Demo {
    public static void main(String[] args) {
        Fu f = new Zi();
        System.out.println(f.num);//4
        Zi z = new Zi();
        System.out.println(z.num);//5
    }
}
```



**多态成员变量**

当子父类中出现同名的成员变量时，多态调用该变量时：
编译时期：参考的是引用型变量所属的类中是否有被调用的成员变量。没有，编译失败。
运行时期：也是调用引用型变量所属的类中的成员变量。
简单记：编译和运行都参考等号的左边。编译运行看左边。

多态出现后会导致子父类中的成员方法有微弱的 变化。看如下代码



```
class Fu {
    int num = 4;
    void show()    {
        System.out.println("Fu show num");
    }
}
class Zi extends Fu {
    int num = 5;
    void show()    {
        System.out.println("Zi show num");
    }
}
class Demo {
    public static void main(String[] args) {
        Fu f = new Zi();
        f.show();
    }
}
```



**多态成员方法**

编译时期：参考引用变量所属的类，如果没有类中没有调用的方法，编译失败。
运行时期：参考引用变量所指的对象所属的类，并运行对象所属类中的成员方法。
简而言之：编译看左边，运行看右边。

### instanceof关键字

我们可以通过instanceof关键字来判断某个对象是否属于某种数据类型。如学生的对象属于学生类，学生的对象也属于人类。
使用格式：

```
boolean b = 对象 instanceof 数据类型;
```

如

```
Person p1 = new Student(); // 前提条件，学生类已经继承了人类
boolean flag = p1 instanceof Student; //flag结果为true
boolean flag2 = p2 instanceof Teacher; //flag结果为false
```

### 多态-转型

多态的转型分为向上转型与向下转型两种：
向上转型：当有子类对象赋值给一个父类引用时，便是向上转型，多态本身就是向上转型的过程。
使用格式：父类类型 变量名 = new 子类类型(); 如：Person p = new Student();
向下转型：一个已经向上转型的子类对象可以使用强制类型转换的格式，将父类引用转为子类引用，这个过程是向下转型。如果是直接创建父类对象，是无法向下转型的！
使用格式：子类类型 变量名 = (子类类型) 父类类型的变量; 如:Student stu = (Student) p; //变量p 实际上指向Student对象

### 多态的好处与弊端

当父类的引用指向子类对象时，就发生了向上转型，即把子类类型对象转成了父类类型。向上转型的好处是隐藏了子类类型，提高了代码的扩展性。
但向上转型也有弊端，只能使用父类共性的内容，而无法使用子类特有功能，功能有限制。看如下代码



```
//描述动物类，并抽取共性eat方法
abstract class Animal {
    abstract void eat();
}

// 描述狗类，继承动物类，重写eat方法，增加lookHome方法
class Dog extends Animal {
    void eat() {
        System.out.println("啃骨头");
    }

    void lookHome() {
        System.out.println("看家");
    }
}

// 描述猫类，继承动物类，重写eat方法，增加catchMouse方法
class Cat extends Animal {
    void eat() {
        System.out.println("吃鱼");
    }

    void catchMouse() {
        System.out.println("抓老鼠");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog(); //多态形式，创建一个狗对象
        a.eat(); // 调用对象中的方法，会执行狗类中的eat方法
// a.lookHome();//使用Dog类特有的方法，需要向下转型，不能直接使用

// 为了使用狗类的lookHome方法，需要向下转型
// 向下转型过程中，可能会发生类型转换的错误，即ClassCastException异常
// 那么，在转之前需要做健壮性判断 
        if( !a instanceof Dog){ // 判断当前对象是否是Dog类型
            System.out.println("类型不匹配，不能转换");
            return;
        }
        Dog d = (Dog) a; //向下转型
        d.lookHome();//调用狗类的lookHome方法
    }
}
```



我们来总结一下：

什么时候使用向上转型：当不需要面对子类类型时，通过提高扩展性，或者使用父类的功能就能完成相应的操作，这时就可以使用向上转型。

如：

```
Animal a = new Dog();
a.eat();
```

什么时候使用向下转型：当要使用子类特有功能时，就需要使用向下转型。如：

```
Dog d = (Dog) a; //向下转型
d.lookHome();//调用狗类的lookHome方法
```

向下转型的好处：可以使用子类特有功能。

弊端是：需要面对具体的子类对象；在向下转型时容易发生ClassCastException类型转换异常。在转换之前必须做类型判断。如： if( !a instanceof Dog){…} 

 

总结下封装、继承、多态的作用：
封装：把对象的属性与方法的实现细节隐藏，仅对外提供一些公共的访问方式。
继承：子类会自动拥有父类所有可继承的属性和方法。
多态：配合继承与方法重写提高了代码的复用性与扩展性；如果没有方法重写，则多态同样没有意义。多态的成员访问特点：方法的运行看右边，其他都看左边

### 类与类，类与接口，接口与接口之间的关系

类与类之间：继承关系，单继承，可以是多层继承
类与接口之间: 实现关系，单实现，也可以多实现
接口与接口之间：继承关系，单继承，也可以是多继承
Java中的类可以继承一个父类的同时，实现多个接口

### 笔记本电脑案例

案例介绍

定义USB接口（具备开启功能、关闭功能），笔记本要使用USB设备，即笔记本在生产时需要预留可以插入USB设备的USB接口，即就是笔记本具备使用USB设备的功能，但具体是什么USB设备，笔记本并不关心，只要符合USB规格的设备都可以。鼠标和键盘要想能在电脑上使用，那么鼠标和键盘也必须遵守USB规范，不然鼠标和键盘的生产出来无法使用。
进行描述笔记本类，实现笔记本使用USB鼠标、USB键盘
USB接口，包含开启功能、关闭功能
笔记本类，包含运行功能、关机功能、使用USB设备功能
鼠标类，要符合USB接口
键盘类，要符合USB接口

案例需求分析

阶段一：使用笔记本，笔记本有运行功能，需要笔记本对象来运行这个功能
阶段二：想使用一个鼠标，又有一个功能使用鼠标，并多了一个鼠标对象。
阶段三：还想使用一个键盘 ，又要多一个功能和一个对象
问题：每多一个功能就需要在笔记本对象中定义一个方法，不爽，程序扩展性极差。
降低鼠标、键盘等外围设备和笔记本电脑的耦合性。

实现代码步骤

定义鼠标、键盘，笔记本三者之间应该遵守的规则

```
interface USB {
    void open();// 开启功能
    void close();// 关闭功能
}
```

鼠标实现USB规则



```
class Mouse implements USB {
    public void open() {
        System.out.println("鼠标开启");
    }

    public void close() {
        System.out.println("鼠标关闭");
    }
}
```



键盘实现USB规则



```
class KeyBoard implements USB {
    public void open() {
        System.out.println("键盘开启");
    }

    public void close() {
        System.out.println("键盘关闭");
    }
}
```



定义笔记本



```
class NoteBook {
    // 笔记本开启运行功能
    public void run() {
        System.out.println("笔记本运行");
    }

    // 笔记本使用usb设备，这时当笔记本对象调用这个功能时，必须给其传递一个符合USB规则的USB设备
    public void useUSB(USB usb) {
        // 判断是否有USB设备
        if (usb != null) {
            usb.open();
            usb.close();
        }
    }

    public void shutDown() {
        System.out.println("笔记本关闭");
    }
}

public class Test {
    public static void main(String[] args) {
// 创建笔记本实体对象
        NoteBook nb = new NoteBook();
// 笔记本开启
        nb.run();
// 创建鼠标实体对象
        Mouse m = new Mouse();
// 笔记本使用鼠标
        nb.useUSB(m);
// 创建键盘实体对象
        KeyBoard kb = new KeyBoard();
// 笔记本使用键盘
        nb.useUSB(kb);
// 笔记本关闭
        nb.shutDown();
    }
}
```





# 自己的小笔记

## 快捷键

```
Ctrl+Alt+v    // new ArrayList<String>(); 后按住快捷键即可自动补全 和.var一样
.var		  // 自动为对象生成声明
psvm           // 快速生成main结构补全
sout		  // 输出函数补全
Ctrl+Alt+m	   // 抽取方法
Alt+Insert     // 构造方法
shift+f6       // 同类全选 方便改变量

先选中该变量，再按shift+F6			  // 改变相同变量的命名
```



## API

### Math (数学函数)

> 不能被实例化

![image-20210906234829595](https://i.loli.net/2021/09/06/ZnEuPaOfs6Uo3QY.png)

### Stytem (系统方法)

> 不能被实例化

![image-20210906235314566](https://i.loli.net/2021/09/06/GtEscFKIbhQ45U1.png)

### Object (对象方法)

> 每个类都可以将Object作为父类。所有类都直接或者间接的继承自该类

![image-20210907001507480](https://i.loli.net/2021/09/07/ynfleuYV7QXFtpJ.png)

**打印一个对象**

![image-20210907001348067](https://i.loli.net/2021/09/07/IEl4OsGBziVKpnj.png)

1. Object类是所有类的直接或者间接父类
2. 直接打印-一个对象就是打印这个对象的toString方法的返回值
3. Object类的toString方法得到的是对象的地址值
4. 我们一般会对toString方法进行重写

### Objects (对象方法)

![image-20210907113317979](https://i.loli.net/2021/09/07/lS3YxVank7TEM1J.png)

### BigDecimal (精准计算)

![image-20210908145905017](https://i.loli.net/2021/09/08/lPc4DfRV8IzyeSK.png)

- BigDecimal类的常用方法

![image-20210908150916381](https://i.loli.net/2021/09/08/dL4ZgYvymkuChJE.png)

1. BigDecimal是用来进行精确计算的
2. 创建BigDecimal的对象,构造方法使用参数类型为字符串的。
3. 四则运算中的除法,如果除不尽请使用divide的三E个参数的方法。

代码示例:

```java
BigDecimal divide = bd1.divide(参与运算的对象,小数点后精确到多少位，舍入模式);
	参数1 ,表示参与运算的BigDecimal对象
	参数2 ,表示小数点后面精确到多少位
	参数3 ,舍入模式
		BigDecimal.ROUND_P 进一法
		BigDecimal.ROUND_LOOR 去尾法
		BigDecimal.ROUND_ALF_UP 四舍五入
```

### 基本类型包装类概述

将基本数据类型封装成对象的好处在于可以在对象中定义更多的功能方法操作该数据

![image-20210908162654435](https://i.loli.net/2021/09/08/BKAfcMeb7LryZHp.png)

#### Integer类的概述和使用

Integer :该对象中包装了-个基本数据类型int的值

![image-20210908162919003](https://i.loli.net/2021/09/08/pUBil9ObmWkeQw4.png)

**自动装箱和自动拆箱**

- 装箱:把基本数据类型转换为对应的包装类类型
- 拆箱:把包装类类型转换为对应的基本数据类型

`注意:`在使用包装类类型的时候,如果做操作,最好先判断是否为null我们推荐的是,**只要是对象,在使用前就必须进行不为null的判断**

```java
Integer i1 = 100;
//jdk1.5的特性---自动装箱
//装箱:把一个基本数据类型变量对应的包装类.
//自动: Java底层会帮我们自动的调用valueof方法

Integer i3 = 100; //自动装箱机制
i3+=200;//i3=i3+200;
//会把i3这个对象变成基本数据类型100.
//100 + 200 = 300
//把基本数据类型300再次自动装箱变成Integer对象赋值给i3
```

#### int和字符串互相转换

基本类型包装类的最常见操作就是:用于基本类型和字符串之间的相互转换
1. int转换为String式

  方式一：加双引号即可
  方式二：public static String valueOf(inti) :返回int参数的字符串表示形式。该访法是String类中的方法

2. String转换为int
    public static int parselnt(Strings) :将字符串解析为int类型。该访法是Integer类中的方法

### 日期类API

1. 北京时间需要在世界标准时间上加8小时。
2. 1秒=1000毫秒
3. 计算机中的时间原点为: 1970年1月1日00:00:00

#### Date的构造方法

![image-20210913174643847](https://i.loli.net/2021/09/13/NqHjB3LcOhIYlet.png)

```java
public class DateDemo {
    public static void main(String[] args) {
        //这个时间表示电脑当前时间
        Date date1 = new Date();
        System.out.println(date1);

        //从计算机的时间原点开始，过了指定毫秒的那个时间。
        Date date2 = new Date(0L);
        System.out.println(date2);//Thu Jan 01 08:00:00 CST 1970
        //从时间原点开始，过了0毫秒。
        //因为我们是在中国，我们是在东八区需要+8小时。
    }
}
```

#### Date的成员方法

![image-20210913174925008](https://i.loli.net/2021/09/13/I8cwaXkQuCFzEA9.png)

```java
public class DateDemo {
    public static void main(String[] args) {
        //        public long getTime()
        //        获取时间对象的毫秒值
        //        public void setTime(long time)
        //        设置时间，传递毫秒值
        Date date1 = new Date();
        long time = date1.getTime();
        System.out.println(time);
        date1.setTime(0L);
        System.out.println(date1);  //Thu Jan 01 08:00:00 CST 1970
    }
}
```

#### SimpleDateFormat类

SimpleDateFormat可以对Date对象,进行格式化和解析

![image-20210913175840754](https://i.loli.net/2021/09/13/B5Oa8CcvH34YSgF.png)

- y   年
- M  月
- d   日 
- H   时
- m  分
- s   秒

![image-20210913180330647](https://i.loli.net/2021/09/13/uiE9hx3rfbnv4ge.png)

```java
public class DateDemo {
    public static void main(String[] args) throws ParseException {
//        当前日期的Date对象
        Date date = new Date();

//        创建日期格式
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");

//        格式化日期
        String res = sdf.format(date);
        System.out.println(res);

//        解析日期
        String s = "2048-02-09";
        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd");
        Date date1 = sdf1.parse(s);
        System.out.println(date1);
    }
}
```

**小结：**

1. 格式化( 从Date到String )
   public final String format(Date date) :把时间按照固定格式进行展示
2. 解析( 从String到Date )
   public Date parse(String source) : 需要对时间进行计算



## JDK8时间类 

![image-20210913192641719](https://i.loli.net/2021/09/13/RETFPgHMSyjvaeD.png)

在jdk8中计算时间：

```java
public class DateDemo {
    public static void main(String[] args) throws ParseException {
        String s = "2020年11月11日 00:00:00";
        DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");
        LocalDateTime localDateTime = LocalDateTime.parse(s, pattern);
        LocalDateTime newlocalDateTime = localDateTime.plusDays(1);
        String res = newlocalDateTime.format(pattern);
        System.out.println(res);
    }
}
```

#### LocalDateTime

![image-20210913193027131](https://i.loli.net/2021/09/13/SBANn4Fd9HkEjfi.png)

```java
public class DateDemo {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.now();
        System.out.println(localDateTime);
        //2021-09-13T19:34:30.896

        LocalDateTime time = LocalDateTime.of(2021, 11, 11, 11, 11, 11);
        System.out.println(time);
        //2021-11-11T11:11:11
    }
}
```

#### LocalDateTime获取方法

![image-20210913194158125](https://i.loli.net/2021/09/13/RY9UfNoEumJ3kvb.png)

#### LocalDateTime转换方法

![image-20210913194329964](https://i.loli.net/2021/09/13/mdkL1jrnSYauew3.png)

#### LocalDateTime格式化和解析

![image-20210913194720267](https://i.loli.net/2021/09/13/CIYktj1hrgv7Z85.png)

 ```java
 public class DateDemo {
     public static void main(String[] args) {
 //        method1();
         
 //        解析日期
         String s = "2020年11月12日 13:14:15";
         DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");
         LocalDateTime parse = LocalDateTime.parse(s, pattern);
         System.out.println(parse);
     }
 
     private static void method1() {
 //        格式化日期
         LocalDateTime localDateTime = LocalDateTime.now();
         System.out.println(localDateTime);
         DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");
         String s = localDateTime.format(pattern);
         System.out.println(s);
     }
 }
 ```

#### LocalDateTime增加或者减少时间方法

- 方法返回一个新的L ocalDate Time对象,返回值就是修改之后的结果。
- 参数为正,就是往后加
- 参数为负,就是往前减

![image-20210913202903562](https://i.loli.net/2021/09/13/uUwxVdD8sr4WKbp.png)

```java
public class DateDemo {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.now();
        System.out.println(localDateTime);
        LocalDateTime localDateTime1 = localDateTime.plusYears(-1);
        DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");
        String s = localDateTime1.format(pattern);
        System.out.println(s);	//2020年09月13日 20:27:17
    }
}
```

#### LocalDateTime修改方法

![image-20210913203143990](https://i.loli.net/2021/09/13/b83YqCF1VsGkMLI.png)

```java
public class DateDemo {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.of(2021, 11, 11, 11, 11, 11);
        LocalDateTime newlocalDateTime = localDateTime.withYear(2048);
        DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");
        String s = newlocalDateTime.format(pattern);
        System.out.println(s);
    }
}
```

#### Period

![image-20210913204545256](https://i.loli.net/2021/09/13/QJBPgzHjaR917mr.png)

```java
public class DateDemo {
    public static void main(String[] args) {
        LocalDate localDate = LocalDate.of(2021, 1, 1);
        LocalDate localDate1 = LocalDate.of(2022, 11, 11);
        Period period = Period.between(localDate, localDate1);
        System.out.println(period);                    //P1Y10M10D
        System.out.println(period.getDays());          //天数差
        System.out.println(period.toTotalMonths());    //获取此期间的总月数
    }
}
```

#### duration

```java
public class DateDemo {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.of(2048, 1, 1, 1, 1, 1);
        LocalDateTime localDateTime1 = LocalDateTime.of(2048, 11, 11, 11, 11, 11);
        Duration duration = Duration.between(localDateTime, localDateTime1);
        System.out.println(duration.toHours());     //获得时间间隔的小时
    }
}
```

**小结：**
LocalDate 表示日期(年月日)
LocalTime 表示时间(时分秒)
LocalDateTime 表示时间+日期(年月日时分秒)

- 创建时间对象(now，of)
- 获取时间对象中的年,月,日,时，分,秒
- 格式化( fomat )
- 解析( parse )
- 增加或减少时间的方法( plus开头, minus开头)
- 修改时间( with开头)

计算时间间隔的两个类:
Period (精确到天)
Duration (精确到纳秒)



##  数组的高阶操作

### 二分查找

1. 定义两个变量,表示要查找的范围。默认min=0，max=最大索引
2. 循环查找,但是min<=max
3. 计算出mid的值
4. 判断mid位置的元素是否为要查找的元素,如果是直接返回对应索引
5. 如果要查找的值在mid的左半边,那么min值不变, max= mid -1.继续下次循环查找
6. 如果要查找的值在mid的右半边,那么max值不变, min= mid + 1.继续下次循环查找
7. 当min> max时,表示要查找的元素在数组中不存在,返回-1.

```java
public class arrsearch {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int number = 3;
        int index = SearchIndex(arr, number);
        System.out.println(index);
    }

    private static int SearchIndex(int[] arr, int number) {
        // 1 定义查找范围
        int min = 0;
        int max = arr.length - 1;
        // 2 循环查找 min <= max
        while (min <= max) {
            // 3 计算出中间位置 mid  这个等于(min + max)/2
            int mid = (min + max) >> 1;
            if (arr[mid] > number) {
                // 表示要查找的元素在左边
                max = mid - 1;
            } else if (arr[mid] < number) {
                // 表示要查找的元素在右边
                min = mid + 1;
            } else {
                // 找到了
                return mid;
            }
        }
        return -1;
    }
}
```

### 冒泡排序

1. 相邻的元素两两比较,大的放右边,小的放左边,找到最大值。
2. 第一次循环结束,最大值已经找到,在数组的最右边。
3. 下一次只要在剩余的元素找最大值就可以了。
4. 因为已经确定了5是最大值,所以4跟5无须再进行比较了。
5. 因为已经确定了5是最大值, 4是次大值。所以3无须跟4和5再进行比较了。
6. 同理3 , 4, 5的位置经确定了, 2也无须这三个值进行比较了
7. 最后只剩下一个值1了,肯定就放在最后-一个格子中

```java
public class 冒泡排序 {
    public static void main(String[] args) {
        int[] arr = {3, 5, 2, 1, 4};
        bubbleSort(arr);
    }
    private static void bubbleSort(int[] arr) {
        // 外层循环控制的是次数比数组的长度少一次.
        for (int i = 0; i < arr.length - 1; i++) {
            // 内存循环就是实际循环比较的
            // -1 是为了让数组不要越界
            // -i 每一轮结束之后，我们就会少比一个数字
            for (int j = 0; j < arr.length - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        printArr(arr);
    }
    private static void printArr(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```

### 递归

递归概述:以编程的角度来看,递归指的是方法定义中调用方法本身的现象递归解决问题的思路:
把一个复杂的问题层层转化为-一个与原问题相似的规模较小的问题来求解递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算递归解决问题要找到两个内容:

- 递归出口 :否则会出现内存溢出
- 递归规则 :与原问题相似的规模较小的问题

![image-20210913135832205](https://i.loli.net/2021/09/13/981Fp3eIGvA6EmC.png)

### 排序

1. 从右开始找比基准数小的
2. 从左开始找比基准数大的
3. 交换两个值的位置
4. 红色继续往左找,色继续往右找,直到两个箭头指向同一一个索引|为止
5. 基准数归位

**基准数左边的,都比基准数小**
**基准数右边的,都比基准数大**
**相当于已经找到基准数应该在的位置**

```java
public class 快速排序 {
    public static void main(String[] args) {
        int[] arr = {6, 1, 2, 7, 9, 3, 4, 5, 10, 8};
        quiteSort(arr, 0, arr.length - 1);
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    private static void quiteSort(int[] arr, int left, int right) {
//        左边值大于右边值，停止递归
        if (right < left) {
            return;
        }

        int left0 = left;
        int right0 = right;

        int baseNumber = arr[left0];

        while (left != right) {
//            1. 从右开始找比基准数小的
            while (arr[right] >= baseNumber && right > left) {
                right--;
            }
//            2. 从左开始找比基准数大的
            while (arr[left] <= baseNumber && right > left) {
                left++;
            }
//            3. 交换两个值的位置
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
        }
//        基准数归位
        int temp = arr[left];
        arr[left] = arr[left0];
        arr[left0] = temp;

//        递归
        quiteSort(arr, left0, left - 1);
        quiteSort(arr, left + 1, right0);
    }
}
```

## 异常

异常:就是程序出现了不正常的情况。程序在执行过程中,出现的非正常的情况,最终会导致JVM的非正常停止。
**注意:语法错误不算在异常体系中。**

### 异常体系

![image-20210913210554809](https://i.loli.net/2021/09/13/SrfaZFJRbQVjpKC.png)

**编译时异常和运行时异常**

![image-20210913210724716](https://i.loli.net/2021/09/13/9xVoprCuTv23tLn.png)

**简单来说:**

编译时异常就是在编译的时候出现的异常
运行时异常就是在运行时出现的异常

### JVM的默认处理方案

如果程序出现了问题,我们没有做任何处理,最终JVM会做默认的处理

- 把异常的名称,异常原因及异常出现的位等信息输出在了控制台
- 程序停止执行

### 异常处理方式一throws

格式:

```java
throws 异常类名
```

**注意:** 这个格式是写在方法的定义处,表示声明一个异常。

- 编译时异常因为在编译时就会检查,所以必须要写在方法后面进行显示声明
- 运行时异常因为在运行时才会发生,所以在方法后面可以不写

 格式:

```java
throw new 异常();
```

注意:这个格式是在方法内的,表示当前代码手动抛出一个异常，下面的代码不用再执行了。

**throws和throw的区别**

| throws                                        | throw                                      |
| --------------------------------------------- | ------------------------------------------ |
| 用在方法声明后面,跟的是异常类名               | 用在方法体内 ,跟的是异常对象名             |
| 表示声明异常,调用该方法有可能会出现这样的异常 | 表示手动抛出异常对象 ,由方法体内的语句处理 |

### 异常处理方式一try..catch...

1. 如果try 中没有遇到问题，怎么执行?

    会把try中所有的代码全部执行完毕,不会执行catch里面的代码

2. 如果try中遇到了问题，那么try 下面的代码还会执行吗?
   那么直接跳转到对应的catch语句中, try下面的代码就不会再执行了
   当catch里面的语句全部执行完毕,表示整个体系全部执行完全,继续执行下面的代码

3. 如果出现的问题没有被捕获，那么程序如何运行?
   那么try...catch就相当于没有写.那么也就是自己没有处理.
   默认交给虚拟机处理.|

4. 同时有可能出现多个异常怎么处理?

   出现多个异常,那么就写多个catch就可以了。
   注意点:如果多个异常之间存在子父类关系.那么父类一 定要写在下面

```java
try {
可能出现异常的代码;
} catch (异常类名变量名) {
异常的处理代码;
}
```

**好处:可以让程序继续往下执行。**

```java
public class throwdemo {
    public static void main(String[] args) {
        int[] arr = null;
        try {   //try 中放有可能出现异常的代码
            printArr(arr);  //就会接受到一个异常 需要处理
        } catch (NullPointerException e) {
//              如果出现了异常，那么我们进行的操作
            System.out.println("参数不能为null");
        }
    }

    private static void printArr(int[] arr) {
        if (arr == null) {
            throw new NullPointerException();  //手动创建了一一个异常对象,抛给了调用者
        } else {
            for (int i = 0; i < arr.length; i++) {
                System.out.println(i);
            }
        }
    }
}
```

### Throwable的成员方法

![image-20210914160629905](https://i.loli.net/2021/09/14/eP6jRhIr4GvcfsB.png)

```java
public class throwdemo {
    public static void main(String[] args) {
//        public String getMessage () 返回此throwable的详细消息字符串
//        public String tostring () 返回此可拋出的简短描述
//        public void printstackTrace () 把异常的错误信息输出在控制台(字体为红色的)
        try {
            int[] arr = {1, 2, 3, 4, 5};
            System.out.println(arr[10]);
        } catch (ArrayIndexOutOfBoundsException e) {
            String message = e.getMessage();
            System.out.println(message);
            String s = e.toString();
            System.out.println(s);
            e.printStackTrace();
        }
        System.out.println("嘿嘿嘿");
    }
}
```

### 异常处理方式

**两种处理异常方式的小结**

- 抛出 throw throws
  ① 在方法中,当传递的参数有误,没有继续运行下去的意义了, 则采取抛出处理。示让该访法结束运行。
  ② 告诉调用者出现了问题。
- 捕获 try...catch
  捕获:能让代码继续往下运行。

```java
//学生类
public class Student {
    private String name;
    private int age;

    public Student() {

    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age >= 18 && age <= 25) {
            this.age = age;
        } else {
            throw new RuntimeException("年龄超出");		//抛出异常
        }
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

}

//主体
public class 异常 {
    public static void main(String[] args) {
        Student s = new Student();
        Scanner sc = new Scanner(System.in);
        System.out.println("姓名");
        String name = sc.nextLine();
        s.setName(name);
        while (true) {
            System.out.println("年龄");
            String ageStr = sc.nextLine();
            try {
                int age = Integer.parseInt(ageStr);
                s.setAge(age);
                break;
            } catch (NumberFormatException e) {
                System.out.println("请输入一个整数");
                continue;
            } catch (RuntimeException e) {
                System.out.println("请输入符合范围的年龄");
                continue;
            }
        }
        System.out.println(s);
    }
}
```

### 自定义异常

步骤

① 定义异常类
② 写继承关系
③ 空参构造
④ 带参构造

> AgeOutOfBoundsException

```java
public class AgeOutOfBoundsException extends RuntimeException{
    public AgeOutOfBoundsException() {
    }

    public AgeOutOfBoundsException(String message) {
        super(message);
    }
}
```

> Student

```java
    public void setAge(int age) {
        if (age >= 18 && age <= 25) {
            this.age = age;
        } else {
//            自定义异常的目的：为了让异常信息更加见名知意
//            throw new RuntimeException("年龄超出");
            throw new AgeOutOfBoundsException("年龄超出");
        }
    }
```

## 集合

### Collection集合

#### 集合和数组的对比小结

1. 数组的长度是不可变的,集合的长度是可变的。
2. 数组可以存基本数据类型和弓|用数据类型。
3. 集合只能存引|用数据类型,如果要存基本数据类型,需要存对应的包装类。

#### 集合类体系结构

![image-20210920121419494](https://i.loli.net/2021/09/20/zQjYnyehB7TfsFb.png)

#### Collection集合概述和使用

#### **Collection**集合概述****

- 是单例集合的顶层接口,它表示一组对象,这些对象也称为Collection的元素
- JDK不提供此接口的任何直接实现,它提供更具体的子接口(如Set和List)实现

#### 创建Collection集合的对象

- 多态的方式
- 具体的实现类ArrayList

#### 常用方法

![image-20210920123642350](https://i.loli.net/2021/09/20/I2xSVmY7cGX8HJL.png)

```java
public class MyCollection {
    public static void main(String[] args) {
        Collection<String> collection = new ArrayList<>();
//        boolean add(E e)添加元素
        collection.add("111");
        collection.add("222");
        collection.add("333");
//        System.out.println(collection);

//        boolean remove(Object o)从集合中移除指定的元素
//        remove(collection);

//        boolean removeif (Object o)根据条件进行删除
//        removeIf(collection);

//        void clear() 清空集合
//        clear(collection);

//        boolean contains(Object o)判断集合虫是否存在指定的元素
//        contains(collection);

//        boolean isEmpty() 判断集合是否为空
//        isEmpty(collection);

//        int size() 集合的长度，也就是集合中元素的个数
        size(collection);
    }

    private static void size(Collection<String> collection) {
        int size = collection.size();
        System.out.println(size);
    }

    private static void isEmpty(Collection<String> collection) {
        collection.clear();
        boolean empty = collection.isEmpty();
        System.out.println(empty);
    }

    private static void contains(Collection<String> collection) {
        boolean contains = collection.contains("111");
        System.out.println(contains);
        boolean contains2 = collection.contains("aaa");
        System.out.println(contains2);
    }

    private static void clear(Collection<String> collection) {
//        就是将集合中所有的元素全部删除
        collection.clear();
        System.out.println(collection);
    }

    private static void removeIf(Collection<String> collection) {
//        removeif底层会遍历集合,得到集合中的每一个元素
//        s依次表示集合中的每一个元素
        collection.removeIf(
                (String s) -> {
                    return s.length() == 3;
                }
        );
        System.out.println(collection);
    }

    private static void remove(Collection<String> collection) {
        boolean remove = collection.remove("111");
        boolean remove2 = collection.remove("444");
//        如果删除成功就会返回true
        System.out.println(remove);
        System.out.println(remove2);
        System.out.println(collection);
    }
}
```



#### Collection集合的遍历

Iterator :迭代器,集合的专用遍历方式

- Ilterator<E> iterator() :返回集合中的迭代器对象,该迭代器对象默认指向当前集合的0索引。

 Iterator中的常用方法

- boolean hasNext( :判断当前位置是否有元素可以被取出
- E next() :获取当前位置的元素 将迭代器对象移向下一个索引位置

```java
public class 迭代器 {
    public static void main(String[] args) {
        Collection<String> list = new ArrayList<>();
        list.add("a");
        list.add("b");
        list.add("c");

//        1. 获取迭代器的对象
//        迭代器对象一 旦被创建出来,默认指向集合的0索引处
        Iterator<String> iterator = list.iterator();

//        利用迭代器里面的方法进行遍历
//        当前位置是否有元素可以被取出
//        System.out.println(iterator.hasNext());
//        取出当前位置的元素 +将迭代器往后移动一个索引的位置
//        System.out.println(iterator.next());
//        System.out.println(iterator.next());

        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
}
```

#### 迭代器原理

![image-20210920143649905](https://i.loli.net/2021/09/20/CBWL2eGwVaR7jJ1.png)

#### 增强for循环

增强for :简化数组和Collection集合的遍历

- 它是JDK5之 后出现的,其内部原理是一个Iterator迭代器
- 实现Iterable接[ ]的类才可以使用迭代器和增强for

**增强for的格式**

```java
for(元素数据类型 变量名:数组或者Collection集合) {
//在此处使用变量即可,该变量就是元素
}
```

```java
//        1,数据类型一定是集合或者数组中元素的类型
//        2, str仅仅是一个变量名而己,在循环的过程中,依次表示集合或者数组中的每- -个元素
//        3,list就是要遍历的集合或者数组.
        Iterator<String> it = list.iterator();
        for (String s : list) {
            if ("b".equals(s)) {
                it.remove();
            }
        }
```

注意：修改第三方变量的值不会影响到集合中的元素 

![image-20210920145841189](https://i.loli.net/2021/09/20/i3TgEFV8QLwHKDI.png)

```java
//无效代码        
for (String s : list) {
            s = "q";
        }
        System.out.println(list);
```

#### 三种循环的使用场景

- 如果需要操作索引,使用普通for循环
- 如果在遍历的过程中需要删除元素,请使用迭代器
- 如果仅仅想遍历,那么使用增强for

```java
public class demo05 {
    public static void main(String[] args) {
        ArrayList<Student> list = new ArrayList<>();

        Student s1 = new Student("小爱同学",23);
        Student s2 = new Student("小李同学",25);
        Student s3 = new Student("小鹿同学",19);

        list.add(s1);
        list.add(s2);
        list.add(s3);

//        迭代器
        Iterator<Student> iterator = list.iterator();
        while (iterator.hasNext()){
            Student s = iterator.next();
            System.out.println(s);
        }

        System.out.println("----------------------------------");

//        增强for
        for (Student s : list) {
            System.out.println(s);
        }
    }
}
```

### List集合

#### List集合概述和特点

List集合概述

- 有序集合, 这里的有序指的是存取顺序
- 用户可以精确控制列表中每个元素的插入位置。户可以通过整数索引访问元素,并搜索列表中的元素
- 与Set集合不同 ,列表通常允许重复的元素

List集合特点

- 有序: 存储和取出的元素顺序一致
- 有索引: 可以通过索弓|操作元素
- 可重复 :存储的元素可以重复

**List集合特有方法**

![image-20210920164015817](https://i.loli.net/2021/09/20/1PKvoj6Cdrf9scM.png)

```java
public class demo02 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("aaa");
        list.add("bbb");
        list.add("ccc");

//        void add(int index,E element) 在此集合中的指定位置插入指定的元素
//        原来位置上的元素会往后挪一位
        list.add(0, "111");
        System.out.println(list);

//        E remove(int index)删除指定索引处的元素， 返回被删除的元素
        //在List集合中有两个删除的方法
        //第一个删除指定的元素,返回值表示当前元素是否删除成功
        //第二个删除指定索引的元素,返回值表示实际删除的元素
        String remove = list.remove(1);
        System.out.println(remove);
        System.out.println(list);

//        E set(int index,E element) 修改指定索引处的元素，返回被修改的元素
        String set = list.set(0, "qqq");
        System.out.println(set);
        System.out.println(list);

//        E get(int index)返回指定索引处的元素
        String s = list.get(2);
        System.out.println(s);
    }
}
```

##### ArrayList集合

ArrayList :底层数据结构是数组,查询快,增删慢

**ArrayList自动扩容源码**

![image-20210920171357550](https://i.loli.net/2021/09/20/5GLdMHvcsufSzwx.png)

##### LinkedList集合

List集合常用子类: ArrayList , LinkedList

- ArrayList :底层数据结构是数组,查询快,增删慢

- LinkedList :底层数据结构是链表,查询慢,增删快

```java
public class Linkdemo01 {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        list.add("aaa");
        list.add("bbb");
        list.add("ccc");

        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }

        System.out.println("------------------------------");

        Iterator<String> it = list.iterator();
        while (it.hasNext()) {
            System.out.println(it.next());
        }

        System.out.println("-----------------------");

        for (String s : list) {
            System.out.println(s);
        }
    }
}
```

**LinkedList特有方法**

![image-20210920171924018](https://i.loli.net/2021/09/20/ES6penbHRfKPwgX.png)

```java
public class Listdemo02 {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        list.add("aaa");
        list.add("bbb");
        list.add("ccc");
//        public void addFirst (E e)在该列表开头插入指定的元素
        list.addFirst("qqq");
        System.out.println(list);
//        public void addlast (E e)将指定的元素追加到此列表的末尾
        list.addLast("ppp");
        System.out.println(list);
//        public E getFirst ()返回此列表中的第一个元素
//        public E getLast ()返回此列表中的最后一个元素
        String first = list.getFirst();
        String last = list.getLast();
        System.out.println(first);
        System.out.println(last);
//        public E removeFirst ( )从此列表中删除并返回第一个元素
//        public E removeLast ( ) 从此列表中删除并返回最后一个元素
        String s = list.removeFirst();
        System.out.println(s);
        String s1 = list.removeLast();
        System.out.println(s1);
        System.out.println(list);
    }
}
```

**LinkedList源码**

![image-20210920174135665](https://i.loli.net/2021/09/20/ET3bzag1m9rXLHh.png)

### 泛型

泛型:是JDK5中引入的特性,它提供了编译时类型安全检测机制

泛型的好处:

- 把运行时期的问题提前到了编译期间
- 避免了强制类型转换

![image-20210921104457185](https://i.loli.net/2021/09/21/oUkaiR6LHm5wSpu.png)

如果一个类的后面有<E> ,表示这个类是一个泛型类。
创建泛型类的对象时,必须要给这个泛型确定具体的数据类型。

```java
//泛型类
public class Box<E> {
    private E elemrnt;

    public E getElemrnt() {
        return elemrnt;
    }

    public void setElemrnt(E elemrnt) {
        this.elemrnt = elemrnt;
    }
}
```

#### 泛型方法

```java
public class GenericityMethod {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("123");
        list.add("123");
        list.add("123");
//        将list集合转成-一个数组并返回
//        如果是空参的，那么返回的数组类型为object类型的。
        Object[] objects = list.toArray();
        System.out.println(Arrays.toString(objects));

//        如果带参，返回值就是参数类型
        String[] strings = list.toArray(new String[list.size()]);
        System.out.println(Arrays.toString(strings));
    }
}
```

#### 自定义泛型方法

泛型方法的定义格式:

- 格式: 修饰符<类型>返回值类型方法名(类型变量名) { }
- 范例: public <T> void show(T t) { }

```java
//        自定义泛型方法
//        定义一个泛型方法，传递一个集合和四个元素，将元素添加到集合中并返回
public class GenericityMethod2 {
    public static void main(String[] args) {
        ArrayList<String> list1 = addElement(new ArrayList<String>(), "a", "b", "c", "d");
        System.out.println(list1);

        ArrayList<Integer> list2 = addElement(new ArrayList<Integer>(), 1, 2, 3, 4);
        System.out.println(list2);
    }

    private static <T> ArrayList<T> addElement(ArrayList<T> list, T t1, T t2, T t3, T t4) {
        list.add(t1);
        list.add(t2);
        list.add(t3);
        list.add(t4);
        return list;
    }
}
```

#### 泛型接口

泛型接口的使用方式:

- 实现类也不给泛型
- 实现类确定具体的数据类型

泛型接口的定义格式:

- 格式: 修饰符interface接口名<类型>{ } 
- 范例: public interface Generic<T> { }

```java
public class GenericityInterface {
    public static void main(String[] args) {
        GenericityImpl1<String> genericity = new GenericityImpl1<>();
        genericity.method("123456");

        GenericityImpl2 GenericityImpl2 = new GenericityImpl2();
        System.out.println(123);
    }
}

//抽象类
interface Genericity<E> {
    public abstract void method(E e);
}

//实现类1 不给类型
class GenericityImpl1<E> implements Genericity<E> {

    @Override
    public void method(E e) {
        System.out.println(e);
    }
}
//实现类2 给定类型
class GenericityImpl2 implements Genericity<Integer>{

    @Override
    public void method(Integer integer) {

    }
}
```

#### 类型通配符

类型通配符: <?>

- ArrayList<?> :表示元素类型末知的ArrayList ,它的元素可以匹配任何的类型
- 但是并不能把元素添加到ArrayList中了,获取出来的也是父类类型
- 类型通配符上限: <? extends类型>
- 比如: ArrayList <? extends Number> :它表示的类型是Number或者其子类型
- 类型通配符下限 : <? super类型>

![image-20210921115153373](https://i.loli.net/2021/09/21/2csXp35z1ilKOdP.png)

```java
public class genericityglobbing1 {
//    ArrayList<?> :表示元素类型末知的ArrayList ,它的元素可以匹配任何的类型
//    但是并不能把元素添加到ArrayList中了,获取出来的也是父类类型
//    类型通配符上限: <? extends类型>
//    比如: ArrayList <? extends Number> :它表示的类型是Number或者其子类型
//    类型通配符下限 : <? super类型>
    public static void main(String[] args) {
        ArrayList<Integer> list1 = new ArrayList<>();
        ArrayList<Number> list2 = new ArrayList<>();
        ArrayList<Object> list3 = new ArrayList<>();

//        printList(list1);
//        printList(list2);

//        method1(list1);
//        method1(list2);
//        method1(list3); 报错

//        method2(list1); 报错
//        method2(list2);
//        method2(list3);
    }
//    表示传递进来集合的类型,可以是Number类型,也可以是Number所有的子类类型
    private static void method1(ArrayList<? extends Number> list){

    }
//    表示传递进来集合的类型,可以是Number类型,也可以是Number让所有的父类类型
    private static void method2(ArrayList<? super Number> list){

    }
//     通配符
    private static void printList(ArrayList<?> list) {

    }
}
```

### Set集合

Set集合特点

- 可以去除重复
- 存取顺序不一致
- 没有带索引的方法,所以不能使用普通for循环遍历,也不能通过索弓|来获取,删除Set集合里面的元素

```java
public class MySet1 {
    public static void main(String[] args) {
        Set<String> set = new TreeSet<>();
        set.add("aaa");
        set.add("ccc");
        set.add("aaa");
        set.add("bbb");


//        for (int i = 0; i < set.size(); i++) {
//            Set集合是没有索引的，所以不能使用通过索引获取元素的方法
//        }
        Iterator<String> it = set.iterator();
        while (it.hasNext()){
            String s = it.next();
            System.out.println(s);
        }
        System.out.println("-------------------");

        for (String s : set) {
            System.out.println(s);
        }
    }
}
```

#### TreeSet集合

TreeSet集合特点

- 不包含重复元素的集合
- 没有带索弓|的方法
- 可以将元素按照规则进行排序	

**` 想要使用TreeSet需要制定排序规则`**

#####  两种排序方法

##### 自然排序Comparable的使用

- 使用空参构造创建TreeSet集合
- 自定义的Student类实现Comparable接口

- **重写里面的compareTo方法**

![image-20210921173257078](https://i.loli.net/2021/09/21/h9fK8qpBlkHYZJe.png)

```java
public class Student implements Comparable<Student>  {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    @Override
    public int compareTo(Student o) {
//        按照对象年龄进行排序
//        主要判断条件
        int result = this.age - o.age;
//        次要判断条件
        result = result == 0 ? this.name.compareTo(o.getName()) : result;
        return result;
    }
}
```

##### 比较器排序Comparator的使用

- TreeSet的带参构造方法使用的是比较器排序对元素进行排序的
- 比较器排序,就是让集合构造方法接收Comparator的实现类对象,重写compare(To1,T o2)方法
- 重写方法时，一定要注意排序规则必须按照要求的主要条件和次要条件来写

```java
public class MyTreeSet3 {
    public static void main(String[] args) {
        TreeSet<Teacher> ts = new TreeSet<>(new Comparator<Teacher>() {
            @Override
            public int compare(Teacher o1, Teacher o2) {
//              o1表示现在要存入的那个元素
//              o2表示已经存入到集合中的元素

//               主要条件
                int result = o1.getAge() - o2.getAge();
//               次要条件
                result = result == 0 ? o1.getName().compareTo(o2.getName()) : result;
                return result;
            }
        });

        Teacher t1 = new Teacher("zhang", 23);
        Teacher t2 = new Teacher("lisi", 23);
        Teacher t3 = new Teacher("wangwu", 24);

        ts.add(t1);
        ts.add(t2);
        ts.add(t3);

        System.out.println(ts);
    }
}
```

##### 两种比较方式小结

- 自然排序:自定义类实现Comparable接口,重写compareTo方法,根据返回值进行排序。
- 比较器排序:创建TreeSet对象的时候传递Comparator的实现类对象,重写compare方法,根据返回值进行排序。
- **在使用的时候,默认使用自然排序,当自然排序不满足现在的需求时,使用比较器排序**

**两种方式中,关于返回值的规测：**

- 如果返回值为负数,示当前存入的元素是较小值,存左边
- 如果返回值为0 ,表示当前存入的元素跟集合中元素重复了， 不存
- 如果返回值为正数,示当前存入的元素是较大值,存右边

```java
public class MyTreeSet4 {
    public static void main(String[] args) {
//        TreeSet<String> ts = new TreeSet<>(new Comparator<String>() {
//            @Override
//            public int compare(String o1, String o2) {
//                int res = o1.length() - o2.length();
//                res = res == 0 ? o1.compareTo(o2) : res;
//                return res;
//            }
//        });
        TreeSet<String> ts = new TreeSet<>(
                (String o1, String o2) -> {
                    int res = o1.length() - o2.length();
                    res = res == 0 ? o1.compareTo(o2) : res;
                    return res;
                }
        );

        ts.add("c");
        ts.add("ab");
        ts.add("df");
        ts.add("qwer");

        System.out.println(ts);
    }
}
```

#### HashSet集合

HashSet集合特点

- 底层数据结构是哈希表
- 不能保证存储和取出的顺序完全一致
- 没有带索弓|的方法,所以不能使用普通for循环遍历
- 由于是Set集合,所以元素唯一

哈希值

哈希值(哈希码值) : 是JDK根据对象的**地址**或者**属性值**,算出来的**int类型的整数**

Object类中有一个方法可以获取对象的哈希值

- public int hash( ode() :根据对象的地址值计算出来的哈希值

**对象的哈希值特点**

- 如果没有重写hashCode方法 ,那么是根据对象的地址值计算出的哈希值。
  - 同一个对象多次调用hashCode0方法返回的哈希值是相同的
  - 不同对象的哈希值是不一样的。
- 如果重写了hashCode方法 , -般都是通过对象的属性值计算出哈希值。
  - 如果不同的对象属性值是一样的,那么计算出来的哈希值也是一样的。

```java
package MyHashSet;

import java.util.Objects;

public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }

//      我们可以对object类中的hashCode方法进行重写
//      在重写之后，就一般是根据对象的属性值来计算哈希值的
//      此时跟对象的地址值就没有任何关系了。|
//      如果HashSet集合要存储自定义对象，那么必须重写hashCode和equals方法	    
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

}
```

HashSet原理总结

**1.7版本**

- 底层结构:哈希表。(数组+链表)
- 数组的长度默认为16 ,加载因子为0.75
- 首先会先获取元素的哈希值,计算出在数组中应存入的索引
  - 判断该索引处是否为null
  - 如果是null ,直接添加
  - 如果不是null ,则与链表中所有的元素,通过equals方法比较属性值
  - 只要有一个相同,就不存,如果都不一样，才会存入集合。

![image-20210924002159566](https://i.loli.net/2021/09/24/oIZijkObnAKC2RB.png)

**1.8版本**

底层结构:哈希表。( 数组、链表、红黑树的结合体)

当挂在下面的元素过多,那么不利于添加,也不利于查询,所以在JDK8以后,当链表长度超过8的时候,自动转换为红黑树。

![image-20210924142054443](https://i.loli.net/2021/09/24/KeElGVuBWmMC5fw.png)

#### **小结**

![image-20210924143356290](https://i.loli.net/2021/09/24/ETPzbZ4yUS8wi2h.png)



### Map

- Interface Map<K,V>

- K:键的数据类型; V :值的数据类型

- 键不能重复,值可以重复

- 键和值是一一对应的 ,每一个键只能找到自己对应的值

- (键+值)这个整体我们称之为"键值对”或者“键值对对象” ,在Java中叫做"Entry对象” 。

- 举例:学生的学号和姓名

  ​	itheima001 小智
  ​	itheima002 小美
  ​	itheima003 大胖

创建Map集合的对象

- 多态的方式
- 具体的实现类HashMap

 ![image-20211001224125662](https://i.loli.net/2021/10/01/e4oVmGW2yCr1bJT.png)

```java
public class MyMapdemo1 {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();

        map.put("001","小智");
        map.put("002","小明");
        map.put("003","小美");

//        如果要添加的键不存在，那么会把键值对都添加到集合中
//        如果要添加的键是存在的，那么会覆盖原先的值，把原先值当做返回值进行返回。
        String s = map.put("001", "aaa");
        System.out.println(s);

        String remove = map.remove("002");
        System.out.println(remove);

//        清空
//        map.clear();

//       检查集合是否包含所指定的值
        boolean aaa = map.containsValue("aaa");
        System.out.println(aaa);

//        检查集合是否为空
        boolean empty = map.isEmpty();
        System.out.println(empty);

//        集合长度
        int size = map.size();
        System.out.println(size);

        System.out.println(map);
    }
}
```

 **两种遍历方法**

```java
public class MyMapdemo2 {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        map.put("1a","1b");
        map.put("2a","2b");
        map.put("3a","3b");
        map.put("4a","4b");
        map.put("5a","5b");
        map.put("6a","6b");

//        第一种方法
//        获取到所有的键
        Set<String> keys = map.keySet();

//        遍历Set集合得到每一个键
        for (String key : keys) {
//            通过每一个键key来获得对应的值
            String value = map.get(key);
            System.out.println(key+"-------"+value);
        }

//        第二种方法
//        首先要获取到所有的键值对对象。
//        Set集合中装的是键值对对象(Entry对象)
//        而Entry里面装的是键和值
        Set<Map.Entry<String, String>> entries = map.entrySet();
        for (Map.Entry<String, String> entry : entries) {
            String key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key+"-------"+value);
        }
    }
}
```

##### HashMap小结

- HashMap底层 是哈希表结构的
- 依赖hashCode方法和equals方法保证**键的唯一**
- 如果**键**要存储的是**自定义对象**,需要重写hashCode和equals方法

![image-20211002224149203](https://i.loli.net/2021/10/02/Mmvejo6TrcCpfWg.png)

案例：HashMap集合存储自定义对象并遍历

```java
public class MyMapdemo03 {
    public static void main(String[] args) {
        HashMap<Student,String> hm = new HashMap<>();

        Student s1 = new Student("xiaohei",21);
        Student s2 = new Student("xiaoming",21);
        Student s3 = new Student("xiaobai",21);

        hm.put(s1,"湖南");
        hm.put(s2,"湖北");
        hm.put(s3,"海南");

//        第一种 先获取到所有的键，再通过每一个键来找对应的值
        Set<Student> keys = hm.keySet();
        for (Student key : keys) {
            String value = hm.get(key);
            System.out.println(key+"------------"+value);
        }
        System.out.println("==================================");

//        第二种:先获取到所有的键值对对象。再获取到里面的每一个键和每一个值
        Set<Map.Entry<Student, String>> entries = hm.entrySet();
        for (Map.Entry<Student, String> entry : entries) {
            Student key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key+"------------"+value);
        }
        System.out.println("==================================");

//      第三种
        hm.forEach(
                (Student key,String value)->{
                    System.out.println(key+"------------"+value);
                }
        );
    }
}
```

![image-20211002231214203](https://i.loli.net/2021/10/02/DJU39Qk18xcnoIH.png)

##### TreeMap小结

- TreeMap底层是红黑树结构的
- 依赖自然排序或者比较器排序,对键进行排序
- 如果键存储的是自定义对象,需要实现Comparable接口或者在创建TreeMap对象时候给出比较器排序规则

![image-20211002232346330](https://i.loli.net/2021/10/02/x95LUqrfXAjFGIC.png)

案例：

```java
public class MyMapdemo4 {
    public static void main(String[] args) {
        TreeMap<Student,String> hm = new TreeMap<>(new Comparator<Student>() {
//          比较器排序   自然排序同 TreeSet 一样
            @Override
            public int compare(Student o1, Student o2) {
                int res = o1.getAge() - o2.getAge();
                res = res == 0 ? o1.getName().compareTo(o2.getName()) : res;
                return res;
            }
        });

        Student s1 = new Student("xiaohei",21);
        Student s2 = new Student("xiaoming",22);
        Student s3 = new Student("xiaobai",23);

        hm.put(s1,"湖南");
        hm.put(s2,"湖北");
        hm.put(s3,"海南");

//        第一种 先获取到所有的键，再通过每一个键来找对应的值
        Set<Student> keys = hm.keySet();
        for (Student key : keys) {
            String value = hm.get(key);
            System.out.println(key+"------------"+value);
        }
        System.out.println("==================================");

//        第二种:先获取到所有的键值对对象。再获取到里面的每一个键和每一个值
        Set<Map.Entry<Student, String>> entries = hm.entrySet();
        for (Map.Entry<Student, String> entry : entries) {
            Student key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key+"------------"+value);
        }
        System.out.println("==================================");

//      第三种
        hm.forEach(
                (Student key,String value)->{
                    System.out.println(key+"------------"+value);
                }
        );
    }
}
```

### 可变参数

可变参数:就是形参的个数是可以变化的

- 格式:修饰符返回值类型方法名(数据类型...变量名) {}
- 范例: public static int sumint..a) { }

可变参数注意事项

- 这里的变量其实是一 一个数组
- 如果一个方法有多个参数,包含可变参数,可变参数要放在最后

```java
public class 可变参数 {
    public static void main(String[] args) {
        int sum = getSum(1, 23, 5, 6, 78);
        System.out.println(sum);
    }

    public static int getSum(int... arr) {
        int sum = 0;
        for (int i = 0; i < arr.length; i++) {
            sum = sum + arr[i];
        }
        return sum;
    }
}
```

### 创建不可变集合

- 在List、 Set、 Map接口中,都存在of方法,可以创建一 个可变的集合。
- 这个集合不能添加,不能删除,不能修改。
- 但是可以结合集合的带参构造,实现集合的批量添加。
- 在Map接口中,还有一个ofEntries方法可以提高代码的阅读性。
- 首先会把键值对封装成一个Entry对象 ,再把这个Entry对象添加到集合当中。





## 数据结构

数据结构是计算机存储、组织数据的方式。是指相互之间存在一种或多种特定关系的数据元素的集合通常情况下,精心选择的数据结构可以带来更高的运行或者存储效率

- 栈
- 队列
- 数组
- 链表

**栈**

![image-20210920165401234](https://i.loli.net/2021/09/20/URPBSVgj7FsqL1Q.png)

**队列**

![image-20210920165333572](https://i.loli.net/2021/09/20/Bav7Yy9sGO6Lo5d.png)

**数组**

![image-20210920165652072](https://i.loli.net/2021/09/20/3J1ro7BKlynTCRW.png)

**链表**

![image-20210920170044693](https://i.loli.net/2021/09/20/ijRpnOTZbB6rkSw.png)

![image-20210920170127130](https://i.loli.net/2021/09/20/fCkx7ewpJONBrvH.png)

###  树

#### 二叉树

![image-20210923155859273](https://i.loli.net/2021/09/23/v1WkGdC7bXuROei.png)

![image-20210923155842040](https://i.loli.net/2021/09/23/cG7QB3SIVszqEHm.png)

#### 二叉查找树

二叉查找树,又称二叉排序树或者二叉搜索树。

特点:

1. 每一个节点上最多有两个子节点
2. 每一个节点的左子结点都是小于自己的
3. 每一个节点的右子结点都是大于自己的

![image-20210923160229839](https://i.loli.net/2021/09/23/wNvWzpfZxiCgRJD.png)

**二叉树查找树添节点**

规则:

- 小的存左边
- 大的存右边
- 一样的不存

![image-20210923160519548](https://i.loli.net/2021/09/23/EXaIKjHRVJG4zoP.png)

#### 平衡二叉树

- 二叉树左右两个子树的高度差不超过1
- 任意节点的左右两个子树都是一颗平衡二叉树

![image-20210923161540561](https://i.loli.net/2021/09/23/yMwBQHieLtXP9UJ.png)

**平衡二叉树-旋转**

- 左旋
- 右旋

触发时机：

当添加一个节点之后,该树不再是一颗平衡二叉树

##### 左旋

- 逆时针旋转
- 右子节点变成父节点(根节点)
- 原先的根节点降级变成左子节点
- 将多余的左子节点出让,给降级的节点作为右子节点

左旋:就是将根节点的右侧往左拉, 原先的右子节点变成新的父节点,并把多余的左子节点出让,给E经降级的根节点当右子节点

![img](https://i.loli.net/2021/09/23/LBFpw6xZtNTaGVj.jpg)

##### 右旋

- 顺时针旋转
- 左子节点变成父节点(根节点)
- 原先的根节点降级变成右子节点
- 将多余的右子节点出让,给降级的节点作为左子节点

右旋:将根节点的左侧往右拉,左子节点变成了新的父节点,并把多余的右子节点出让, 给已经降级根节点当左子节点

![img](https://i.loli.net/2021/09/23/8qM6Zm4tT5X3B2c.jpg)

#####  双旋转

对于有些树，单旋是无法解决问题的：

![在这里插入图片描述](https://i.loli.net/2021/09/23/SozvxwQreJfPLV5.png)

先对这个结点的左节点进行左旋转，再对当前结点进行右旋转即可。

![在这里插入图片描述](https://i.loli.net/2021/09/23/U6Vwe9JakqHpbZr.png)

#### 红黑树

红黑树是一种自平衡的二叉查找树,是计算机科学中用到的一种数据结构。
1972年出现,当时被称之为**平衡二叉B树**。后来，1978年被修改为如今的**"红黑树"**。
它是一种特殊的二叉查找树,红黑树的每一个节 点上都有存储位表示节点的颜色,
**每一个节点可以是红或者黑**;红黑树**不是高度平衡的**,它的平衡是通过"红黑规则"进行实现的

**红黑树特点**

- 平衡二叉B树
- 每一个节点可以是红或者黑
- 红黑树不是高度平衡的,它的平衡是通过“自己的红黑规则"进行实现的

**红黑规则**

1. 每一个节点或是红色的,或者是黑色的。
2. 根节点必须是黑色
3. 如果一个节点没有子节点或者父节点,则该节点相应的指针属性值为Nil ,这些Ni视为叶节点,每个叶节点(Nil)是黑色的;
4. 如果某一个节点是红色,那么它的子节点必须是黑色(不能出现两个红色节点相连的情况)
5. 对每一个节点,从该节点到其所有后代叶节点的简单路径上,均包含相同数目的黑色节点;

![image-20210923172549572](https://i.loli.net/2021/09/23/hfA8Vmg7pI6atlr.png)

##### **添加节点的小结**

红黑树在添加节点的时候：

添加的节点默认是红色的

![image-20210923231820483](https://i.loli.net/2021/09/23/DuR3W5QfUpar4Xi.png)

> Student类

```java
package Treesettest;

public class Student implements Comparable<Student> {
    private String name;
    private int chinese;
    private int math;
    private int engliah;

    public Student() {
    }

    public Student(String name, int chinese, int math, int engliah) {
        this.name = name;
        this.chinese = chinese;
        this.math = math;
        this.engliah = engliah;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getChinese() {
        return chinese;
    }

    public void setChinese(int chinese) {
        this.chinese = chinese;
    }

    public int getMath() {
        return math;
    }

    public void setMath(int math) {
        this.math = math;
    }

    public int getEngliah() {
        return engliah;
    }

    public void setEngliah(int engliah) {
        this.engliah = engliah;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", chinese=" + chinese +
                ", math=" + math +
                ", engliah=" + engliah +
                '}' + "总分为" + getSum();
    }

    public int getSum() {
        return this.chinese + this.engliah + this.math;
    }

    @Override
    public int compareTo(Student o) {
//        按照总分排序
        int res = this.getSum() - o.getSum();
//        总分一样比语文
        res = res == 0 ? this.getChinese() - o.getChinese() : res;
//        语文一样比数学
        res = res == 0 ? this.getMath() - o.getMath() : res;
//        数学一样比英语
        res = res == 0 ? this.getEngliah() - o.getEngliah() : res;
//        英语一样比姓名
        res = res == 0 ? this.getName().compareTo(o.getName()) : res;
        return res;
    }
}
```

> TreeSetdemo

```java
package Treesettest;

import java.util.TreeSet;

public class TreeSetdemo {
    public static void main(String[] args) {
        TreeSet<Student> ts = new TreeSet<>();

        Student s1 = new Student("dahei", 80, 80, 80);
        Student s2 = new Student("erhei", 90, 90, 90);
        Student s3 = new Student("sanhei", 100, 100, 100);

        ts.add(s1);
        ts.add(s2);
        ts.add(s3);

        for (Student student : ts) {
            System.out.println(student);
        }
    }
}
```

遍历:

1. 先获取左边
2. 再获取中间
3. 再获取右边

<img src="https://i.loli.net/2021/09/23/NAzmb3fLKSyO7wn.png" alt="image-20210923234539670" style="zoom:50%;" /><img src="https://i.loli.net/2021/09/23/xV64LpnP7urtOhX.png" alt="image-20210923234551580" style="zoom:33%;" /><img src="https://i.loli.net/2021/09/23/FEriNuIv6AtsVPg.png" alt="image-20210923234603811" style="zoom: 33%;" /><img src="C:/Users/Roy_Dust/AppData/Roaming/Typora/typora-user-images/image-20210923234727517.png" alt="image-20210923234727517" style="zoom: 33%;" />

<img src="C:/Users/Roy_Dust/AppData/Roaming/Typora/typora-user-images/image-20210923234804516.png" alt="image-20210923234804516" style="zoom: 80%;" />

