# Tomcat

- 基于Tomcat8
<a name="S5N2b"></a>
### 快速入门
<a name="SYLwW"></a>
#### 目录结构
```xml
tomcat
|--bin：存放tomcat相关脚本和部分jar
	|--catalina.bat/sh：tomcat主要的启动执行脚本
|--conf：存放配置文件
	|--service.xml：主要的服务配置文件
	|--logging.properties：tomcat日志输出配置
|--lib：存放公共jar# Tomcat

- 基于Tomcat8
<a name="S5N2b"></a>
### 快速入门
<a name="SYLwW"></a>
#### 目录结构
```xml
Tomcat
|--bin：存放tomcat相关脚本和部分jar
	|--catalina.bat/sh：tomcat主要的启动执行脚本
|--conf：存放配置文件
	|--service.xml：主配置文件
	|--web.xml：Servlet配置文件
	|--context.xml：host的默认配置信息文件
	|--logging.properties：日志配置文件
|--lib：存放公共jar
|--logs：存放tomcat相关日志文件
	|--catalina.out：生成当前日期的tomcat运行日志（应用及Tomcat日志信息输出）
	|--localhost.log：程序未捕获异常日志（类似common-error.log）
	|--localhost_access_log.txt：Tomcat访问记录日志
|--temp：临时文件存放
|--webapps：web应用默认发布目录
|--work：存放JSP生成servlet文件
```
<a name="9e9J1"></a>
#### Server.xml配置
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 	port：指定端口监听tomcat关闭请求，默认仅本机访问，默认值8005
			shutdown：向指定端口发送的命令字符串，默认值SHUTDOWN
 -->
<Server port="8005" shutdown="SHUTDOWN">
  <!-- 默认配置的Listener -->
  <Listener className="org.apache.catalina.startup.VersionLoggerListener" />
  <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
  <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
  <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />

  <GlobalNamingResources>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>

	<!-- 	Service可配置多个，由多个Connector和单个Container组合（Container由Engine、Realm、Value、Hosts组成）
				name：service名称标签
 	-->
  <Service name="Catalina">
     <!-- 线程池配置，默认情况下每个Connector有着自己创建的线程池
				 	name：线程池名称（唯一）
					namePrefix：JVM线程前缀名（namePrefix + 线程编号）
					maxThreads：最大活跃线程数（默认200）（500~800推荐）
					maxQueueSize：最大等待列数,超出则拒绝请求
					minSpareThreads：最小保持线程数（默认25）
					maxIdleTime：线程空闲最大时间，的那个空闲时间超过该值则关闭线程（除非线程数小于minSpareThreads）（默认60000，单位毫秒）
					daemon：是否后台线程，默认true
					threadPriority：线程优先级，默认5
    -->
    <Executor name="tomcatThreadPool" namePrefix="Http-8080-exec-"
              prestartminSpareThreads="true" maxThreads="800" maxQuueSize="100"
              minSpareThreads="50" maxIdleTime="60000" />
    
		<!-- 	Connector，Tomcat请求接收和响应返回的端点，支持Http、AJP、ARP等协议
					address：指定Connector监听地址：默认为0.0.0.0（所有地址）
					port：监听端口，默认0
					protocol：协议，默认HTTP/1.1（APJ默认AJP/1.3）
					connectionTimout：等待客户端发送请求超时时间（默认60000，单位毫秒），设置0为永不超时
					maxHtreads：支持的最大并发连接数，默认200
					redirectPort：Connector协议为HTTP，接收客户端发送的HTTPS请求时，转发到该属性值指定端口
					enableLookups：是否通过request.getRemoteHost()进行DNS查询获取客户端主机名，默认true（反查域名，如提高处理能力可设false）
					acceptCount：设置等待队列的最大长度，默认10，超出则不予处理（一般设置>=maxThreads）
					executor：指定共享的线程池组件			
					maxHttpHeaderSize：http请求头信息最大大小，超出部分不处理（一般8K，单位B）
					compression：是否开启压缩:on-开启;off-关闭;force-强制开启
          compressionMinSize：指定压缩的最小数据大小,单位为字节（默认2KB）
         	compressableMimeType：指定哪些文件类型需要倍压缩
					URIEncoding：指定Tomcat容器的URL编码格式
		-->
    <Connector port="8080" protocol="HTTP/1.1" connectionTimeout="30000"
               executor="tomcatThreadPool" enableLookups="false" acceptCount="1000"
               redirectPort="8443" compression="on" compressionMinSize="10240"
               compressableMimeType="text/html,text/css,text/xml,text/palain,application/javascript"
               URLEncoding="UTF-8" />
    
    <!-- Define an SSL/TLS HTTP/1.1 Connector on port 8443
         This connector uses the NIO implementation. The default
         SSLImplementation will depend on the presence of the APR/native
         library and the useOpenSSL attribute of the
         AprLifecycleListener.
         Either JSSE or OpenSSL style configuration may be used regardless of
         the SSLImplementation selected. JSSE style configuration is used below.
    -->
    <!--
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/localhost-rsa.jks"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
    -->
	<!-- test config -->
	<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/3038120_www.lubokui.cn.pfx"
						 certificateKeystorePassword="Lk5X3Bau"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
    <!-- Define an SSL/TLS HTTP/1.1 Connector on port 8443 with HTTP/2
         This connector uses the APR/native implementation which always uses
         OpenSSL for TLS.
         Either JSSE or OpenSSL style configuration may be used. OpenSSL style
         configuration is used below.
    -->
    <!--
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11AprProtocol"
               maxThreads="150" SSLEnabled="true" >
        <UpgradeProtocol className="org.apache.coyote.http2.Http2Protocol" />
        <SSLHostConfig>
            <Certificate certificateKeyFile="conf/localhost-rsa-key.pem"
                         certificateFile="conf/localhost-rsa-cert.pem"
                         certificateChainFile="conf/localhost-rsa-chain.pem"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
    -->
 
    <!-- AJP是Tomcat与Http服务器之间通信制定的协议，提供较高的通信效率,基于nginx反向代理
				 不需该连接器,故需注销 -->
    <!-- <Connector port="8009" protocol="AJP/1.3" redirectPort="443" /> -->
    

		<!-- Engine-全局Servlet引擎 -->
    <Engine name="Catalina" defaultHost="localhost">

      <!--For clustering, please take a look at documentation at:
          /docs/cluster-howto.html  (simple how to)
          /docs/config/cluster.html (reference documentation) -->
      <!--
      <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster"/>
      -->

      <!-- Use the LockOutRealm to prevent attempts to guess user passwords
           via a brute-force attack -->
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <!-- This Realm uses the UserDatabase configured in the global JNDI
             resources under the key "UserDatabase".  Any edits
             that are performed against this UserDatabase are immediately
             available for use by the Realm.  -->
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>

      <!-- 虚拟主机配置，支持配置多个 
			-->
      <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="false">

        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->

        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />
				<!-- 热加载：reloadable="true" ，热部署：autoDeploy="true" -->
				<Context path="/" docBase="antcs" autoDeploy="true" crossContext="true" />
      </Host>
    </Engine>
  </Service>
</Server>

```

