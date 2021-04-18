---
title: java基础(8) - 字符串介绍
tags: [java基础,字符串]
keywords: 'java基础,字符串'
categories: []
abbrlink: s6te1u1Eg6EFh
date: 2021-04-16 23:14:50
description:
cover: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
top_img: https://cdn.jsdelivr.net/gh/alterhu2020/CDN/img/blog/20210414175757.jpeg
---


## 1. StringBuffer vs StringBuilder

- StringBuffer是线程安全，可以不需要额外的同步用于多线程中;
- StringBuilder是非同步,运行于多线程中就需要使用着单独同步处理，但是速度就比StringBuffer快多了;
- StringBuffer与StringBuilder两者共同之处:可以通过append、indexOf进行字符串的操作。

- 首先说运行速度，或者说是执行速度，在这方面运行速度快慢为：StringBuilder > StringBuffer > String

- StringBuffer中很多方法可以带有`synchronized`关键字，所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，所以不能保证线程安全，有可能会出现一些错误的操作。所以**如果要进行的操作是多线程的，那么就要使用StringBuffer，但是在单线程的情况下，还是建议使用速度比较快的StringBuilder。**


## 2. 如何优雅的判空，判定对象为空，NPE？

代码如下：
```java
    @Test
    public void testNullString() {
        String str = null;
        final boolean present = Optional.ofNullable(str).isPresent();
        Assertions.assertTrue(present);

        final boolean nonNull = Objects.nonNull(str);
        Assertions.assertTrue(nonNull);
    }
```

## 3. string相关类型转换？


类型 | 字符串转其他类型 | 其他类型转字符串1 | 其他类型转字符串2
---------|----------|---------|---------
 byte | Byte.parseByte(str) | String.valueOf([byte] bt) | Byte.toString([byte] bt)
 short | Short.parseShort(str) | String.valueOf([short] s) | Short.toString([short] s)
 int |  Integer.parseInt(str) |  String.valueOf([int] i) |   Int.toString([int] i)
 long | Long.parseLong(str) | String.valueOf([long] l)| Long.toString([long] l)
 float | Float.parseFloat(str) |  String.valueOf([float] f)|  Float.toString([float] f)
 double | Double.parseDouble(str) |  String.valueOf([double] d)| Double.toString([double] b)


 ## 4. 读取字符串获取hash值

 ```java

    public static String md5(File path) {
        Preconditions.notNull(path, "path:%s is null".formatted(path));
        String md5Text;
        try {
            final MessageDigest md5 = MessageDigest.getInstance("MD5");
            try (FileInputStream fileInputStream = new FileInputStream(path)) {
                byte[] buffer = new byte[8192];
                int length = -1;
                while ((length = fileInputStream.read(buffer)) != -1) {
                    md5.update(buffer, 0, length);
                }
            }
            final byte[] digest = md5.digest();
            md5Text = new BigInteger(1, digest).toString(16);
        } catch (NoSuchAlgorithmException | FileNotFoundException e) {
            throw new RuntimeException("file not found exception");
        } catch (IOException e) {
            throw new RuntimeException("read file exception");
        }
        // or guava way
        //  Files.asByteSource(path).hash(Hashing.md5()).toString();
        return md5Text;
    }

    public static String md5(String text) {
        Preconditions.notBlank(text, "text: %s is null".formatted(text));
        String md5Text;
        try {
            final byte[] textBytes = text.getBytes();
            final MessageDigest messageDigest = MessageDigest.getInstance("MD5");
            messageDigest.update(textBytes);
            final byte[] digest = messageDigest.digest();
            md5Text = new BigInteger(1, digest).toString(16);
        } catch (NoSuchAlgorithmException e) {
            throw new RuntimeException("NoSuchAlgorithmException for %s".formatted(text));
        }
        return md5Text;

    }

 ```

 ## 5. 字符串分割操作

 如何进行字符串的分割操作？

 ```java
 // StringJoiner
 
 // java8
final String commandStr = compileCommand.stream().map(String::toString)
                    .collect(Collectors.joining(" "));
 ```