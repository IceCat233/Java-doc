# 常用API

## Object类

### toString方法

`public String toString()`默认是返回当前对象再堆内存中的地址信息：类的全类名@十六进制哈希值

#### 用途：

在开发过程中直接输出对象看到对象地址是毫无意义的，更多时候是希望看到对象中的内容数据而不是假地址信息

所以toString()方法存在的意义就是为了被子类重写，以便返回对象的内容信息，而不是地址信息。

### equals方法

`public boolean equals(Object 0)`默认是比较当前对象与另一对象地址值是否相同，返回boolean类型

#### 意义：

父类equals方法存在的意义就是为了子类重写，以便于子类自己定制比较规则

**IDEA中重写的equals方法：**

```java
public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }
```

### **Objects类中的equals方法**

避免了空指针异常问题

```java
public static boolean equals(Object a, Object b) {
    return (a == b) || (a != null && a.equals(b));
}
```

双&&或者双||，都是执行左边若为false或者true则右侧不执行

![image-20250401155734366](https://gitee.com/icecat2233/picture/raw/master/20250401155745359.png)