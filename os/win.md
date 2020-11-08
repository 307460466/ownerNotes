# Windows系统相关FAQ

## 图标显示不正常

- 原因：win10系统为加速图标的显示，会在文件图标第一次显示时，进行缓存，后续显示图标会直接从缓存中读取数据
- 思路：缓存文件出现问题，则清除缓存重新构建即可
- 方法

1. 资源管理器中勾选【查看】-【隐藏的项目】
2. 【Win + R】执行命令：`%localappdata%` 
3. 在打开的文件夹中找到【Iconcache.db】文件，并将其删除
4. 打开任务管理器，找到【Windows资源管理器】右键【重新启动】即可