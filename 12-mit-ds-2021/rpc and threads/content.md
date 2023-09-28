## Threads & RPC (golang)

选择 golang 的原因

1. 对 RPC 和 Threads 有非常好的支持
2. 有垃圾收集器
3. 类型安全的
4. 语言很简单，学起来容易
5. 可编译的，运行时开销小



## 线程的执行

在 golang 中的线程是 go routine 例程；

每一个线程都有 PC ；Stack ；Registers

 