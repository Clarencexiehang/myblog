---
title: Java Note
date: 2022-06-13 13:43:25
tags: 
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2F5b0988e595225.cdn.sohucs.com%2Fimages%2F20170919%2Fae57f3300aa54066872d463473b8c9b8.png&refer=http%3A%2F%2F5b0988e595225.cdn.sohucs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1657691830&t=08370e2f724600cbb494c0d08a5239a8
---


# Java Note

[TOC]



## 1.基础语法

###  **1.Random 的使用**

<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203101133024.png" alt="image-20220310113342920" style="zoom: 50%;" />



### **2.输入**

```java
import java.util.Scanner;
Scanner sc=new Scanner(System.in);	//create new object
int i=sc=nextInt();		//receive data
```



### 3**.数组**

动态初始化：	![image-20220310125459251](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203101254281.png)

`int [] arr=new int[3]`;



静态初始化：<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203101309573.png" alt="image-20220310130933539" style="zoom:80%;" />

或者使用简化格式：

![image-20220310131048992](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203101310022.png)



Arrays类：

```java
Arrays.sort(arrayName);
system.out.println("After sort: "+Array.toString(arrayName));
```

因为函数是static类型，所以说明可以直接用类名访问



### 4.API

​	Application Programming Interface 	应用程序编程接口

常用API：

* Math

  





### 5.**string**

<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203102231848.png" alt="image-20220310223109786" style="zoom:80%;" />

`String s=new String();`



<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203102238537.png" alt="image-20220310223815448" style="zoom:80%;" />



**字符串的比较**

![image-20220310224018232](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203102240272.png)

<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203102242243.png" alt="image-20220310224234170" style="zoom: 80%;" />

注意：若字符串内容相同，则不同变量指向的地址相同。



**遍历字符串**

<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203111434949.png" alt="image-20220311143453837" style="zoom:80%;" />



* string类型和int转换

  推荐使用**String.valueOf()**和**Integer.parseInt()**静态函数互相转换

  ```java
  int number=100;
  //method 1
  String s1=String.valueOf(number);
  //method 2
  String s2=""+number;
  System.out.println(s1);
  //the output is 100
  
  //String convert to int type
  //method 1
  Integer i=Integer.valueOf(s1);
  int x=i.intValue();
  //method 2
  int y=Integer.parseInt(s);	
  ```

* String的函数split可以分开字符串中的元素

  

### **6.StringBulider：**

StringBuilder内容可变



<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203111525194.png" alt="image-20220311152543135" style="zoom:80%;" />



![image-20220311152759650](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203111527685.png)



![image-20220311153019848](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203111530897.png)



链式编程

![image-20220311153139505](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203111531549.png)



<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203111533176.png" alt="image-20220311153340107" style="zoom:67%;" />





```java
System.exit(0);	//JVM退出
```



### 7. Interger包装类

Integer i=Integer.valueOf("100" Or 100);

其他包装类使用方法大同小异

* 装箱：基本数据类型转换为包装类型

* 拆箱：包装类型转换为基本数据类型

  ```java
  Integer i=Integer.valueOf(100);//手动
  i=i.intValue()+100;
  i++=100;	//自动拆箱
  ```

  

  





## 2.IDEA

* 快捷键

  psvm	主函数

  sout	输出

  



## 3. 类

![image-20220310215529444](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203102155840.png)







![image-20220310221016978](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203102210056.png)



### SimpleDateFormat类

1.格式化（从Date到String）

public final String format(Date date)

2.解析（从String到Date)

public Date parse(String source)

```java
public class Time {
    public static void main(String[] args) throws ParseException {
        Date d =new Date();
        System.out.println("Default format is: "+d);  //default format

        SimpleDateFormat sdf1=new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        String s=sdf1.format(d);
        System.out.println(s);
        System.out.println("----------------------");

        //convert from String to Date
        //Note: the date format must match with each other
        String ss="2022年5月1日 11:11:11";
        SimpleDateFormat sdf2=new SimpleDateFormat("yyyy年M月d日 HH:mm:ss");
        Date dd=sdf2.parse(ss);
        System.out.println(dd);
    }
}
```

### Calendar







## 4. 集合基础

![image-20220409200836652](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202204092008759.png)



### Collection

常用方法

boolean add(E e)	添加元素

boolean remove(Object o)	移除指定长度

void clear()

boolean contains(object o)	集合中是否存在指定元素

boolean isEmpty()

int size()	集合长度

```java
public static void main(String[] args) {
        Collection<String> c=new ArrayList<String>();
        System.out.println(c.add("Hello"));
        c.add("World");
        c.add("Friend");

        System.out.println(c);

        System.out.println(c.remove("World"));

        System.out.println("if exist hello:"+c.contains("hello"));

        //the traverse of Collection
        Iterator<String> i=c.iterator();
        while(i.hasNext()){
            System.out.print(i.next()+" ");
        }
    }
```



### List

特有方法：

void add(int index,E element)

E remove(int index)

E set(int index,E element)	修改指定位置的元素

E get(int index)



Listiterator	允许沿任意方向遍历列表

可以向集合中添加元素 add（E e）

