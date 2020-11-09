# MapStruct

<a name="rn8Kl"></a>
### 参考文档
[MapStruct（官网）](https://mapstruct.org/)

- 实体类之间的属性映射，基于编译期生成对应的class文件
   - 基于约定优于配置的方法：通过普通方法调用而非反射
   - 编译时生成Bean映射
   - 一个注释处理器
- 实现原理
   - MapStruct是一个接口，具体功能实现是由MapStruct在代码编译期创建具体实现类，通过字段的Getter/Setter方法实现字段的赋值，从而实现对象的映射



<a name="Wiz72"></a>
### 2.快速使用

- Maven
```xml
<dependency>
  <groupId>org.mapstruct</groupId>
  <artifactId>mapstruct-jdk8</artifactId>
  <version>1.4.1.Final</version>
</dependency>
<dependency>
  <groupId>org.mapstruct</groupId>
  <artifactId>mapstruct-processor</artifactId>
  <version>1.4.1.Final</version>
</dependency>
```

- 实体类
```java
@Setter
@Getter
@Data
public class GithubReq {
    private String name;
    private Date birth;
    private int age;
    private String gender;
    private Date createDate;
    private List<Integer> followerList;
}

@Setter
@Getter
@Data
public class GithubDO {
    private Long id;
    private String name;
    private Date birth;
    private int age;
    private String gender;
    private Date gmtCreate;
    private Date gmtModified;
    private String followers;
}
```

- 转换工具类
```java
public class CoolectionUtils {
    public static List<Integer> string2List(String str) {
        if (StringUtils.isNoneBlank(str)) {
            return Arrays.asList(str.split(",")).stream()
                .map(s -> Integer.valueOf(s.trim()))
                .collect(Collections.toList());
        }
        return null;
    }
}
```

- 声明转换接口
```java
/* 定义Converter接口
 * 在编译期生成class文件，避免运行期反射消耗资源
 * componentModel：实现类型
 *  - default：默认，通过Mappers.getMapper(class)获取实例对象
 *  - spring：接口实现类自动添加@Component，通过@Autowired注入
 * */
@Mapper
public interface PersonConverter {
	/** 定义实例 */
    GithubConverter INSTANCE = Mappers.getMapper(GithubConverter.class);

    /**
     * req转DO
     * @param req req
     * @return do
     */
    /* @Mappings 配置多个@Mapping */
    @Mappings(value = {
        /* @Mapping：属性映射，源对象与目标对象名字一致，则自动映射对应属性
         * source:源属性
         * target：目标属性
         * dateFormat：String to Date的转换，通过SimpleDateFormat转换，对应其日期格式
         * ignore：是否忽略属性，默认false
         * expression：表达式调用
         * */
        @Mapping(target = "id", ignore = true),
        @Mapping(target = "gmtCreate", dateFormat = "yyyy-MM-dd", source="createDate"),
        @Mapping(target = "gmtModified", ignore = true)
        @Mapping(target = "
    })
    GithubDO req2do(GithubReq req);
        
    /**
     * 
     * */
    @Mapping(target = "saleChannel", expression = "java(com.xx.demo.utils.CollectionUtils.string2List(githubDO.getFollowers))")
    GithubReq do2Req(GithubDO githubDO);
}
```
