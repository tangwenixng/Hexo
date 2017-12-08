---
title: 搭建hexo博客
categories: 教程
tags: [Hexo]
---

![唯](/images/wei.png "小唯")

## 本地安装
1. 安装 hexo
> npm install -g hexo

2. 随便新建一个目录（比如E:/Hexo），在此目录下执行 `hexo init`

3. 安装依赖包  `npm install`

4. 本地执行
    ```text
     hexo g
     hexo s
    ```
    然后在浏览器中输入 `http://localhost:4000/`访问

  **附注**：常用命令

  ```text
      hexo g 
      hexo s 
      hexo d 
      hexo n  
  ```
---

## 上传到Git

1. 在自己的github上创建一个仓库，比如我的 `tangwenixng.github.io`

2. 然后打开 `E:/Hexo/_config.yml`,编辑
    ```text
    deploy:
          type: git
          repo: git@github.com:tangwenixng/tangwenixng.github.io.git
          branch: master
    ```
3. 配置好第2步后，执行以下命令，部署到git上:

    ```text
      hexo g
      hexo d
    ``` 

---


## 主题仓库

地址： `https://hexo.io/themes/`

---

## 在文章中添加图片
   
   [Hexo博客搭建之在文章中插入图片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)

1. 把图片统一放入到`source/images`文件夹中,使用 `![description](/images/***.jpg)`来访问
2. ***


## 更改主题huno侧边栏图片

**打开 `huno/source/css/uno.css`,修改 `background url`**  
> .panel-cover {
  display: block;
  position: fixed;
  z-index: 900;
  width: 100%;
  max-width: none;
  height: 100%;
  background: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1510661078587&di=3d6f9cb43764dc70114498f6b6b3d648&imgtype=0&src=http%3A%2F%2Fi2.hdslb.com%2Fbfs%2Farchive%2Fad56241053dba699a81c1a528b47ba3b4069f08b.jpg) top left no-repeat #666666;
  background-size: cover; }



参考来源:

[hexo干货系列：（一）hexo+gitHub搭建个人独立博客](http://tengj.top/2016/02/22/hexo1/)






