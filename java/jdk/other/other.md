# JDK Other

<a name="tfxw4"></a>
### 1.参考文档

<a name="KGljG"></a>
### 2.获取系统环境变量和进程变量
<a name="Xjfxv"></a>
#### 1）获取系统环境变量
当前用户主目录下的 `./.bashrc` 文件

- `Map<String, String> System.getEnv()` ：获取所有系统环境变量
- `String System.getEnv(String name)` ：获得指定的系统环境变量值

| 常用系统变量Key        | 描述                             |
| ---------------------- | -------------------------------- |
| USERPROFILE            | 当前用户目录                     |
| USERDNSDOMAIN          | 用户域                           |
| PATHEXT                | 可执行后缀                       |
| JAVA_HOME              | java安装目录                     |
| TEMP                   | 用户临时文件目录                 |
| SystemDrive            | 系统盘符                         |
| ProgramFiles           | 默认程序目录                     |
| USERDOMAIN             | 账户的域的名称                   |
| ALLUSERSPROFILE        | 用户公共目录                     |
| SESSIONNAME            | Session名称                      |
| TMP                    | 临时目录                         |
| Path                   | path环境变量                     |
| CLASSPATH              | classpath环境变量                |
| PROCESSOR_ARCHITECTURE | 处理器体系机构                   |
| OS                     | 操作系统类型                     |
| PROCESSOR_LEVEL        | 处理级别                         |
| COMPUTERNAME           | 计算机名                         |
| Windir                 | 系统安装目录                     |
| SystemRoot             | 系统启动目录                     |
| USERNAME               | 用户名                           |
| ComSpec                | 命令行解释器可执行程序的准确路径 |
| APPDATA                | 应用程序数据目录                 |

<a name="s83KN"></a>
#### 2）获取进程变量

- `Properties getProperties()` 
- `String getProperty(String key)` 

| 常用进程变量Key    | 描述                   |
| ------------------ | ---------------------- |
| java.version       | Java运行时环境版本     |
| java.vendor        | Java运行时环境供应商   |
| java.home          | Java安装目录           |
| java.vm.version    | Java虚拟机实现版本     |
| java.vm.name       | Java虚拟机实现名称     |
| java.class.version | Java类格式版本号       |
| java.lcass.path    | Java类路径             |
| java.library.path  | 加载库时搜索的路径列表 |
| java.io.tmpdir     | 默认的临时文件路径     |
| java.compiler      | JIT编译器名称          |
| java.ext.dirs      | 一个或多个扩展目录路径 |
| os.name            | 操作系统名称           |
| os.arch            | 操作系统架构           |
| os.version         | 操作系统版本           |
| file.separator     | 文件分隔符             |
| path.separator     | 路径分隔符             |
| line.separator     | 行分隔符               |
| user.name          | 用户账号名称           |
| user.home          | 用户主目录             |
| user.dir           | 用户的当前工作目录     |


