## Golang调度器的背景，协程，线程区别
协程在用户空间，协程切换相比于线程，非常**轻量级**
## gmp模型和调度
m表示内核线程数量
g是goroutine
p用来调度goroutine，每个p包含一个本地队列，用来保存goroutine。p本身是有多个的（p列表），一个p对应一个m

### 被废弃的goroutine调度器
前面又说p有一个本地队列，早期没有p，就一个全局队列，全局队列优化后依然保留
### p和m的数量
$GOMAXPROCS控制，实际上是goroutinue的并发度
m的最大数量是10000
p对应一个m，如果m阻塞，会去创建新的m，p和m没有必然对应关系
### 调度优化
- work stealing机制，
  p在本地队列没有g时，m会取其他的p队列中偷取g运行
- hand off机制，
  g因为系统调用阻塞时，m会释放p，p会绑定到其他空闲线程继续执行
- 并行，
  $GOMAXPROCS并行度，同时占用CPU
- 抢占，
  goroutine最多占用CPU10秒
- 全局队列，
  work stealing无法偷取到g时，会从全局队列偷取g
### 生命周期
  m0主线程，负责初始化启动第一个g（g0）
  g0负责调度g
## go tool trace
## gmp调度全场景分析

https://learnku.com/articles/41728
