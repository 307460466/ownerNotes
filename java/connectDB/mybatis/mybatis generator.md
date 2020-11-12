# mybatis generator

<a name="0spRV"></a>
## 参考
[详细配置](https://blog.csdn.net/testcs_dn/article/details/79295065)<br />

<a name="FMGCq"></a>
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
            defaultModelType:生成Model类型
                conditional:类似hierarchical
                flag:单表单Model
                hierarchical:主键生成XxxKey,Blod等单独生成,其他简单属性一个对象
            targetRuntime:设置生成的文件适用mybatis具体版本
                MyBatis3(default)
                MyBatis3Simple:无Example内容
    -->
    <context id="default" defaultModelType="flat" targetRuntime="MyBatis3Simple">
        <!-- 自动识别数据库关键字,默认false -->
<!--        <property name="autoDelimitKeywords" value="true"/>-->
        <!-- 格式化java代码 -->
<!--        <property name="javaFormatter" value="org.mybatis.generator.api.dom.DefaultJavaFormatter"/>-->
        <!-- 格式化XML代码 -->
<!--        <property name="xmlFormatter" value="org.mybatis.generator.api.dom.DefaultXmlFormatter"/>-->

        <!-- 注释生成（可选）
                type: 指定实现类;默认实现类DefaultCommentGenerator
        -->
        <commentGenerator >
            <!-- 是否去除自动生成日期的注释 -->
            <property name="suppressDate" value="true"/>
            <!-- 是否去除所有自动生成的注释 -->
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>
        <!-- jdbc connect setting -->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/test_ab?characterEncoding=utf8&amp;useUnicode=true&amp;serverTimezone=GMT&amp;useSSL=false"
                        userId="root"
                        password="root" />
        <!-- 类型处理器（可选） -->
        <javaTypeResolver>
            <!-- 是否强制Decimal和Numeric类型转换为BigDecimal,默认值false
                精度 > 0 || length > 18 -> java.math.BigDecimal
                精度 = 0 && 10 <= length <= 18 -> java.lang.Long
                精度 = 0 && 5 <= length <= 10 -> java.lang.Integer
                精度 = 0 && length < 5 -> java.lang.Short
             -->
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
            <!-- 是否使用构造方法入参,默认false -->
<!--            <property name="constructorBased" value="true"/>-->
            <!-- 是否清理从数据库中查询出的字符串左右两边的空白字符,默认false -->
<!--            <property name="trimStrings" value="false"/>-->
            <!-- 建立modal对象属性是否不可改变 即生成的modal对象不会有setter方法，只有构造方法 -->
<!--            <property name="immutable" value="false"/>-->
            <!-- 继承根类 -->
            <property name="rootClass" value="com.owner.demo.core.model.base.ToString"/>
        </javaModelGenerator>
        <!-- SqlMap生成 -->
        <sqlMapGenerator targetPackage="mybatis.test.mapper"
                         targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!-- Mappers生成
            type:预定义Mapper生成器
                Mybatis3/Mybatis3Simple:
                    ANNOTATEDMAPPER:基于注解Mapper接口，无XML
                    MIXEDMAPPER：XML与注解混合式形式
                    XMLMAPPER：XML形式
         -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.owner.demo.common.dal.test.dao" 
                             targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!-- 表映射
                tableName:数据库对应表名,生成全部表则使用%,支持SQL通配符匹配多个表
                domainObjectName:生成Java实体类类名
         -->
        <table tableName="t_sys_user" domainObjectName="SysUserDO" />
        <table tableName="t_sys_user_role" domainObjectName="SysUserRoleDO" />
        <table tableName="t_sys_role" domainObjectName="SysRoleDO" />
    </context>
</generatorConfiguration>
```

- 执行Maven -> Plugins -> mybatis-generator