向前遍历boolean hasPrevious()

E previous()

#### 1.ArrayList



![image-20220314193232862](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203141932936.png)

```java
public class Time {
    public static void main(String[] args) throws ParseException {
        Date d =new Date();
        System.out.println("Default format is: "+d);  //default format

        SimpleDateFormat sdf1=new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        String s=sdf1.format(d);
        System.out.println(s);
        System.out.println("----------------------");

        //convert from String to Date
        //Note: the date format must match with each other
        String ss="2022年5月1日 11:11:11";
        SimpleDateFormat sdf2=new SimpleDateFormat("yyyy年M月d日 HH:mm:ss");
        Date dd=sdf2.parse(ss);
        System.out.println(dd);
    }

```







![image-20220314193746047](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203141937133.png)



获取元素：

![image-20220314200217416](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203142002456.png)



![image-20220314200539274](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203142005319.png)



#### 2.LinkedList

底层原理是链表

![image-20220410105754031](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202204101057123.png)





### Set

不含重复元素

不带索引方法，不能用for遍历

HashSet： 对集合迭代顺序不作任何保证

public int hashCode()	返回对象的哈希值



TreeSet 的Comparable用法

int默认按大小排序

对象return 0存一个，return -1降序，return 1升序（存储先后顺序）

重写compareTo()



### Map集合

Interface Map<K,V>

添加： V put(K key,V value)

删除： V remove(Object key)

移除所有键值对	void clear()

是否包含指定键	boolean containsKey(Object key)

boolean containsValue(Object value)

集合是否为空	Set<Map.Entry<K,V>> boolean isEmpty()

键值对个数	int size()

获取值	V get(Object key);



map集合的遍历

1.键找值

```java
Set<String> f=map.keySet();	//获取所有键的集合
for(String key:f){
    String value=map.get(key);
}
```

2.键值对对象找键和值

```java
Set<Map.Entry<K,V>> name=map.entrySet();
for(Set<Map.Entry<K,V>> me: name){
    
}
```



应用：输入字符串统计字符个数：

```java
public class SumOfCharacters {
    public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        System.out.print("Input one string: ");
        String line=sc.nextLine();

        TreeMap<Character,Integer> l=new TreeMap<>();

        for(int i=0;i<line.length();i++){
            char key=line.charAt(i);

            Integer value=l.get(key);

            if(value==null){
                l.put(key,1);
            }
            else{
                value++;
                l.put(key,value);
            }
        }

        Set<Character> a=l.keySet();
        for(Character key:a){
            Integer value=l.get(key);
            System.out.println(key+":"+value);
        }
    }
}
```



### Connections

排序 sort()

翻转 reverse（）

随机排列 shuffle()





## 5.继承



![image-20220314205039676](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203142050728.png)





![image-20220314210422952](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203142104062.png)



![image-20220314210857644](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203142108730.png)







## 6.快捷键

生成构造函数	alt+ins

导包	alt+enter

查看函数属性	Ctrl+左击





## 7.接口

### 1,接口特性

- 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 **public abstract**（只能是 public abstract，其他修饰符都会报错）。

- 接口中可以含有变量，但是接口中的变量会被隐式的指定为 **public static final** 变量（并且只能是 public，用 private 修饰会报编译错误）。

- 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。

  

### 2.抽象类和接口的区别

- \1. 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
- \2. 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。
- \3. 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
- \4. 一个类只能继承一个抽象类，而一个类却可以实现多个接口。

### 3.接口的实现

当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。

类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。

实现一个接口的语法，可以使用这个公式：

`...implements 接口名称[, 其他接口名称, 其他接口名称..., ...] ...`

![image-20220319111614111](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203191116161.png)



## 8.异常

getMessage() 返回throwable的详细消息字符串

toString()	返回可抛出的简单描述，包含了getMessage的内容

**printStackTrace()**	把异常的错误信息输出到控制台，信息最全



分为两类

* 编译时异常：必须显示处理
* 运行时异常：无需显示处理，也可和编译时异常处理一样





## 9.泛型



### 1.泛型类与方法的使用

```java
public class Generic <T>{
    private T t;

    public T getT(){
        return t;
    }

    public void setT(T t) {
        this.t = t;
    }
    //generic method
    public<T> void show(T t){
        System.out.println(t);
    }
}
```

```java
public class GenericDemo {
    public static void main(String[] args) {
        Generic<String> a=new Generic<String>();
        a.setT("Tom");
        System.out.println(a.getT());

        Generic<Integer> b=new Generic<Integer>();
        b.setT(30);
        System.out.println(b.getT());

        // generic method
        b.show("jack");
    }
}
```



### 2.泛型接口

```java
public interface Generic<T>{
    void show(T t);
}
```



### 类型通配符



### 3.可变参数

参数个数可变

原理是封装到数组中

```java
public static int sum(int... a){
    int sum=0;
    for(int i:a){
        sum+=i;
    }
    return sum;
}
```

其他参数可以放到可变参数前面，放到后面会报错







## 10.正则表达式

public boolean matches()





## 11. 线程





## 12.Logback

LoggerFactory.getlogger();
