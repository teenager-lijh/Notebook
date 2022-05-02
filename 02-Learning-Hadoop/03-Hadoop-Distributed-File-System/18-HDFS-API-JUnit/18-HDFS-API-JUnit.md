# HDFS-API-JUnit 

JUnit 怎么用 ？

编辑器： IDEA

在标有 @Test 的函数上边右键选中运行使用 @Test 所标注函数，就可以直接运行它了！

并且会先运行 @Before 所标注的函数 然后运行 @Test 标注的函数 最后运行 @After 所标注的函数

@Before ==> @Test ==> @After



用 JUnit 来封装代码

代码资源的申请和释放

```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;


// 申请资源 ==> 在 @Test 之前运行 Before Test
    @Before
    public void setUp() throws Exception {
        /**
         * 构造一个访问指定 HDFS 系统的客户端对象
         * 第一个参数 ： HDFS 的 URI
         * 第二个参数 ： 客户端指定的配置参数
         * 第三个参数 ： 访问 HDFS 系统的身份，即 用户名
         */
        System.out.println("-------setUp------");
        configuration = new Configuration();
        
        // configuration 的使用
        // 设置副本系数为 1 
        configuration.set("dfs.replication", "1");
        fileSystem = FileSystem.get(new URI(HDFS_PATH), configuration, "hadoop");
    }


// 释放资源 ==> 在 @Test 之后运行 After Test
    @After
    public void tearDown(){
        configuration = null;
        fileSystem = null;
        System.out.println("------tearDown------");
    }


```



需要测试的代码

```java
    @Test
    public void testCode() throws Exception {
        /**
         * 在这里执行需要测试的代码
         */
        // ...
    }
```



```java
    @Test
    public void mkdir() throws Exception {
        /**
         * 在 HDFS 中创建文件夹的 API
         */
        boolean result = fileSystem.mkdirs(new Path("/hdfsapi/hello111/"));
        System.out.println(result);
    }
```

