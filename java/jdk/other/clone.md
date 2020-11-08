# 拷贝

拷贝是针对一个已有对象的操作

- 深拷贝和浅拷贝是在引用类型的复制操作不同的区分
   - 浅拷贝对引用类型的属性只进行引用传递
   - 深拷贝对引用类型的属性创建新对象并复制其内部成员变量
<a name="uKvRj"></a>
### 浅拷贝

- 对基本数据类型的属性：值传递
- 对引用类型的属性：引用传递（指向同一引用地址，改变一个会同时影响另一个）
<a name="fgUWp"></a>
### 深拷贝

- 对基本数据类型的属性：值传递
- 对引用类型的属性：新建对象，并拷贝其属性（引用地址不同，改变一个不会影响另一个）
- 性能开销较浅拷贝大



<a name="XdRyO"></a>
### 浅拷贝的使用
被调用对象实现Cloneable接口，并调用clone方法即可
<a name="QgLnM"></a>
### 深拷贝的使用

- 被调用对象及其引用类型的类都实现Cloneable接口
- 被拷贝对象实现Serializable接口，通过序列化实现返回新对象