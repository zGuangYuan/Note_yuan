## 1. 什么是分支？


分支就像通道一样，不用的通道都能到达同一个终点，如果多人占用了一个通道，工作速度就会很慢，但是如果每个人都有一个分支（通道），他们就不会互相影响，高效率的完成自己的工作。


## 2.分支的创建和合并

 通过学习我们已经知道，我们每次提交（commit）了文件之后就会连成一条线，都会添加到一个分支（master）,这个成为主分支，到目前为止，我们只有一个分支。`HEAD`严格来说不是指向提交，而是指向`main`，`main`指向提交的，所以，`HEAD`指向的就是当前分支。
 
### 2.1 分支运行机制的图例



一开始main分支是一条线，Git用main指向最新的提交，再用HEAD指向main,
就能知道当前所在分支和当前的提交。
例如：原本如下所示

![Clip_20230328_172840.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281728131.png)


每次提交master分支会向前移动一步： 


![Clip_20230328_172847.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281728580.png)


再次提交一次 ：git commit -m "D",就会如下所示

![Clip_20230328_172855.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281728744.png)



当我们**新建了一个分支**，link,Git就会新建一个指针link,指向和master 相同的提交，然后再把HEAD指向link,表示当前在link这条分支上。

![Clip_20230328_172909.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281729088.png)



注意，现在HEAD指向了link ,现在的提交和修改就是操作 link这个分支了。
比如现在我们提交一个新文件，link指针向前移动一步，而master指针不变。

![Clip_20230328_172918.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281729656.png)




那如果我把我的分支工作完成了，如何合并分支呢？ 


最简单的方法，就是直接把master指向link的当前提交，就完成了合并：

![Clip_20230328_172927.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281729470.png)


合并完成后我们甚至可以删除分支link ,这样我们就剩下一条master分支了。

![Clip_20230328_172934.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281729568.png)



### 2.2 分支的创建和合并的命令

```
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

```

```

git branch -r       #查看远程所有分支
 
git branch           #查看本地所有分支
 
git branch -a       #查看本地及远程的所有分支，如下图
 
git fetch   #将某个远程主机的更新，全部取回本地：
 
git branch -a  #查看远程分支
 
git branch  #查看本地分支：
 
git checkout 分支 #切换分支：
 
git push origin -d 分支名  #删除远程分支: 
 
 git branch -d 分支名  #删除本地分支
 
git remote show origin  #查看远程分支和本地分支的对应关系
 
git remote prune origin #删除远程已经删除过的分支

```

### 2.3 分支创建和合并的例子(远程同步)

承接上面的第二节的例子。

![Clip_20230328_172943.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281729086.png)



![Clip_20230328_172956.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281729899.png)


此时只有一个 main 分支

**1.创建一个新的分支 link**


![Clip_20230328_173004.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281730007.png)


**2.切换到link分支，并查看当前的分支有多少**


![Clip_20230328_173015.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281730877.png)


**3.在Githubfile 新建一个文件提交到link分支上**

![Clip_20230328_173025.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281730287.png)


![](index_files/6f8612a1-d235-4c49-825b-e6edd5f90048.png)

**4.把版本库的变化推送到远程仓库中**

![Clip_20230328_173035.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281730117.png)


- 查看远程仓库

![Clip_20230328_173055.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281730840.png)


**5.在本地切换到 main分支上，查看有什么变化**


![Clip_20230328_173105.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281731376.png)


- 这是为什么呢？

![Clip_20230328_173112.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281731092.png)


>因为此时，HEAD 执行的是 main分支，但是并没有删除 link分支上的东西

**6.把 main 分支上的东西合并到link分支上**

>因为link分支是做了比main更多的工作，因此合并之后，main分支应该会多出一个 testfiel1.txt 文件，并不会发生什么冲突（但是如果link分支是删除文件，main合并之后会发生什么东西呢？）

我们把master分支的工作成果合并到link分支上： 
使用命令：`git merge <name>`
    
![Clip_20230328_173124.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281731720.png)


![](index_files/3e9265d9-f7f5-4cbe-a117-15a8b0e8976c.png)

**7.现在把这个合并的操作同步到github中，让远程仓库也进行合并**


