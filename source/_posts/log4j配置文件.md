---
title: log4j配置文件
categories:
- Java
tags:
- log4j
---

`log4j.rootLogger=DEBUG,app,[level],[appenderName...]`

`log4j.appender.app="目的地"`

`log4j.appender.app.layout=org.apache.log4j.PatternLayout(自定义布局)`

`log4j.appender.app.ConversionPattern="自定义格式"`

**详情自行google: [log4j配置](http://www.cnblogs.com/ITEagle/archive/2010/04/23/1718365.html)**


### 设置###  
log4j.rootLogger = debug,stdout,D,E  
  
### 输出信息到控制抬 ###  
log4j.appender.stdout = org.apache.log4j.ConsoleAppender  
log4j.appender.stdout.Target = System.out  
log4j.appender.stdout.layout = org.apache.log4j.PatternLayout  
log4j.appender.stdout.layout.ConversionPattern = [%-5p] %d{yyyy-MM-dd HH:mm:ss,SSS} method:%l%n%m%n  
  
### 输出DEBUG 级别以上的日志到=E://logs/error.log ###  
log4j.appender.D = org.apache.log4j.DailyRollingFileAppender  
log4j.appender.D.File = E://logs/log.log  
log4j.appender.D.Append = true  
log4j.appender.D.Threshold = DEBUG   
log4j.appender.D.layout = org.apache.log4j.PatternLayout  
log4j.appender.D.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n  
  
### 输出ERROR 级别以上的日志到=E://logs/error.log ###  
log4j.appender.E = org.apache.log4j.DailyRollingFileAppender  
log4j.appender.E.File =E://logs/error.log   
log4j.appender.E.Append = true  
log4j.appender.E.Threshold = ERROR   
log4j.appender.E.layout = org.apache.log4j.PatternLayout  
log4j.appender.E.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n  