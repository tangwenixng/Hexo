---
title: NPAPI控件遮挡弹出框解决方案
date: 2017-12-08 14:16
tags:
- html
- javascript
categories:
- html
- javascript
---

在使用东方网力公司的NP PVA Plugins的过程中，

```html
<object width="100%" height="100%" id="pixwin" standby="Waiting..." type="applicatin/x-firebreath" classid="clsid:294EEBEC-7677-4EBA-B2D7-3FD669FBF2A2" style="z-index: 0;">
    <param name="wmode" value="transparent" />
</object>
```

视频控件总是会挡住弹出窗口。

网上搜索出来的解决方案都是针对Flash和ActiveX，他们都是通过添加
`<param name="wmode" value="transparent" />`设置窗口模式来解决。

我尝试了之后，并不能解决我的问题。

---

后来快绝望的时候，看到一篇文章[关于弹出DIV层被视频显示插件遮挡的解决方案](http://bbs.anychat.cn/forum.php?mod=viewthread&tid=447),终于解决问题了。

**解决方法：**

在要弹出的窗口(Dialog或者Popup)里添加一个透明的、z-index=-1的iframe。这个iframe的作用就是把弹出窗口顶到视频控件的前面。
```html
<iframe frameborder=0 scrolling=no style="background-color:transparent; position: absolute; z-index: -1; width: 100%; height: 100%; top: 0;left:0;"></iframe>
```

或者通过js来动态生产iframe
```js
jQuery(".html5lightbox").append("<iframe style=\"position: absolute; z-index: -2; width: 100%; height: 100%; top: 0;left:0;scrolling:no;\" frameborder=\"0\"></iframe>");
```
