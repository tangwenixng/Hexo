---
title: Git一点点操作而已
categories: Git
tags: [Git]
---

添加远程仓库地址： `git remote add origin git@blabla.com`
删除远程仓库地址： `git remote rm origin`
修改远程仓库地址： `git remote set-url origin git@bilibili.com`

---

添加到暂存区(Index)同时提交到HEAD: `git commit -am 'blabla' `
> 注意：这种方法只对已经存在Index里的文件有效。假如有一个新文件a.txt,还从未被添加Index中，那-a就不管用了，需要手动`git add`
-a： Tell the command to automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected.

---
命令取别名：打开~/.gitconfig,添加如下配置
    ```
    [alias]
    st = status
    cm = commit
    ct = checkout
    ```
现在可以使用`git st`代替`git status`

---

重新修改提交信息： `git commit --amend`

---

1、 `git reset`==`git reset --mixed`：Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) 
**通过git add添加到Index,但还没通过git commit添加到HEAD区里的**文件，可以通过git reset来撤销git add。
**说白了，就是撤销git add。此条命令不会影响工作区。**

2、 `git reset --soft`: Does not touch the index file or the working tree at all。This leaves all your changed files "Changes to be committed"
此条命令不会影响到目前的Index和工作区，只是把HEAD重置到commit。但是重置到HEAD区后，Index区会有一些未提交的信息。相当于  HEAD-commit 之间Index区没提交的信息。
**说白了，就是撤销git commit**

3、 `git reset --hard`: Resets the index and working tree.
**慎用此命令，你的Index和工作区全部回到commit这个状态，意思就是你当前所有做的改变都会丢失。**

---

忽略跟踪已在远程仓库里的文件:

1、 在worktree里：

`git rm --cached file`(把文件从暂存区index中删除)

在.gitignore中添加此此文件

`git commit -m  'mark'`

`git push`

2、 其他用户在pull代码之后，他们的暂存区也没有了那个文件，同时忽略了此文件，所有用户即使更新了此文件也不会在git status中显示，也不能被添加（git add）;

3、 .gitignore只能忽略不在index里的内容

---
[HEAD^ 和 HEAD~ 区别](https://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git)

有一个概念很重要： **Git 提交不只一个父节点**

其实看文字描述不是很容易懂，直接看stackflow上大神的神图吧

说明： **节点B、C都是A的父节点。提交顺序从左到右。**

```
G   H   I   J
 \ /     \ /
  D   E   F
   \  |  / \
    \ | /   |
     \|/    |
      B     C
       \   /
        \ /
         A

A =      = A^0   
B = A^   = A^1     = A~1
C = A^2  = A^2                                      #A^2  A的第二个父节点
D = A^^  = A^1^1   = A~2                            #A^=C C^=D ==>> A^^=D
E = B^2  = A^^2
F = B^3  = A^^3
G = A^^^ = A^1^1^1 = A~3
H = D^2  = B^^2    = A^^^2  = A~2^2
I = F^   = B^3^    = A^^3^
J = F^2  = B^3^2   = A^^3^2
```
从上面这张图可以看出，A~2=D,说明`~`是主干线上的提交记录。

---

> gitk: 用于查看某个文件的所有提交记录