![Clip_20230328_173138.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281731474.png)


>注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向link的当前提交，所以合并速度非常快。
当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。
合并完成后就可删除link了，其实就是删除一个指针，指针master 和 link 指的是同一个地方，所以可以删除一个。  


**8.删除link分支**


![Clip_20230328_173147.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281731356.png)


- 此时远程仓库并不会删除的

![Clip_20230328_173159.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281732028.png)



**9.同步本地和远程仓库 的版本库**

`强制删除远程分支：`

```

git push --delete origin [branch name]

```

![Clip_20230328_173209.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281732725.png)


![Clip_20230328_173218.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281732128.png)


### 2.4 分支创建和合并例子2

**1.新建一个分支 link1 并切换到该分支上**

```
创建+切换分支：git checkout -b <name>

```

![Clip_20230328_173226.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281732167.png)


**2.在本地仓库新建一个文件 tstefile2**

![Clip_20230328_173336.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281733306.png)



**3.把这个改变提交到版本库**

![Clip_20230328_173345.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281733443.png)



**4.查看当前分支并把本地分支更新到github**

![Clip_20230328_173354.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281733210.png)


![Clip_20230328_173404.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281734049.png)


- 查看远程的所有分支

![Clip_20230328_173415.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281734344.png)



**5.切换到main分支上**

![Clip_20230328_173548.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281735953.png)


**6.本地把main分支合并到link1分支上**

![Clip_20230328_173556.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281736787.png)


![Clip_20230328_173606.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281736511.png)



**7.把本地的合并操作同步到远程仓库**

![Clip_20230328_173627.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281736887.png)


**8.查看远程和本地的分支**

![Clip_20230328_173637.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281736280.png)


**9.删除本地分支，并删除github的分支**

```
  a.使用git branch -d 分支名来删除本地分支。
  b.使用git push origin -d 分支名直接来删除远程分支。在次使用git branch -a,发现分支已经不存在了。
or
   a.使用git branch -d 分支名来删除本地分支。
    b.最简单的解决办法就是直接到gitlab/github进行删除.
```

![Clip_20230328_173645.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281736175.png)


### 2.5 例子3：远程删除分支，本地同步

**1.本地新建一个分支 link2,并在该分支上添加testfile3文件 **


![Clip_20230328_173707.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281737756.png)


**2.把本地的分支推送到远程分支上**

![Clip_20230328_173714.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281737249.png)


![Clip_20230328_173728.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281737373.png)



**3.直接在github远程仓库中删除 link2分支**

![Clip_20230328_173738.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281737289.png)


![Clip_20230328_173750.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281737271.png)

```
1.git branch -a查看远程分支，红色的是本地远程远程分支记录。
 
2.执行下面命令查看远程仓库分支和本地仓库的远程分支记录的对应关系：
 
  git remote show origin  
 
3.会看到：
 
 refs/remotes/origin/远程仓库已经删除的分支名            stale (use 'git remote prune' to remove)
 
 其中：
 
 Local refs configured for 'git push':  命令下面的分支是本地仓库的远程分支记录中仍存在的分支，但远程仓库已经不存在。
 
4.输入git remote prune origin来删除远程仓库已经删除过的分支
 
5.验证 git branch -a
 
  此时可以看到本地远程分支记录已经和远程仓库保持一致了。

```

![Clip_20230328_173810.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281738460.png)


- 删除远程仓库已经删除过的分支

![Clip_20230328_173819.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281738471.png)


- 强制删除 link2分支

![Clip_20230328_173826.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281738454.png)


## 3.分支合并冲突的解决


### 3.1 例子1：解决冲突的文件

**1.在main 分支上创建一个testfile4文件**

![Clip_20230328_173834.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281738442.png)


- 提交到版本库（main）

![Clip_20230328_173843.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281738867.png)



**2.建立一个新的分支 link3 ，并切换到link3分支**

![Clip_20230328_173851.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281738433.png)




**3.修改testfile4文件**

![Clip_20230328_173900.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281739096.png)


**4.提交文件到link1上**

![Clip_20230328_173910.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281739254.png)


**5.切换回到main分支上**

>此时main分支上是旧的数据，没有新增文字




