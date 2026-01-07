# 日志

## 日志框架

![image-20260104152029322](https://gitee.com/icecat2233/picture/raw/master/20260104152038794.png)

![image-20260104152046997](https://gitee.com/icecat2233/picture/raw/master/20260104152050886.png)

# 枚举

**一般用作信息的标记和分类**

![image-20260104152756174](https://gitee.com/icecat2233/picture/raw/master/20260104152757423.png)

## 枚举的特点

<img src="https://gitee.com/icecat2233/picture/raw/master/20260104153711421.png" alt="image-20260104153710216" style="zoom:50%;" />

作用：

代码优雅，可读性高，入参约束严谨

# 类加载器

**过程**

<img src="https://gitee.com/icecat2233/picture/raw/master/20260105160250925.png" alt="image-20260105160242903" style="zoom: 50%;" />

类加载器的分类

![image-20260105161129784](https://gitee.com/icecat2233/picture/raw/master/20260105161131223.png)

**双亲委派模型：**



# 反射：

## 如何创建类的字节码对象：



## 反射类中的构造方法

其中返回单个构造方法对象括号中给的参数是可变参数，给的是字节码文件参数，用来代表返回的是有参构造还是无参构造，可看下边例子

![image-20260105170936519](https://gitee.com/icecat2233/picture/raw/master/20260105170937538.png)

**反射到Constructor类中后的创建对象方法**

![image-20260105171056746](https://gitee.com/icecat2233/picture/raw/master/20260105171057963.png)

其中newInstance方法中的参数代表了是走的带参构造还是无参构造

```Java
public class Demo1 {
    public static void main(String[] args) throws Exception{
        //获取类的字节码对象
        Class<?> class1 = Class.forName("com.ice.cat.domain.Student");
        //反射构造方法对象
        Constructor<?> constructor = class1.getDeclaredConstructor(String.class,int.class);//此方法无视权限返回单个所有权限的构造方法对象
        //设置为true 表示取消访问检查
        constructor.setAccessible(true);
        //通过此方法实例化，创建对象
        Object o = constructor.newInstance("杏菜",15);
        System.out.println(o);
    }
}
```

## 反射类中的成员变量：

![image-20260105173059327](https://gitee.com/icecat2233/picture/raw/master/20260105173100700.png)

## 设置成员变量的方法

![image-20260105173145296](https://gitee.com/icecat2233/picture/raw/master/20260105173146440.png)

例子：

```Java
public class Demo2 {
    public static void main(String[] args)throws Exception{
        //获取Student的字节码文件
        Class<Student> studentClass = Student.class;
        //暴力获取单个所有权限无参构造方法
        Constructor<Student> constructor = studentClass.getDeclaredConstructor();
        //取消检查权限
        constructor.setAccessible(true);
        //实例化
        Student stu1 = constructor.newInstance();
        Student stu2 = constructor.newInstance();
        //暴力反射内部成员变量
        Field name = studentClass.getDeclaredField("name");
        Field age = studentClass.getDeclaredField("age");
        //因为是暴力获取，得设置访问权限
        name.setAccessible(true);
        age.setAccessible(true);
        //通过set给成员变量赋值
        name.set(stu1,"杏菜");
        name.set(stu2,"佳树");
        age.set(stu1,15);
        age.set(stu2,13);
        System.out.println(name.get(stu1));
        System.out.println(name.get(stu2));
    }
}
```

## 反射的建议：禁止暴力反射

小知识点：Java中的泛型是假的，只有在编译期间有效

```Java
public class Test1 {
    //在一个泛型为Integer的集合里面添加一个字符串
    //思路：Java中的泛型是假的，只有在编译期间有效
    public static void main(String[] args) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        ArrayList<Integer> list = new ArrayList<>();
        Collections.addAll(list,1,2,3,4);
        Class<? extends ArrayList> class1 = list.getClass();
        Method add = class1.getMethod("add", Object.class);
        add.invoke(list,"hhh");
        System.out.println(list);
    }
}
```

# 方法引用：

<img src="https://gitee.com/icecat2233/picture/raw/master/20260106153308790.png" alt="image-20260106153259853" style="zoom:50%;" />

# Junit单元测试：

<img src="https://gitee.com/icecat2233/picture/raw/master/20260106153753082.png" alt="image-20260106153751296" style="zoom:50%;" />

## 总结：

<img src="https://gitee.com/icecat2233/picture/raw/master/20260106154608910.png" alt="image-20260106154607624" style="zoom:50%;" />