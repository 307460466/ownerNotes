# CAS

<a name="PiaEQ"></a>
## 参考文档
[CAS底层原理与ABA问题](https://www.cnblogs.com/lzhdonald/p/13328780.html)<br />

<a name="c4GIM"></a>
## 定义
CAS（Compare And Swap）：无锁算法；CAS算法是乐观锁的一种实现。

- CAS包含三个参数：内存值V，预期值A，新值B
   - 当内存值V等于预期值A时，才会将内存值修改为新值B，返回true
   - 当不等于时，说明已被其他线程修改了，返回false
<a name="fdJFB"></a>
### 优点

- 线程安全
   - CAS是自旋锁算法，使用do-while（无锁）不断判断，保证一致性和并发性，但会损耗CPU资源
   - 原子性保证：Unsafe提供硬件级别的原子操作
   - 内存可见性和禁止指令重排序：通过对value使用volatile修饰，保证多线程下value值为同一份
<a name="56fir"></a>
### 缺点

- 循环时间长开销大
   - CAS判定变量被修改后，会继续尝试发起CAS，如多次尝试失败，会造成大量时间消耗和性能浪费
- 仅能保证一个共享变量的原子操作
   - 操作多个变量时，CAS无法保证操作的原子性（JDK5开始提供AtomicReference保证引用对象间的原子性，即多个变量放在一个对象进行CAS操作）
<a name="Bqa6J"></a>
### ABA问题

- 在获取初始预期值和当前内存值的时间间隔内，内存值由A变为B再变为A，此时对CAS来说，是无法感知的（解决方式：每次获取时加入版本号，使用AtomicStampedReference）



