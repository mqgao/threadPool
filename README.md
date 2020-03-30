线程池学习总结

## 为什么要使用线程池
  线程池提供了一种限制和管理资源（包括执行一个任务）。每个线程池还维护一些基本统计信息，例如已完成任务的数量。池化技术的思想主要是为了减少每次获取资源的消耗，提高对资源的利用率。
这里借用《Java 并发编程的艺术》提到的来说一下使用线程池的好处：
1. 降低资源消耗。通过重复利用已创建的线程降低线程创建和销毁造成的消耗。
2. 提高响应速度。当任务到达时，任务可以不需要的等到线程创建就能立即执行。
3. 提高线程的可管理性。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控
## 线程池类图
 Executor接口 -> ExecutorService接口 -> AbstractExecutorService抽象类 -> ThreadPoolExecutor实现类
## 线程池初始化核心参数
 + int corePoolSize,  核心线程数
 + int maximumPoolSize,  最多线程数
 + long keepAliveTime, 大于core线程数的线程空闲时的回收时间
 + TimeUnit unit,  计时器
 + BlockingQueue<Runnable> workQueue,  要执行的任务队列
 + ThreadFactory threadFactory,  创建线程的工程
 + RejectedExecutionHandler handler  拒绝任务时的，选择的拒绝策略
 ## 线程池提交任务时的执行流程
 submit时，如果小于core线程数量，开启新的线程执行，如果大于core线程数量，则把任务放到队列中，如果队列满了，此时才会创建新的线程，如果新创建的线程数大于max线程数则执行拒绝策略，线程池尽量可能的少创建线程

