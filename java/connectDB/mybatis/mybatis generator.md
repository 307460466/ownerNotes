# mybatis generator

<a name="0spRV"></a>
## 快速使用
- pom
```xml
<plugin>
  <groupId>org.mybatis.generator</groupId>
  <artifactId>mybatis-generator-maven-plugin</artifactId>
  <version>1.3.7</version>
  <configuration>
    <!-- Console print log -->
    <verbose>true</verbose>
    <!-- 重复生成覆盖 -->
    <overwrite>true</overwrite>
    <configurationFile>src/main/resources/generatorConfig.xml</configurationFile>
  </configuration>
  <dependencies>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>6.0.5</version>
    </dependency>
  </dependencies>
</plugin>
```

- resources创建generatorConfig.xml文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <!-- context:逆向工程主要配置信息
            id:名称
            targetRuntime:设置生成的文件适用mybatis具体版本
    -->
    <context id="default" targetRuntime="MyBatis3">

        <!-- 生成mysql带有分页的sql的插件  这个可以自己写，-->
        <!--        <plugin type="generator.MysqlPaginationPlugin" />-->
<!--        <plugin type="org.mybatis.generator.plugins.ToStringPlugin" />-->
<!--        <plugin type="org.mybatis.generator.plugins.SerializablePlugin" />-->

        <!-- 注释规则（可选）:创建class时,对注释进行控制
                type: 指定实现类;默认实现DefaultCommentGenerator
        -->
        <commentGenerator type="">
            <!-- 是否去除自动生成日期的注释 -->
<!--            <property name="suppressDate" value="true"/>-->
            <!-- 是否去除所有自动生成的注释 -->
<!--            <property name="suppressAllComments" value="true"/>-->
        </commentGenerator>
        <!-- jdbc connect setting -->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/test_ab?characterEncoding=utf8&amp;useUnicode=true&amp;serverTimezone=GMT&amp;useSSL=false"
                        userId="root"
                        password="" />
        <!-- 类型处理器（可选） -->
        <javaTypeResolver>
            <!-- default: decimal/bigInt 对应java中的BigDecimal -->
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>
        <!-- Model生成
                targetPackage:生成实体类所在包
                targetProject:生成实体类所在硬盘位置
         -->
        <javaModelGenerator targetPackage="com.owner.demo.common.dal.test.dos"
                            targetProject="src/main/java">
            <!-- 是否允许子包 -->
            <property name="enableSubPackages" value="true"/>
            <!-- 是否对modal添加构造函数 -->
            <property name="constructorBased" value="true"/>
            <!-- 是否清理从数据库中查询出的字符串左右两边的空白字符 -->
            <property name="trimStrings" value="false"/>
            <!-- 建立modal对象是否不可改变 即生成的modal对象不会有setter方法，只有构造方法 -->
            <property name="immutable" value="false"/>
        </javaModelGenerator>
        <!-- SqlMap生成 -->
        <sqlMapGenerator targetPackage="mybatis.test.mapper"
                         targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!-- DAO生成 -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.owner.demo.common.dal.test.dao" 
                             targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!-- 表映射
                tableName:数据库对应表名   domainObjectName:生成Java实体类类名
         -->
        <table tableName="t_sys_user" domainObjectName="SysUserDO"
               enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false"
               selectByExampleQueryId="false"/>
    </context>
</generatorConfiguration>
```

- 执行Maven -> Plugins -> mybatis-generator
