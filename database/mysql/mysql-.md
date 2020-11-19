# MySQL

<a name="wdzN6"></a>
## 运行机制
- 客户端发起请求
- 服务端接收并验证权限
   - 验证失败，直接输出结果
- 执行分析器（语法分析）
   - 查询缓存
      - 命中缓存则直接输出结果
- 执行优化器（生产执行分析）
- 执行器（执行语句）
- 输出结果
<a name="eFxpf"></a>
### 语句执行顺序

- FROM
   - 组装不同数据源的数据
- WHERE
   - 基于指定条件进行数据筛选
- GROUP BY
   - 将数据划分多个组
- 聚合函数
   - 进行聚合函数计算
- HAVING
   - 筛选分组
- 计算表达式
- ORDER BY
   - 对结果进行排序
- LIMIT
   - 结果分页


<br />

<a name="LvTiU"></a>
## 安装

- yum安装
   - 访问[官网Community Downloads](https://dev.mysql.com/downloads/repo/yum/)，确认rep源（如：mysql80-community-release-el7-3.noarch.rpm）
```bash
# 下载mysql repo源
$ wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
# 使用rpm安装
$ rpm -ivh mysql80-community-release-el7-3.noarch.rpm
# 安装mysql-server
$ yum install -y mysql-server
# 启动mysql
$ systemctl start mysqld
# 查看root临时密码
$ grep 'temporary password is' /var/log/mysqld.log
2020-09-11T03:48:09.935555Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: FKJ)53rf1K&R
# mysql登录
$ mysql -uroot -p"FKJ)53rf1K&R"
# 重置root密码
mysql > SET password="Test1234.";
```


<a name="TZS6n"></a>
## 命令
<a name="vPpWf"></a>
### 备份数据库
```bash
$ mysqldump -uroot -p --all-databases > /home/admin/back/mysql_all_back_5.7.sql
```


<a name="1AEkR"></a>
## 升级
<a name="ULLMD"></a>
### Windows（管理员模式）

- 准备新版MySQL：[官网](https://downloads.mysql.com/archives/community/)
```bash
# 停止MySQL服务
$>net stop mysql
# 移除MySQL服务
$>mysqld --remove mysql
# 如在系统/用户环境变量中配置MySQL/bin,需要将其指定为新版MySQL/bin地址
# 安装MySQL服务
$>mysqld -install
Service successfully installed.
# 初始化MySQL，并查看初始化ROOT密码
$>mysqld --initialize --user=mysql --console
2020-11-13T05:41:11.222974Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
2020-11-13T05:41:12.195163Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
2020-11-13T05:41:13.675553Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: 0o!6+f#)ruwE
# 启动MySQL服务
$>net start mysql
```


<a name="5xA6W"></a>
## 问题排查
<a name="AWJIu"></a>
### MySQL错误日志排查

- 通过MySQL配置查找对应错误日志
   - log_error
```sql
mysql>SHOW VARAABLES LIKE "%error%";
+---------------------+---------------------------------------------------------------------------+
| Variable_name       | Value                                                                     |
+---------------------+---------------------------------------------------------------------------+
| binlog_error_action | ABORT_SERVER                                                              |
| error_count         | 0                                                                         |
| log_error           | D:\\software\mysql\mysql-5.7.30-winx64\data\MININT-8FTMM5L.err |
| log_error_verbosity | 3                                                                         |
| max_connect_errors  | 100                                                                       |
| max_error_count     | 64                                                                        |
| slave_skip_errors   | OFF                                                                       |
+---------------------+---------------------------------------------------------------------------+
7 rows in set, 1 warning (0.00 sec)
```

- 通过配置的datadir查找，如my.ini中配置的datadir位置下
<a name="F9XdM"></a>
### 连接数据库提示警告使用SSL

- 数据库服务端没有身份验证下，不推荐使用SSL；5.7.6+版本会默认启用
   - 关闭：在url后追加参数 `&useSSL=false` 
<a name="DcvoR"></a>
### 由于找不到vcruntime140_1.dll，无法继续执行代码

- MySQL8.0 Server需要Microsoft Visual C++ 2015，当前系统缺少这部分发行组件包导致报错
   - [微软平台下载](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads)
