# List-Files

```
查看所有文件 ==> 递归列出所有文件
hadoop fs -ls -R /
```



```java
// 查看单个目录中的所有文件

	@Test
    public void listFiles() throws Exception{
        /**
         * 列出 HDFS 文件系统中的文件信息
         */
        Path path = new Path("/hdfsapi/test/hello.txt");
        // fileStatuses 中的每个元素都是一个文件的 描述信息
        FileStatus[] fileStatuses = fileSystem.listStatus(path);

        // 遍历 fileStatuses 数组
        for(FileStatus file : fileStatuses){
            String isDir = file.isDirectory() ? "文件夹" : "文件";
            String permission = file.getPermission().toString();
            short replication = file.getReplication();
            long length = file.getLen();

            System.out.println(isDir + "\t" + permission + "\t"
                + replication + "\t" + length
            );
        }

    }
```





```java
// 递归查此目录下的所有文件

    @Test
    public void listFilesRecursive() throws Exception{
        /**
         * 列出 HDFS 文件系统中的文件信息
         */
        Path path = new Path("/hdfsapi/test");
        // 查看源码 ==> listFiles 返回一个迭代器
        // 第二个参数 recursive=true ==> 表明递归列出所有文件
        RemoteIterator<LocatedFileStatus> files = fileSystem.listFiles(path, true);
        while(files.hasNext()){
            LocatedFileStatus file = files.next();

            String isDir = file.isDirectory() ? "文件夹" : "文件";
            String permission = file.getPermission().toString();
            short replication = file.getReplication();
            long length = file.getLen();
            Path name = file.getPath();

            System.out.println(isDir + "\t" + permission + "\t"
                    + replication + "\t" + length + "\t" + name
            );

        }
    }
```

