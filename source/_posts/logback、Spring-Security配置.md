---
title: logback、Spring Security配置
date: 2017-11-14 19:32:46
tags: [Spring,logback,Security]
categories: [Spring]
---

## logback配置

1. 在pom.xml中增加如下依赖
    ```xml
    <!-- *****************logback************* -->
      <dependency>
          <groupId>org.slf4j</groupId>
          <artifactId>jcl-over-slf4j</artifactId>
          <version>1.7.21</version>
      </dependency>
      <dependency>
          <groupId>ch.qos.logback</groupId>
          <artifactId>logback-classic</artifactId>
          <version>1.2.3</version>
      </dependency>
    ```

    另外需要排除springmvc自带的log
    ```xml
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>4.3.10.RELEASE</version>
          <exclusions>
              <exclusion>
                  <groupId>commons-logging</groupId>
                  <artifactId>commons-logging</artifactId>
              </exclusion>
          </exclusions>
    </dependency>
    ```

2. 在src/main/resources/ 下新建logback.xml文件。
    
    [logback.xml](https://github.com/tangwenixng/mvc/blob/master/mvc-xml-demo/src/main/resources/logback.xml)
---

## 配置Spring Security

1. 在pom.xml中增加如下依赖：

    ```xml
        <dependency>
              <groupId>org.springframework.security</groupId>
              <artifactId>spring-security-config</artifactId>
              <version>4.2.0.RELEASE</version>
        </dependency>
        <dependency>
              <groupId>org.springframework.security</groupId>
              <artifactId>spring-security-web</artifactId>
              <version>4.2.0.RELEASE</version>
        </dependency>
    ```

2. 在web.xml中添加

    ```xml
    <filter>
        <filter-name>springSecurityFilterChain</filter-name>
        <filter-class>org.springframework.web.filter.DelegatingFilterProxy
        </filter-class>
      </filter>
    
      <filter-mapping>
        <filter-name>springSecurityFilterChain</filter-name>
        <url-pattern>/*</url-pattern>
      </filter-mapping>
    ```
3. 新建 com.twx.config.SecurityConfig.java
    ```java
        package com.twx.config;

        import org.springframework.context.annotation.Configuration;
        import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
        import org.springframework.security.config.annotation.web.builders.HttpSecurity;
        import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
        import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

        /**
         * Created by twx on 2017/11/4.
         */
        @Configuration
        @EnableWebSecurity
        public class SecurityConfig extends WebSecurityConfigurerAdapter {

            @Override
            protected void configure(HttpSecurity http) throws Exception {
                http.authorizeRequests()
                        .antMatchers("/list/**").access("hasRole('ADMIN')")
                        .and().formLogin();
            }

            @Override
            protected void configure(AuthenticationManagerBuilder auth) throws Exception {
                auth.inMemoryAuthentication()
                        .withUser("user").password("password").roles("USER").and()
                        .withUser("admin").password("admin").roles("USER","ADMIN");
            }
        }
    ```

4. 让应用上下文扫描到SecurityConfig，在applicationContext.xml中添加如下：

    ```xml
    <context:annotation-config/>
    <bean class="com.twx.config.SecurityConfig"/>
    ```
