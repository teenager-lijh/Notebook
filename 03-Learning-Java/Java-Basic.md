参考课程:
https://www.youtube.com/watch?v=P7izmVK-dCE&list=PLmuZ8T57c_h0rRCzwT5hYQNRUYkAF1y9y&index=12

# 001-Javac 和 Java 两个程序

java 文件： java 文件的类名必须与文件名保持一致
javac ==> 编译 java 程序 （Java Compiler）
java ==> 运行 java 字节码 （file_name.class 文件）

    javac file_name.java
    java file_name (运行的是 class 文件，字节码)

# 002-Java 项目结构

![image-20220422103245086](Java-Basic.assets/image-20220422103245086-16505947870101.png)

Java-Package（Java 的包）是一组文件夹组成的
com.lijh.hdfs ==> 三个文件夹 ==> com ==> lijh ==> hdfs


# 003-IDEA 快捷键
生成 main 方法: psva (public static void main)
生成 println 输出语句: sout (system.out.println)
修复错误代码快捷键：Alt + Enter 会给出修复建议
删除光标所在行：Ctrl + y
复制光标所在行：Ctrl + d
格式化代码: Ctrl + Alt + l
上下移动代码：Alt + Shift + 上/下

# 004-IDEA导入新的 Module
Moudle 文件夹拷贝当项目目录下后，通过下图的方式导入
File ==> Settings ==> Project Structure ==> Modules ==> "+"加号 ==> Import Module

![image-20220422144853484](Java-Basic.assets/image-20220422144853484.png)

# 005-成员函数重载

同名不同参数 ==> 重载

# 006-数组

1 动态初始化数组
dataType[] arrayName = new dataType[arrayLength]

2 静态初始化
dataType[] arrayName = new dataType[] {value, ...}

3 静态初始化...省略格式
dataType[] arrayName =  {value, ...}

#  007-Java 内存划分

Java 的内存划分为五个部分:

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

# 008-接口 Interface

接口是多个类的公共规范，
接口是一种引用数据类型，最重要的内容就是其中的抽象方法
接口被编译后生成的文件仍然是 .class 类型的文件
如果实现类并没有覆盖重写接口中的所有抽象方法，那么这个实现类自己必须就是抽象类

接口使用规则：

1. 接口不能直接使用，必须有一个实现类来实现接口
2. 接口中所有的抽象方法必须全部覆盖重写
3. 接口中不能定义构造函数，不能定义静态代码块
4. 如果一个类实现的多个接口中，有重复的抽象方法，那么只需要覆盖重写一次即可

Java 7 可包含：

- 成员变量：常量
- 抽象方法

Java 8 可额外包含

- 默认方法
- 静态方法

Java 9 可额外包含

- 私有静态方法

接口中方法的定义：
1 定义常量
2 定义抽象方法
3 定义默认方法
为了解决接口升级的问题，因为之前的版本要求覆盖所有的抽象方法，但是当接口改动之后新添加了一个方法，可是实现类并没有实现这些新添加的抽象方法那么就会出现问题
4 定义静态方法
5 定义私有方法
		1）普通私有方法，解决多个默认方法之间代码重复问题
		2）静态私有方法，解决多个静态方法之间重复代码问题

```Java
public interface interfaceName {
    // 1 定义成员变量:常量
    //   从效果上看就是常量
    public static final 数据类型 常量名称 = 数据值;
    public static final dataType VAR_NAME = value;
    // public ==> 都可使用
    // static ==> 静态的，直接接口名点属性
    // final ==> 不可改变
    // 即使不写这些关键字，也默认是这个属性
    // 接口中的常量必须赋值
    
    // 2 定义抽象方法 - 四种方式等效
	public abstract void methodOne();
    abstract void methodTwo();
    public void methodThree();
    void methodFour();
 	
    // 3 定义默认方法
    public default void method() {
        // ...
        // 若
    }
    
    // 4 定义静态方法
    public static void methodStatic() {
        // ...
        // 不能通过接口实现类来调用接口的静态方法
        // 应该通过接口名直接调用静态方法
        // 静态方法的调用不需要创建一个实例对象
        
        // 适用于不想让实现类访问的情况
        // 用于抽取公共方法
        
        // 如，可以让默认方法使用
        // 但是不能让实现类使用
    }
    
    // 5-1 普通私有方法
    private void method() {
        // ...
    }
    
    // 5-2 静态私有方法
    private static void method() {
        // ...
    }
}
```

# 009-类  ==> 封装 继承 多态

面向对象的三大特征：
        1 封装性：父类 ==> 基类、超类（高层）；子类 ==> 派生类
        2 继承性：主要解决 **共性抽取，代码复用** (所有类的祖宗都是java.lang.Object)
        3 多态性：

1 封装性如图：

![image-20220425163139343](Java-Basic.assets/image-20220425163139343.png)

2 继承：仅支持单继承

```java
public class 类名 extends 父类名 {
    // ...
    // extends class_name ==> 扩展自 class_name 
}
```

成员变量的规则：成员变量重名，优先访问子类的成员变量，若没有则向上查询。

