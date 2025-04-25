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

## Math类：工具类

方法都为静态方法，通过类名.的形式调用

<img src="https://gitee.com/icecat2233/picture/raw/master/20250401161501296.png" alt="image-20250401161443811" style="zoom: 50%;" />

## System类

<img src="https://gitee.com/icecat2233/picture/raw/master/20250401162215459.png" alt="image-20250401162210232" style="zoom: 50%;" />

注意：返回时间为现在时间减去1970年1月1日0时的毫秒值，为何？1970年1月1日是c语言的生日

## BigDecimal类

### 创建对象传入数据：

![image-20250403164058289](https://gitee.com/icecat2233/picture/raw/master/20250403164059630.png)

仅推荐用后两个，解决小数运算不精确的问题

### 常用成员方法

![image-20250403163929123](https://gitee.com/icecat2233/picture/raw/master/20250403163938062.png)

## 包装类

用处：将基本数据类型包装成类，变成引用数据类型

**只做Integer类的讲述，其余可以类比Integer来进行**

![image-20250403170839818](imgh/image-20250403170839818.png)

注意：从JDK5版本开始，出现了自动拆装箱技术

自动装箱：基本数据类型的变量可以直接赋值给包装类型（引用数据类型）的变量;

自动拆箱：包装类型（引用数据类型）的变量转化为基本数据类型的变量；

总结：基本数据类型和对应的包装类，可以直接运算，不用转换了

### 常用方法：

![image-20250403171301091](https://gitee.com/icecat2233/picture/raw/master/20250403171304123.png)

### 面试题

<img src="https://gitee.com/icecat2233/picture/raw/master/20250403173626000.png" alt="image-20250403173623260" style="zoom: 50%;" />

## Arrays类

数组工具类，方法都为静态方法


![image-20250404170313844](https://gitee.com/icecat2233/picture/raw/master/20250404170322675.png)

1. 其中binarySearch()方法，给予的数组必须是排好序的。因为使用了二分法

2. sort()方法中，对数组进行了默认升序排序，要进行其他顺序排序，需学习**红黑树**

   

## JDK7时间类

### Date类

<img src="https://gitee.com/icecat2233/picture/raw/master/20250410163120955.png" alt="image-20250410163119332" style="zoom:67%;" />



### SimpleDateFormat类：用于日期格式化

**将Date日期转化为易懂的形式**  我个人理解为可以将这个类作为修饰Date日期对象的类。

<img src="https://gitee.com/icecat2233/picture/raw/master/20250410163252914.png" alt="image-20250410163250157" style="zoom:67%;" />



如何使用

其中在创建日期格式化对象时，可以使用代参构造方法传入pattern,修改格式，代表元素如下图

```java
        //创建了一个日期格式化对象，使用默认模式
        SimpleDateFormat format = new SimpleDateFormat(parttern"");
        //创建日期对象，封装此刻时间
        Date date = new Date();
        //将日期对象转换为字符串
        String resul = format.format(date);
        System.out.println(resul);
```

<img src="https://gitee.com/icecat2233/picture/raw/master/20250410161300015.png" alt="image-20250410161244449" style="zoom: 67%;" />

### Calendar类：

表示一个时间的日历对象

#### 如何获取对象

`Calendar c = Calendar.getInstance();`

##### 常见方法

set 修改

get 获取  **注意获取月份时要进行+1操作**    

​                **获取星期时**

<img src="https://gitee.com/icecat2233/picture/raw/master/20250410174127785.png" alt="image-20250410174126335" style="zoom:67%;" />

add 在原有基础上添加或减少

##### 细节点：

<img src="https://gitee.com/icecat2233/picture/raw/master/20250410173853270.png" alt="image-20250410173852190" style="zoom:50%;" />

##### 案例：

```java
//键盘录入一个字符串，判断今天是今年的第几天
public class CalendarTest {
    public static void main(String[] args) throws ParseException {
        System.out.println("请输入你想要求的日期 格式\"xxxx年xx月xx日\"");
        Scanner sc =new Scanner(System.in);
        String input = sc.nextLine();

        //使用SimpleDateFormat 将日期字符串转化为日期对象
        SimpleDateFormat format = new SimpleDateFormat("yyyy年MM月dd日");
        Date riqi = format.parse(input);
        
        //将日期对象转化为Calendar对象
        Calendar c = Calendar.getInstance();
        c.setTime(riqi);
        
        //使用get方法获取第几天
        int day = c.get(Calendar.DAY_OF_YEAR);
        System.out.println("今天是这一年的第"+day+"天");
    }
}
```

## JDK8版本后时间类（常用）

### 日历类 LocalDateTime

如何将字符串转化为日期对象：

**注意：尽量将格式化中的MM月dd日等只写一个字符，要不然容易报错**

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411171745728.png" alt="image-20250411171744338" style="zoom:80%;" />

```Java
LocalDate date = LocalDate.parse(birthday, DateTimeFormatter.ofPattern("yyyy年M月d日"));
```

如何格式化日期对象

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411171614157.png" alt="image-20250411171612632" style="zoom: 80%;" />

```java
DateTimeFormatter.ofPattern("yyyy年M月d日")
```

#### 创建对象？

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411163642595.png" alt="image-20250411163640532" style="zoom:50%;" />

**LocalDate time举例  LocalTime  LocalDateTime三者方法一致**

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411163543670.png" alt="image-20250411163541466" style="zoom:50%;" />

#### 注意点：

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411163358361.png" alt="image-20250411163349987" style="zoom: 50%;" />



### instant时间戳类

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411165138747.png" alt="image-20250411165137534" style="zoom:50%;" />

### ZoneDateTime 带时区的时间对象

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411165733292.png" alt="image-20250411165732086" style="zoom:50%;" />

### Zoneld类(时区类)

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411165031419.png" alt="image-20250411165030046" style="zoom:50%;" />

### 时间中的工具类：ChronUnit

<img src="https://gitee.com/icecat2233/picture/raw/master/20250411171007818.png" alt="image-20250411171004330" style="zoom: 67%;" />

## 基本算法：

### 1:冒泡排序

```java
/**
 * 冒泡排序 相邻两数据作比较，前者大于后者则做交换，往后进行
 */
public class Bubbling {
    public static void main(String[] args) {
        int[] arr = {3,2,1,6,4,7,10,1};
        //外循环控制比较的轮数
        for (int i = 0; i < arr.length - 1; i++) {
            //比较的次数
            //-1是避免索引越界
            //-i 是对内存做优化 不用每次都比较到最后减少循环次数
            for (int j = 0; j < arr.length - 1 - i; j++) {
                if(arr[j] > arr[j+1]){
                    int temp;
                    temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}
```

### 2:选择排序

让数组中第一个数据依次和后面的数据作比较，和数据小的做交换，然后再第二个，第三个，最后完成从小到大的排序

```Java
public class SelectSort {
    //选择排序，让数组中第一个数据依次和后面的数据作比较，和数据小的做交换，然后再第二个，第三个，最后完成从小到大的排序
    public static void main(String[] args) {
        int[] arr = {22,11,33,33,44,55,14};
        for (int i = 0; i < arr.length - 1; i++) {
            //外循环，控制第几个数据和后面数据做比较
            for (int j = i+1; j < arr.length; j++) {
                //内循环：控制第一个数据和后数据依次比较
                if (arr[i] > arr[j]){
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}
```

### 3:二分查找

<img src="https://gitee.com/icecat2233/picture/raw/master/20250406171300941.png" alt="image-20250406171252031" style="zoom: 50%;" />

**使用场景：查找有序数组中对应元素的索引可以用二分查找。**

定义三个元素，最大索引，最小索引，中间索引，将中间索引指向元素和目标数据比较，中间索引元素大则右边以及中间索引元素本身则不用在比较，将最大索引缩小为 mid -1,与之相反，若小于目标元素，则本身以及左边元素不用在比较，将最小索引为mid +1,一直循环直到mid = 目标元素索引，或min > max;返回对应mid即可

```Java
public class BinarySearch {
    public static void main(String[] args) {
        int[] arr = {11,22,33,44,55,66,77};
        int num = binSearch(arr,22);
        System.out.println(num);
    }

    private static int binSearch(int[] arr, int i) {
        int max = arr.length-1;
        int min = 0;
        int mid;
        while (min <= max){
            mid =(max + min) / 2;
            if (arr[mid] < i){
                min = mid +1;
            }else if(arr[mid] > i){
                max = mid -1;
            } else {
                return mid;
            }
        }
        return -1;
    }
}

```

