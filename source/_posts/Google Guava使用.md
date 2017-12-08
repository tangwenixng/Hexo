---
title: Google Guava使用
date: 2017-12-08 23:05
tags: 
- java
categories:
- java
---

## 读取classpath下的文件

```java
URL url = Resources.getResource("mapping/掏箱规则.properties");
ImmutableList<String> lines =  Resources.asCharSource(url, Charsets.UTF_8).readLines();
lines.forEach(str -> System.out.println(str));
```