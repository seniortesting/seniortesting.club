---
title: java基础(10) - equals和hashcode
tags: [java基础]
keywords: 'java基础'
categories: []
abbrlink: eh8x51Eg6EFh
date: 2021-04-14 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---

## Java 深拷贝浅拷贝

### 1、什么是浅拷贝、深拷贝？

这里总结一下就是：
• 浅拷贝：对于基本类型的数据进行值传递，对于指向对象的引用本质也是值传递，传递的是对象在堆中的内存地址，这样有个问题就是浅拷贝后的两个引用，都是指向的同一个对象，改变其中一个都会影响到另一个。
![](https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210530164725.png)

• 深拷贝：对于基本类型的数据进行值传递，对于指向对象的应用，直接new一个对象出来，并复制老对象的内容给新对象，深拷贝后的两个引用指向的是两个不同的对象，但对象的成员属性都相等（equals）。
!()[https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210530164749.png]

### 2、Object的clone方法和Cloneable接口

实现拷贝是调用的clone方法，该方法在Object里定义，如下：
protected native Object clone() throws CloneNotSupportedException;
可以看到这个方法用了native关键字修饰，native关键字意思是这个方法不是用java语言实现的，而是用的底层的C语言去实现的，具体实现过程肯定在java源文件里找不到的。这里我们需要知道的是：**Object类里的clone方法实现的是浅拷贝**。

所有调用clone方法的对象都必须实现Cloneable接口，否则会抛出CloneNotSupportedException异常，Cloneable接口源码如下：

```java
public interface Cloneable {
}
```

可以看到它其实什么方法都不需要实现。对Cloneable接口可以简单的理解只是一个标记，意思是如果一个类实现了Cloneable接口，这个类的对象就允许被拷贝。

## 3、浅拷贝示例

Student类:

```java
package Clone;
import lombok.EqualsAndHashCode;
import lombok.Getter;
import lombok.Setter;
@Getter
@Setter
@EqualsAndHashCode
public class Student implements Cloneable{
    private String name;
    private int age;
    private Subject subject;
    public Student(String name, int age, Subject subject)
    {
        this.name = name;
        this.age = age;
        this.subject = subject;
    }
    @Override
    protected Object clone() {
        try
        {
            return super.clone();
        }
        catch (CloneNotSupportedException e)
        {
            e.printStackTrace();
        }
        return null;
    }
}
```

Subject类：

```java
package Clone;
import lombok.EqualsAndHashCode;
import lombok.Getter;
import lombok.Setter;
@Setter
@Getter
@EqualsAndHashCode
public class Subject {
    private String subjectName;
    private int score;
    public Subject(String subjectName, int score)
    {
        this.subjectName = subjectName;
        this.score = score;
    }
}
Main:
public class Main {
    public static void main(String[] args) {
        Subject subject = new Subject("Math", 100);
        String studentName = "Jerry";
        int age = 27;
        Student studentJerry = new Student(studentName, age, subject);
        // 调用clone方法克隆一个Student对象
        Student studentClone = (Student) studentJerry.clone();
        System.out.println("两个Student对象比较：" + String.valueOf(studentJerry == studentClone));
        System.out.println("两个Student对象的subject对象比较：" + String.valueOf(studentJerry.getSubject() == studentClone.getSubject()));
    }
}
```

执行结果如下：
两个Student对象比较：false
两个Student对象的subject对象比较：true

可以看到，Student对象已经重新生成了一个，但是两个Student对象里的Subject引用还是指向的同一个Subject对象，这就是浅拷贝的效果。

### 4、深拷贝示例

实现深拷贝比较常用的方案有两种：

1. 序列化（serialization）这个对象，再反序列化回来，就可以得到这个新的对象，无非就是序列化的规则需要我们自己来写。
2. 继续利用 clone() 方法，在要进行深拷贝的类里重写clone方法（该类必须实现了Cloneable接口），我们可以对类内的引用类型的变量递归地进行clone，直到没有引用类型的成员属性为止。

这里以clone方法为例，实际上clone方法也是实现深拷贝最常用的方法。
改造上面的Subject类，也令其实现Cloneable接口，并实现clone方法。

Student类：

```java
package Clone;
import lombok.EqualsAndHashCode;
import lombok.Getter;
import lombok.Setter;
@Getter
@Setter
@EqualsAndHashCode
public class Student implements Cloneable{
    private String name;
    private int age;
    private Subject subject;
    public Student(String name, int age, Subject subject)
    {
        this.name = name;
        this.age = age;
        this.subject = subject;
    }
    @Override
    protected Object clone() {
        try
        
        {
            Student student = (Student) super.clone();
            student.subject = (Subject) this.subject.clone();
            return student;
        }
        catch (CloneNotSupportedException e)
        {
            e.printStackTrace();
        }
        return null;
    }
}
```

Subject类：

```java
package Clone;
import lombok.EqualsAndHashCode;
import lombok.Getter;
import lombok.Setter;
@Setter
@Getter
@EqualsAndHashCode
public class Subject implements Cloneable{
    private String subjectName;
    private int score;
    public Subject(String subjectName, int score)
    {
        this.subjectName = subjectName;
        this.score = score;
    }
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

main方法不变，执行结果如下：
两个Student对象比较：false
两个Student对象的subject对象比较：false

可以看到，生成了两个Student对象，每个Student对象的Subject引用都指向了不同的Subject对象，达到了深拷贝的效果。
总结一下就是：**深拷贝就是将一个类的所有引用类型的成员变量对应的类递归实现浅拷贝（实现Cloneable接口重写clone方法）**。
参考
<https://www.cnblogs.com/plokmju/p/7357205.html>