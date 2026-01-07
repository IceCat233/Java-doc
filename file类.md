# file类

创建对象

# 相对路径绝对路径：(重点)

相对路径：相对于当前项目的路径

# File类常用方法：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251222170009271.png" alt="image-20251222170000954" style="zoom:67%;" />

# File类的创建和删除：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251222172801923.png" alt="image-20251222172800813" style="zoom:50%;" />

# File类的遍历方法：

<img src="https://gitee.com/icecat2233/picture/raw/master/20251222174209999.png" alt="image-20251222174208835" style="zoom: 50%;" />

案例展示：

寻找文件夹

```java
public class FileDemo2 {
    public static void main(String[] args) {
 getDir();
    }
    public static File getDir() {
        System.out.println("请输入要找的文件夹");
        Scanner sc = new Scanner(System.in);
        while (true) {
            String put = sc.nextLine();
            File dir = new File(put);
            if (!dir.exists()) {
                System.out.println("你输入的文件夹不存在，请重新输入");
            } else if (dir.isFile()) {
                System.out.println("你输入的是一个文件不是文件夹，请重新输入");
            } else {
                return dir;
            }
        }
    }
}
```

```java
//打印输入文件夹下所有的.java文件
public class FileDemo3 {
    public static void main(String[] args) {
        File diry = FileDemo2.getDir();
        find(diry);
    }

    private static void find(File dir) {
        //获取当前文件夹下所有文件和文件夹对象，转化为file数组形式
        File[] files = dir.listFiles();
        for (File file : files) {
            //若是文件，判断是否为.java后缀
            if (file.isFile() && file.getName().endsWith(".java")){
                System.out.println(file);
                //若是文件夹则进到下一级继续判断
            } else if (file.isDirectory()) {
                //注意事项，可能遍历的数组会返回为null
                if (file.listFiles() != null) {
                    find(file);
                }
            }
        }
    }
}
```

```java
//删除文件夹
public class FileDemo4 {
    public static void main(String[] args) {
        //谨慎测试
        deleteDir(new File("D:\\测试Java1"));
    }
    public static void deleteDir(File dir){
        File[] files = dir.listFiles();
        //遍历当前flie数组获取到每一个文件对象
        for (File file : files) {
            if (file.isFile()){
                file.delete();
                //若是文件夹，则进到里面继续删文件，运用递归
            }else if (file.isDirectory()){
                //判断数组集合是否为空
                if (file.listFiles()!=null){
                deleteDir(file);
                }
            }
        }
        dir.delete();
    }
}
```

```java
//统计文件大小
public class FileDemo5 {

    public static void main(String[] args) {
        //键盘录入文件夹路径，统计文件大小
        File dir = FileDemo2.getDir();
        int i = fileSize(dir);
        System.out.println(i);
    }
    public static int fileSize(File di){
        int size = 0;
        //遍历
        File[] files = di.listFiles();
        for (File file : files) {
            //判断是否是文件
            if (file.isFile()){
           int a = (int)file.length();
           size+=a;
            }else {
                if (file.listFiles() != null){
                    size += fileSize(file);
                }
            }
        }
        return size;
    }
}
```