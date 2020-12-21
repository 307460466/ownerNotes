# Chrome

<a name="jZAuz"></a>
## FAQ
<a name="GneS5"></a>
### 访问任何网页提示【喔唷 崩溃啦】

- Win7升级Win10，次日开启电脑触发上述问题
- 解决办法
   - 打开注册表编辑器（regedit）,找到路径【HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome】，在右侧窗口【新建】-【DWORD（32位）】
      - 名称：RendererCodeIntegrityEnabled
      - 值：0
   - 重启Chrome即可
<a name="Nu4KQ"></a>
### 80版本以上，请求第三方未携带Cookie问题
参考：[Chrome 80新Cookie策略](https://zhuanlan.zhihu.com/p/103420328) | [SameSite属性](http://www.ruanyifeng.com/blog/2019/09/cookie-samesite.html)<br />场景：本地localhost请求DEV机器，发现未携带Cookie信息，导致无法本地调试<br />本地调试解决办法：

- 访问 `chrome://flags` 
   - 关闭下列两项功能（默认是default -> disabled）
      - SameSite by default cookies
      - Cookies without Samesite must be secure

线上解决：

- 对Cookie设置SameSite配置（未设置则默认为LAX，GET无影响）
   - SameSite如设置NONE，还需要设置Secure；同时三方网站调用时必须使用HTTPS
<a name="Y4NKm"></a>
### 本地联调开发机浏览器提示跨域（CORS）
参考：[chrome浏览器跨域安全策略关闭](https://www.cnblogs.com/laden666666/p/5544572.html)

- 新建目录：D:\userData
- chrome快捷方式设置：【属性】-【目标】
   - 在最后追加参数
```
 --disable-web-security --user-data-dir=D:\userData
```

- 关闭chrome浏览器，重新打开
   - 提示：不受支持的命令行标记：--disable-web-security
