# 问题集合
1. Mybatis配置Mapper文件时，`<if>`标签的判断条件无法匹配字符串
- 多字符支持，单字符需要使用`''.toString()`

### 1.JDBC链接未配置zone
- 报错：`Failedjava.sql.SQLException: The server time zone value 'Coordinated Universal Time' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.`
- 解决方法：在DB配置中,DB链接后追加`&serverTimezone=UTC`(通过指定时区解决问题)
  - UTC：统一标准世界时间