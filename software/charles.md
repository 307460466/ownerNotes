# Charles

<a name="dNFZf"></a>
## 原理
- 中间人攻击（MITM）：攻击者与通讯的两端分别建立独立的联系，并交换其所收到的数据，使通讯的两端认为他们正通过一个私密的连接与对方直接对话，但事实上整个会话都被攻击者完全控制。
- 安装文件：[Charles 64位_4.2.7.4.msi](https://yuque.antfin.com/attachments/lark/0/2020/msi/118172/1591951771573-9a58375d-837a-40d5-b37f-52d6ebd2d157.msi?_lake_card=%7B%22uid%22%3A%221591951764878-0%22%2C%22src%22%3A%22https%3A%2F%2Fyuque.antfin.com%2Fattachments%2Flark%2F0%2F2020%2Fmsi%2F118172%2F1591951771573-9a58375d-837a-40d5-b37f-52d6ebd2d157.msi%22%2C%22name%22%3A%22Charles+64%E4%BD%8D_4.2.7.4.msi%22%2C%22size%22%3A67894272%2C%22type%22%3A%22%22%2C%22ext%22%3A%22msi%22%2C%22progress%22%3A%7B%22percent%22%3A99%7D%2C%22status%22%3A%22done%22%2C%22percent%22%3A0%2C%22id%22%3A%22t5s5C%22%2C%22card%22%3A%22file%22%7D)



<a name="kNYaW"></a>
## 快速开始
<a name="Z9ejx"></a>
### 本地电脑抓包

- 安装charles证书：【Help】-【SSL Proxying】-【Install Charles Root Certificate】
   - 【所有的证书都放入下列存储】-【浏览】-【受信任的根证书颁发机构】-【下一步....】
- 重启电脑以便证书生效

<br />
<a name="vl21I"></a>
### 透明代理配置
<a name="FO812"></a>
#### Http代理

- 【Proxy】-【Proxy Settings】设置代理端口及启用Http代理

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/118172/1563780210800-8a88a919-b574-45ac-b99b-93b3760398fe.png#align=left&display=inline&height=477&margin=%5Bobject%20Object%5D&name=image.png&originHeight=477&originWidth=569&size=63719&status=done&style=none&width=569)

<a name="616N8"></a>
#### Https代理

- 【Proxy】-【SSL Proxying Settings】-【SSL Proxying】
   - 启用【SSL Prxying】
   - 配置对应的Https代理【Add】（所有则Hosts设置为*）<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/118172/1607507005903-25566911-1e86-4497-b2fc-c319a70de388.png#align=left&display=inline&height=206&margin=%5Bobject%20Object%5D&name=image.png&originHeight=206&originWidth=438&size=10516&status=done&style=none&width=438)



<a name="C5ad9"></a>
### 移动端代理

- 移动端与桌面端处于同一个局域网内
- 桌面端确认移动端需要填写的代理信息（IP和Port）
   - 【Help】-【SSL Proxying】-【Install Charles Root Certificate on a Mobile Device or Remote Broser】![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/118172/1607507400658-4fb073f1-7470-41c1-96e9-fc247e910c97.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=image.png&originHeight=158&originWidth=539&size=15005&status=done&style=none&width=539)
- 移动端在WIFI配置中填写对应手动代理信息
   - 访问【chls.pro/ssl】，下载并安装证书
      - 安卓：【设置】中手动添加信任证书（Https另外处理）
      - IOS：无测试机参考百度



<a name="7yDvY"></a>
## FAQ
<a name="Zark9"></a>
### Android HTTPS抓包报错：SSL Handshanke:Recevied fatal alert unknown_ca

- [Android 7.0版本以上 && targetSdkVersion >= 24](https://android-developers.googleblog.com/2016/07/changes-to-trusted-certificate.html)，只信任系统证书（即用户证书不被信任）
   - Root Android手机，将Charles证书放到系统证书内
   - 将APP的公秘钥导入Charles中（具备APP开发权限）
   - [APP编译为信任用户证书的版本](https://developer.android.google.cn/training/articles/security-config.html)（具备APP开发权限）
   - 使用[Xposed](https://www.jianshu.com/p/01a9e86581b9)的JustTrustMe模块信任所有证书
   - 使用沙箱应用
<a name="Wa9sz"></a>
### 移动端无法连接桌面端代理（Win）

- 现象：移动端访问chls.pro/ssl，无提示证书下载/保存
- 确认防火墙是否拦截
   - 【控制面板】-【所有控制面板项】-【Windows Defender 防火墙】-【允许的应用】
   - 确认是否存在【Charles Web Debbuging Proxy】，且是否勾选，对应（专用/共用）网络是否符合环境
