# IO流体系结构

<img src="https://gitee.com/icecat2233/picture/raw/master/20251223143732944.png" alt="image-20251223143723814" style="zoom: 50%;" />

# 字节流：

## FileOutPutStream 字节输出流

### 构造方法和成员方法和注意事项：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251223145353953.png" alt="image-20251223145352942" style="zoom:67%;" />

### 成员方法

![image-20251223145424559](https://gitee.com/icecat2233/picture/raw/master/20251223145427575.png)

### IO流的异常处理方式

![image-20251223151208770](https://gitee.com/icecat2233/picture/raw/master/20251223151210250.png)

示例：

```JAVA
public static void main(String[] args) throws IOException {
    //记住输出流一定要关闭，使用try catch保证不管如何都会执行关闭
    //创建字节输出流对象是，可以传两个参数第一个是字符串或者是file对象，第二个是打开或关闭复写的开关
    //try小括号里的对象必须实现了AutoCloseAble接口
    try (FileOutputStream fos = new FileOutputStream("D:\\A.txt",true);){
        fos.write(97);
        fos.write(97);
        fos.write("八奈见杏菜".getBytes());
    }catch (IOException e){
        e.printStackTrace();
    }
}
```

## FileInPutStream字节输入流：

### 构造和成员方法：

![image-20251223162029993](https://gitee.com/icecat2233/picture/raw/master/20251223162031046.png)

## 案例：copy数据：

```Java
/**
拷贝文件
 */
public static void main(String[] args) throws IOException {
    //创建输入流对象读取要复制的数据
    FileInputStream fis = new FileInputStream("C:\\Users\\asus\\Pictures\\老八.jpg");
    byte[] bys= new byte[1024];//定义一个空字节数组用来装数据
    //创建输出流对象粘贴读取的数据
    FileOutputStream fos= new FileOutputStream("D:\\老八.jpg");
    int len;
    while ((len = fis.read(bys)) != -1){
        fos.write(bys,0, len);
    }
    //记得关闭流
        fis.close();
        fos.close();
}
```

## 字节缓冲流：（未听）

# 小知识点：字符编码：

![image-20251223171153656](https://gitee.com/icecat2233/picture/raw/master/20251223171154676.png)

## 编码和解码：

![image-20251223171247753](https://gitee.com/icecat2233/picture/raw/master/20251223171249689.png)

## 总结：（可记）

<img src="https://gitee.com/icecat2233/picture/raw/master/20251223171936927.png" alt="image-20251223171919671" style="zoom:50%;" />

# FileWriter字符输出流

## **成员方法**：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251223173014161.png" alt="image-20251223173006416" style="zoom: 50%;" />

# 字符缓冲流：

## 构造方法：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224164934256.png" alt="image-20251224164929596" style="zoom: 50%;" />

## 特有成员方法：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224165014103.png" alt="image-20251224165012852" style="zoom:50%;" />

## 重点：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224164902592.png" alt="image-20251224164854046" style="zoom:50%;" />

## 案例：

三组对象写入文件后读取文件并封装成对象打印

```Java
public static void main(String[] args) throws IOException {
    Student stu1 = new Student("杏菜",15);
    Student stu2 = new Student("梦子",16);
    Student stu3 = new Student("佳树",17);
    BufferedWriter bw = new BufferedWriter(new FileWriter("D:\\测试.txt"));
    bw.write(stu1.getName()+"-"+stu1.getAge());
    bw.newLine();
    bw.write(stu2.getName()+"-"+stu2.getAge());
    bw.newLine();
    bw.write(stu3.getName()+"-"+stu3.getAge());
    bw.newLine();
    //写入程序三组数据
    bw.close();
    //读取三组数据
    BufferedReader br = new BufferedReader(new FileReader("D:\\测试.txt"));
    String line;
    while ((line = br.readLine()) != null){
        String[] split = line.split("-");
        Student stu = new Student(split[0],Integer.parseInt(split[1]));
        System.out.println(stu);
    }
}
```

# 转换流：

## 作用：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224171828583.png" alt="image-20251224171827438" style="zoom:50%;" />

## 总结：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224171551986.png" alt="image-20251224171550851" style="zoom:50%;" />

# 序列化流：

## 构造方法：

![image-20251224172353234](https://gitee.com/icecat2233/picture/raw/master/20251224172354411.png)

## 序列化流的操作：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224173737299.png" alt="image-20251224173735968" style="zoom: 50%;" />

## 注意事项：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224173938954.png" alt="image-20251224173937811" style="zoom:50%;" />

**transient 瞬态关键字类中某些成员变量不想被序列化操作即可加上此关键字**

## 注意：要是序列化多次对象，有两种方式

**try catch捕获异常，来结束循环**

```Java
public static void main(String[] args) throws IOException, ClassNotFoundException {
    ObjectInputStream ois = new ObjectInputStream(new FileInputStream("D:\\a.txt"));
    while (true){

        try {
            Object o = ois.readObject();
            System.out.println(o);
        } catch (EOFException O) {
            break;
        }
    }
    ois.close();
}

private static void write() throws IOException {
    Student stu1 = new Student("杏菜",15);
    Student stu2 = new Student("佳树",16);
    Student stu3 = new Student("梦子",17);
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("D:\\a.txt"));
    oos.writeObject(stu1);
    oos.writeObject(stu2);
    oos.writeObject(stu3);
    oos.close();
}
```

**只序列化一次，将对象装入一个集合中，读取和写入只进行一次**

```java
public static void main(String[] args) throws IOException, ClassNotFoundException {
    //运用集合，使其只读取（序列化和反序列化一次）
    ObjectInputStream ois = new ObjectInputStream(new FileInputStream("D:\\a.txt"));
    ArrayList<Student> list = (ArrayList<Student>) ois.readObject();
    for (Student student : list) {
        System.out.println(student);
    }
    ois.close();
}

private static void write() throws IOException {
    Student stu1 = new Student("杏菜", 15);
    Student stu2 = new Student("佳树", 16);
    Student stu3 = new Student("梦子", 17);
    //创建一个集合将对象装入集合并序列化操作一次写入文件
    ArrayList<Student> list = new ArrayList<>();
    Collections.addAll(list, stu1, stu2, stu3);
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("D:\\a.txt", true));
    oos.writeObject(list);
    oos.close();
}
```

# 打印流：

## 基本使用：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251224184742093.png" alt="image-20251224184740951" style="zoom: 67%;" />

 

<img src="https://gitee.com/icecat2233/picture/raw/master/20251226154205072.png" alt="image-20251226154156446" style="zoom:50%;" />

## 字符打印流：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251226154313700.png" alt="image-20251226154307707" style="zoom:50%;" />

# properties

## 和io有关的方法：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251226162808390.png" alt="image-20251226162807035" style="zoom: 67%;" />

**本质是一个map集合**

## 总结： 

<img src="https://gitee.com/icecat2233/picture/raw/master/20251226162640827.png" alt="image-20251226162638992" style="zoom: 50%;" />