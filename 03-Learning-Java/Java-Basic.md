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

