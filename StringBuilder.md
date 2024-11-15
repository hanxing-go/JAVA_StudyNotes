***StringBuilder的基本操作***
StringBuilder 可以看成是一个容器，创建之后里面的内容是可变的。
可以提高字符串操作的效率。 

**StringBuilder常用方法**
```java
public StringBuilder append(任意类型)
添加数据，并返回对象本身
public StringBuilder reverse()
反转容器中的内容
public int length()
返回长度（字符出现的个数）
public String toString()
通过toString()就可以实现吧StringBuider转换为String
```

***StringJoiner的基本操作***
StringJoiner跟StringBuilder一样，也可以看成是一个容器，创建之后里面的内容是可变的。

```java
public StringJoiner add(添加的内容)
添加数据，并返回对象本身
public int length()
返回长度（字符出现的个数）
public String toString()
返回一个字符串（该字符串就是拼接之后的结果）
```