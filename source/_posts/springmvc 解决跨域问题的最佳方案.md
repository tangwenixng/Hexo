---
title: springmvc 解决跨域问题的最佳方案
categories: Spring
tags: Spring
---

[原文链接](https://spring.io/blog/2015/06/08/cors-support-in-spring-framework)

You can add to your @RequestMapping annotated handler method a @CrossOrigin annotation in order to enable CORS on it (by default @CrossOrigin allows all origins and the HTTP methods specified in the @RequestMapping annotation):

```java
@RestController
@RequestMapping("/account")
public class AccountController {

    @CrossOrigin
    @GetMapping("/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }

    @DeleteMapping("/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
```