<br />

<a name="HW3nO"></a>
## 3.设置域名访问和禁止IP直接访问

- 编辑conf/server.xml
```xml
...
<!-- name为引擎逻辑名
		 defaultHost为默认指定主机,未匹配虚拟地址时，由该值对应的主机处理，与Host标签的name匹配
 -->
<Engine name="Catalina" defaultHost="www.test.cn">
  <!--name：虚拟主机地址（域名或IP）
			autoDeploy：是否允许自动部署（默认true）
			unpackWARs：设置是否自动展开WAR再运行WEB（默认true）
			appBase：WEB应用路径（应用组，非单个应用目录），可相对Tomcat根目录或绝对路径
  -->
  <Host name="www.test.cn" appBase="webapps" unpackWARs="true" autoDeploy="true">
    ...
    <!--path：WEB应用访问路径
				docBase：WEB应用路径，可相对appBase路径或绝对路径
				reloadable：是否允许热加载WEB应用
 		-->
    <Context path="" docBase="antcs" debug="0" reloadable="true" />
  </Host>
  <!-- 配置当前机器的公网IP，设置appBase禁止访问 -->
  <Host name="192.168.10.111" appBase="ipapps" unpackWARs="true" autoDeploy="true" />
  ...
</Engine>
```


<a name="p8gcG"></a>
## 98.漏洞问题
<a name="cTA5C"></a>
### 1.AJP漏洞

