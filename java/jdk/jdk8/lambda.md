# lambda

<a name="MjnrS"></a>
## 概述
lambda即一个匿名的方法，是简洁的编写代码方式<br />匿名方法与匿名类是有区别的，后者需实例化对象，前者是与作用分离的

   - 类必须实例化，而方法不必；
   - 当一个类被新建时，需要给对象分配内存；
   - 方法只需要分配一次内存，它被存储在堆的永久区内；
   - 对象作用于它自己的数据，而方法不会；
   - 静态类里的方法类似于匿名方法的功能。
- 基本结构 `(arguments) -> body` 
   - 参数类型可推导时，不需指定类型： `(a,b) -> a + b` 
   - 当仅有一个参数且类型可推导时，不强制写 `()` ： `a -> a + 1` 
   - 参数指定类型，必须有括号： `(Integer i) -> i + 1` 
   - 参数可为空： `() -> "hello, lambda"` 
   - body需要用 `{}` 包含语句，当仅有一条语句时可省略



<a name="c63466b3"></a>
## 函数式接口
函数式接口声明，在接口上添加注解 `@FunctionalInterface`

- JDK8之前已存在被标注为函数式接口的接口
   - java.lang.Runnable
   - java.util.COmparator
   - java.util.concurrent.Callable
   - java.io.FileFilter
   - java.security.PrivilegedAction
   - java.beans.PropertyChangeListener
- JDK8新增的函数式接口（基于java.util.function包下）
   - Function：函数，T -> R
   - BiFunction：函数，(T,U) ->R
   - Predicate：断言/判断，T -> boolean
   - BiPredicate：断言/判断，(T,U) -> boolean
   - Supplier：生产者，() -> T
   - Consumer：消费者，(T) -> ;
   - BiConsumer：消费者，(T,U) ->;
   - UnaryOperator：单元运算，(T) -> T
   - BinaryOperator：二元运算，(T,T) -> T
   - BooleanSupplier, DoubleBinaryOperator, DoubleConsumer, DoubleFunction, DoublePredicate, DoubleSupplier, DoubleToIntFunction, DoubleToLongFunction, DoubleUnaryOperator, IntBinaryOperator, IntConsumer, IntFunction, IntPredicate, IntSupplier, IntToDoubleFunction, IntToLongFunction, IntUnaryOperator, LongBinaryOperator, LongConsumer, LongFunction, LongPredicate, LongSupplier, LongToDoubleFunction, LongToIntFunction, LongUnaryOperator, ToDoubleBiFunction, ToDoubleFunction, ToIntBiFunction, ToIntFunction, ToLongBiFunction, ToLongFunction等



<a name="5e00833b"></a>
### 快速使用
<a name="WXmiH"></a>
##### 1）简化匿名函数式接口实现
函数式接口：只包含一个抽象方法声明的接口
```java
List<String> names = Arrays.asList("peter", "anna", "mike", "xenia");

Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return b.compareTo(a);
    }
});
```

- 写法
```java
// 写法1：简化匿名类写法
Collections.sort(names, (String a, String b) -> { 
    return b.compareTo(a)
    });
// 写法2：在1的基础上，省略方法参数类型
Collections.sort(names, (a, b) -> { 
    return b.compareTo(a)
    });
// 写法3：在2的基础上，单行方法省略return和{}
Collections.sort(names, (a, b) -> b.compareTo(a));
```


<a name="6Jb3v"></a>
##### 2）方法和构造函数引用

- Converter接口
```java
@FunctionalInterface
interface Converter<F, T> {
   T convert(F from);
}
```

- 写法
```java
Converter<String, Integer> converter1 = (from) -> Integer.valueOf(from);
Integer converted1 = converter1.convert("123");

// 更进一步的简化写法
Converter<String, Integer> converter2 = Integer::valueOf;
Integer converted2 = converter2.convert("123");
```


