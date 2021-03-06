# Pluggable Business Logic

可插拔的业务逻辑，关键在于使用 Java 的反射机制

通过在配置文件中配置需要使用的类的   全类名

实例化此类的时候 ==> 使用反射机制创建实例对象

使用多态，完成相似任务的代码都继承了同样的接口或者父类

一般化写法 `Class<?> cls= Class.forName()`

多态写法 `ImoocMapper mapper = (ImoocMapper)cls.newInstance(); `

## 核心代码

```java
// getClassLoader().getResourceAsStream() 默认从 mian 下的 resources 中加载文件
properties.load(ParamsUtils.class.getClassLoader().getResourceAsStream("wc.properties"));

// 使用反射来创建对象 ==> 其中 ? 问号 是通配符 ==> 因为它知道类的元信息所以可以自动适配类型
// 这样也更易容可插拔的设计 ==> 因为一旦 forName 后边的参数变了，它的类型也会跟着变
Class<?> cls= Class.forName(properties.getProperty(Constants.MAPPER_CLASS));

// 使用多态的写法 ==> 父类接口 指向子类对象
ImoocMapper mapper = (ImoocMapper)cls.newInstance(); // 用来写缓存
```



## 配置文件 

```
// filename ==> wc.properties
// src/main/resources/wc.properties   wc = word count 单词统计

INPUT_PATH=/hello.txt
OUTPUT_PATH=/hellol.txt
OUTPUT_FILE="OUTPUT_FILE";
HDFS_URI=hdfs://hadoop000:8020
USER=lijh
MAPPER_CLASS=com.imooc.bigdata.hadoop.hdfs.utils.CaseIgnoreWordCountMapper
```



## 配置文件加载类

```java
package com.imooc.bigdata.hadoop.hdfs.utils;

import java.io.IOException;
import java.util.Properties;

/**
 * 读取属性配置文件
 */
public class ParamsUtils {
    private static Properties properties = new Properties();

    static {
        try {
             properties.load(ParamsUtils.class.getClassLoader().getResourceAsStream("wc.properties"));
//            properties.load(ParamsUtils.class.getResourceAsStream("/wc.properties"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static Properties getProperties() throws  Exception {
        return properties;
    }

    public static void main(String[] args) throws Exception {
        System.out.println(getProperties().getProperty("USER"));
    }

}
```



## 业务逻辑

```java
package com.imooc.bigdata.hadoop.hdfs.app;


import com.imooc.bigdata.hadoop.hdfs.Constants;
import com.imooc.bigdata.hadoop.hdfs.ImoocMapper;
import com.imooc.bigdata.hadoop.hdfs.utils.ImoocContext;
import com.imooc.bigdata.hadoop.hdfs.utils.ParamsUtils;
import com.imooc.bigdata.hadoop.hdfs.utils.WordCountMapper;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.*;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.URI;
import java.util.Map;
import java.util.Properties;
import java.util.Set;


/**
 *1) 读取 HDFS 上的文件 ==> HDFS API
 *2) 业务处理（词频统计）: 对文件中的每一行数据都要进行业务处理(按照分隔符分割)
 *3) 将处理结果缓存起来
 *4) 将结果输出到 HDFS ==> HDFS API
 */
public class HDFSWCApp03 {

    public static void main(String[] args) throws Exception{

        Properties properties = ParamsUtils.getProperties();


//        1) 读取 HDFS 上的文件 ==> HDFS API
        Path input = new Path(properties.getProperty(Constants.INPUT_PATH));

//        获取要操作的 HDFS 文件系统
        FileSystem fs = FileSystem.get(new URI(properties.getProperty(Constants.HDFS_URI)), new Configuration(), properties.getProperty(Constants.USER));
        RemoteIterator<LocatedFileStatus> iterator= fs.listFiles(input, false);

        // 使用反射来创建对象 ==> 其中 ? 问号 是通配符 ==> 因为它知道类的元信息所以可以自动适配类型
        // 这样也更易容可插拔的设计 ==> 因为一旦 forName 后边的参数变了，它的类型也会跟着变
        Class<?> cls= Class.forName(properties.getProperty(Constants.MAPPER_CLASS));

        // 使用多态的写法 ==> 父类接口 指向子类对象
        ImoocMapper mapper = (ImoocMapper)cls.newInstance(); // 用来写缓存
        // WordCountMapper mapper = new WordCountMapper(); // 用来写缓存
        ImoocContext context = new ImoocContext(); // 缓存对象

        while(iterator.hasNext()) {
            // 遍历输入路径下的所有文件
            LocatedFileStatus file = iterator.next();
            FSDataInputStream in = fs.open(file.getPath());
            BufferedReader reader = new BufferedReader(new InputStreamReader(in));

            String line = "";
            while((line = reader.readLine()) != null) {
//              2) 业务处理 ==> 处理单个文件
                // TODO... 在业务逻辑完成后将结果写到Cache中去
                mapper.map(line, context);
            }

            reader.close();
            in.close();
        }

//      3) 将处理结果缓存起来

        Map<Object, Object> contextMap = context.getCacheMap();


//      4) 将结果输出到 HDFS ==> HDFS API
        Path output = new Path(properties.getProperty(Constants.OUTPUT_PATH));
        FSDataOutputStream out = fs.create(output);

        // TODO... 将第三步缓存中的内容输出到 out 中去
        Set<Map.Entry<Object, Object>> entries = contextMap.entrySet();
        for(Map.Entry<Object, Object> entry : entries) {
            out.write((entry.getKey().toString() + "\t" + entry.getValue() + "\n").getBytes());

        }

        
        out.close();
        fs.close();

        System.out.println("完成了词频统计 Lijh");

    }
}

```

