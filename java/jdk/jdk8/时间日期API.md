# 时间日期API

<a name="OmtmR"></a>
## 参考文档
[时间类型](https://lw900925.github.io/java/java8-newtime-api.html)<br />

<a name="q33D4"></a>
## 快速使用
<a name="L7TlO"></a>
### LocalTime

- 未指定时区和日期的时间对象，含毫秒值
```java
// 获取当前时间
LocalTime nowTime = LocalTime.now();	//14:21:24.932
// 毫秒值设置为0
nowTime = nowTime.withNano(0);	// 14:21:24
// 设置时间参数
nowTime = LocalTime.of(0, 0, 1);	// 00:00:01
// 解析字符串转化时间对象，默认格式为HH:mm:ss
nowTime = LocalTime.parse("12:00:01");	// 12:00:01
```
<a name="aWSp6"></a>
### LocaDate

- 日期对象
```java
// 设置日期参数
LocalDate today = LocalDate.of(2019, 3, 22);	// 2019-03-22
// 解析字符串，默认格式为yyyy-MM-dd，不符合则抛出异常
today = LocalDate.parse("2019-04-01");	// 2019-04-01
// 获取当前日期
today = LocalDate.now();	// 2019-03-12

// 获取本月第一天
LocalDate firstDayOfCurrentMonth = today.with(TemporalAdjusters.firstDayOfMonth());	// 2019-03-01
// 获取本月最后一天
LocalDate lastDayOfCurrentMonth = today.with(TemporalAdjusters.lastDayOfMonth());	//2019-03-31
// 获取本月第10天
LocalDate tenDayOfCurrentMonth = today.withDayOfMonth(10);	//2014-03-10，如超过当月最长日则抛出异常
// 获取明天
LocalDate nextDayOfMonth = lastDayOfCurrentMonth.plusDays(1L);	//2019-04-01
```
<a name="SoZX3"></a>
### LocalDateTime

- 日期时间对象
```java
// 设置日期时间参数
LocalDateTime dateTime = LocalDateTime.of(2020, 10, 14, 15, 40, 11);	// 2020-10-14 15:40:11
// 解析字符串，默认格式为yyyy-MM-ddTHH:mm:ss
dateTime = LocalDateTime.parse("2020-10-14T15:40:11");	// 2020-10-14 15:40:11
// 指定解析格式
dateTime = LocalDateTime.parse("2019-09-24 13:54:00", DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")); // 2019-09-24T13:54:00

// 比较两个日期时间对象之间的差值
LocalDateTime start = LocalDateTime.parse("2019-09-24 13:54:00", DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")); // 2019-09-24T13:54:00
LocalDateTime end = LocalDateTime.of(2019, 9, 24, 14, 54, 0); // 2019-09-24T14：54：00
long differenceHours = start.until(end, ChronoUnit.HOURS); // 1 -> 以start时间值为计算,大于1小时小于2小时返回1
end = end.withMinute(53); // 2019-09-24T14:53:00
long differenceHours = start.until(end, ChronoUnit.HOURS); // 0 -> 比较是会结合天和分钟计算，如只需计算小时单位，则应取小时单位在比较
```
<a name="UxVfO"></a>
### 转换
```java
// LocalDateTime 转换为LocalDate或LocalTime
LocalDateTime now = LocalDateTime.now();
LocalDate today = now.toLocalDate();
LocalTime nowTime = now.toLocalTime();

// LocalDate + LocalTime转换LocalDateTime
now = LocalDateTime.of(today, nowTime);

// LocalDateTime 转换为 Date (添加时区信息即可转换Date对象）
Date date = Date.from(now.atZone(ZoneId.systemDefault()).toInstant());

// Date转换LocalDateTime
now = date.toInstant().atZone(ZoneId.systemDefault()).toLocalDateTime();
```
<a name="D31mB"></a>
### Instant
含时区信息的时间日期对象
```java
// 获取当前时间
Instant now = Instant.now();	// 2019-04-02T08:20:26.781Z
// 通过ofEpochSecond(秒, 纳秒)构建，以1970-01-01 00:00:00为基准线
now = Instant.ofEpochSecond(3);	// 1970-01-01T00:00:03Z
```
<a name="xK5Oo"></a>
### DateTimeFormat
jdk8之前的DateFormat线程上是不安全的，使用了全局变量，未做保护措施；DateTimeFormat是线程安全的<br />

<a name="dwloO"></a>
### Duration

- 表示一个时间段（天、时、分、秒、毫秒、纳秒），通过betwwen(开始时间, 截止时间)方式创建对象
```java
LocalDateTime from = LocalDateTime.of(2019, Month.APRIL, 2, 0, 0, 0);
LocalDateTime to = LocalDateTime.of(2019, Month.APRIL, 2, 16, 33, 0);
Duration duration = Duration.between(from, to);	//PT16H33M
long days = duration.toDays();              // 这段时间的总天数
long hours = duration.toHours();            // 这段时间的小时数
long minutes = duration.toMinutes();        // 这段时间的分钟数
long seconds = duration.getSeconds();       // 这段时间的秒数
long milliSeconds = duration.toMillis();    // 这段时间的毫秒数
long nanoSeconds = duration.toNanos();      // 这段时间的纳秒数
//设置时间段为3秒
duration = Duration.ofMinutes(3);
```
<a name="HYqJb"></a>
### Period
表示一个时间段（年、月、日），与Duration用法类似<br />

<a name="Rc2Jt"></a>
### 操作日期类

- TemporalAdjuster：用于在复杂情况下调整日期；如预定义的api无法满足需求，可通过实现TemporalAdjuster接口去定义
- 使用with()方法或plus()方法
```java
LocalDateTime now = LocalDateTime.now(); //2019-04-02 16:58:47
//返回本月最后一个周六
LocalDateTime with = now.with(TemporalAdjusters.lastInMonth(DayOfWeek.SATURDAY)); //2019-04-27 16:58:47
//返回下一个距离当前时间最近的周日
with = now.with(TemporalAdjusters.nextOrSame(DayOfWeek.SUNDAY)); //2019-04-07 16:58:47
```
<a name="9vhWK"></a>
### 时区
可通过of()方法创建，也可以通过systemDefualt()获取系统默认时区
```
//获取指定时区
ZoneId zoneId = ZoneId.of("Asia/Shanghai");	//Europe/Rome
//获取系统默认时区
zoneId = ZoneId.systemDefault(); //Asia/Shanghai
```


<a name="73xub"></a>
## 补充

```
Instant：时间戳
Duration：持续时间，时间差（天时分秒---）
LocalDate：只包含日期，比如：2016-10-20
LocalTime：只包含时间，比如：23:12:10
LocalDateTime：包含日期和时间，比如：2016-10-20 23:14:21
Period：时间段（年月日）
ZoneOffset：时区偏移量，比如：+8:00
ZonedDateTime：带时区的时间
Clock：时钟，比如获取目前美国纽约的时间
```
```
JDBC支持DB的日期类型和JDK8的新类型相关联：
SQL -> Java
----------
date -> LocalDate
time -> LocalTime
timestamp -> LocalDateTime
```
