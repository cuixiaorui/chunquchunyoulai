
## 背景
做开源的时候，经常会收到别人的 pr， 那么如何可以运行别人的代码呢？

github 告诉我们别人提交的 pr 都涉及到哪些代码的更改，但是还不够，因为有时候光看代码的话根本不知道到底有没有运行时错误。那怎么办呢？我们就要想办法把别人的 pr 代码跑起来

这篇文章就是记录如何把别人的 pr 代码跑起来


## 思路

思路其实很简单，就是把别人的代码 pull 到我们本地分支，然后跑一跑看看有没有问题就完事了。

那怎么做到呢？

## How
接着模拟整个 pr 的过程，说明整个流程

当你早上起来的时候上了一下 github ，发现有社区里的同学给你的开源库提交了一个 pr

那你赶紧去看看这个 pr 质量如何

发现噢，代码还不错，github 告诉我们都是改动了哪些代码

但是呢，你会考虑一个问题，那这个代码在运行时会不会有问题呢？

为了验证这个问题，你需要想办法把这个代码拉取到你的本地，然后跑一下看看有没有问题

那拉取的时候肯定要先创建一个分支，然后把别人的代码拉取过来

接着你打开终端敲入了一行 git 命令

```js
git checkout -b "name-branchName" master
// 例如
// git checkout -b “yeyuqiudeng-refactor/emitter” “master”
```

先创建一个分支，这里的分支名规范是：
- name 贡献者名称
- branchName 对应的分支名

> 这里的 branchName 其实就是代码所在仓库的分支

好，分支我们已经创建好了 接着就需要把贡献者的代码拉取过来了
> 有没有感觉创建一个分支就好比准备了一个容器啊

```js
 git pull [url] [branchName]
 // 例如
 // git pull https://github.com/yeyuqiudeng/element3.git "refactor/emitter" 
```
好，上面这个命令就是要把贡献者的代码给拉取到我们的分支来

平时我们更多的使用 git pull 的场景都是这么来用
```js
git pull origin master
```

其实它还可以指定远程的 git 仓库 + 具体的 branch 来拉取代码

这样的话，我们就已经把代码给拉取下来了

接着就是 review 代码，跑起来 看看运行时有没有问题，或者是解决一些冲突

当都处理完成后，你就需要把代码 merge 到我们的 master 分支了

那怎么合并呢

```js
 git checkout master
 
 git merge --no-ff [name-branchName]
```

先回到你的主分支，这里是 master 

然后用 merge --no-ff 合并之前的分支

这里要注意 --no-ff 是为了保留之前分支的提交记录，方便后续查看

到这里的时候其实你就已经处理完整个流程了

剩下的就是把当前 master 分支的代码 push 到远程上即可

```js
git push origin master
```



## 总结
小小总结一下，就是拉取贡献者的分支到本地，然后 review 完成后，push 到主分支

第一步：创建分支，拉取贡献者提交的代码
```js
git checkout -b motao314-master master
git pull https://github.com/motao314/element3.git master
```

第二步：合并新的代码然后更新到 github 上

```js
git checkout master
git merge --no-ff motao314-master
git push origin master
```
