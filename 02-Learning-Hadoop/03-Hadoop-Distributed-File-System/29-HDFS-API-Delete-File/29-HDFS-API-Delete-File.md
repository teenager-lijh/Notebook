# Delete File

```java
    @Test
    public void delete() throws Exception {
        /**
         * 删除 HDFS 系统中的文件
         */
        Path path= new Path("/hdfsapi/test/hello.txt");
        // 选择是否要递归删除 ==> true
        boolean result = fileSystem.delete(path, true);
        System.out.println("result : " + result);
    }
```

