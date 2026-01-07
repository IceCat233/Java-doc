# XML

语法：

## XML约束-schema约束

本质还是一个xml文件

![image-20260106164151697](https://gitee.com/icecat2233/picture/raw/master/20260106164155129.png)

### 代码演示：

**此为xsd文件**

complexType:复杂属性

sequence：序列  后可加maxOccurs来表示元素是否可为多个

attribute：属性 后可加属性标签来约束xml标签属性有什么为什么类型是否是必需

element：元素 后写名称来标识你在xml中应有的元素

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<schema xmlns="http://www.w3.org/2001/XMLSchema"
        targetNamespace="ice.cat.home"
        elementFormDefault="qualified">
<element name="students">
    <complexType>
        <sequence maxOccurs="unbounded">
            <element name="Student">
                <complexType>
                    <sequence maxOccurs="unbounded">
                        <element name="name"></element>
                        <element name="age"></element>
                    </sequence>
                    <attribute name="id" type="string" use="required"/>
                </complexType>
            </element>
        </sequence>
    </complexType>
</element>
</schema>
```

**下方为约束效果**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<students xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
          xmlns = "ice.cat.home"
          xsi:schemaLocation="ice.cat.home schema.xsd">
<Student id="1">
    <name>张三</name>
    <age>12</age>
    <name>杏菜</name>
    <age>14</age>
</Student>
</students>
```

## 解析：

将xml文件读取到Java

### SAX解析：

![image-20260106170911320](https://gitee.com/icecat2233/picture/raw/master/20260106170912993.png)

### DOM解析：

![image-20260106170924376](https://gitee.com/icecat2233/picture/raw/master/20260106170928898.png)

**一般用DOM**

**首先导入DOM4j的jar包**

方法：

<img src="imgh/image-20260106172208442.png" alt="image-20260106172208442" style="zoom: 67%;" />

### DOM解析代码：

<img src="https://gitee.com/icecat2233/picture/raw/master/20260106172046827.png" alt="image-20260106172045711" style="zoom:150%;" />

