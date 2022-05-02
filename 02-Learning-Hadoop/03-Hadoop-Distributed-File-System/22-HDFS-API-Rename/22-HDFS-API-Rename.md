# 22-HDFS-API-Rename

```java
// Path 在这里边 
import org.apache.hadoop.fs.*;


	@Test
    public void rename() throws Exception {
        /**
         * 测试修改文件名
         */
        Path oldPath = new Path("/hdfsapi/test/b.txt");
        Path newPath = new Path("/hdfsapi/test/bb.txt");

        boolean result = fileSystem.rename(oldPath, newPath);
        System.out.println("Rename result : " + result);

    }
```

