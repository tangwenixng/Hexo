title: java8语法
date: 2017-12-08 23:10
tags:
- java
categories:
- java
---

对 Stream 的使用就是实现一个 filter-map-reduce 过程，产生一个最终结果，或者导致一个副作用（side effect）

## 流的构造与转换

### 构造

```java
public static<T> Stream<T> of(T... values)    //Stream.of(arr)
public static <T> Stream<T> stream(T[] array)  //Arrays.stream(arr)
List<String> list = Arrays.asList(strArray);
stream = list.stream();
```

**IntStream、LongStream、DoubleStream 特别为这三种基本数值型提供了对应的 Stream**

### 转换

```java
// 1. Array
String[] strArray1 = stream.toArray(String[]::new);
// 2. Collection
List<String> list1 = stream.collect(Collectors.toList());
List<String> list2 = stream.collect(Collectors.toCollection(ArrayList::new));
Set set1 = stream.collect(Collectors.toSet());
Stack stack1 = stream.collect(Collectors.toCollection(Stack::new));
// 3. String
String str = stream.collect(Collectors.joining()).toString();
```

## 流的操作

常见操作归类:

- Intermediate(中间,中级)
> map (mapToInt, flatMap 等)、 filter、 distinct、 sorted、 peek、 limit、 skip、 parallel、 sequential、 unordered

- Terminal
> forEach、 forEachOrdered、 toArray、 reduce、 collect、 min、 max、 count、 anyMatch、 allMatch、 noneMatch、 findFirst、 findAny、 iterator

- Short-circuiting
> anyMatch、 allMatch、 noneMatch、 findFirst、 findAny、 limit


**map/flatMap**

```java
/**
 * 转换大写
 */
public static void transferUpperCase(){
    List<String> wordList = Arrays.asList("fdhf","wrwad","aufhe");
    List<String> output = wordList.stream()
            .map(String::toUpperCase).collect(Collectors.toList());
    output.forEach(System.out::println);
}

```

*map 生成的是个 1:1 映射，每个输入元素，都按照规则转换成为另外一个元素。*
还有一些场景，是一对多映射关系的，这时需要 flatMap。

```java
/**
* 一对多
*/
public static void one2Many(){
Stream<List<Integer>> inputStream = Stream.of(
        Arrays.asList(1),
        Arrays.asList(1,2,3,4),
        Arrays.asList(7,8,9)
);
Stream<Integer> output = inputStream.flatMap((childList) -> childList.stream());
output.forEach(System.out::println);
}
```


**forEach**

forEach 方法接收一个 Lambda 表达式，然后在 Stream 的每一个元素上执行该表达式

```java
// Java 8
roster.stream()
 .filter(p -> p.getGender() == Person.Sex.MALE)
 .forEach(p -> System.out.println(p.getName()));
```

*forEach 是 terminal 操作，因此它执行后，Stream 的元素就被“消费”掉了，你无法对一个 Stream 进行两次 terminal 运算*,下面的代码是错误的：

```java
stream.forEach(element -> doOneThing(element));
stream.forEach(element -> doAnotherThing(element));
```

**reduce**

这个方法的主要作用是把 Stream 元素组合起来。它提供一个起始值（种子），然后依照运算规则（BinaryOperator），和前面 Stream 的第一个、第二个、第 n 个元素组合。

```java
// 字符串连接，concat = "ABCD"
String concat = Stream.of("A", "B", "C", "D").reduce("", String::concat);
System.out.println(concat);
// 求最小值，minValue = -3.0
double minValue = Stream.of(-1.5, 1.0, -3.0, -2.0).reduce(Double.MAX_VALUE, Double::min);
System.out.println(minValue);
// 求和，sumValue = 10, 有起始值
int sumValue = Stream.of(1, 2, 3, 4).reduce(0, Integer::sum);
System.out.println(sumValue);
// 求和，sumValue = 10, 无起始值
sumValue = Stream.of(1, 2, 3, 4).reduce(Integer::sum).get();
System.out.println(sumValue);
// 过滤，字符串连接，concat = "ace"
concat = Stream.of("a", "B", "c", "D", "e", "F").
        filter(x -> x.compareTo("Z") > 0).
        reduce("", String::concat);
System.out.println(concat);
```


**sorted**


```java
//排序前进行 limit 和 skip
List<Person> persons = new ArrayList();
 for (int i = 1; i <= 5; i++) {
 Person person = new Person(i, "name" + i);
 persons.add(person);
 }
List<Person> personList2 = persons.stream().limit(2).sorted((p1, p2) -> p1.getName().compareTo(p2.getName())).collect(Collectors.toList());
System.out.println(personList2);
```

**min/max/distinct**

```java
//找出最长一行的长度
BufferedReader br = new BufferedReader(new FileReader("c:\\SUService.log"));
int longest = br.lines().
 mapToInt(String::length).
 max().
 getAsInt();
br.close();
System.out.println(longest);
```

```java
//找出全文的单词，转小写，并排序
List<String> words = br.lines().
 flatMap(line -> Stream.of(line.split(" "))).
 filter(word -> word.length() > 0).
 map(String::toLowerCase).
 distinct().
 sorted().
 collect(Collectors.toList());
br.close();
System.out.println(words);
```