## 1. 什么是远程仓库（Github）？

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。怎么分布呢？最早，肯定只有一台机器有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分。

你肯定会想，至少需要两台机器才能玩远程库不是？但是我只有一台电脑，怎么玩？

其实一台电脑上也是可以克隆多个版本库的，只要不在同一个目录下。不过，现实生活中是不会有人这么傻的在一台电脑上搞几个远程库玩，因为一台电脑上搞几个远程库完全没有意义，而且硬盘挂了会导致所有库都挂掉，所以我也不告诉你在一台电脑上怎么克隆多个仓库。

实际情况往往是这样，找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

完全可以自己搭建一台运行Git的服务器，不过现阶段，为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub的神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的，所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库。


## 2.新建远程仓库

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以在Github官网进行设置

**第1步**：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Git Bash，创建SSH Key：
使用命令：

```
ssh-keygen -t rsa -C "youremail@example.com"

```

![Clip_20230328_171656.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281716562.png)



如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

![Clip_20230328_171706.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281717556.png)


**第2步**：登陆GitHub，打开“Account settings”，“SSH Keys”页面

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：


![Clip_20230328_171721.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281717430.png)


![Clip_20230328_171732.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281717372.png)


>此时Github会发一条邮箱提示你添加了一个新的 SSH

### 2.1 为什么GitHub需要SSH Key呢？


因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。

确保你拥有一个GitHub账号后，我们就即将开始远程仓库的学习。


## 3.添加远程库


 远程库其实和本地库的实质是一样的，而在GitHub创建一个Git仓库 ，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

![Clip_20230328_171805.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281718216.png)


![Clip_20230328_171815.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281718812.png)


创建成功后，Gitfile仓库是空的,GitHub告诉我们，可以从这个仓库克隆出新的仓库（克隆到本地），也可以把一个已有的本地仓库与之**关联**，然后，把本地仓库的内容推送（push）到GitHub仓库：

![Clip_20230328_171825.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281718743.png)

现在，我们根据GitHub的提示，在本地的Github仓库下运行命令（把本地仓库和远程仓库进行关联） :

- 按步骤添加文件和远程地址

```
echo "# gittest_repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zGuangYuan/gittest_repo.git
git push -u origin main

```

![Clip_20230328_171842.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281718300.png)




**1.初始化仓库**

```
git init 
```

![Clip_20230328_171854.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281719441.png)


**2.添加所有文件到暂存区**

```
git add .
```

- 查看状态

![Clip_20230328_171905.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281719455.png)


**3.提交暂存区的文件到版本库**

```

git commit -m "添加test01和test02文件到版本库"
```

![Clip_20230328_171924.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281719266.png)


**4.切换到 main 分支上**

```
git branch -M main
```

![Clip_20230328_171934.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281719708.png)


**5.添加远程仓库的地址**

```
git remote add origin https://github.com/zGuangYuan/gittest_repo.git
```

>备注：添加后，远程库的名字就是`origin`，这是git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是**远程库。**

![Clip_20230328_171955.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281719730.png)


**6.推送到远程仓库的主分支上**

```
git push -u origin main
```

>实际上是把当前本地分支`main`推送到远程Github的main分支上。**备注：**
**由于远程库是空的，我们第一次推送`main`分支时，加上了`-u`参数，Git不但会把本地的`main`分支内容推送的远程新的`main`分支，还会把本地的`main`分支和远程的`main`分支关联起来，在以后的推送或者拉取时就可以简化命令（使用git push）。**

![Clip_20230328_172003.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281720628.png)


- 查看github的内容

![Clip_20230328_172051.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281720078.png)


从现在起，只要本地做了提交（git commit ） 就可以通过命令：
 git push origin main. 推送到远程github的仓库（把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！）。
 
### 3.1 在本地添加新文件推送到github的例子

**1.在本地工作区新建一个文件**

![Clip_20230328_172058.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281721174.png)


**2.提交到暂存区**


![Clip_20230328_172126.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281721002.png)


**3.提交到本地版本库**

![Clip_20230328_172139.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281721287.png)


**4.把本地版本库和远程版本库进行同步**

>注意：
1.因为前面设置过远程地址了，所有不需要设置远程地址
2.第一次推送的时候版本库和github可能存在文件差异问题，需要使用 -u参数，现在知道没有什么不同，则不需要加-u参数，直接push即可

![Clip_20230328_172150.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281722367.png)


- 查看github的变化

![Clip_20230328_172219.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281722137.png)


## 4.克隆远程仓库

这种方法其实和前面的原理是相似的，目的都是为了把本地的版本库和远程的版本库进行**同步操**作：

> **前面的一种方式完成的工作：**`步骤`
1. 首先在github官网我的账户中建立了一个仓库名为 ： Gitfile
2. 然后在本地创建一个文件夹Gitfile(注意此时这个文件夹并没有初始化为git可以管理的文件夹)
3. 执行命令：git remote add origin https://github.com/xxxx/Gitfile.git ，把本地的版本库和远程的仓库进行关联起来，此时这个命令就包含了git init了，也就意味着已经初始化这个文件夹为git 可管理的，且和远程进行关联。
4. 但是现在工作区和git版本库并没有任何东西，因此创建几个文件，使用 git add 命令把文件添加到暂存器，再使用 git commit 命令把，暂存器的文件提交到版本库的master分支上。
5. 因为本地和远程已经进行关联了，因为远程仓库空的，所以当你把本地文件夹Gitfile 推送到远程仓库（github）的仓库 Gitfile，不会产生冲突，最后使用命令：git push -u origin master ，就可以把本地的master 和远程的master关联起来。



现在假设我们是从头开始，我们先创建远程库，然后从远程库（Github）克隆到本地，完成同步。

**第一步：登陆GIthub ,建立一个新的库命名为：Githubfile**

![Clip_20230328_172304.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281723359.png)


![Clip_20230328_172312.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281723231.png)


> 我们勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件
注意Git仓库地址：

>你也许还注意到，GitHub给出的地址不止一个，还可以用git@github.com:zGuangYuan/Githubfile.git这样的地址。实际上，Git支持多种协议，默认的 git://使用ssh，但也可以使用https等其他协议。使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。
![Clip_20230328_172324.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281723757.png)

**备注**：这里使用的是 https协议。


**2.把远程库创建好了，准备把它克隆到本地：**


`使用命令：git clone  <仓库地址>`

```
git clone https://github.com/zGuangYuan/Githubfile.git
```

新建一个文件夹并在此处Git Bash here

![Clip_20230328_172337.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281723180.png)


![Clip_20230328_172356.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281724661.png)


>备注：
这种方式，则是直接把github仓库中的 Githubfile文件夹克隆到本地，本初始化这个文件夹为git可管理的文件夹，且默认本地版本库的master和远程仓库的master是关联的


### 4.1 在已经克隆的本地仓库中添加文件，并和Github同步

![Clip_20230328_172411.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281724819.png)


**1.把工作区的内容添加到暂存区**


![Clip_20230328_172420.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281724120.png)



>注意：在git add `<file>`命令之前，一定要看一下cmd窗口显示的当前所在目录，比如我是是Githabfile文件夹下，且会显示当前分支是master,如果不在这个文件夹下提交，将会提示失败，切记。
    

**2.提交文件到版本库**

![Clip_20230328_172431.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281724693.png)


![Clip_20230328_172457.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281725651.png)



**3.推送到github 同步本地和远程的版本库**


![Clip_20230328_172504.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281725580.png)


- 查看github文件内容

![Clip_20230328_172517.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281725037.png)


![Clip_20230328_172533.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281725964.png)


同步成功！


