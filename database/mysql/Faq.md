# FAQ

### 1.Linux安装社区版MySQL

- 远程下载MySQL repo源：`wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm`
  - CentOs通过yum安装默认是安装Mariadb
  - 在`/etc/yum.repos.d`目录下会生成相关`mysql-community..`前缀的repo文件
- 通过rpm安装mysql：`rpm -ivh mysql57-community-release-el7-9.noarch.rpm`
  - 查看mysql可安装选项：`rpm -aq| grep mysql`
- 安装mysql 5.7：`yum install -y mysql-server`

### 2.MySQL 5.7版本以上Root初始化密码问题
- MySQL 5.7版本以上会自动生成随机密码,不在支持默认空密码登录
  - 查看mysql默认root初始化密码：`grep 'temporary password is generated' /var/log/mysqld.log`
  - 举例初始化密码：`A!-1SD-3242F`
- 修改初始密码，否则进行MySQL相关操作会报错：`ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.`
```Bash
$ mysql -uroot -p'A!-1SD-3242F'
$ mysql> SET PASSWORD='Test1234.';
```
- 设置MySQL密码策略相关配置
  - 关闭密码复杂性策略：`SET GLOBAL VALIDATE_PASSWORD_POLICY=0;`
  - 查看密码复杂性策略：`SELECT @@VALIDATE_PASSWORD_POLICY;`
  - 密码要求最低长度：`SET GLOBAL VALIDATE_PASSWORD_LENGTH=1;`
  - 查看密码最低长度：`SELECT @@VALIDATE_PASSWORD_LENGTH;`