- 实现Person类构造函数的引用
```java
class Person {
    String firstName;
    String lastName;

    Person() {}

    Person(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
----
interface PersonFactory<P extends Person> {
   P create(String firstName, String lastName);
}
----
PersonFactory<Person> personFactory = Person::new;
Person person = personFactory.create("Peter", "Parker");
```
<a name="qoOeU"></a>
##### 3) lambda访问范围

- 局部变量
   - 外部变量在lambda内部使用时，会在编译时隐式声明final修饰
```java
int num = 1;	// 等同于final int num = 1;
Converter<Interge, String> converter = (from) String.valueOf(from + num);
```

- 成员变量与静态成员变量
   - 支持在lambda内部读写操作
```java
public class VarTest {
    int num;
    static staticNum;
    @Test
    public void test() {
        Converter<Integer, String> converter = (from) -> {
            num = 1;
            return String.valueOf(from + num);
        };
        Converter<Integer, String> staticConverter = (from) -> {
            staticNum = 2;
            return String.valueOf(from + staticNum);
        };
    }
}
```

- default接口方法
   - 编译不支持



<a name="7ixpd"></a>
## 内置函数式接口
<a name="J5TRG"></a>
### Predicate<T>

- 布尔类型函数，处理复杂逻辑判断，test方法为执行方法
   - and(Predicate p)：与其他Predicate对象组成全满足关系
   - or(Predicate p)：与其他Predicate对象组成满足任一即可关系
   - negate()：结果取反
```java
// 判断整数是否在[60,100]区间内
Predicate<Integer> predicate = i -> i >= 60 && i <= 100;
// test方法最终执行逻辑判断
predicate.test(10);	// false
predicate.test(100);	// true
```
<a name="c0oeK"></a>
### Function<T, R>

- 接收单一参数返回单一结果，apply方法为执行方法
   - andThen(Function f)：下一个执行Function
   - compose(Function f)：在此之前执行Function
```java
Function<Integer, Integer> add = x -> x + 10;
Function<Integer, Integer> mul = x -> x * 2;
add.andThen(mul).apply(3);	// (3 + 10) * 2 = 26
```
<a name="bL5o6"></a>
### Supplier<T>

- 获得一个给定类型的结果，无入参
```java
Supplier<Integer> supplier = () -> 1;
supplier.get();	// 1
```
<a name="1QlI8"></a>
### Consumer<T>

- 接收单一入参无返回结果
   - andThen(Consumer c)：链式追加
```java
Consumer<Person> consumer = p -> {
    p.setAge(p.getAge() + 1);
}
consumer.accept(new Person("Test", 1));
```
<a name="uvBH0"></a>
### Comparators

- 接收两个同类型参数，比较大小
```java
List<Person> list = ListUtils.list(new Person("a", 33), new Person("d", 15), 
                                   new Person("b", 22), new Person("e", 15));
// 按age降序,再按name倒序
list.sort(Comparator.comparing(Person::getAge)
          .thenComparing(Person::getName).reversed());
```


<a name="5CRVN"></a>
### Optionals

- 存储一个对象值，可能为NULL可能非NULL


<br />

<a name="375729eb"></a>
## 方法引用
语法： `Type::methodName` 或 `instanceName::methodName` ，后者methodName为new
<a name="C4Bv7"></a>
### 1）构造方法引用
语法： `Type::new` 
```java
// 整数String转换为Integer
// 方法引用写法
Function<String, Integer> f = Integer::new;
// lambda写法
f = s -> new Interger(s);
// 传统写法
f = new Function() { public Integer apply(String s) { return new Integer(s);}}
```
<a name="SErFa"></a>
### 2）数组构造方法引用
语法： `Type[]::new` 
```java
// 构造指定长度的String数组
// 方法引用写法
Function<Integer, String[]> f = String[]::new;
// lambada
f = length -> new String[length];
```
<a name="b812ada7"></a>
### 3）静态方法引用
```java
// lambda写法
Function<String,Integer> f = s -> Integer.parseInt(s);
// 方法引用写法
Function<String,Integer> f = Integer::parseInt;
```
<a name="Q2lXR"></a>
### 4）实例方法引用
```java
// 判断List中是否存在指定String
List<String> names = Arrays.asList(new String[]{"Tom", "summery"});
Predicate check = names::contains;
check.test("Tom");	// true
```
<a name="DTlaX"></a>
### 5）类型方法引用
```java
// 输出String的长度
Function<String, Integer> f = String::length;
System.out.println(f.apply("TomCat"));
// 输出List中每个String元素的长度
List<String> names = Arrays.asList(new String[]{"Tom", "summery"});
names.stream().map(String::length).forEach(System.out::println);
// 切割字符串
BiFunction<String, String, String[]> sp = String::split;
String[] apply = sp.apply("this.is.Test,sdjsk.sdfav", "\\.");
```


