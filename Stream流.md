# **Stream流介绍：**

**配合lambda表达式，简化集合和数组操作**

## **获取Stream流对象**

![image-20251221181445689](https://gitee.com/icecat2233/picture/raw/master/20251221181446881.png)

## **Stream流中间操作方法：**

![image-20251221182850306](https://gitee.com/icecat2233/picture/raw/master/20251221182851889.png)

## 获取对象流演示：

![image-20251221194116622](https://gitee.com/icecat2233/picture/raw/master/20251221194131811.png)

### **示例：**

```Java
ArrayList<String> list = new ArrayList<>();
        list.add("杏菜");
        list.add("佳树");
        list.add("小鞠");
        list.add("梦子");
        //集合Stream流对象
        list.stream().filter(s -> s.startsWith("杏")).forEach(s -> System.out.println(s));
        //数组流对象
        int[] arr = {1, 2, 3};
        Arrays.stream(arr).forEach(s-> System.out.println(s));
        HashSet<Integer> hs = new HashSet<>();
        hs.add(1);
        hs.add(4);
        hs.add(3);
        hs.add(5);
        //map集合流对象，需要间接获取 - map.entrySet().stream
        HashMap<String,Integer> hm = new HashMap<>();
        hm.put("张",13);
        hm.put("李",14);
        hm.put("王",15);
        Set<Map.Entry<String, Integer>> entries = hm.entrySet();
        entries.stream()
                .filter(entry -> !entry.getKey().startsWith("张"))
                .forEach(entry -> System.out.println(entry.getKey()+"---"+entry.getValue()));
        //零散数据获取Stream流对象
        Stream.of("1","e",3).forEach(s-> System.out.println(s));
```

## 中间操作方法

![image-20251221200537334](https://gitee.com/icecat2233/picture/raw/master/20251221200538411.png)

示例：

```java
ArrayList<Integer> list = new ArrayList<>();
        Stream<Integer> s2 = list.stream();
        ArrayList<Integer> list1= new ArrayList<>();
        Stream<Integer> s1 = list1.stream();
        Collections.addAll(list1,5,6,7);
        Collections.addAll(list,1,2,3,4);
        //filter过滤方法
        list.stream().filter(s -> s!=2).forEach(s-> System.out.print(s));
        System.out.println('\n');
        //limit获取前几个元素
        list.stream().limit(2).forEach(integer -> System.out.print(integer));
        System.out.println('\n');
        //skip跳过几个元素
        System.out.println("跳过之后的元素");
        list.stream().skip(1).forEach(s-> System.out.print(s));
        System.out.println('\n');
        //concat(Stream a,Stream b)合并ab为一个流
        Stream<Integer> s3 = Stream.concat(s1, s2);
        s3.forEach(new Consumer<Integer>() {
            @Override
            public void accept(Integer s) {
                System.out.println(s);
            }
        });
        //distinct方法去除流中重复的元素依赖(hashCode 和 equals方法)
        //在此会报错，因为上面已经消费过了不能重新使用
        list.stream().distinct().forEach(s-> System.out.println(s));
```

![image-20251221203020331](https://gitee.com/icecat2233/picture/raw/master/20251221203021575.png)

**注意：若流已经被使用过，或已使用终结方法，就不允许再次使用**

## 终结方法

![image-20251221203822185](https://gitee.com/icecat2233/picture/raw/master/20251221203823266.png)

**示例：**

```java
//count方法，返回元素个数
Stream<Integer> s1 = Stream.of(2, 3, 4, 5, 6, 7, 8).filter(integer -> integer % 2 == 0);
long count = s1.count();
System.out.println(count);
```

## 重点：收集操作

为何：因为Stream流操作是不会修改数据源的，图为示例：

![image-20251221203945267](https://gitee.com/icecat2233/picture/raw/master/20251221203946590.png)

### **如何收集：**

![image-20251221205629800](https://gitee.com/icecat2233/picture/raw/master/20251221205631348.png)

**示例：**

```java
//Stream流收集操作
Stream<Integer> s1 = Stream.of(1, 2, 3, 4, 5, 6, 7);
List list1 = s1.limit(3).collect(Collectors.toList());//JDK17版本之后可以将Collectors去除
System.out.println(list1);
```

### **转为map操作（较为复杂）**

**重点示例**

```java
//    将ArrayList中年龄大于15的收集到一个新的map集合中去
    public static void main(String[] args) {
        //将Stream流收集到map所需操作
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list,"杏菜,15","佳树,16","老马,17");
        Map<String, Integer> map = list.stream().filter(new Predicate<String>() {
            @Override
            public boolean test(String s) {
                //过滤操作，将字符串数据从逗号切割装入数组，0号索引为名字，1号为年龄
                String[] split = s.split(",");
                //将字符串转为int类型并比较年龄，返回大于等于16岁的
                int age = Integer.parseInt(split[1]);
                return age >= 16;
            }
        }).collect(Collectors.toMap(new Function<String, String>() {
            //创建map集合，第一个匿名内部类为装入键值
            @Override
            public String apply(String s) {
                return s.split(",")[0];
            }
        }, new Function<String, Integer>() {
            //第二个为装入年龄值，并将类型从String改为int
            @Override
            public Integer apply(String s) {
                return Integer.parseInt(s.split(",")[1]);
            }
        }));
        System.out.println(map);
```

# Stream流综合案例

```java
package com.icacat.day12;

import java.util.ArrayList;
import java.util.function.Consumer;
import java.util.function.Predicate;
import java.util.stream.Stream;

public class StreamDemo6 {
    public static void main(String[] args) {
        ArrayList<String> manList = new ArrayList<>();
        manList.add("温水和彦");
        manList.add("社长");
        manList.add("桐谷和人");
        manList.add("勇太");
        ArrayList<String> womanList = new ArrayList<>();
        womanList.add("杏菜");
        womanList.add("小鞠");
        womanList.add("佳树");
        womanList.add("千早");

        Stream<String> s1 = manList.stream().filter(new Predicate<String>() {
            @Override
            public boolean test(String s) {
                return s.length() == 4;
            }
        }).limit(2);
        Stream<String> s2 = womanList.stream().skip(1).filter(s -> s.startsWith("佳"));
        Stream<String> total = Stream.concat(s1, s2);
        total.forEach(new Consumer<String>() {
            @Override
            public void accept(String name) {
                Actor ac = new Actor(name);
                System.out.println(ac);
            }
        });
    }
}

class Actor{
    private String name;

    public Actor() {
    }

    public Actor(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    public String toString() {
        return "Actor{name = " + name + "}";
    }
}
```