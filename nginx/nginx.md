# Nginx

<a name="OwbsR"></a>
## 参考文档
[Nginx配置文件详解](https://www.cnblogs.com/54chensongxia/p/12938929.html) | [配置文件](https://www.cnblogs.com/bluestorm/p/4574688.html)<br />

<a name="t3R3a"></a>
## 常用命令
```bash
# 启动nginx
$ nginx
# 关闭nginx
$ nginx -s stop
# 检测配置文件是否有误
$ nginx -t
# 重新加载配置文件
$ nginx -s reload
# 查看nginx版本
$ nginx -v
```


<a name="aWLQd"></a>
## 配置文件

- nginx.conf
   - 由四部分组成：main（全局配置）、server（主机配置）、upstream（上游服务器配置，如反向代理、负载均衡等）、location（URL匹配特定位置配置）
      - main指定为全局有效
      - server指令用于指定虚拟主机詺、IP、端口
      - upstream指令用于后端服务器设置反向代理及负载均衡
      - location用于匹配网页位置（根目录等）
   - location继承server，server继承main，upstream独立
```nginx
# 可运行nginx服务的用户和用户组
# nobody或注释掉,则所有用户可运行(win不生效)
user nginx;
# worker工作进程个数,master进程负责接收并分配请求给woker处理
# 通常为cpu核数,如开启SSL/GZIP则设置为逻辑CPU数量一样或2倍
# worker_processes number | auto;
worker_processes 2;

# 错误日志的路径及日志级别
# error_log [path] [debug | info | notice | warn | error | crit | alert | emerg]
error_log logs/error.log;
#error_log logs/error.log notice;
#error_log logs/error.log info;

# nginx进程pid存放路径
pid logs/nginx.pid;

# 设置nginx服务与用户的网络连接
events {
  # 是否开启nginx进程接收连接序列化（防止多个进程争抢连接）,默认开启
  # accept_mutex on;
  # 指定网络IO模型,可选[select | poll | kqueue | epoll | rtsig | /dev/poll | eventport]
  # 默认使用epoll事件模型
  #use epoll;
  # 每个worker进程并发处理最大连接数
	worker_connections 1024;
}

# http服务相关配置
http {
  # 包含其他配置文件
	include mime.types;
  # 配置默认类型,默认text/plain
	default_type application/octet-stream;
  # 服务版本是否隐藏，默认on
  server_tokens off;
  
  # nginx服务器提供服务过程应答前端请求的日志
  # 关闭access_log
  #access_log off;
  # 日志格式设置
  #		$remote_add与$http_x_forwarded_for：记录客户端IP
  #		$remote_user：记录客户端用户名称
  #		$time_local：记录访问时间与时区
  #		$request：记录请求url与http协议
  #		$status：记录请求状态
  #		$body_bytes_send：记录发送给客户端文件主体内容大小
  #		$http_referer：记录从哪个页面链接访问
  #		$http_user_agent：记录客户浏览器相关信息
  #log_format main '$remote_addr - $remote_user [$time_local] "$request" '
  # '$status $body_bytes_sent "$http_referer" '
  # '"$http_user_agent" "$http_x_forwarded_for"';
  # 访问日志,需设置log_format
	#access_log logs/access.log main;
  
  # 是否开启高效文件传输模式（减少用户控件到内核控件的上下文切换）
  sendfile on;
  # sendfile最大数据量,默认0（无限制）
  # sendfile_max_chunk 0；
  # 是否允许socket的TOP_CORK选项
  # tcp_nopush on;
 
  # 长连接超时时间（秒）
	keepalive_timeout 65;
  # 指定响应客户端超时时间
  # send_timeout 60;
  # 允许客户端请求的最大单文件字节数
  client_max_body_size 10m;
  # 缓冲区代理缓冲客户端请求的最大字节数
  client_body_buffer_size 128k;
  
  # gzip压缩功能设置
  # 是否开启gzip压缩
  gzip on;
  # 允许压缩的页面最小字节数（默认20，建议大于等于1k，取值content-length判断）
  gzip_min_length 1k;
  # 设置系统获取几个单位的缓存用于存储gzip的压缩结果数据流; 4 16k，以16K为单位，申请4倍单位的内存
  gzip_buffers 4 16k;
  # 识别http协议版本
  gzip_http_version 1.0;
  # gzip压缩比
  gzip_comp_level 6;
  # 匹配mime类型进行压缩
  gzip_types text/html text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml;
  # 允许让前端缓存服务器经过gzip压缩页面
  gzip_vary on;
  
  # http_proxy 设置（反向代理/缓存）
  # 代理连接超时时间
  proxy_connect_timeout 75;
  proxy_send_timeout 75;
  # 代理接收超时时间
  proxy_read_timeout 75;
  # 从后端服务读取并保存用户头信息的缓冲区大小（默认与proxy_buffers相同）
  proxy_buffer_size 4k;
  # 缓冲区大小
  proxy_buffers 4 32k;
  # 高负荷下缓冲大小（proxy_buffers * 2）
  proxy_busy_buffers_size 64k;
  # 缓存倍代理的服务器响应到临时文件时,限制每次临时文件写入大小
  proxy_temp_file_write_size 64k;
  proxy_temp_path /usr/local/nginx/proxy_temp 1 2;

  # 设定负载均衡后台服务器列表
  upstream backend {
    # weight权重,权值越高被分配的几率越高
    # upstream支持4中分配方式
    # 1.轮询（默认）：每个请求按时间顺序逐一分配到不同server,server发生down会自动剔除
    # 2.weight：指定轮询几率，weight与访问几率成正比（server性能不均情况）
    #		server 192.168.0.14:8080 weight=10;
    #		server 192.168.0.15:8080 weight=10;
    # 3.ip_hash：每个请求按访问IP的hash结果分配，访客固定server（解决session问题）
    # 	ip_hash;
    #		server 192.168.0.14:8080;
    #		server 192.168.0.15:8080;
    ip_hash;
    server 192.168.10.100:8080 max_fails=2 fail_timeout=30s ;
    server 192.168.10.101:8080 max_fails=2 fail_timeout=30s ;
  }
  
  # 虚拟机配置,每个虚拟机对应一个server配置
  server {
    # 监听端口,默认80
    # 127.0.0.1:8000; 只监听来自127.0.0.1:8000的请求
    # localhost:8000;	效果同上
    # 127.0.0.1;	只监听127.0.0.1的请求（不指定端口默认80）
    # 8000;	监听所有IP:8000的请求
    # *:8000;	效果同上
    listen 80;
    # 服务器名 域名多个则以空格分隔
    server_name localhost;
		# 字符集设置
    #charset utf-8;
    access_log logs/host.access.log main;
  
    #对 / 所有做负载均衡+反向代理
    location / {
      # 定义服务器默认网站根目录位置
      root /apps/oaapp;
      # 定义路径下默认访问的文件名
      index index.jsp index.html index.htm;

     	# 请求转向指定的服务器列表（反向代理,对应upstream负载均衡器）或ip:port
      proxy_pass http://127.0.0.1:8080;
      #proxy_redirect off;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      # 后端的Web服务器可以通过X-Forwarded-For获取用户真实IP
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;

    }
  
    #静态文件，nginx自己处理，不去backend请求tomcat
    location ~* /download/ {
    	root /apps/oa/fs;
    }
    
    # 静态资源缓存时间设置
    location ~ .*\.(gif|jpg|jpeg|bmp|png|ico|txt|js|css)$
    {
      root /apps/oaapp;
      expires 7d;
    }
    
    # 访问控制模块（顺序匹配）
    location /nginx_status {
      stub_status on;
      access_log off;
      allow 192.168.10.0/24;
      deny all;
    }

    location ~ ^/(WEB-INF)/ {
    	deny all;
    }
    
    # 错误跳转页面
    #error_page 404 /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
    	root html;
    }
  }
  
  # Https Server
  #server {
  	# https监听端口
  	#listen 443 ssl;  
    # 域名
    #server_name localhost;
    
    # ssl证书
    #ssl_certificate /etc/nginx/ssl/ssl.crt;
    # 私钥位置
    #ssl_certificate_key /etc/nginx/ssl/ssl.rsa;
  #}
}
```