<a name="yZvOE"></a>
## Stream
JDK8引入的新特性， `java.util.stream` 包中，是一组支持串行并行聚合操作的元素，即集合/迭代器的增强版

- stream()：串行执行流对象操作
- paralleStream()：并行执行流对象操作
- 特性
   - 单次处理，即一次处理完毕后，当前Stream关闭
   - 支持并行操作
<a name="Um4YB"></a>
### 方法
<a name="a7iFl"></a>
#### forEach

- 流中止操作，遍历每个元素
```java
List<String> list = Arrays.asList("B", "C", "H", "A");
list.stream().forEach(System.out::println);
```
<a name="cFowe"></a>
#### filter

- 流中间操作，接收一个Predicate对象，对每一个元素进行过滤，常用配合collect或其他操作
```java
// 过滤过于大于50和小于0的元素，取最大值
List<Integer> list = Arrays.asList(40, 2, 33, 55, 32, 14, 5, 10, -10, -33);
Integer max = list.stream().filter(i -> i <= 50 && i >= 0).max(Integer::compareTo).get();
```
<a name="EPF6t"></a>
#### sorted

- 流中间操作，对集合进行排序并返回流对象；该操作不改变原集合对象顺序，仅返回一个排序过的流对象视图
```java
List<String> list = Arrays.asList("B", "C", "H", "A");
// 默认自然排序
list.stream().sorted().forEach(System.out::println);
// 降序
list.stream().sorted(Comparator.reverseOrder()).forEach(System.out::println);
// 自定义排序
list.stream().sorted(Comparator.comparing(String::toString)).forEach(System.out::println);
```
<a name="MYPiV"></a>
#### map

- 流中间操作，将流中的每个元素对应到另一个对象中
```java
List<String> list = Arrays.asList("Bob", "Car", "Height", "ALICE");
# 将字符串变为全小写输出
list.stream().map(s -> s.toLowerCase(Locale.CHINA)).forEach(System.out::println);
```
<a name="FWPyn"></a>
#### match操作

- 流中止操作，判断某一种规则是否与流对象中的元素匹配，返回Boolean值
```java
List<String> list = Arrays.asList("Bob", "Car", "Height", "ALICE");
// 判断元素中是否任一满足首字符为B
list.stream().anyMatch(s -> s.startsWith("B"));	// true
// 判断元素中是否都满足首字符为B
list.stream().allMatch(s -> s.startsWith("B"));	// false
// 判断元素中是否都不满足首字符为B
list.stream().noneMatch(s -> s.startsWith("B"));	// false
```
<a name="TqFsv"></a>
#### count

- 流中止操作，返回当前流对象中元素数目
```java
List<String> list = Arrays.asList("Bob", "Car", "Height", "ALICE");
// 满足开头首字符为B或A的元素数目
list.stream().filter(s -> s.startsWith("B") || s.startsWith("A")).count(); // 2
```
<a name="LCII6"></a>
#### reduce

- 规约，可作为累加器、累乘器
```java
// Optional<T> reduce(BinaryOperator<T> accumulator);
Arrays.asList(1, 2, 3).stream().reduce((a, b) -> a + b).get());	// 6
// T reduce(T identity, BinaryOperator<T> accumulator);	相对上一个使用多了一个初始值设置
Arrays.asList(1, 2, 3).stream().reduce(0， (a, b) -> a + b));	// 6
```
<a name="FB87c"></a>
#### concat

