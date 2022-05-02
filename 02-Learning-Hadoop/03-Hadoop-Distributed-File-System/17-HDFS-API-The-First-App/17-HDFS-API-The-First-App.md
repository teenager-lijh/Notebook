# The First Application

```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

public class App {
    public static void main(String[] args) throws Exception{

        // 在 FileSystem 中共有共有三个 get 方法
        // 调用 get 方法返回一个 FileSystem 的实例对象
        Configuration configuration = new Configuration();
        Path path = new Path("/hello");
        FileSystem fileSystem = FileSystem.get(new URI("hdfs://hadoop000:8020"), configuration, "lijh");
        
        // 创建文件夹
        boolean result = fileSystem.mkdirs(path);
        System.out.println(result);

    }
}
```

