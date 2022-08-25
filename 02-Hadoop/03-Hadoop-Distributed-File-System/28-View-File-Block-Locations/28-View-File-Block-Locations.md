# View-File-Block-Locations

```java
// 查看文件所分割的块数
// 查看文件块都具体存放在了哪些节点上

	@Test
    public void getFileBlockLocations() throws Exception {
        Path path= new Path("/hdfsapi/test/hello.txt");
        FileStatus fileStatus = fileSystem.getFileStatus(path);
        BlockLocation[] blocks = fileSystem.getFileBlockLocations(fileStatus, 0, fileStatus.getLen());

        for(BlockLocation block : blocks){
            for(String name : block.getNames()){
                System.out.println(name + "\t" + block.getOffset() + "\t" + block.getLength() + "\t" + block.getHosts());
            }
        }
    }
```