- 流连接
```java
// 连接两个流并打印
Stream.concat(Stream.of(1, 2), Stream.of(3)).forEach(System.out::print);	// 123
```
<a name="elcZx"></a>
#### peek

- 生成包含原Stream流所有元素的新Stream流，且新Stream流每个元素被消费前执行peek给定的消费函数
```java
// 打印元素前先打印元素-1的值
Stream.of(2, 4).peek(x -> System.out.print(x - 1)).forEach(System.out::print);	// 1234
```
<a name="JMtb2"></a>
#### max/min

- 获取最大或最小元素
   - 存在多个最值相同的元素，则返回首个最值元素
```java
List<Integer> list = Arrays.asList(40, 2, 33, 55, 32, 14, 5, 10);
Integer max = list.stream().max(Integer::compareTo).get();
```
<a name="3auTk"></a>
##### limit

- 截取前N个元素
```java
// 截取前四位取最小值
List<Integer> list = Arrays.asList(40, 2, 33, 55, 32, 14, 5, 10, -10, -33);
list.stream().limit(4).forEach(System.out::println);
```
<a name="5kDAz"></a>
#### collect
将处理后的Stream流组装成集合
```java
// 过滤负数元素
List<Integer> list = Arrays.asList(33, -10, 60 ,-4, 6, 80 , -33);
List<Integer> collect = list.stream().filter(i -> i >= 0).collect(Collectors.toList());
```
<a name="p5WlC"></a>
#### mapToInt/mapToLong/mapToDouble

- 汇总数据对象：IntSummaryStatistics, DoubleSummaryStatistics, LongSummaryStatistics
   - 对应方法：getCount（总数）、getMax（最大值）、getMin（最小值）、getAverage（平均值）
```java
List<Integer> list = Arrays.asList(33, -10, 60 ,-4, 6, 80 , -33);
IntSummaryStatistics summary = list.stream().mapToInt(Integer::intValue).summaryStatistics();
```
<a name="7LyOb"></a>
### 用法

- 遍历索引
```java
List<String> list = Arrays.asList("a", "b", "c", "d");
Stream.iterate(0, i -> i + 1).limit(list.size()).forEach(i -> {
    System.out.println(i + ":"+ list.get(i));
});
```

- 分组统计
```java
/* [Person{c='A', d=10, e=75}, Person{c='B', d=24, e=61}, Person{c='D', d=16, e=20}, 
 * Person{c='A', d=17, e=99}, Person{c='C', d=20, e=67}, Person{c='D', d=10, e=14}, 
 Person{c='B', d=4, e=41}, Person{c='A', d=29, e=35}, Person{c='A', d=6, e=61}, 
 Person{c='D', d=4, e=42}]
 */
// 按C进行分组，并对D汇总
Map<String, Integer> d = list.stream()
    .collect(Collectors.groupingBy(Person::getC, Collectors.summingInt(Person::getD)));
// {A=62, B=28, C=20, D=30}

// 按C进行分组，并对E汇总（不支持BigDecimal，使用reducing解决）
Map<String, BigDecimal> e = list.stream().collect(Collectors.groupingBy(Person::getC, Collectors.reducing(BigDecimal.ZERO, Person::getE ,BigDecimal::add)));
// {A=270, B=102, C=67, D=76}

// 一次返回以分组统计好的通类型对象
List<Person> collect = group.entrySet().stream().map(entry -> {
    Person p = new Person();
    p.setC(entry.getKey());
    p.setD(entry.getValue().stream().map(Person::getD).reduce(Integer::sum).orElse(0));
    p.setE(entry.getValue().stream().map(Person::getE).reduce(BigDecimal.ZERO, BigDecimal::add));
    return p;
}).collect(Collectors.toList());
// [Person{c='A', d=75, e=304}, Person{c='B', d=4, e=17}, Person{c='D', d=36, e=255}]
```


