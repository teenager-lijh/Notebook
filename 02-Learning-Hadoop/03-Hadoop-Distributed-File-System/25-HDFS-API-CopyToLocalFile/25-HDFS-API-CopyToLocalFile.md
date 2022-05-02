# CopyToLocalFile

```java
    @Test
    public void copyToLocalFile() throws Exception {
        /**
         * 拷贝 HDFS 文件系统的文件到本地
         * @throws Exception
         */

        Path dst = new Path("C:\\Users\\lijh\\Desktop");
        Path src = new Path("/hdfsapi/test/hello.txt");

        // 空指针错误 ==> 在课程中 CDH 使用的是这个 API
        // fileSystem.copyToLocalFile(src, dst);
        
        // 经过搜索后 ==> Apache 使用如下 API
        // delSrc : false
        // useRawLocalFileSystem : true
        fileSystem.copyToLocalFile(false, src, dst, true);
    }
```