```java
// 三者重名
// 局部成员变量、类成员变量、父类(super)成员变量
// 1 访问局部变量 ==> 直接使用变量名
int nums;
nums = 666;

// 2 访问类成员变量
public class class_name {
    int hello;
    public static int getHello() {
        return this.hello
    }
}

// 2 访问父类成员变量
// super ==> 表示超级 ==> 也就是超类 即 父类
public class sub_class_name extends class_name {
    int hello;
    public static int getParentHello() {
        return super.hello
    }
}

```

成员函数重名时的访问规则：实例化对象优先访问当前类，若没有则向上查找。在编写子类的时候使用 super 点的方式调用父类的成员函数。

方法的重写（覆盖）Override
1 要求成员函数名相同、参数列表相同
2 子类重写的方法的返回值必须小于等于父类的返回值（这里的小是指子类方法的返回值的类型必须是父类方法返回值类型的子类或者与父类返回值类型相同）
3 权限大小关系:public > protected > (default) < private
default 不是关键字而是留空，子类方法的权限必须大于等于父类方法的权限
疑问：default 是个什么鬼权限？

```java
public class Parent {
    public void method() {
        
    }
}


// 为了保证检测是否重写成功
// 使用注解 @Override 来检查，可选项
// 疑问：
// 预编辑阶段注解起作用，就像 C 语言的预处理？
public class Son {
    
    @Override
    public void method() {
        
    }
}

```

构造函数 ==> super 就相当于父类的实例对象

1. 子类构造函数中有默认的 super() 的调用，super() 相当于调用父类的实例对象的构造函数
2.  java: 对super的调用必须是构造器中的第一个语句
3. 当父类中没有默认的无参数构造函数的时候，必须手动写出调用父类构造函数的语句
4. 若显示的写出 super() 构造器的调用，则编译器只会默认添加一个无参数构造的 super() 调用
5. super() 和 this() 只能选择一个

```java
public class Parent {
    public Parent() {
        // ...
    }
}

public class Son extends Parent {
    public Son() {
        super(); // 可选，默认会带这个语句
        // ...
    }
}

Son son = new Son();
// 此时会先执行父类的构造函数
// 然后才会执行子类构造函数
// 因为子类用到父类的资源
// 所以父类需要先初始化才可以
```


super 关键字的三种用法

1. 在子类中访问父类实例对象的成员变量
2. 在子类中访问父类实例对象的成员函数
3. 在子类的构造函数中访问父类的构造函数

```java
public class Parent {
    public Parent() {
        // ...
    }
    
    // ...
}

public class Son extends Parent {
    public Son() {
        // 3 
        super(); // 可选，默认会带这个语句
        // 1 
        super.var_name;
        
        // 2 
        super.method();
    }
}

Son son = new Son();
```

this关键字的三种用法

1. 访问本类的成员变量
2. 访问本类的构造函数
3. 访问本类的成员函数

```java
public class class_name {
    public Son() {
        // 在无参构造函数中
        // 调用本类的有参构造函数
        // 同样必须 this(666) 是第一条语句
        // 且只能使用一次调用
		this(666);
    }
    
    public Son(int nums) {
        
    }
}

Son son = new Son();
```



抽象
抽象的概念：
图形的面积 ==> 各种各样的图形独有其面积计算方法
类中的方法不确定如何实现，那么此方法应是一种抽象方法，具体实现要放在子类中

![image-20220426143232682](Java-Basic.assets/image-20220426143232682.png)

一段代码实例：

```java
// 抽象方法所在的类必须是抽象类
// 抽象类不能够实例化
// 定义抽象类
public abstract class Animal {
    // 若出现抽象方法，则必须是抽象类
    public abstract void eat();
    
    // 普通方法的定义不受影响
    // 普通方法可以出现在抽象类中
    public void method() {
        // ...
    }
}

// 必须使用一个子类来继承抽象类来使用它
// 子类必须实现父类的所有抽象方法
public class Cat extends Animal {
    @Override
    public void eat() {
        // ...
    }
}

// 使用
Cat cat = new Cat();
cat.eat();
```

抽象类的四点注意事项：

1. 抽象类不能创建抽象对象，如果创建，编译无法通过而报错，只能创建其非抽象子类的对象。
2. 抽象类中可以有构造函数，是提供子类创建对象时，初始化父类成员使用的。
3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类
4. 抽象类的子类，必须重写父类中所有的抽象方法，否则编译无法通过，除非该子类也是抽象类则不必重写所有父类抽象方法。

静态代码块 static block

```java
// 静态代码块位于类的内部 接口中不能够定义静态代码块
// 静态代码块的执行优先于类的构造函数
// 静态代码块可以存在多个，并且执行顺序是按照在类中
// 定义的先后顺序由上至下依次执行的
public class Parent {
    
    public Parent() {
        System.out.println("I am parent class constructor");
    }

    static {
        System.out.println("I am static code block - two");
    }

    static {
        System.out.println("I am static code block");
    }

    static {
        System.out.println("I am static code block - three");
    }

}

// 执行如下语句后
Parent parent = new parent();

// 输出示例：
// I am static code block - two
// I am static code block
// I am static code block - three
// I am parent class constructor
```

























