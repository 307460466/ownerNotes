# MapStruct

<a name="rn8Kl"></a>
### 1.参考文档
- 实体类之间的属性映射，基于编译期生成对应的class文件

[MapStruct（官网）](https://mapstruct.org/)<br />

<a name="Wiz72"></a>
### 2.快速使用

- Maven
```xml
<dependency>
  <groupId>org.mapstruct</groupId>
  <artifactId>mapstruct-jdk8</artifactId>
  <version>1.3.1.Final</version>
</dependency>
<dependency>
  <groupId>org.mapstruct</groupId>
  <artifactId>mapstruct-processor</artifactId>
  <version>1.0.0.Final</version>
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
         * */
        @Mapping(target = "id", ignore = true),
        @Mapping(target = "gmtCreate", ignore = true),
        @Mapping(target = "gmtModified", ignore = true)
    })
    GithubDO req2do(GithubReq req);
}
```



```java
/**
 * Excel工具类
 * @author xie.xu
 * @version ExcelUtils.java, v 0.1 2020-07-23 18:00 xie.xu.hry Exp $$
 */
public class ExcelUtils {
    /** Logger */
    private static final Logger LOGGER = LoggerFactory.getLogger(ExcelUtils.class);
    /** 扩展名：xls */
    private static final String EXTENSION_XLS = "xls";
    /** 扩展名：xlsx */
    private static final String EXTENSION_XLSX = "xlsx";

    /**
     * 根据扩展名和文件输入流构建Workbook对象
     * @param extension 扩展名
     * @param is 输入流
     * @return workbook
     */
    public static Workbook getWorkbookByExtension(String extension, InputStream is) throws IOException {
        if (StringUtils.equals(EXTENSION_XLS, extension)) {
            return new HSSFWorkbook(is);
        }
        if (StringUtils.equals(EXTENSION_XLSX, extension)) {
            return new XSSFWorkbook(is);
        }
        LogUtils.warn(LOGGER, "不支持扩展名,extension=", extension);
        throw new BaseException(BaseResultEnum.EXTENSION_IS_NOT_SUPPORTED);
    }

    /**
     * 根据扩展名创建的Workbook对象
     * @param extension 扩展名
     * @return workbook
     */
    public static Workbook getWorkbookByExtension(String extension) {
        if (StringUtils.equals(EXTENSION_XLS, extension)) {
            return new HSSFWorkbook();
        }
        if (StringUtils.equals(EXTENSION_XLSX, extension)) {
            return new XSSFWorkbook();
        }
        LogUtils.warn(LOGGER, "不支持扩展名,extension=", extension);
        throw new BaseException(BaseResultEnum.EXTENSION_IS_NOT_SUPPORTED);
    }

    /**
     * 设置四边单元格边框
     * @param cellStyle 单元格样式对象
     * @param borderStyle 边框样式
     * @return cellStyle
     */
    public static CellStyle setFillCellBorder(CellStyle cellStyle, BorderStyle borderStyle) {
        cellStyle.setBorderBottom(borderStyle);
        cellStyle.setBorderTop(borderStyle);
        cellStyle.setBorderLeft(borderStyle);
        cellStyle.setBorderRight(borderStyle);
        return cellStyle;
    }

    /**
     * 获取单元格数据字符串格式
     * @param cell 单元格对象
     * @return value string
     */
    public static String getCellValueString(Cell cell) {
        CellType cellType = cell.getCellTypeEnum();
        switch (cellType) {
            case STRING:
                return cell.getStringCellValue();
            case BOOLEAN:
                return Boolean.toString(cell.getBooleanCellValue());
            case NUMERIC:
                return Double.toHexString(cell.getNumericCellValue());
            default:
                return null;
        }
    }
}
```