参考课程:
https://www.youtube.com/watch?v=P7izmVK-dCE&list=PLmuZ8T57c_h0rRCzwT5hYQNRUYkAF1y9y&index=12

## 两个程序

java 文件： java 文件的类名必须与文件名保持一致
javac ==> 编译 java 程序 （Java Compiler）
java ==> 运行 java 字节码 （file_name.class 文件）

    javac file_name.java
    java file_name (运行的是 class 文件，字节码)

## Java 项目结构

![image-20220422103245086](Java-Basic.assets/image-20220422103245086-16505947870101.png)

Java-Package（Java 的包）是一组文件夹组成的
com.lijh.hdfs ==> 三个文件夹 ==> com ==> lijh ==> hdfs


## IDEA 快捷键
生成 main 方法: psva (public static void main)
生成 println 输出语句: sout (system.out.println)
修复错误代码快捷键：Alt + Enter 会给出修复建议
删除光标所在行：Ctrl + y
复制光标所在行：Ctrl + d
格式化代码: Ctrl + Alt + l
上下移动代码：Alt + Shift + 上/下

## 导入新的 Module
Moudle 文件夹拷贝当项目目录下后，通过下图的方式导入
File ==> Settings ==> Project Structure ==> Modules ==> "+"加号 ==> Import Module

![image-20220422144853484](Java-Basic.assets/image-20220422144853484.png)

## 成员函数重载

同名不同参数 ==> 重载

## 数组

1 动态初始化数组
dataType[] arrayName = new dataType[arrayLength]

2 静态初始化
dataType[] arrayName = new dataType[] {value, ...}

3 静态初始化...省略格式
dataType[] arrayName =  {value, ...}

##  Java 的内存需要划分为 5 个部分 

1 栈 Stack : 存放的是方法中的局部变量
        局部变量：方法的参数，或者是方法内部的变量
2 堆 Heap：凡是 new 出来的东西，都在堆当中
        堆内存里面的东西都有一个地址值：16 进制的
        堆内存里边的数据都有默认值，规则：
        整型 默认为 0
        浮点数 默认为 0.0
        字符 默认为 '\u0000'
        布尔 默认为 false
        引用类型 默认为 null
3 方法区 Method Area：存储 .class 的相关信息，包含方法的信息，但是正在运行的方法都存放在栈中，方法区仅仅是死数据
4 本地方法栈 Native Method Stack : 与操作系统相关
5 寄存器 Register : 与 CPU 相关
一段代码的内存描述图：
![image-20220422232701035](Java-Basic.assets/image-20220422232701035.png)

## 接口 Interface

接口是多个类的公共规范，
接口是一种引用数据类型，最重要的内容就是其中的抽象方法
接口被编译后生成的文件仍然是 .class 类型的文件

Java 7 可包含：
1 常量
2 抽象方法
Java 8 可额外包含
3 默认方法
4 静态方法
Java 9 可额外包含
5 私有方法

public interface interfaceName {
	// 接口内容
}

当前应看视频 173





