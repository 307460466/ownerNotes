# 多线程

<a name="4KY5e"></a>
### 1.参考文档
[并发编程网](http://ifeve.com/tag/semaphore/)<br />CountDownLatch：[掘金文档](https://juejin.im/post/5aeec3ebf265da0ba76fa327) | [源码分析](https://liuzhengyang.github.io/2017/05/22/countdownlatch/) | [简述文档](https://www.jianshu.com/p/128476015902)<br />Semaphore：[简书](https://www.jianshu.com/p/38630b7dbe73) | [CDSN](https://blog.csdn.net/eson_15/article/details/51577191)<br />volatile：[博客园](https://www.cnblogs.com/dolphin0520/p/3920373.html)
<a name="Lc1S0"></a>
### 2.CountDownLatch
java.util.concurrent.CountDownLatch<br />类似倒计时的线程工具类，基于AQS实现<br />场景：多线程协作完成业务功能时，需要等待其他多个线程完成任务后，主线程才能继续往下执行业务功能<br />该类在构造时需要传入整型数count，之后每次调用CountDownLatch的countDown()都会对count减一，当count减至0时，调用CountDownLatch.await()的线程才能继续执行

- 相关方法
  - await() throws InterruptedException：调用该方法的线程需等待构造方法传入的count减至0时，才可继续向下执行
  - await(long timeout, TimeUnit unit)：与await()功能一致，但有超时限制，超过指定时间后，不管count为多少，都会继续往下执行
  - countDown()：使CountDownLatch初始值count减一
  - long getCount()：获取当前CountDownLatch维护的count值
- 示例代码
```java
public class CountDownLatchTest {
    private static final Logger LOGGER = LoggerFactory.getLogger(CountDownLatchTest.class);
    /** 控制主线程等待子线程执行CountDownLatch的count减至0 */
    private static CountDownLatch endSign = new CountDownLatch(10);
    /** 控制主线程下的子线程等待主线程的通知 */
    private static CountDownLatch startSign = new COuntDownLatch(1);
    
	public static void main(String[] args) throws Exception{
        ExecutorService executorService = Executors.newFixedThreadPool(10);

        for (int i = 0; i < 10; i++) {
            executorService.execute(() -> {
                try {
                    System.out.println(Thread.currentThread().getName(), " await");
                    startSignal.await();
                    System.out.println(Thread.currentThread().getName(), " start");
                    System.out.println(Thread.currentThread().getName(), " end");
                } catch (InterruptedException ie) {
                    ie.printStackTrace();
                } finally {
                    endSignal.countDown();
                }
            });
        }

        System.out.println(Thread.currentThread().getName(), " start");
        startSignal.countDown();
        endSignal.await();
        System.out.println(Thread.currentThread().getName(), " end");
        executorService.shutdown();
    }
}
```
<a name="H8LGP"></a>
### 3.Semaphore
java.util.concurrent.Semaphore<br />信号量，用于控制访问特定资源的线程数目，用于流量控制，限制最大的并发访问数<br />本身不保证线程安全性

- 构造方法
  - Semaphore(int permits)
  - Semaphore(int permits, boolean fair)
    - permits：许可线程数量
    - fair：公平性，默认false，如设为true，下次执行的线程为等待最久的线程
- 方法
  - void acquire() throws InterruptedException：表示阻塞并获取许可
  - void release()：表示释放许可
  - int availablePermits()：获取当前未发放的许可数量
- 示例代码
```java
public class SemaphoreTest {
	public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(10);
        Semaphore semaphore = new Semaphore(2);
        Syste
        for (int i = 0; i < 10; i++) {
            executorService.execute(() -> {
                try {
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getName() + " acquire");
                    TimeUnit.SECONDS.sleep(1);
                    System.out.println(Thread.currentThread().getName() + " release");
                } catch (InterruptedException ie) {
                    ie.printStackTrace();
                } finally {
                    semaphore.release();
                }
            });
        }
        executorService.shutdown();
    }
}
```

