# MySQL

<a name="wdzN6"></a>
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
## 版本升级
<a name="xG6Hp"></a>
### 5.6->5.7（Win）
<a name="HwF4S"></a>
#### 1.关闭MySQL5.6相关服务及进程
```basic
# 管理员模式	
X:\software\mysql\mysql5.6\bin>mysqld --remove mysql5.6
Service successfully removed.
```

- 在任务管理器进程中查看是否存在mysqld，如存在强制关闭
<a name="gna7D"></a>
#### 2.下载相关MySQL5.7压缩包
[官方](https://dev.mysql.com/downloads/mysql/)

- 5.7压缩包中无data目录及my.ini文件
- 将5.6目录下的data目录及my.ini复制到5.7目录下
- 修改my.ini文件
```
[mysqld]
# 设置mysql的安装目录
basedir=X:/software/mysql/mysql-5.7.30-winx64
# 设置mysql数据库的数据的存放目录，必须是data
datadir=X:/software/mysql/mysql-5.7.30-winx64/data
# mysql端口
port=3306
# 允许最大连接数
max_connections=200
# 服务端字符集（默认8bit编码的latin1字符集）
character-set-server=utf8
# 建立新表默认存储引擎
default-storage-engine=INNODB
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
# skip-grant-tables
[mysql]
# mysql客户端默认字符集
default-character-set=utf8
```
<a name="ySW6p"></a>
#### 3.配置5.7相关并启动
```basic
# 将mysql5.7服务添加win服务队列中
X:\software\mysql\mysql5.7.30-winx64\bin>mysql --install mysql5.7
Service successfully installed.
# 启动mysql
X:\software\mysql\mysql5.7.30-winx64\bin>net start mysql5.7
# 升级mysql
X:\software\mysql\mysql5.7.30-winx64\bin>mysql-upgrade -uroot -p
# 省略....
# 重启Mysql即可
X:\software\mysql\mysql5.7.30-winx64\bin>net stop mysql5.7
X:\software\mysql\mysql5.7.30-winx64\bin>net start mysql5.7
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
