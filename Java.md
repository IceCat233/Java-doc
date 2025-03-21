# Java学习

## 静态 static修饰成员的特点

![image-20250227144846893](https://gitee.com/icecat2233/picture/raw/master/20250321161353509.png)

## 运算符

### 扩展赋值运算符

扩展赋值运算符，内部自带强转效果

![image-20250227150015125](https://gitee.com/icecat2233/picture/raw/master/20250321161402334.png)

### 关系运算符

![image-20250227150114816](https://gitee.com/icecat2233/picture/raw/master/20250321161407355.png)

![image-20250227150145972](https://gitee.com/icecat2233/picture/raw/master/20250321161413451.png)

![image-20250227151132676](https://gitee.com/icecat2233/picture/raw/master/20250321161419490.png)

不用记，若想让哪个先运算，只需加小括号

## 成员变量和局部变量的区别

![image-20250303150638312](https://gitee.com/icecat2233/picture/raw/master/20250321161432068.png)

## this关键字

<img src="https://gitee.com/icecat2233/picture/raw/master/20250321161439257.png" alt="image-20250303152002372" style="zoom:67%;" />

## 标准Javabean

![image-20250303161759800](https://gitee.com/icecat2233/picture/raw/master/20250321161447983.png)

## String类的特点

![image-20250306160712424](https://gitee.com/icecat2233/picture/raw/master/20250321161455651.png)

### String类截取方法

![image-20250307151219381](https://gitee.com/icecat2233/picture/raw/master/20250321161500034.png)

![image-20250307153940677](https://gitee.com/icecat2233/picture/raw/master/20250321161506006.png)

## StringBuilder的特点

### 构造方法和介绍

![image-20250307163606184](https://gitee.com/icecat2233/picture/raw/master/20250321161512641.png)

### 提高了字符串的效率

![image-20250307154712819](https://gitee.com/icecat2233/picture/raw/master/20250321161519952.png)

### 常用的成员方法

![image-20250307163441799](https://gitee.com/icecat2233/picture/raw/master/20250321161529510.png)



### StringBuilder和StringBuffer区别

成员方法一致

但是StringBuilder多线程不安全但效率偏高

StringBuffer多线程安全但效率偏低

## ArrayList集合

![image-20250311170523666](https://gitee.com/icecat2233/picture/raw/master/20250321161549694.png)

![image-20250311170433866](https://gitee.com/icecat2233/picture/raw/master/20250321161545631.png)

### ArrayList集合成员方法

![image-20250312180718819](https://gitee.com/icecat2233/picture/raw/master/20250321161718414.png)

## extends继承

![image-20250317154909941](https://gitee.com/icecat2233/picture/raw/master/20250321161713079.png)

注意事项：

<img src="https://gitee.com/icecat2233/picture/raw/master/20250321161708773.png" alt="image-20250317154930258" style="zoom:67%;" />

### 只支持单继承，不支持多继承，支持多层继承

例子：

<img src="https://gitee.com/icecat2233/picture/raw/master/20250321161701648.png" alt="image-20250317161000220" style="zoom: 50%;" />

不能多继承原因：如果多继承  会导致子类若执行俩父类中声明完全相同方法时，不知道会执行哪一个

## 权限修饰符

![image-20250317160532814](https://gitee.com/icecat2233/picture/raw/master/20250321161656034.png)

***其中protected***不常用访问麻烦  需要在子类中通过创建新方法然后通过super方法进行调用

## This和super

### 开闭原则：

![image-20250318161204589](https://gitee.com/icecat2233/picture/raw/master/20250321161649403.png)

例如

1.0版本有三个成员变量

1.1版本有四个成员变量

则在不修改原来代码的基础上，对原有构造方法进行重载，加上新成员变量

代码如下

```java
public A(){

this.(a,b,c)

this.d = d

}
```

### this和super

![image-20250318161614034](https://gitee.com/icecat2233/picture/raw/master/20250321161643294.png)

##  final关键字

![image-20250318163415671](https://gitee.com/icecat2233/picture/raw/master/20250321161635539.png)

### 细节补充：

![image-20250318163435173](https://gitee.com/icecat2233/picture/raw/master/20250321161630257.png)

## abstract抽象类和抽象方法

![image-20250318170528242](https://gitee.com/icecat2233/picture/raw/master/20250321161624677.png)

### 什么时候用：

把子类共性的方法抽取到父类，发现描述不清时，就可以把此方法变为抽象方法来让子类重写

### 定义格式

![image-20250318170848511](https://gitee.com/icecat2233/picture/raw/master/20250321161619634.png)

### abstract关键字冲突

final：被final修饰的方法无法进行重写

private：抽象方法需子类重写。private修饰后不能跨类调用无法重写

static：类名可调用static修饰的方法，对于抽象方法无意义

### abstract抽象类注意事项

1.不能实例化（不能创建对象）

防止调用内部方法

2.存在构造方法

通过子类super调用抽象父类构造方法

3.存在普通方法体

可以通过子类进行访问

4.抽象类的子类

要么重写所有抽象方法，要么本身就是抽象类

## 接口介绍：

接口：体现的思想是对规则的声明

**成员变量：默认被public static final所修饰，所以只能为常量**

**成员方法：默认被public abstract所修饰，只能为抽象方法*****但是JDK7 和8有一些新特性***

接口无构造方法

​           Java中更多的体现是对行为的抽象

<img src="https://gitee.com/icecat2233/picture/raw/master/20250321161613388.png" alt="image-20250319161530044" style="zoom:50%;" />

### 定义方法：

```java
interface inter{
    public abstract void a();
    public abstract void b();
}

class interfac implements inter{

​    @Override
​    public void a() {

​    }

​    @Override
​    public void b() {

​    }
}
```

没啥用  做个测试 哈哈哈哈哈 图床使用

![image-20250319174939799](https://gitee.com/icecat2233/picture/raw/master/20250319174950083.png)

## 多态：

### 前提：

1. 有继承/实现关系
2. 有方法重写
3. **父类引用指向子类对象**

​           

### 成员访问特点：

成员变量：编译看左边（父类）运行看左边（父类）

成员方法：编译看左边（父类）运行看右边（子类）

-  在编译时会检查父类中有无这个方法。无就报错，有则编译通过，但执行子类方法

- 原因：防止父类方法为抽象方法

- 多态创建对象，调用静态成员

  静态成员仅推荐用类名调用，即使通过对象名调用也是假象，生成字节码文件后会自动改为类名调用

### 好处和弊端：

拓展性！拓展性！我理解为复用性也有  代码量减少了一点

<img src="https://gitee.com/icecat2233/picture/raw/master/20250320151239316.png" alt="image-20250320151226123" style="zoom: 67%;" />

#### 多态转型：转型问题

![image-20250320153129346](https://gitee.com/icecat2233/picture/raw/master/20250320153130897.png)

![image-20250320153229495](imgh/image-20250320153229495.png)

解决方法：

instanceof类型

格式：`对象名 instanceof 类型`

判断一个对象是否是右边的引用类型

返回boolean类型的结果

## JDK8和9版本的新特性：

### JDK8中：

允许在接口定义非抽象方法，但是需要关键字default修饰，这些方法时默认方法

作用：解决接口升级问题

接口中默认方法定义格式

格式：`public default 返回值类型 方法名(参数列表){}`

重新interface接口里的默认方法时，要将标识interface接口名加在前

例如 `inter.super.method()`

#### 2:接口中允许定义static静态方法

接口中静态方法的定义格式：

格式：public static 返回值类型 方法名(参数列表){}

注意事项：

![image-20250321162816640](https://gitee.com/icecat2233/picture/raw/master/20250321162818542.png)

### JDK9中：

![image-20250321162851893](imgh/image-20250321162851893.png)

#### 为和允许定义私有方法：

![image-20250321162940062](https://gitee.com/icecat2233/picture/raw/master/20250321162941500.png)

提升复用性，减少冗余代码

## 代码块

**了解即可**

![image-20250321171212459](https://gitee.com/icecat2233/picture/raw/master/20250321171221621.png)

## 内部类：

### 成员内部类：了解

**了解即可**

翻看Java源代码会有内部类，所以得了解，无知识盲区

![image-20250321172536776](https://gitee.com/icecat2233/picture/raw/master/20250321172539305.png)

#### 内部类成员访问：

内部类中，访问外部类成员：直接访问，私有也可以

外部类中，访问内部类成员：需要创建对象访问，

![image-20250321172717338](https://gitee.com/icecat2233/picture/raw/master/20250321172718684.png)

#### 为何要学习内部类？

**封装性更好**

例如：

![image-20250321172953230](https://gitee.com/icecat2233/picture/raw/master/20250321172955117.png)

### 静态内部类：了解

### 局部内部类：了解

### 匿名内部类：必须掌握！！
