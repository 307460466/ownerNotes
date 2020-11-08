# IDEA

<a name="2Ncei"></a>
## 2.配置项
- 项目编码及文件编码转换

【File】-【Settings】-【File Encodings】

   - Global Encoding：UTF-8
   - Project Encoding：UTF-8

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/118172/1595314505881-cfcf6b80-f884-4271-9d6e-dc97713cc13b.png#align=left&display=inline&height=184&margin=%5Bobject%20Object%5D&name=image.png&originHeight=184&originWidth=745&size=13792&status=done&style=none&width=745)

   - 勾选【Transparent native-to-ascii conversion】，会自动转换相应编码为中文



<a name="OPRw1"></a>
## 99.FAQ
<a name="cFTdz"></a>
### 1）社区版IDEA启动Tomcat配置：Smart Tomcat
非Smart Tomcat插件配置启动方式：[Gradle脚本](https://github.com/Adrninistrator/IDEA-IC-Tomcat/)

- 通过菜单栏【File】-【Settings...】-【Plugins】：安装【Smart Tomcat】
- 在【Settings】-【Other Settings】-【Tomcat Server】配置本地Tomcat路径（Tomcat根目录）
   - 配置路径时注意路径不要存在空格、特殊符号等，否则可能导致读取失败
- 【Run】-【Eidt Configurations...】，创建Smart Tomcat配置

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/118172/1586416131153-483da5eb-07e9-424c-95e8-07594ba2ddf7.png#align=left&display=inline&height=317&margin=%5Bobject%20Object%5D&name=image.png&originHeight=317&originWidth=1092&size=69163&status=done&style=none&width=1092)

   - Tomcat Server：选择配置的本地Tomcat
   - Deployment Directory：webapps目录
   - Context Path：上下文路径，即请求路径
   - Server Port：监听端口
<a name="Uv5Sh"></a>
### 2）IDEA启动项目报错：java.lang.NoClassDefFoundError: hotcode2/plugin/spring/reload/SpringReloaderManager

- 重启IDEA
- 【Edit Configurations】-【SOFA Application】取消勾选【Enable HotCode】
<a name="2INw6"></a>
### 3）IDEA启动项目报错：Command line is too long

- 编辑【项目目录/.idea/workspace.xml】
```xml
<component name="PropertiesComponent">
  <!-- 添加项 -->
	<property name="dynamic.classpath" value="true" />
</component>
```
