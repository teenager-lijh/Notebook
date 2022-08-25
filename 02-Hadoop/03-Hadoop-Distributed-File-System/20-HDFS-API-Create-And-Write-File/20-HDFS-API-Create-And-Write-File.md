# Create-And-Write-File

```java
import org.apache.hadoop.fs.*;

	@Test
    public void create() throws Exception {
        /**
         * 创建文件并添加到 HDFS 中
         */

        FSDataOutputStream out = fileSystem.create(new Path("/hdfsapi/test/b.txt"));
        out.writeUTF("hello world. \n");
        out.flush();
        out.close();
    }
```

