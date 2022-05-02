# View-File-Contents

```java
import org.apache.hadoop.fs.*;
import org.apache.hadoop.io.IOUtils;

	@Test
    public void text() throws Exception {
        /**
         * 查看 HDFS 的文件内容的 API
         */
        
        FSDataInputStream in = fileSystem.open(new Path("/hdfsapi/output/hellokk.txt"));
        // 输出到控制台
        IOUtils.copyBytes(in, System.out, 1024);

    }
```

