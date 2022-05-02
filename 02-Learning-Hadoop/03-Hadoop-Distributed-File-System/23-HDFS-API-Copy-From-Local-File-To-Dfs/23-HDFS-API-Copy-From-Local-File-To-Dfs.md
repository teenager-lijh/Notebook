# Copy-From-Local-File

从本地拷贝文件到文件系统中

```java
    @Test
    public void copyFromLocalFile() throws Exception {
        /**
         * 拷贝本地文件到 HDFS 文件系统
         * @throws Exception
         */

        Path src = new Path("C:\\Users\\lijh\\Desktop\\hellokk.txt");
        Path dst = new Path("/hdfsapi/test/");

        fileSystem.copyFromLocalFile(src, dst);
    }
```



// ................................. 待处理 ..................................................

// 拷贝大文件

```java
    @Test
    public void copyFromLocalBigFile() throws Exception {

        InputStream in = new BufferedInputStream(new FileInputStream(new File("/Users/rocky/tmp/software/jdk-8u91-linux-x64.tar.gz")));

        FSDataOutputStream out = fileSystem.create(new Path("/hdfsapi/test/jdk.tgz"),
                new Progressable() {
                    public void progress() {
                        System.out.print(".");
                    }
                });

        IOUtils.copyBytes(in, out ,4096);

    }
```

