# SQL学习笔记

## 简单应用
- 查看所有数据库:`SHOW DATABASES;`
- 指定操作的数据库:`USE 数据库名;`
- 显示操作的数据库下的所有表:`SHOW TABLES;`
- 显示指定表的属性:`SHOW COLUMNS FROM 表名;`
- 显示指定表的详细索引信息:`SHOW INDEX FROM 表名;`
- 设置密码
  - `SET PASSWORD FOR 'username'@'host' = PASSWORD('newpassword');`
  - 当前登录用户设置：`SET PASSWORD = PASSWORD('newpassword');`
- 删除用户：`DROP USER 'username'@'host';`

## 权限设置
- 查看当前用户权限:`SHOW GRANTS;`
- 查看其他用户权限:`SHOW GRANTS FOR 用户名;`
- 查看所有用户：`SELECT user, host FROM mysql.user`
- 创建用户：`CREATE USER 'username'@'host' IDENTIFIED BY 'password';`
  - username：创建的用户名
  - host：本地用户使用localhost,远程主机访问可使用%通配符,或指定指定IP
  - password：登录密码,为空则不需要密码
- 赋予用户操作指定表所有权限：`GRANT authCode PRIVILEGES ON databasename.tablename TO 'username'@'host';` 
  - authCode：用户操作权限，如`SELECT、INSERT、UPDATE`等，全部则为`ALL`
  - databasename:数据库名，如所有库下的所有表则为`*.*`
  - tablename：表名，如该库下所有表则使用`*`
  - 上述命令授权的用户不能给其他用户授权，如需可授权，则在最后追加`WITH GRANT OPTION`
- 撤销用户权限：`REVOKE authCode PRIVILEGE ON databasename.tablename FROM 'username'@'host';`
  - 同授权解释

## 日期函数

1. current_timestamp()  
获取当前时间戳

2. date_format(date, format) / time_format(time, format)
日期转换为字符串：%Y%m%d%H%i%s

3. 