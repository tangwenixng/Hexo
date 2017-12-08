---
title: Promise
date: 2017-12-08 23:02
tags:
- javascript
categories:
- javascript
---

Promise对象是一个构造函数
```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code
  //resolve和reject。它们是两个函数，由 JavaScript 引擎提供
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});

promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```
then方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。其中，第二个函数是可选的，

**实例**
```javascript
/************100ms后回掉resolve
**************************/
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});

/*******************************/

let promise = new Promise((resolve, reject) => {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});
/********Promise resolved**************/
```