- 漏洞详情
   - Tomcat默认配置是默认开启AJP Connector，用于与其他WEB服务器通过AJP协议交互。
      - 默认配置，Tomcat配置两个Connector：HTTP Connector和AJP Connector
         - HTTP Connector：处理HTTP协议请求（HTTP/1.1），默认监听端口：8080
         - AJP Connector：处理AJP协议请求（AJP/1.3），默认监听端口：8009
- 漏洞危害
   - 攻击者可读取Tomcat所有webapp目录下的任意文件；如网站应用支持上传，攻击者可上传内含恶意JSP文件，利用Ghostcat漏洞执行
- 漏洞复现（[参考](https://my.oschina.net/u/4411093/blog/3240327/print)）
- 修复方案
   - 应用不涉及使用AJP协议
      - 方式一：tomcat配置server.xml注释
         - <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
      - 方式二：iptables封禁8009端口： ``iptables -A INPUT -p tcp --dport 8009 -j DROP` 
   - 涉及Tomcat版本：9.0.31以上或8.5.51以上或7.0.100以上；并配置secret中AJP协议认证凭证
<a name="4qG2r"></a>
## 99.FAQ
<a name="LsPYP"></a>
### 1.Tomcat启动报错:At least one JAR was scanned for TLDs yet contained no TLDs
> org.apache.jasper.servlet.TldScanner.scanJars At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.

- 编辑conf/catalina.properties
   - 将tomcat.util.scan.StandardJarScanFilter.jarsToSkip的值变更为*.jar
   - 作用忽略jar的TLDs扫描
<a name="xUHCz"></a>
### 2.Tomcat8启动加载十几分钟或更长

- 熵池阻塞：[参考](https://blog.csdn.net/chszs/article/details/49494701) | [/dev/random和/dev/urandom区别](https://blog.csdn.net/weixin_38239856/article/details/81979959)
- Tomcat环境解决
   - 编辑bin/catalina.sh
      - 在JAVA_OPTS=".."中追加 `-Djava.security.egd=file:/dev/./urandom`
- Java黄精解决
   - 编辑$JAVA_PATH/jre/lib/security/java.security
      - 替换securerandom.source值为 `file:/dev/urandom` 
<a name="9ikN0"></a>
### 3.Tomcat配置Context并设置项目为根目录会加载项目两次

- 问题原因
   - <Host>标签属性配置unpackWARs和autoDeploy为true
   - <Host>标签属性appBase路径与<Host>子标签<Context>属性docBase为上下级目录关系（就是说指定项目在appBase内）
- 问题原理
   - Tomcat启动时，会将webapps目录下的所有项目部署
   - 再根据Context配置部署指定路径的项目
- 解决方法
   - 将<Host>下的<Context>配置的docBase目录改为绝对路径，且不为webapps下即可

|--logs：存放tomcat相关日志文件
	|--catalina.out：生成当前日期的tomcat运行日志（应用及Tomcat日志信息输出）
	|--localhost.log：程序未捕获异常日志（类似common-error.log）
	|--localhost_access_log.txt：Tomcat访问记录日志
|--temp：临时文件存放
|--webapps：web应用默认发布目录
|--work：存放JSP生成servlet文件
```
<a name="9e9J1"></a>
#### Server.xml配置
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 	port：指定端口监听tomcat关闭请求
			shutdown：向指定端口发送的命令字符串
 -->
<Server port="8005" shutdown="SHUTDOWN">
  <Listener className="org.apache.catalina.startup.VersionLoggerListener" />
  <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
  <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
  <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />

  <GlobalNamingResources>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>
  
  <!-- 线程池配置
				 	name：共享线程池名称（唯一）
					namePrefix：JVM线程前缀名
					maxThreads：最大并发数（默认200）（500~800推荐）
					maxQueueSize：最大等待列数,超出则拒绝请求
					minSpareThreads：Tomcat初始化时创建的线程数（默认25）
					maxIdleTime：最大空闲线程数，空闲线程数超出该值则Tomcat会关闭不活跃线程（默认60000，单位毫秒）
 	-->
  <Executor name="tomcatThreadPool" namePrefix="Http-8080-exec-"
            prestartminSpareThreads="true" maxThreads="800" maxQuueSize="100"
            minSpareThreads="50" maxIdleTime="60000" />

	<!-- 容器配置 name：指定service名称 -->
  <Service name="Catalina">
		<!-- 	Connector-客户端与Service的连接标签
					executor:线程池
					port：服务器监听客户端请求的端口
					redirector：重定向端口，https请求访问自动重定向https端口
					protocol：网络协议,默认使用nio处理
 					acceptCount：处理队列中的请求数（默认10），超过该数值的请求不予处理（一般设置>=maxThreads）
					connectionTimeout：网络连接超时（默认20000,单位毫秒）,设置为0则永不超时
					maxHttpHeaderSize：http请求头信息最大大小，超出部分不处理（一般8K，单位B）
					enableLookups：是否反查域名（默认true）（提高处理能力可设为false）
					compression：是否开启压缩:on-开启;off-关闭;force-强制开启
          compressionMinSize：指定压缩的最小数据大小,单位为字节（默认2KB）
         	compressableMimeType：指定哪些文件类型需要倍压缩
					URIEncoding：指定Tomcat容器的URL编码格式
		-->
    <Connector port="8080" protocol="HTTP/1.1" connectionTimeout="30000"
               executor="tomcatThreadPool" enableLookups="false" acceptCount="1000"
               redirectPort="8443" compression="on" compressionMinSize="10240"
               compressableMimeType="text/html,text/css,text/xml,text/palain,application/javascript"
               URLEncoding="UTF-8" />
    
    <!-- Define an SSL/TLS HTTP/1.1 Connector on port 8443
         This connector uses the NIO implementation. The default
         SSLImplementation will depend on the presence of the APR/native
         library and the useOpenSSL attribute of the
         AprLifecycleListener.
         Either JSSE or OpenSSL style configuration may be used regardless of
         the SSLImplementation selected. JSSE style configuration is used below.
    -->
    <!--
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/localhost-rsa.jks"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
    -->
	<!-- test config -->
	<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/3038120_www.lubokui.cn.pfx"
						 certificateKeystorePassword="Lk5X3Bau"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
    <!-- Define an SSL/TLS HTTP/1.1 Connector on port 8443 with HTTP/2
         This connector uses the APR/native implementation which always uses
         OpenSSL for TLS.
         Either JSSE or OpenSSL style configuration may be used. OpenSSL style
         configuration is used below.
    -->
    <!--
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11AprProtocol"
               maxThreads="150" SSLEnabled="true" >
        <UpgradeProtocol className="org.apache.coyote.http2.Http2Protocol" />
        <SSLHostConfig>
            <Certificate certificateKeyFile="conf/localhost-rsa-key.pem"
                         certificateFile="conf/localhost-rsa-cert.pem"
                         certificateChainFile="conf/localhost-rsa-chain.pem"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
    -->
 
    <!-- AJP是Tomcat与Http服务器之间通信制定的协议，提供较高的通信效率,基于nginx反向代理
				 不需该连接器,故需注销 -->
    <!-- <Connector port="8009" protocol="AJP/1.3" redirectPort="443" /> -->
    

    <!-- An Engine represents the entry point (within Catalina) that processes
         every request.  The Engine implementation for Tomcat stand alone
         analyzes the HTTP headers included with the request, and passes them
         on to the appropriate Host (virtual host).
         Documentation at /docs/config/engine.html -->

    <!-- You should set jvmRoute to support load-balancing via AJP ie :
    <Engine name="Catalina" defaultHost="localhost" jvmRoute="jvm1">
    -->
    <Engine name="Catalina" defaultHost="localhost">

      <!--For clustering, please take a look at documentation at:
          /docs/cluster-howto.html  (simple how to)
          /docs/config/cluster.html (reference documentation) -->
      <!--
      <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster"/>
      -->

      <!-- Use the LockOutRealm to prevent attempts to guess user passwords
           via a brute-force attack -->
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <!-- This Realm uses the UserDatabase configured in the global JNDI
             resources under the key "UserDatabase".  Any edits
             that are performed against this UserDatabase are immediately
             available for use by the Realm.  -->
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>

      <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="false">

        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->

        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />
		<!-- 热加载：reloadable="true" ，热部署：autoDeploy="true" -->
		<Context path="/" docBase="antcs" autoDeploy="true" crossContext="true" />
      </Host>
    </Engine>
  </Service>
</Server>

```

<br />

<a name="HW3nO"></a>
## 3.设置域名访问和禁止IP直接访问

- 编辑conf/server.xml
```xml
...
<!-- name为引擎逻辑名
		 defaultHost为默认指定主机,未匹配虚拟地址时，由该值对应的主机处理，与Host标签的name匹配
 -->
<Engine name="Catalina" defaultHost="www.test.cn">
  <!--name：虚拟主机地址（域名或IP）
			autoDeploy：是否允许自动部署（默认true）
			unpackWARs：设置是否自动展开WAR再运行WEB（默认true）
			appBase：WEB应用路径（应用组，非单个应用目录），可相对Tomcat根目录或绝对路径
  -->
  <Host name="www.test.cn" appBase="webapps" unpackWARs="true" autoDeploy="true">
    ...
    <!--path：WEB应用访问路径
				docBase：WEB应用路径，可相对appBase路径或绝对路径
				reloadable：是否允许热加载WEB应用
 		-->
    <Context path="" docBase="antcs" debug="0" reloadable="true" />
  </Host>
  <!-- 配置当前机器的公网IP，设置appBase禁止访问 -->
  <Host name="192.168.10.111" appBase="ipapps" unpackWARs="true" autoDeploy="true" />
  ...
</Engine>
```


<a name="p8gcG"></a>
## 98.漏洞问题
<a name="cTA5C"></a>
### 1.AJP漏洞

- 漏洞详情
   - Tomcat默认配置是默认开启AJP Connector，用于与其他WEB服务器通过AJP协议交互。
      - 默认配置，Tomcat配置两个Connector：HTTP Connector和AJP Connector
         - HTTP Connector：处理HTTP协议请求（HTTP/1.1），默认监听端口：8080
         - AJP Connector：处理AJP协议请求（AJP/1.3），默认监听端口：8009
- 漏洞危害
   - 攻击者可读取Tomcat所有webapp目录下的任意文件；如网站应用支持上传，攻击者可上传内含恶意JSP文件，利用Ghostcat漏洞执行
- 漏洞复现（[参考](https://my.oschina.net/u/4411093/blog/3240327/print)）
- 修复方案
   - 应用不涉及使用AJP协议
      - 方式一：tomcat配置server.xml注释
         - <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
      - 方式二：iptables封禁8009端口： ``iptables -A INPUT -p tcp --dport 8009 -j DROP` 
   - 涉及Tomcat版本：9.0.31以上或8.5.51以上或7.0.100以上；并配置secret中AJP协议认证凭证
<a name="4qG2r"></a>
## 99.FAQ
<a name="LsPYP"></a>
### 1.Tomcat启动报错:At least one JAR was scanned for TLDs yet contained no TLDs
> org.apache.jasper.servlet.TldScanner.scanJars At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.

- 编辑conf/catalina.properties
   - 将tomcat.util.scan.StandardJarScanFilter.jarsToSkip的值变更为*.jar
   - 作用忽略jar的TLDs扫描
<a name="xUHCz"></a>
### 2.Tomcat8启动加载十几分钟或更长

- 熵池阻塞：[参考](https://blog.csdn.net/chszs/article/details/49494701) | [/dev/random和/dev/urandom区别](https://blog.csdn.net/weixin_38239856/article/details/81979959)
- Tomcat环境解决
   - 编辑bin/catalina.sh
      - 在JAVA_OPTS=".."中追加 `-Djava.security.egd=file:/dev/./urandom`
- Java黄精解决
   - 编辑$JAVA_PATH/jre/lib/security/java.security
      - 替换securerandom.source值为 `file:/dev/urandom` 
<a name="9ikN0"></a>
### 3.Tomcat配置Context并设置项目为根目录会加载项目两次

- 问题原因
   - <Host>标签属性配置unpackWARs和autoDeploy为true
   - <Host>标签属性appBase路径与<Host>子标签<Context>属性docBase为上下级目录关系（就是说指定项目在appBase内）
- 问题原理
   - Tomcat启动时，会将webapps目录下的所有项目部署
   - 再根据Context配置部署指定路径的项目
- 解决方法
   - 将<Host>下的<Context>配置的docBase目录改为绝对路径，且不为webapps下即可
