---
title: Swing
date: 2022-06-13 13:43:25
tags:
cover: https://images.pexels.com/photos/12015343/pexels-photo-12015343.jpeg?cs=srgb&dl=pexels-ryan-klaus-12015343.jpg&fm=jpg
---

# Swing 

[TOC]



## JFrame窗体

要显示窗体用到 对象名.setVisible(true)



In order to close frame, use method **setDefaultCloseOperation(参数)**

![image-20220320111149219](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201111268.png)



设置窗体大小与显示位置

![image-20220320111357856](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201113890.png)



对于窗体的操作

![image-20220320112631865](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201126924.png)

设置窗体是否可以改变大小

`setResizable(true/false)`



```java
import javax.swing.*;
import java.awt.*;

public class Swing_demo1
{
    public static void main(String[] args){
        //JFrame 指定一个窗口，构造方法的参数为窗口标题
        JFrame frame=new JFrame("Example");
        //显示窗口
        frame.setVisible(true);

        JPanel root=new JPanel();
        frame.setContentPane(root);

        JButton button=new JButton("Click");
        root.add(button);

//        //设置窗口大小
//        frame.setSize(400,300);
//        //设置窗口显示位置
//        frame.setLocation(500,200);
        //以上两个函数可以合并到一个函数
        frame.setBounds(500,200,400,300);

        Container c=frame.getContentPane(); //获取窗体容器
        c.setBackground(Color.white);
        JLabel l=new JLabel("Hello World");
        c.add(l);

        //窗口不可改变大小
        frame.setResizable(false);

        //当关闭窗口时，退出整个程序
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}

```





**在实际开发中，一般将对象放到类的构造方法中初始化，不需要建立对象**

```java
import javax.swing.*;
import java.awt.*;

public class Swing_demo1 extends JFrame
{
    public Swing_demo1(){
        setTitle("Window");
        setVisible(true);

        JPanel root=new JPanel();
        setContentPane(root);

        JButton button=new JButton("Click");
        root.add(button);

//        //设置窗口大小
//        frame.setSize(400,300);
//        //设置窗口显示位置
//        frame.setLocation(500,200);
        //以上两个函数可以合并到一个函数
       setBounds(500,200,400,300);

        Container c=getContentPane(); //获取窗体容器
        c.setBackground(Color.white);
        JLabel l=new JLabel("Hello World");
        c.add(l);

        //窗口不可改变大小
        setResizable(false);

        //当关闭窗口时，退出整个程序
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    public static void main(String[] args){
        new Swing_demo1();
    }
}

```









## JDialog

![image-20220320143741430](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201437469.png)

//主函数

```java
public class Swing_demo1{
    public static void main(String[] args) {
        JFrame f=new JFrame("Father Window");
        f.setBounds(500,200,300,200);
        Container c=f.getContentPane();
        JButton btn=new JButton("Click");
        c.setLayout(new FlowLayout());
        c.add(btn);
        f.setVisible(true);
        f.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE;

        btn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                Dialog1 d=new Dialog1(f);
                d.setVisible(true);

            }
        });
    }
}
```



//弹窗类

```java
import javax.swing.*;
import java.awt.*;

public class Dialog1 extends JDialog{
    public Dialog1(JFrame frame){
        super(frame,"Title",true);

        Container c=getContentPane();
        c.add(new JLabel("这是一个对话框"));


        setBounds(500,200,400,300);
        //窗口不可改变大小
        setResizable(false);
    }
}


```





## Label

![image-20220320164524441](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201645511.png)



标签插入图片

![image-20220320165520029](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201655107.png)

```java
//import pic.*;
import javax.swing.*;
import java.awt.*;
import java.net.URL;
import java.util.jar.JarEntry;

//插入图片
public class frame01 extends JFrame {
    public frame01(){

        setBounds(100,100,400,350);
        setTitle("Insert picture");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        Container c=getContentPane();

        JLabel l=new JLabel();
//        URL url=frame01.class.getResource("wallpaper01.png");
//        Icon icon=new ImageIcon(url);

        Icon icon=new ImageIcon("src/wallpaper01.png");
        l.setIcon(icon);    //添加图片
        c.add(l);
        setVisible(true);
    }

    public static void main(String[] args) {
        new frame01();
    }
}

```





## 布局

* 绝对布局

![image-20220320172941285](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201729332.png)

* 流布局

  ` setLayout(new FlowLayout(LEFT/RIGHT))	` 

  `给容器设置流布局,左对齐或者右对齐`

​	![image-20220320174045347](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201740404.png)



* 边界布局

​	![image-20220320174725203](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203201747312.png)



* 网格布局

  ![image-20220320215524385](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203202155522.png)



* 网格组（包）布局管理器

​	![image-20220320215708258](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203202157385.png)



![image-20220320215734831](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202203202157959.png)