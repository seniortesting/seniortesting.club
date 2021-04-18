---
title: java基础(4) - 集合List
tags: [java基础,集合]
keywords: 'java基础,集合'
categories: []
abbrlink: k01251Eg6EFh
date: 2021-04-16 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---



## 1. list去重复操作？

```java
//1.提取出list对象中的一个属性
List<String> stIdList1 = stuList.stream().map(Person::getId).collect(Collectors.toList());

//2.提取出list对象中的一个属性并去重
List<String> stIdList2 = stuList.stream().map(Person::getId).distinct().collect(Collectors.toList());

```

去除List中的重复对象

```java
// Person 对象
public class Person {
    private String id;
    
    private String name;
    
    private String sex;

    <!--省略 get set-->
}

// 根据name去重
List<Person> unique = persons.stream().collect(
            Collectors.collectingAndThen(
                    Collectors.toCollection(() -> new TreeSet<>(Comparator.comparing(Person::getName))), ArrayList::new)
);

// 根据name,sex两个属性去重
List<Person> unique = persons.stream().collect(
           Collectors. collectingAndThen(
                    Collectors.toCollection(() -> new TreeSet<>(Comparator.comparing(o -> o.getName() + ";" + o.getSex()))), ArrayList::new)
);

//

```

## 2. 查找list中最大和最小的对象值？

```java
// 获取某个属性的最大值
Optional<Dish> maxDish = Dish.menu.stream().
      collect(Collectors.maxBy(Comparator.comparing(Dish::getCalories)));
maxDish.ifPresent(System.out::println);

// 获取某个属性的最小值
Optional<Dish> minDish = Dish.menu.stream().
      collect(Collectors.minBy(Comparator.comparing(Dish::getCalories)));
minDish.ifPresent(System.out::println);
```

## 3. 求和操作

```java
//计算 总金额
BigDecimal totalMoney = appleList.stream().map(Apple::getMoney).reduce(BigDecimal.ZERO, BigDecimal::add);

```

## 4. 对list中的元素如何进行分组？

```java

//List 以ID分组 Map<Integer,List<Apple>>
Map<Integer, List<Apple>> groupBy = appleList.stream().collect(Collectors.groupingBy(Apple::getId));

// 多属性分组

 // 方法1：嵌套调用 Java8 Collectors groupingBy 方法
Map<String, Map<String, List<Student>>> map1 = stuList.stream()
                .collect(Collectors.groupingBy(Student::getAge, Collectors.groupingBy(Student::getSex)));
```

## 5. list如何转为map，例如id为key，对象为value？

```java
/**
 * List -> Map
 * 需要注意的是：
 * toMap 如果集合对象有重复的key，会报错Duplicate key ....
 *  apple1,apple12的id都为1。
 *  可以用 (k1,k2)->k1 来设置，如果有重复的key,则保留key1,舍弃key2
 */
Map<Integer, Apple> appleMap = appleList.stream().collect(Collectors.toMap(Apple::getId, a -> a,(k1,k2)->k1));
```

## 6. 如何进行排序操作？

```java
// 正常的升序操作
List<Integer> collect = list.stream().sorted().collect(Collectors.toList());
// 倒序操作
List<Person> collect = list.stream().sorted(Comparator.comparing(Person::getSalary).reversed()).collect(Collectors.toList());
//按年龄排序(Integer类型)
List<StudentInfo> studentsSortName = studentList.stream().sorted(Comparator.comparing(StudentInfo::getAge).reversed()).collect(Collectors.toList());

//使用年龄进行降序排序，年龄相同再使用身高升序排序
List<StudentInfo> studentsSortName = studentList.stream()
                .sorted(Comparator.comparing(StudentInfo::getAge).reversed().thenComparing(StudentInfo::getHeight))
                .collect(Collectors.toList());

```

