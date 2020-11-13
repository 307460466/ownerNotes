面试题目收集
面试题目1
#基础面试题 Java基础
实例方法和静态方法有什么不一样?
Java中的异常有哪几类?分别怎么使用?
常用的集合类有哪些?比如List如何排序?
ArrayList和LinkedList内部的实现大致是怎样的?他们之间的区别和各自适应的场景
是什么?
内存溢出是怎么回事?
ClassLoader有什么用?
==和equals的区别?
hashCode方法的作用?
Object类中有哪些方法?列举3个以上。
NIO是什么?适用于何种场景?
HashMap数据结构、扩展策略,Hash冲突攻击如何防范,如何实现线程安全的
HashMap?
JVM内存结构,GC算法,CMS、G1的原理
NIO模型,select/epoll的区别,多路复用的原理
Java中一个字符占多少个字节,扩展再问int, long, double占多少字节
创建一个类的实例都有哪些办法?
final/finally/finalize的区别?
LinkingBlockingQueue与ArrayBlockingQueue的区别,他们的适用场景?
Session/Cookine的区别?
String/StringBuffer/StringBuilder的区别,扩展再问他们的实现?
Servlet的生命周期?
如何用Java分配一段连续的1G的内存空间?需要注意些什么?
Java有自己的内存回收机制,但为什么还存在内存泄露的问题呢?
Java里面用对象作为Key需要注意些什么? 如何实现hashcode?
Java内存泄漏场景
1. 长生命周期对象持有短生命周期对象，如对静态的list大量调用add却没有remove
2. Hash值发生变化，无法被查找，如，静态的HashMap持有对象的hashKey发生了变化，那么这个对象基本就不可达了
3. 注册监听器，没有remove
4. 各种连接，没有显式的close
JVM
JVM堆的基本结构：新生代，老年代，永久带，Eden/Suvival
JVM的垃圾算法有哪几种? CMS收集算法的流程?
JVM有哪些常用启动参数可以调整?
如何查看JVM的内存使用情况?
Java程序是否会内存溢出?
你常用的JVM配置和调优参数都有哪些?分别什么作用? 7. Java内存分代模型,GC算法,JVM常见的启动参数;
CMS算法的过程,CMS回收过程中JVM是否需要暂停(这块回答较好,也可以只是 看毕玄的Java分布式开发或网上文章的学习, 可以结合JVM启动参数常见配置, jstat等命令,看下动手能力,意愿;以及实际线上问题排查)
什么情况下会出现OOM(堆内存,永久区,堆外区,方法栈)
Java内存结构(堆结构,新生代[S0/S1/Elden],年老代,持久代)
常用的GC策略,什么时候会触发YGC,什么时候触发FGC
数据结构与算法基础
说一下几种常见的排序算法和分别的复杂度。
什么是跳表?
如何确认一个链表有环? 进一步,确认环的位置。
如何遍历一棵二叉树?
倒排一个LinkedList。
HashSet的实现方式 ### 多线程/并发
Java中常见的锁,互斥锁,读写锁,信号量
原子Atomic类,如何保证原子性,CAS硬件指令
volatile,可见性问题的原因,硬件架构,L3 Cache,QPI,乐观锁
如何实现一个线程安全的数据结构 11. 如何避免死锁
如何解决ABA问题
Synchronized关键字的作用?
Volatile关键字的作用?
Java内存模型是怎样的?
线程
HashMap在多线程环境下使用需要注意什么?为什么?
Java程序中启动一个线程是用run()还是start()?
什么是守护线程?有什么用?
什么是死锁?如何避免
线程和进程的差别是什么?
Java里面的Threadlocal是怎样实现的?
ConcurrentHashMap的实现原理是?
sleep和wait区别
notify和notifyAll区别
volatile关键字的作用
ThreadLocal的作用与实现
两个线程如何串行执行
上下文切换是什么含义
可以运行时kill掉一个线程吗?
什么是条件锁、读写锁、自旋锁、可重入锁?
什么是协程(用户态线程,减少数据拷贝,降低CPU开销,无callback函数)?
线程池ThreadPoolExecutor的实现原理?
J.U.C下的常见类的使用。lock, synchronized, ThreadPool的深入考
察; BlockingQueue的使用。(take,poll的区别,put,offer的区别);原子类的
实现。
各种常见锁使用如果上面这些掌握很好,还可以看看更深一点的 False Sharing,
Cache Line,可见性与原子性等;
Linux使用与问题分析排查
硬链接和软链接的区别?
inode是什么?
Linux常用命令有哪些?
怎么看一个Java线程的资源耗用?
Load过高的可能性有哪些?
/etc/hosts文件什么做用?
/etc/resolv.conf文件什么作用?
如何快速的将一个文本中所有“abc”替换为“xyz”?
你常用的Linux下用来进行网络和磁盘IO分析的工具有哪些?
你常用的Linux下用来进行内存和CPU分析的工具有哪些?
发现磁盘空间不够,如何快速找出占用空间最大的文件?
Java服务端问题排查(OOM,CPU高,Load高,类冲突)
Java常用问题排查工具及用法
(top, iostat, vmstat, sar, tcpdump, jvisualvm, jmap, jconsole)
Thread dump文件如何分析(Runnable,锁,代码栈,操作系统线程ID关联)
grep,awk,sed; 是否自己写过shell脚本;
常见的cpu load过高,us过高,一般是什么问题。引申出是否用过top,jstat,jstack
等。
常见的内存问题一般有哪些。 引申出是否用过free,top, jmap等。
框架使用
Spring中Bean的生命周期。
SpringMVC或Struts处理请求的流程。
Spring AOP解决了什么问题?怎么实现的?aop与cglib,与asm的关系。
Spring IoC AOP自己用代码如何实现
Spring事务的传播属性是怎么回事?它会影响什么?
Spring中BeanFactory和FactoryBean有什么区别?
Spring框架中IOC的原理是什么?
spring的依赖注入有哪几种方式
用Spring如何实现一个切面?
Spring 如何实现数据库事务?
Hibernate和Ibatis这类ORM框架的区别?什么是ORM,解决的痛点是什么?
spriong ioc的生命周期,(init-method,intilizingbean接口方法afterPropertiesSet的
先后顺序)等。
Hibernate对一二级缓存的使用,Lazy-Load的理解;
RPC的负载均衡、服务发现怎么做的
几种推送模型的区别,long polling,websocket
bean生命周期
1，实例化（当我们的程序加载beans.xml文件），把我们的bean（前提是scope=singlton）实例化到内存
　　2，调用set方法设置属性
　　3，如果你实现了bean名字关注接口（BeanNameAware）则可以通过setBeanName获取id号
　　4，如果你实现了bean工厂关注接口（BeanFactoryAware）则可以通过setBeanFactory获取BeanFactory
　　5，如果你实现了ApplicationContextAware关注接口（ApplicationContextAware）则可以通过setApplicationContext获取ApplicationContext
　　6，如果bean和一个后置处理器关联(BeanPostProcessor),则会调用postProcessBeforeInitialization（Before）方法
　　7，如果你实现了InitializingBean关注接口（InitializingBean）则可以调用afterPropertiesSe
　　8，如果自定义了初始化方法则调用自定义的初始化方法（注自定义初始化方法在bean中通过init-method方法配置）
　　9，如果bean和一个后置处理器关联(BeanPostProcessor),则会调用postProcessAfterInitialization（After）方法
　  10，bean可以使用了
　  11，容器关闭
　  12，如果实现DisposableBean接口则可以调用其destory（）方法，也可以定制自定义的销毁方法（注自定义初始化方法在bean中通过init-method方法配置）
数据库相关
MySQL InnoDB的特点?
乐观锁和悲观锁的区别?
数据库隔离级别是什么?有什么作用?
MySQL主备同步的基本原理。
如何从一张表中查出name字段包含“XYZ”的所有行?
索引数据结构(字典+BitTree)
如何优化数据库性能(索引、分库分表、批量操作、分页算法、升级硬盘SSD、业务优化、主从部署)
SQL什么情况下不会使用索引(不包含,不等于,函数，like %%)
一般在什么字段上建索引(过滤数据最多的字段)
如何从一张表中查出name字段不包含“XYZ”的所有行?
MySQL,B+索引实现,行锁实现,SQL优化
Redis,RDB和AOF,如何做高可用、集群
如何解决高并发减库存问题
mysql存储引擎中索引的实现机制;
数据库事务的几种粒度;
行锁,表锁;乐观锁,悲观锁
网络协议和网络编程
TCP断开连接的过程。
浏览器发生302跳转背后的逻辑?
HTTP协议的交互流程。HTTP和HTTPS的差异,SSL的交互流程?
Rest和Http什么关系? 大家都说Rest很轻量,你对Rest风格如何理解? 6. TCP的滑动窗口协议有什么用?讲讲原理。
HTTP协议都有哪些方法?
交换机和路由器的区别?
什么是VLAN,有什么作用?
什么是VXLAN,有什么作用?
http协议(报文结构,断点续传,多线程下载,什么是长连接) 12. tcp协议(建连过程,慢启动,滑动窗口,七层模型)
webservice协议(wsdl/soap格式,与rest协议的区别)
spdy/http2.0协议是否有了解
NIO的好处,Netty线程模型,什么是零拷贝
REDIS
redis等缓存系统/中间件/NoSQL/一致性Hash等
列举一个常用的Redis客户端的并发模型。
HBase如何实现模糊查询?
列举一个常用的消息中间件,如果消息要保序如何实现?
如何实现一个Hashtable?你的设计如何考虑Hash冲突?如何优化? 5. 分布式缓存,一致性hash
LRU算法,slab分配,如何减少内存碎片
如何解决缓存单机热点问题
什么是布隆过滤器,其实现原理是? False positive指的是?
memcache与redis的区别
zookeeper有什么功能,选举算法如何进行
map/reduce过程,如何用map/reduce实现两个数据源的联合统计
设计模式与重构
你在设计一个工厂的包的时候会遵循哪些原则?
你能列举一个使用了Visitor/Decorator模式的开源项目/库吗?
你在编码时最常用的设计模式有哪些?在什么场景下用?
如何实现一个单例?
代理模式(动态代理)
单例模式(懒汉模式,恶汉模式,并发初始化如何解决,volatile与lock的使用) 7. JDK源码里面都有些什么让你印象深刻的设计模式使用,举例看看?
Reactor模式
学习与进取心
平时会关注哪些技术?
会看那些技术博客和网站?
技术上有没有偶像?
看过哪些技术书籍?
你平常都看些什么书?你去年和今年看的书中印象最深的基本技术书籍和非技术书
籍是?
(如果不看书)你平常都上哪些技术论坛?最喜欢哪个?为什么?
7. 项目或产品中用到了什么新技术或框架
8. 最近研究过什么业界流行的技术或框架
9. 对现在所做的项目或产品的缺陷是否了解,有何规划
10. 是否有带过项目,如何管理项目
11. 是否有带过团队,团队管理最大的挑战点是什么
抗压能力及抗压意愿
刚才你说的XXX实现跟那个开源的YYY很像,是不是抄来的? 2. 对加班怎么看?
平台是否有加班,是主动还是被动,是否非常抗拒
是否有负责多件事情,多件事情如何并行处理
你对你最近负责项目中最自豪的点是什么? 稳定性考察
了解家庭婚姻状况, 了解购房及居住地,籍贯情况,了解目前薪资,评估稳定性 2. 如果让你接手一个历史悠久的模块,你会怎么做?
看简历跳槽情况,针对性发问,如跳槽频繁的话问清楚为什么
开放性问题
一个大文件4G,里面一行行的数字,这时内存只有256M,如果做排序?
如果你部署的应用所在机器硬盘坏了,会发生什么?你的程序要如何处理这种异 常?(分布式系统中故障是一种常态,设计要避免单点故障,能容错,保证系统高
可用)
实现一个消息队列系统
如何设计一个高可用的架构
多次Hash来解决URL重复访问问题。
全局唯一ID问题。
秒杀如何设计。
如何进行性能优化。
发现CPU 100%,如何排查?
实现一个分布式打点系统。
taobao.com和tmall.com的互相登录的问题。
如何快速对一个2亿数据的List进行排序?
面试题目2
<3阶段
技术基础（JAVA、系统、Linux系统）
hashTable和hashMap的异同；concurrenthashmap与hashtable区别；conx1.7和1.8实现的最大区别；并发访问hashmap会有什么可能的结果；-
hashcode方法与equals有啥关系，能否引入随机机制；-
iterator 什么场景会抛ConcurrentModificationException异常；+
Collections和Collection有什么关系;-
描述下JVM内存模型；
描述下线程池的调度过程；
transient, volatile是什么含义；
threadlocal解决什么问题；-
string，intern，stringbuffer，stringbuilder区别；-
描述类的加载过程；+
描述线程的几种状态以及转换；-
线上实操能力（编程、运维、排错，找Bug）
OOM包含哪几种，碰到OOM怎么排查   （堆的OOM：jmap   jmap的时候需要注意一些什么细节，如果分析jmap内容 ）;+
如何查看一个系统的load;-
如何查看应用中线程的状态；-
mysql的存储引擎有哪些，区别是；+
如何查看系统的io情况；+
印象最深刻的一次内存泄漏情况；
io或者网络情况下如何做单元测试；+
出现toomanyconnections一般怎么解决；
请说明几种典型的字符集编码格式；
mysql增加一个字段大致的过程；
经验部分（系统能力、监控、容错、扩展性等）
乐观锁和悲观锁各自适合的场景;
用过那些序列化方式，异同是什么;
简单介绍几种常见的设计模式；
如何做到服务优雅上下线;
联合索引如何建立，有什么原则；
分布式锁都可以用哪些系统实现？分别对应什么场景；
如何定位慢sql；
描述下一个请求从浏览器到服务端的全部过程；
什么是sql注入；
http和https区别；
设计一个洗牌的程序，尽量均匀，为什么；
3<5阶段
技术基础（JAVA、系统、Linux系统）
java包冲突都有哪些解决办法；
锁的重入性；乐观/悲观锁区别；公平调度、优先级调度的场景；
spring mvc运作方式；
spring aop实现原理，动态代理有哪些方式，有什么区别；
select，poll，epoll有啥区别；
简述cms或者g1的垃圾回收过程;
简单叙述java里都有哪些引用类型；
深拷贝与浅考虑；copyonwrite介绍下；
java怎么设置进程为守护进程；
hashcode与性能的关系；
线上实操能力（编程、运维、排错，找Bug）
分库分表的案例分析；如何从单库单表最小线上的迁移到分库表；
load很高但cpu不高一般什么情况；
经验部分（系统能力、监控、容错、扩展性等）
分布式session的实现方案，怎么解决跨域  答案：很多，看思路，session同步，Redis等，跨子域，跨大域；
实现一个远程rpc框架，最小MVP是那些；
nio为什么效率高，bio的问题出在哪里，和aio有什么关系， 非阻塞是否是异步；
怎么防止死循环，写一个工具去发现执行中的死循环;
幂等设计
4层负载与7层的区别；tcp的三次我手过程；
time_wait和close_wait什么原因；
请列举缓存击穿的可能场景和解决办法；雪崩如何防止；
如果业务层已经做了数据的容错，如何结合tcp和udp各自优点来做协议优化；
为什么连续内存的操作效率更高；
mysql在执行sql的主要过程有哪些；
数据倾斜问题如何解决；
mysql的事务级别有哪些；
行与列存储的优缺点分析；
如何做业务和系统监控；
如何拆分公布式事务，BASE的原理；
5<阶段
技术基础（JAVA、系统、Linux系统）
lock-free的数据结构介绍；
协程的优势是什么；
java里直接分配堆外内存的途径；
如何最大限度的避免GC；
new, malloc, mmap关系；
请描述下读写锁升级／降级的场景；
正则表达式的贪婪和非贪婪模式；
线上实操能力（编程、运维、排错，找Bug）
经验部分（系统能力、监控、容错、扩展性等）
什么是numa，如何利用numa来优化性能；
cpu cacheline，如何优化；
oauth1.0和2.0区别
数据令牌是如何工作的；
红包系统如何实现；
如何拆分公布式事务，BASE的原理；
系统脑裂的案例列举；
multipaxos简单介绍；
系统什么情况用推，什么情况用拉；
如何在不停服务情况下，设计一个数据迁移流程；
面试题目3
一、 基本的数据类型&数据结构知识
1.0  String,StringBuffer与StringBuilder的区别：https://blog.csdn.net/weixin_41101173/article/details/79677982
1、String的值是不可变的，这就导致每次对String的操作都会生成新的String对象，效率低下；如何避免呢？
2、谷歌引入了两个新的类——StringBuffer类和StringBuild类来对此种变化字符串进行处理
3、StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象
4、StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。
5、由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。
1.1  hashMap 底层是怎么实现的？ 允许null key吗？ 为啥数组长度一定得是2的幂次方？
http://www.cnblogs.com/chengxiao/p/6059914.html#t3
hashMap 和 hashTable 的区别： https://blog.csdn.net/qq_39137554/article/details/75040096
1.2  ArrayList与LinkedList 的比较：
ArrayList是基于数组的实现，LinkedList是基于带头结点的双向循环链表的实现；
ArrayList支持随机访问，LinkedList不支持；
LinkedList可作队列和栈使用，实现了Dequeue接口，而ArrayList没有；
ArrayList 寻址效率较高，插入/删除效率较低；LinkedList插入/删除效率较高，寻址效率较低
1.ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。 （LinkedList是双向链表，有next也有previous）
2.对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。
3.对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。
二、 JVM 相关知识
2.0 Java 类加载原理: https://www.cnblogs.com/yixianyixian/p/8145506.html
我们首先看一下JVM预定义的三种类型类加载器，当一个 JVM启动的时候，Java缺省开始使用如下三种类型类装入器：
启动（Bootstrap）类加载器：引导类装入器是用本地代码实现的类装入器，它负责将<Java_Runtime_Home>/lib下面的核心类库或-Xbootclasspath选项指定的jar包加载到内存中。由于引导类加载器涉及到虚拟机本地实现细节，开发者无法直接获取到启动类加载器的引用，所以不允许直接通过引用进行操作.
扩展（Extension）类加载器：扩展类加载器是由Sun的ExtClassLoader（sun.misc.LauncherAppClassLoader）实现的。它负责将系统类路径java -classpath或-Djava.class.path变量所指的目录下的类库加载到内存中。开发者可以直接使用系统类加载器。
　　 除了以上列举的三种类加载器，还有一种比较特殊的类型就是线程上下文类加载器，这个将在后面单独介绍。
2.1 简单介绍一下JVM 内存模型 ： https://www.jianshu.com/p/a60d6ef0771b
2.2 ThreadLocal 怎么实现的？底层数据结构是啥？ 有没有内存泄漏问题？为啥？
http://www.importnew.com/22039.html
ThreadLocal的实现是这样的：每个Thread 维护一个 ThreadLocalMap 映射表，这个映射表的 key 是 ThreadLocal实例本身，value 是真正需要存储的 Object。
也就是说 ThreadLocal 本身并不存储值，它只是作为一个 key 来让线程从 ThreadLocalMap 获取 value。值得注意的是图中的虚线，表示 ThreadLocalMap 是使用 ThreadLocal 的弱引用作为 Key 的，弱引用的对象在 GC 时会被回收。
2.3 sleep() 和 wait() 有什么区别?
1、sleep是线程类（Thread）的方法，导致此线程暂停执行指定时间，给执行机会给其他线程，但是监控状态依然保持，到时后会自动恢复。调用sleep不会释放对象锁。
2、wait是Object类的方法，对此对象调用wait方法导致本线程放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象发出notify方法（或notifyAll）后本线程才进入对象锁定池准备获得对象锁进入运行状态。
三、 数据库相关
3.1 一条sql执行过长的时间，你如何优化，从哪些方面？
答：1、查看sql是否涉及多表的联表或者子查询，如果有，看是否能进行业务拆分，相关字段冗余或者合并成临时表（业务和算法的优化）
2、涉及链表的查询，是否能进行分表查询，单表查询之后的结果进行字段整合
3、如果以上两种都不能操作，非要链表查询，那么考虑对相对应的查询条件做索引。加快查询速度
4、针对数量大的表进行历史表分离（如交易流水表）
5、数据库主从分离，读写分离，降低读写针对同一表同时的压力，至于主从同步，mysql有自带的binlog实现 主从同步
6、explain分析sql语句，查看执行计划，分析索引是否用上，分析扫描行数等等
7、查看mysql执行日志，看看是否有其他方面的问题
个人理解：从根本上来说，查询慢是占用mysql内存比较多，那么可以从这方面去酌手考虑
四、 平常常用的设计模式说1~2个
单例模式；工厂模式；
五、 说说 SpringMVC 工作原理
1、客户端请求提交到DispatcherServlet
2、由DispatcherServlet控制器查询一个或多个HandlerMapping，找到处理请求的Controller
3、DispatcherServlet将请求提交到Controller
4、Controller调用业务逻辑处理后，返回ModelAndView
5、DispatcherServlet查询一个或多个ViewResoler视图解析器，找到ModelAndView指定的视图
6、视图负责将结果显示到客户端
六、Redis 底层实现原理，数据结构和相关算法: https://blog.csdn.net/wcf373722432/article/details/78678504
七、Storm 源码看过吗？ 说说大致架构和系统原理吧
八、hadoop 源码看过吗？ hdfs & MapReduce , 说一说MapReduce的原理及执行过程吧：https://www.cnblogs.com/ahu-lichang/p/6645074.html
1、Map任务处理
　　1.1 读取HDFS中的文件。每一行解析成一个<k,v>。每一个键值对调用一次map函数。                <0,hello you>   <10,hello me>
　　1.2 覆盖map()，接收1.1产生的<k,v>，进行处理，转换为新的<k,v>输出。　　　　　　　　　　<hello,1> <you,1> <hello,1> <me,1>
　　1.3 对1.2输出的<k,v>进行分区。默认分为一个区。详见《Partitioner》
　　1.4 对不同分区中的数据进行排序（按照k）、分组。分组指的是相同key的value放到一个集合中。　排序后：<hello,1> <hello,1> <me,1> <you,1>  分组后：<hello,{1,1}><me,{1}><you,{1}>
　　1.5 （可选）对分组后的数据进行归约。详见《Combiner》
2、Reduce任务处理
　　2.1 多个map任务的输出，按照不同的分区，通过网络copy到不同的reduce节点上。（shuffle）详见《shuffle过程分析》
　　2.2 对多个map的输出进行合并、排序。覆盖reduce函数，接收的是分组后的数据，实现自己的业务逻辑，　<hello,2> <me,1> <you,1> 处理后，产生新的<k,v>输出。
　　2.3 对reduce输出的<k,v>写到HDFS中。
九、编程题：多线程相关，主子线程之间通信：https://zhidao.baidu.com/question/755640218254546924.html
场景是这样的，主线程里面创建了两个相同的thread，分别命名为A和B吧。
想实现的目的是，主线程可能在等待10秒钟，让子线程A和B去分别完成相同的任务，有可能由于某个原因，A和B执行所需的时间会不同，但是我想他们两者其中一个完成之后就马上唤醒主线程(如果是A先完成了，那么主线程就不等待B)，然后主线程继续去执行其他任务。如果过去10秒钟，A和B都没完成任务，那么主线程就唤醒，继续完成其他的任务。
面试题目4
java基础
Arrays.sort实现原理和Collection实现原理
foreach和while的区别(编译之后)
线程池的种类，区别和使用场景
分析线程池的实现原理和线程的调度过程
线程池如何调优
线程池的最大线程数目根据什么确定
动态代理的几种方式
HashMap的并发问题
了解LinkedHashMap的应用吗
反射的原理，反射创建类实例的三种方式是什么？
cloneable接口实现原理，浅拷贝or深拷贝
Java NIO使用
hashtable和hashmap的区别及实现原理，hashmap会问到数组索引，hash碰撞怎么解决
arraylist和linkedlist区别及实现原理
反射中，Class.forName和ClassLoader区别
String，Stringbuffer，StringBuilder的区别？
有没有可能2个不相等的对象有相同的hashcode
简述NIO的最佳实践，比如netty，mina
TreeMap的实现原理
JVM相关
类的实例化顺序，比如父类静态数据，构造函数，字段，子类静态数据，构造函数，字段，他们的执行顺序
JVM内存分代
Java 8的内存分代改进
JVM垃圾回收机制，何时触发MinorGC等操作
jvm中一次完整的GC流程（从ygc到fgc）是怎样的，重点讲讲对象如何晋升到老年代，几种主要的jvm参数等
你知道哪几种垃圾收集器，各自的优缺点，重点讲下cms，g1
新生代和老生代的内存回收策略
Eden和Survivor的比例分配等
深入分析了Classloader，双亲委派机制
JVM的编译优化
对Java内存模型的理解，以及其在并发中的应用
指令重排序，内存栅栏等
OOM错误，stackoverflow错误，permgen space错误
JVM常用参数
tomcat结构，类加载器流程
volatile的语义，它修饰的变量一定线程安全吗
g1和cms区别,吞吐量优先和响应优先的垃圾收集器选择
说一说你对环境变量classpath的理解？如果一个类不在classpath下，为什么会抛出ClassNotFoundException异常，如果在不改变这个类路径的前期下，怎样才能正确加载这个类？
说一下强引用、软引用、弱引用、虚引用以及他们之间和gc的关系
JUC/并发相关
ThreadLocal用过么，原理是什么，用的时候要注意什么
Synchronized和Lock的区别
synchronized 的原理，什么是自旋锁，偏向锁，轻量级锁，什么叫可重入锁，什么叫公平锁和非公平锁
concurrenthashmap具体实现及其原理，jdk8下的改版
用过哪些原子类，他们的参数以及原理是什么
cas是什么，他会产生什么问题（ABA问题的解决，如加入修改次数、版本号）
如果让你实现一个并发安全的链表，你会怎么做
简述ConcurrentLinkedQueue和LinkedBlockingQueue的用处和不同之处
简述AQS的实现原理
countdowlatch和cyclicbarrier的用法，以及相互之间的差别?
concurrent包中使用过哪些类？分别说说使用在什么场景？为什么要使用？
LockSupport工具
Condition接口及其实现原理
Fork/Join框架的理解
jdk8的parallelStream的理解
分段锁的原理,锁力度减小的思考
Spring
Spring AOP与IOC的实现原理
Spring的beanFactory和factoryBean的区别
为什么CGlib方式可以对接口实现代理？
RMI与代理模式
Spring的事务隔离级别，实现原理
对Spring的理解，非单例注入的原理？它的生命周期？循环注入的原理，aop的实现原理，说说aop中的几个术语，它们是怎么相互工作的？
Mybatis的底层实现原理
MVC框架原理，他们都是怎么做url路由的
spring boot特性，优势，适用场景等
quartz和timer对比
spring的controller是单例还是多例，怎么保证并发的安全
分布式相关
Dubbo的底层实现原理和机制
描述一个服务从发布到被消费的详细过程
分布式系统怎么做服务治理
接口的幂等性的概念
消息中间件如何解决消息丢失问题
Dubbo的服务请求失败怎么处理
重连机制会不会造成错误
对分布式事务的理解
如何实现负载均衡，有哪些算法可以实现？
Zookeeper的用途，选举的原理是什么？
数据的垂直拆分水平拆分。
zookeeper原理和适用场景
zookeeper watch机制
redis/zk节点宕机如何处理
分布式集群下如何做到唯一序列号
如何做一个分布式锁
用过哪些MQ，怎么用的，和其他mq比较有什么优缺点，MQ的连接是线程安全的吗
MQ系统的数据如何保证不丢失
列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题。
算法&数据结构&设计模式
海量url去重类问题（布隆过滤器）
数组和链表数据结构描述，各自的时间复杂度
二叉树遍历
快速排序
BTree相关的操作
在工作中遇到过哪些设计模式，是如何应用的
hash算法的有哪几种，优缺点，使用场景
什么是一致性hash
paxos算法
在装饰器模式和代理模式之间，你如何抉择，请结合自身实际情况聊聊
代码重构的步骤和原因，如果理解重构到模式？
数据库
MySQL InnoDB存储的文件结构
索引树是如何维护的？
数据库自增主键可能的问题
MySQL的几种优化
mysql索引为什么使用B+树
数据库锁表的相关处理
索引失效场景
高并发下如何做到安全的修改同一行数据，乐观锁和悲观锁是什么，INNODB的行级锁有哪2种，解释其含义
数据库会死锁吗，举一个死锁的例子，mysql怎么解决死锁
Redis&缓存相关
Redis的并发竞争问题如何解决了解Redis事务的CAS操作吗
缓存机器增删如何对系统影响最小，一致性哈希的实现
Redis持久化的几种方式，优缺点是什么，怎么实现的
Redis的缓存失效策略
缓存穿透的解决办法
redis集群，高可用，原理
mySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据
用Redis和任意语言实现一段恶意登录保护的代码，限制1小时内每用户Id最多只能登录5次
redis的数据淘汰策略
redis的集群架构，主从复制模型、哈希槽与一致性hash
网络相关
http1.0和http1.1有什么区别
TCP/IP协议
TCP三次握手和四次挥手的流程，为什么断开连接要4次,如果握手只有两次，会出现什么
TIME_WAIT和CLOSE_WAIT的区别
说说你知道的几种HTTP响应码
当你用浏览器打开一个链接的时候，计算机做了哪些工作步骤
TCP/IP如何保证可靠性，数据包有哪些数据组成
长连接与短连接
Http请求get和post的区别以及数据包格式
简述tcp建立连接3次握手，和断开连接4次握手的过程；关闭连接时，出现TIMEWAIT过多是由什么原因引起，是出现在主动断开方还是被动断开方。
其他
maven解决依赖冲突,快照版和发行版的区别
Linux下IO模型有几种，各自的含义是什么
实际场景问题，海量登录日志如何排序和处理SQL操作，主要是索引和聚合函数的应用
实际场景问题解决，典型的TOP K问题
线上bug处理流程
如何从线上日志发现问题
linux利用哪些命令，查找哪里出了问题（例如io密集任务，cpu过度）
场景问题，有一个第三方接口，有很多个线程去调用获取数据，现在规定每秒钟最多有10个线程同时调用它，如何做到。
用三个线程按顺序循环打印abc三个字母，比如abcabcabc。
常见的缓存策略有哪些，你们项目中用到了什么缓存系统，如何设计的
设计一个秒杀系统，30分钟没付款就自动关闭交易（并发会很高）
请列出你所了解的性能测试工具
后台系统怎么防止请求重复提交？
有多个相同的接口，我想客户端同时请求，然后只需要在第一个请求返回结果的时候返回给客户端
面试题目5
田永乾	7. equals及hashcode作用、联系		java	1
张旭	java中的map知识	hashmap、hashtable区别。Thread-safe的hashmap有哪些。Concurrent hashmap原理。	java	2
田永乾	3. ThreadLocal使用场景及实现原理		java	2
王涛	"Integer和int的区别，以下代码的输出并解释原因：
Integer i1 = new Integer(1000);
Integer i2 = new Integer(1000);
int i3 = 1000;
System.out.println(i1 == i2);
System.out.println(i1 == i3);
System.out.println(i3 == i1);"	"false
true
true
了解包装类和基础数据类型的判断，以及拆箱机制。
"	Java	2
王涛	"Java类初始化过程，给出以下程序的输出结果
class A
{
public A(String s)
{
System.out.println(s+"" Constructor A"");
}
}
class B
{
public B(String s)
{
System.out.println(s+ "" Constructor B"");
}
}
class C
{
public C(String s)
{
System.out.println(s+ "" Constructor C"");
}
}
class Base
{
static A a1 = new A(""a1: static"");
A a2 = new A(""a2: normal"");
public Base()
{
A a3 = new A(""a3: normal"");
System.out.println(""Constructor Base"");
}
}
class Derived extends Base
{
static B b1 = new B(""b1: static"");
B b2 = new B(""b2: normal"");
public Derived()
{
B b3 = new B(""b3: normal"");
System.out.println(""Constructor Derived"");
}
}
public class Test {
static C c1 = new C(""c1: static"");
C c2 = new C(""c2: normal"");
public static void main(String[] args) {
C c3 = new C(""c3: normal"");
Derived derived = new Derived();
System.out.println(""end"");
}
} "	"1c1: static Constructor C
c3: normal Constructor C
a1: static Constructor A
b1: static Constructor B
a2: normal Constructor A
a3: normal Constructor A
Constructor Base
b2: normal Constructor B
b3: normal Constructor B
Constructor Derived
end
先加载类（父类到子类），再初始化对象（父类到子类）。"	Java	2
鲁晨光	q: 能否自己写一个类，也叫java.lang.String？	a: 可以写，但是不会被类加载器加载，期望答出双亲委派加载机制：AppClassLoader->ExtClassLoader->BootStrap	java	2
孙龙海	在关闭资源方面，java有一个try-with-resource，能讲讲什么是try-with-resource 吗？以及 int a = 1000_000_000; 这条语句是否合法？	"预期：候选人是否对技术感兴趣，跟踪jdk中的新feature
解法：https://www.cnblogs.com/itZhy/p/7636615.html，http://www.importnew.com/12998.html"	java	2
沈宗强	"String s1 = “ab1”;
String s2 = “ab” + 1;
s1 == s2; true
String s3 = “ab”;
String s4 = s3 + 1;
s1 == s4; false
final String s5 = “ab”;
String s6 = s5 + 1; true
s6 == s1; intern() 完善。。。讨论点"		java	2
付冠生	打印某一个路径下的所有文件名长度超过3个字符的文件名称，并写入固定文件中	预期了解基本文件操作api，递归/非递归的掌握	java	3
王宇	"short s=5;
s=s+2; s+=2 ok的。符号位扩展。
这段代码是否可以编译通过"	考察对java自动向上转型问题的了解	java	3
王宇	"哪些情况下会造成OOM,能否通过简单的代码，模拟各类OOM
什么情况下会引发FULL GC"	考察对JVM内存模型及垃圾回收机制的了解	java	3
王宇	"以下这段程序，是否可以在str被赋值为任何中文的情况，都获得期望的输出
String str = ""XXXXX"";
byte[] bytes1 = str.getBytes(""UTF-8"");
str = new String(bytes1, ""GBK"");
byte[] bytes2 = str.getBytes(""GBK"");
System.out.println(new String(bytes2, ""UTF-8""));"	考察对基本字符集的了解	java	3
蔡超	hashmap 存入一个Integer类型的10，查询时使用Long类型的10，能否查出来，为什么？		java	3
鲁晨光	q: void apply(List a)和 void apply(List b)是否能实现重载？	a: 不能，期望回答出泛型编译时会进行类型擦除：https://www.cnblogs.com/drizzlewithwind/p/6101081.html	java	3
董子鹏	String的最大长度是多少（字符）？	"考察String的底层存储以及特殊的赋值方式。同时可以考察int的表示值范围。
如果new的方式的话，底层是char[],能够容纳的最大长度就是Int的最大值。
以常量的方式复制的时候，受java class格式的限制，只能存储到2^16-1"	java	3
徐振伟	图示如何产生死锁，能否将图示转成Java示例代码，如果出现了死锁可以借助哪些java工具定位	"public class DeadLockSample extends Thread {
private String lock1;
private String lock2;
public DeadLockSample(String name, String lock1, String lock2) {
super(name);
this.lock1 = lock1;
this.lock2 = lock2;
}
@Override  
public void run() {
synchronized (lock1) {
System.out.println(this.getName() + "" obtained: "" + lock1);
try {
Thread.sleep(1000);
synchronized (lock2) {
System.out.println(this.getName() + "" obtained: "" + lock2);
}
} catch (InterruptedException e) {
}
}
}
public static void main(String[] args) throws InterruptedException {
String lock1 = ""lock1"";
String lock2 = ""lock2"";
DeadLockSample t1 = new DeadLockSample(""Thread1"", lock1, lock2);
DeadLockSample t2 = new DeadLockSample(""Thread2"", lock2, lock1);
t1.start();
t2.start();
t1.join();
t2.join();
}
}
可以用jstack来查看死锁，
jps -v | grep xxx #获取对应JVM的进程号
jstack -l pid | grep BLOCK
"	java	3
沈宗强	ConcurrentHashMap原理 get/put/size加锁		java	4
徐振伟	java是解释型的编程语言，这个说法正确吗？如何理解“Write Once, Run Anywhere”这句话？	"答：
1.Java源代码经过Javac编译成.class文件，class文件中保存的是字节码，而不是操作系统可执行的机器码
2.常用JVM中的JIT编译器，能够在运行时将热点代码编译成机器码，从而做到编译执行
我们大学学习的C语言，在编写程序时要考虑操作系统的因素，操作系统不同，相应的系统API也有不同。相应代码中要引入各类宏定义，编译脚本也要分不同平台开发多个版本，最终通过编译器生成机器指令。
所以说Java通过引入了JVM这个中间层，来实现了“Write Once, Run Anywhere”
"	java	4
杨化伟	实现一个java中java.util.Timer	"调度：堆/时间轮
精度：线程通信机制实现调度线程唤醒"	java	5
杨化伟	"内存区域分布理解
class Test{
static Integer a ;
static int b;
Integer c;
int d;
}
public static void main(String args[]){
Test test =new Test();
}"	至于明确能说出潜在的优化方式堆中对象栈上分配，加分项	java	4
汪雄杰	在一个线程中throw了一个runtimeException会发生什么？	异常抛出的知识	java	3
汪雄杰	参数传递一个Integer，在函数中修改这个值是否影响调用函数中的值？	java的值传递和引用值传递	java	2
汪雄杰	java中子类是否可以重写父类的private方法？父类中调用子类中被重写过的方法，是静态绑定还是动态绑定？重新描述。Invoke。	java的面向对象知识	java	
Question Designer	Questions	Description	Problem Area	Rating 1->5(最难)
徐振伟	给定一个目录，该目录下某种类型的文件（如png）散落在各个子目录中，如何计算这些png文件的总大小？不限使用的命令，不要求完全正确	"答：一般作为最后一题，如果时间还有一些会考察一下shell。
比较好的答案
find . -name ""*.sh"" | xargs ls -l | awk 'BEGIN{total=0}{total+=$5}END{printf(""%.2fkb\n"", total/1024)}';
find . -name ""*.sh"" -exec ls -l {} ; | awk 'BEGIN{total=0}{total+=$5}END{printf(""%.2fkb\n"", total/1024)}';
#!/bin/bash
total=0
for file in find . -name ""*.sh""; do
size=du -s $file | awk '{print $1}'
echo ((size))
done
echo $total
"	shell	
唐新军	spring申明式事务实现原理是什么？	动态代理、PlatformTransactionManager设计逻辑	spring	3
唐新军	spring aop的实现原理是什么？	jdk动态代理、cglib两种方式的区别及原理	spring	3
杨化伟	spring事务管理器实现原理，如何实现嵌套事务？	aop、通过savepoint机制实现嵌套事务	spring	4
张旭	设计一个短网址服务		system design	3
唐新军	如何设计一个rpc框架	远程调用实现方式、通信协议、服务路由等	system design	4
蔡超	api调用如何控制调用频率  单机版、分布式		system design	4
杨化伟	count数服务设计	"        要求：支撑qps能力1w+，count结果分布[0,1kw]，亿级count key，数据生效秒级延迟
考察点：冗余数据一致性
思路：
数据的支撑能力有限，需要做count缓存，基于redis秒级失效key的方案反查数据库的控制不住qps
1、binlog消费等最终一致性数据流出机制
2、count存储事务方面至少支持单行事务+cas机制，（db、hbase）保证幂等消费
3、实现参照融汇"	system design	4
杨剑飞	如何设计一个消息队列		system design	5
杨剑飞	Java中的ConcurrentHashMap的存储模型，如果计算size	jdk7和8在存储模型上有所不同，取size的方式也不同	多线程&并发	3
杨剑飞	Java中synchronized和volatile的区别	两者的区别，以及造成volatile语义的原因，进而可以考察JMM	多线程&并发	2
田永乾	1. 线程池工作的基本原理以及注事事项		多线程&并发	2
田永乾	5. volatile使用场景、解决问题及实现原理		多线程&并发	2
杨剑飞	有一个长度为N的队列中存放了一些数字，如何在8核的机器上用Java快速求出这些数字之和	"考察多线程使用上。考点如下：
1、使用多线程来分段求和，启动线程数是否合理(与核数的关系)。
2、Java线程池的用法。
3、如何等各个线程运行完之后拿到结果。
4、进一步可以考察一下fork-join模型"	多线程&并发	3
田永乾	6. sleep、wait区别		多线程&并发	3
付冠生	启动两个线程分别交替打印A,B	线程1打印A，线程2打印B，交替输出，类似ABABABAB	多线程&并发	3
王宇	一个完整的线程池应该具备哪些要素	考察对线程池机制的了解及框架设计能力	多线程&并发	3
蔡超	java 内存模型，happens-before，volatile、synchronized作用  内存可见，重排序		多线程&并发	3
孙龙海	在资源竞争中，有公平锁和非公平锁，java在并发包中，一般默认会使用哪种锁，为什么？	"预期：候选人是否对并发和资源竞争有比较深入的了解和研究
https://blog.csdn.net/zmx729618/article/details/51593666"	多线程&并发	3
杨剑飞	给一个4核的机器上设计一个计数器，怎么设计高效一些？	计数器是个写多读少的场景，多核机器上可以设置分段计数器充分利用核数，只有在取实际加和的时候才需要锁全局	多线程&并发	4
张红强	写一个生产者与消费者的样例代码？不能用java并发集合		多线程&并发	4
董国双	什么是线程池？为什么使用线程池？如何做线程池监控、隔离等？线程池如何调优及利特尔法则？	"描述&解法：
主要考察多线程及线程池相关知识。
参考资料：
https://juejin.im/post/5b5e5fa96fb9a04fb900e1ce
https://segmentfault.com/a/1190000000685637"	多线程&并发	4
付冠生	多线程并发计算100亿内的素数个数	线程池的使用，并发的使用	多线程&并发	4
汪雄杰	start一个thread的时候，会新申请哪些资源	线程资源的知识	多线程&并发	2
张红强	byte取值范围?byte最大值+1赋值给byte是多少？为什么?		基础知识	2
蔡超	计算机原码、反码、补码转化规则，计算时使用的是哪种？为什么要使用这种？		基础知识	2
董子鹏	float和long谁表示的最大值更大？	考察基本数据类型的表示范围，以及浮点数的表示方法。	基础知识	3
杨化伟	java int占用字节数？Bit数？表示的整数范围？什么是字节序？如何选定序列化字节序实现正整数升序和字典序一致(场景hbase rowkey设计)？	int基础知识，大端，高位字节在低地址位	基础知识	3
董子鹏	编写一个单例模式的类	考察单例的多种写法：饿汉式、懒汉式、双重校验锁、枚举式、登记式。	设计模式	2
张红强	设计模式在生产中有哪些应用？如何理解所用的设计模式？		设计模式	3
董国双	Java领域常见的设计模式有哪些？Java8有哪些新特性？支持函数式编程之后对常见设计模式产生了什么影响？	"描述&解法：
考察常见设计模式，及Java8编程新特性，以及结合函数式编程对设计模式的理解。
参考资料：
https://github.com/jpsoroulas/java8-patterns
https://github.com/iluwatar/java-design-patterns"	设计模式	3
董国双	什么是架构模式？常用的架构模式的概念、用法及其优缺点？	"描述&解法：
主要考察常用的分层模式、客服端/服务器模式、主/从模式等常用架构模式。
参考资料：
https://towardsdatascience.com/10-common-software-architectural-patterns-in-a-nutshell-a0b47a1e9013
"	架构模式	4
张旭	mysql 数据引擎有哪些？有哪些不同		数据库	2
张旭	mysql为什么使用b+树做索引？		数据库	2
田永乾	4. mysql事务隔离级别		数据库	2
王涛	MySQL的存储引擎有哪些，Innodb的默认事务隔离级别是什么，事务隔离级别有哪些，阐述一下每个的含义。		数据库	2
沈宗强	mysql  update test set name = '123' where id = 1;  加锁情况	"期待：补充存储引擎，隔离级别，id的索引情况
然后分情况解答"	数据库	2
王宇	"name course score
张三 数学 70
张三 语文 58
张三 英语 90
李四 数学 80
李四 语文 82
1. 找出平均成绩大于60分的学生
2. 找出所有成绩都大于80分的学生
3. 找出数学成绩比语文成绩高的学生"	sql基础考察	数据库	2
沈宗强	mysql死锁案例分析，解决方案		数据库	3
鲁晨光	"mysql innodb引擎对于下面的两个sql如何加锁？
SQL1：select * from t1 where id = 10;
SQL2：delete from t1 where id = 10;"	"期望分多钟情况来回答，id是否主键，是否有索引，索引是否唯一索引，事务隔离级别是什么，最后如何执行还要看执行计划
http://hedengcheng.com/?p=771"	数据库	3
孙龙海	请描述一下多版本并发控制：MVCC	"预期：了解候选人对于数据库方面事务以及并发方面的认识
解法：https://blog.csdn.net/aoxida/article/details/50689619"	数据库	3
杨化伟	"ssd相对于机械盘，在随机写、顺序写、随机读、顺序读这些场景吞吐能力有何变化？
lsm类存储引擎在ssd上是否还有价值？"	"iops能力整体提升
随机写需要面临gc带来的背景流量，考虑数据分布，一般来说比不上顺序写
顺序写仍然快
随机读和顺序读在没有预读的场景区别不大，极限读吞吐能力一致。
lsm相对于b+树类存储引擎仍有顺序写的优势"	数据库	4
徐振伟	"讲一下mysql的索引原理。如下建表语句的两个索引，在哪些情况下会命中，为什么？
CREATE TABLE daily_charge (
userid int not null,
date   DATE,
charge int not null default 0,
key idx_userid (userid),
key idx_userid_date (userid, date)
) ENGINE=INNODB DEFAULT CHARSET=utf8;
"	"答：索引原理候选人在描述时，可以在纸上画一画，重在理解，而非死记硬背。
SELECT * from daily_charge WHERE userid = 1;
这种查询会命中索引idx_userid，原因：idx_userid和idx_userid_date两个索引都是辅助索引，叶子节点并不包含行记录的全部数据，只包含该键对应的值，以及该行数据的聚集索引键。Mysql在查询时会首先加载索引页到INNODB缓冲区，因为idx_userid仅包含单个键值，所以一个索引页包含的记录更多。
SELECT * from daily_charge WHERE userid = 1 and date = '2018-01-01';会命中idx_userid_date
EXPLAIN SELECT * from daily_charge WHERE userid = 3 order by date; 会命中idx_userid_date，因为idx_userid_date这个联合索引中，date字段已经排好序了，利用该联合索引可以避免再对date字段做一次额外的排序操作。
"	数据库	4
张旭	一个数组找相加和等于k的两个数字	https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#two-sum	算法	1
王宇	设计一个简单的扑克牌洗牌程序	最基本的算法考察	算法	1
张旭	一个数组把0都挪到后面去	https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#move-zeros	算法	2
张旭	检查是否是回文字符串	"https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#validpalindrome
扩展到难度3分。https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#valid-palindrome-ii"	算法	2
张旭	反转字符串	"期待多种解法
https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#reverse-string"	算法	2
王涛	两个升序整型数组的合并输出	归并排序，每个有序数组置个游标，比较两个游标的值，小的输出，并右移游标，直至一个到头，注意需要处理游标到头后，另一个数组剩余值的输出。	算法	2
王涛	多叉树的宽度优先搜索BFS	"1.用队列（先进先出）保存遍历路径。
2.搜索顺序：对节点A，先访问节点的左节点（第一个孩子节点），从该左节点开始一直向右遍历直到最右叶子节点（所有兄弟节点），此时遍历完A的所有直接孩子。遍历的同时，节点入队列。
3.遍历完A的孩子后，取队列中的下一个节点，继续遍历其孩子节点。直到队列为空。"	算法	2
付冠生	判断链表是否成环	基本数据结构链表的掌握	算法	2
王宇	如何判断一个单向链表是否成环		算法	2
张旭	徒手写一个hashmap实现	"预期其知道java hashmap的内部实现。可以写出put/get方法。
知道loading factor，知道re-hash的过程。"	算法	3
张旭	写一个LRU cache	知道用hashmap，header和tail，可以写伪代码	算法	3
张红强	jdk中排序算法都有哪些&时间复杂度？快速排序的思路？枢纽元如何选择?		算法	3
付冠生	二分查找算法	基本算法	算法	3
董子鹏	用两个栈实现一个队列	考察栈和队列的不同特点以及coding 能力。	算法	3
董国双	常见的负载均衡算法及其代码实现？	"描述&解法：
考察编码能力及对负载均衡相关知识的了解。
参考资料：
https://segmentfault.com/a/1190000004492447"	算法	3
张旭	找数组里面第k大的数	https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#kth-largest-element-in-an-array	算法	4
张旭	合并k个有序的链表	https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/fb.md#merge-k-sorted-lists	算法	4
张旭	解迷宫问题	"https://github.com/neoremind/coddding/blob/master/codding/src/main/java/net/neoremind/mycode/argorithm/leetcode/Maze.java
有3种不同难度的，依次递增"	算法	4
王宇	如何判断两个无环单向链表是否相交	给予思路提示，期待多种解法，比较优劣	算法	4
孙龙海	请描述一下一致性哈希的原理	"预期：了解候选人对分布式系统的认识
解法：https://www.cnblogs.com/lpfuture/p/5796398.html"	算法	4
鲁晨光	q：有哪些算法可以解决敏感词匹配的问题？	"敏感词较少可以用单模字符串匹配算法：正则、kmp(减少回溯，匹配每个敏感词复杂度o(n+m),n和m分别为匹配和被匹配字符长度)
敏感词比较多时使用多模匹配算法，预先将敏感词表建立匹配词典，空间换时间：倒排、trie树(搜索的时间复杂度O(n),n为树高度)
其他方法：布隆过滤器"	算法	5
唐新军	spring controller是单例还是多例		中间件	1
唐新军	一个http请求从浏览器发出到达controller前都经历了哪些过程，以Tomcat为例	socket连接建立、http协议解析、Servlet规范工作原理、Spring MVC工作原理	中间件	3
田永乾	2. spring aop及事务实现原理		中间件	3
唐新军	如何设计一个tomcat	socket监听、线程池、http协议、session管理、servlet规范、jsp引擎等	中间件	4
唐新军	kafka broker leader选举算法	zk的节点特性、协调者控制模式	中间件	4
杨化伟	zookeeper为何不适合用做分布式存储	"1、写入能力无法实现随着集群机器数增多而线性增长，最大2w+
2、全量数据放置于内存内，存储大小有限制"	中间件	4
杨化伟	zookeeper实现的分布式锁是否会导致脑裂，如果不存在，靠什么机制？	"1、zab协议保证一致的决策，cp系统
2、session超时机制，保证决策被client正确执行，client端超时时间设定为server端2/3，zk有个假设不同机器时间流速大概一致"	中间件	4
