# try-with-resource

新增异常处理机制

- 原理：编译期自动帮助生成finally块，并调用对应声明资源的close方法；同时解决可能隐藏的异常屏蔽问题（将close方法关闭可能抛出的异常加载到上一个异常中）



<a name="b9h8f"></a>
### JDK7之前关闭资源
```java
InputStream is = null;
OutputStream os = null;
try {
    is = new FileInputStream(new File("a.txt"));
    os = new FileOutputStream(new File("b.txt"));
    byte[] buff = new byte[1024];
    for (int count; (count = is.read(buff)) != -1; ) {
        os.write(buff, 0, count);
    }
} catch (Exception e) {
    ioe.printStackTrace();
} finally {
    if (is != null) {
        try { is.close() } catch (Exception e) { }
    }
    if (os != null) {
        try { os.close() } catch (Exception e) { }
    }
}
```
<a name="QaGqy"></a>
### JDK7新增特性
```java
try (InputStream is = new FileInputStream(new File("a.txt"));
     OutputStream os = new FileOutputStream(new File("b.txt"))) {
    byte[] buff = new byte[1024];
    for (int count; (count = is.read(buff)) != -1; ) {
        os.write(buff, 0, count);
    }
} catch (Exception e) {
    e.printStackTrace();
}
```

- 编译文件反编译
```java
try {
    InputStream is = new FileInputStream(new File("a.txt")); 
    Throwable localThrowable6 = null;
    try { 
        OutputStream os = new FileOutputStream(new File("b.txt"));
        Throwable localThrowable7 = null;
        try {
            byte[] buff = new byte[1024];
            int count;
            while ((count = is.read(buff)) != -1)
                os.write(buff, 0, count);
        } catch (Throwable localThrowable1) {
            localThrowable7 = localThrowable1;
            throw localThrowable1;
        } finally {
            if (os != null)
                if (localThrowable7 != null)
                    try {
                        os.close();
                    } catch (Throwable localThrowable2) {
                        localThrowable7.addSuppressed(localThrowable2);
                    }
            else
                os.close();
        }
    } catch (Throwable localThrowable4) {
        localThrowable6 = localThrowable4;
        throw localThrowable4;
    } finally {
        if (is != null)
            if (localThrowable6 != null)
                try {
                    is.close();
                } catch (Throwable localThrowable5) {
                    localThrowable6.addSuppressed(localThrowable5);
                } 
        else 
            is.close();
    }
} catch (Exception e) {
    e.printStackTrace();
}
```


<a name="rUwtF"></a>
### try使用注意点

- finally块中存在return语句，则try/catch块中的return会被忽略；同时会忽略上述两个块的异常信息，即异常屏蔽
- finally块中应避免捕获或抛出异常
