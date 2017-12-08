---
title: Jpa一对多映射
categories:
- 数据库
- Java
tags:
- 数据库
- Java
---

https://www.ibm.com/developerworks/cn/java/j-lo-jparelated/   很重要的 

在JPA规范中，一对多的双向关系由**多端(Employee)来维护**。就是说多端(Employee)为关系维护端，负责关系的增删改查。一端(Company)则为关系被维护端，不能维护关系。

一端(Company)使用@OneToMany注释的mappedBy="company"属性表明Company是关系被维护端。

多端(Employee)使用@ManyToOne和@JoinColumn来注释属性company,@ManyToOne表明Employee是多端，@JoinColumn设置在employee表中的关联字段(外键)。

```java
20 @Entity
21 @Table(name="company")
22 public class Company {
23     
24     @Id
25     @GeneratedValue
26     private Long id;
27     
28     /**公司名称*/
29     @Column(name="name",length=32)
30     private String name;
31     
32     /**拥有的员工*/
33     @OneToMany(mappedBy="company",cascade=CascadeType.ALL,fetch=FetchType.LAZY)
34     //拥有mappedBy注解的实体类为关系被维护端
35     //mappedBy="company"中的company是Employee中的company属性
36     private Set<Employee> employees = new HashSet<Employee>();
```

```java
17 @Entity
18 @Table(name="employee")
19 public class Employee {
20     
21     @Id
22     @GeneratedValue
23     private Long id;
24     
25     /**雇员姓名*/
26     @Column(name="name")
27     private String name;
28     
29     /**所属公司*/
30     @ManyToOne(cascade={CascadeType.MERGE,CascadeType.REFRESH},optional=false)//可选属性optional=false,表示company不能为空
31     @JoinColumn(name="company_id")//设置在employee表中的关联字段(外键)
32     private Company company;
33   }
```

FetchType.EAGER = <font style="color:red;">取出这条数据时，它关联的数据也同时取出放入内存中  (维护的一端用eager)
如果是LAZY，那么取出这条数据时，它关联的数据并不取出来，在同一个session中，什么时候要用，就什么时候取(再次访问数据库)。</font>