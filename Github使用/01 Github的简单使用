## 1. Git的安装


从官网直接下载即可，正常安装，但是不要有中文路径，地址：[官方安装地址](https://git-scm.com/downloads)
安装完成会在桌面的菜单键看到 git Bask 字样。



![Clip_20230328_165306.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281653485.png)



因为git是分布式版本系统，每个机器都得有自己的认证识别号，输入下面的命令设置。

### 1.1 git config的介绍

>参考：https://blog.csdn.net/liuxiao723846/article/details/83113317

Git的三个重要配置文件分别是
`/etc/gitconfig`

>安装目录下的gitconfig![Clip_20230328_165602.png|500](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281656806.png)





`${HOME}/.gitconfig`
>在用户目录下![Clip_20230328_165631.png|500](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281656015.png)




`.git/config`
> 具体项目下 ![Clip_20230328_165645.png|500](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281656954.png)
这三个配置文件都是Git运行时所需要读取的，但是它们分别作用于不同的范围。


**/etc/gitconfig**: 系统范围内的配置文件，适用于系统所有的用户； 使用 git config 时， 加 --system 选项，Git将读写这个文件。

**${HOME}/.gitconfig**: 用户级的配置文件，只适用于当前用户； 使用 git config 时， 加 --global 选项，Git将读写这个文件。

**.git/config**: Git项目级的配置文件，位于当前Git工作目录下，只适用于当前Git项目； 使用 git config 时，不加选项（ --system 和 --global ），Git将读写这个文件。

每个级别的配置都会覆盖（ override ）上层的相同配置，覆盖的顺序是 ：
.git/config --> ${HOME}/.gitconfig --> /etc/gitconfig , 可越级覆盖。
比如 .git/config 里的配置会覆盖 /etc/gitconfig 中的同名变量。在 Windows 系统上，Git 会寻找用户主目录下的 .gitconfig 文件。主目录即 ${HOME} 变量指定的目录，一般都是C:\Documents and Settings\${USER}。另外，你也可以使用 --file 或者 -f 来指定想要读写的配置文件。比如：

```
git config --file .git/config user.name  # 查阅项目配置信息里的用户信息。
git config --file .git/config user.name "Harrison F" # 将用户信息配置到项目的配置文件中。

```

#### 1.1.1 gitconfig 文件的生成

了解了这三个文件后，下面我们来看看git config的使用。当你在第一次安装完Git后，直接运行 

```
git config --system --list 
git config --global --list

```

你将会分别看到下面的错误信息。没关系，这是因为你还没有配置过Git，Git的配置文件还没有生成。当你配置了一个信息后，相应的文件就会自动生成。

```

harrison@ubuntu:~$ git config --global --list
fatal: unable to read config file '/home/harrison/.gitconfig': No such file or directory
harrison@ubuntu:~$ git config --system --list
fatal: unable to read config file '/etc/gitconfig': No such file or directory

```

#### 1.1.2 gitconfig 常用的配置信息

**1）用户信息（user.*）**

首先，需要配置的是你的用户名和Email地址。这两条配置非常重要，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录。

```

$ git config --global user.name "Harrison F"
$ git config --global user.email harrison.f@gmail.com

```

使用了 --global 选项，所以，这些信息将被写入` ${HOME}/.gitconfig` 中； 如果在特定的项目中，要使用其他的用户名或者Email地址，只需重新配置时去掉 --global选项，新的信息将被写入 .git/config 中。 设置完这两条基本信息后，你应该可以提交更新了，但是为了让我们更方便的使用Git，我们还有几个重要的信息需要配置。

**2）文本编辑器（core.editor)**
Git会在 需要你输入一些额外消息的时候自动调用一个外部文本编辑器给你使用。 默认会使用操作系统指定的默认编辑器，一般可能会是 Vi 或者 Vim。如果你有其他偏好，比如 Gedit的话，可以重新设置：

```
$ git config --global core.editor gedit
```

**3）字体颜色（color.*）**
如果这个信息不配置，那么你与Git交互时，所有字体的颜色都将是默认系统的一个颜色，很难看，而也不方便我们看出更新和变化。

```
$ git config --global color.ui auto
$ git config --global color.status auto
$ git config --global color.branch auto
$ git config --global color.diff auto
$ git config --global color.interactive auto

```

**4）差异分析工具（merge.tool)**
差异分析工具是用来解决合并冲突的，Git将在出现合并冲突时自动调用配置好的差异分析工具。

```
$ git config --global merge.tool vimdiff                # 使用Vimdiff作为差异分析工具
```

**5）配置代理（http.proxy)**
一般在公司内想要获取互联网上的Git项目，都要求设置HTTP代理。这里将设置最简单的HTTP代理。

```
$ git config --global http.proxy http://proxy.companyname.com:8080/ 
```

#### 1.1.3 基本命令（增、删、改、查）

我们这里学习最基本的Git配置和git config命令基本的用法。那么我们如果想删除一些不想要的配置怎么办呢？最直接办法就是编辑配置文件，但是这里还有更简单的命令来删除不想要的配置信息。



1）增：

```
git config --global --add configName configValue
```

2）删：

```
git config  --global --unset configName   (只针对存在唯一值的情况)
```

3）改：

```
git config --global configName configValue
```

4）查：

```
git config --global configName
```

示例：

```
//查
git config --global --list
git config --global user.name
 
//增
git config  --global --add user.name jianan
 
//删
git config  --global --unset user.name
 
//改
git config --global user.name jianan
```

#### 1.1.4 git的基本命令

`提交文件的步骤`

**1.把文件添加到本地仓库**

```

git add 文件名

```

**2.把文件提交到本地仓库**

```
git commit -m "备注信息"

```

---

`查看当前目录下git文件是否改变status`

```

git status

```

---

`查看和上一次发生的变化 diff`

```

git diff 文件名

```

---

`查看修改的历史记录`

```

git log

```

- 简化参数

```
git log --pretty=oneline
```

---

`版本返回`

```

git reset

```

使用示例：git reset --heard HEAD^

---


`历史命令`

```

git reflog

```

### 1.2 设置机器识别号(名称和邮箱)

>`注意`：把 "Your name" 换成自己的名字，把 "email@example.com"换成自己的邮箱！


`查看当前的Git是否有设置用户名和邮箱（这是一个识别号）`

**方法一：在gitBash 使用以下代码可以或查看 名字和邮箱**

```
#名字

git config user.name

#邮箱

git config user.email

```

![Clip_20230328_165727.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281657621.png)



**方法二：本地查找 .gitconfig 文件（可以使用everything进行搜索）**

> - 文件一般在：**C:\Users\84156 ** 用户目录下

![Clip_20230328_165739.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281657170.png)



- 代码

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

```

>这个改变的是 用户目录下 的 .config文件


## 2.本地版本库的创建和使用（respository)

**前言**

`版本库`：简单一点可以看作一个目录，创建这个目录可以被Git管理，在里面的文件，你可以看到他的修改内容和历史修改痕迹，以及数据还原恢复。

### 2.1 版本库的创建和基本使用实例-添加、提交文件


**1.创建一个版本库**

```
# 创建一个目录

mkdir 目录名

#跳转到当前目录

cd 目录名

# 显示当前目录

pwd 


```

- 在指定目录下 Git Bash here

![Clip_20230328_165828.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281658369.png)


**2.把目录变成git可以管理的目录**

```
# 初始化

git init

```

![Clip_20230328_165841.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281658964.png)



**3.创建文件添加到版本库**

- 创建一个testfile.txt 文件
- 编辑文本并保存

![Clip_20230328_165855.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281659309.png)


- 把文件添加仓库 到 仓库

```

git add testfile.txt

```

- 把文件提交到仓库

```

git commit -m "第一次提交textfile文件"

```

![Clip_20230328_165909.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281659961.png)


### 2.2 版本库的创建和基本使用实例-修改文件

上面已经完成在git创建一个textfile.txt 文件，并且Git已经可以管理。

**4.修改testfile文件**

![Clip_20230328_165925.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281659214.png)


既然，git可以管理我们这个文件，那么他肯定已经知道我们已经修改了文件里面的信息了。


- 查看文件状态

```

git status

```

![Clip_20230328_165936.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281659302.png)



>`备注`：git status 命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，textfile.txt被修改过了，但还没有准备提交的修改。



**5.查看某个文件是否变化**

![Clip_20230328_165948.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281659114.png)



**6.提交当前改变的文件到本地版本库**



![Clip_20230328_170002.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281700946.png)

>显示一个文件改变，删除一行，插入一行。（就是改变一行）



**7.再次修改文件，提交**


![Clip_20230328_170013.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281700926.png)


![Clip_20230328_170020.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281700181.png)



### 2.3 退回上一次编辑的位置


>GIt如何从上一次提交后的文件退回到上一次的文件编辑，（就像你打单机游戏一样，你过关斩将，等游戏结束了之后，你需要存盘，但是如果新的一关成绩不理想，你可以重新退出到上一次的游戏重新开始玩，回到上一次存盘的地方）。

**1.查看历史记录**

![Clip_20230328_170030.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281700778.png)


>注意：在commit一行上看到一大串的 93753...... 的数字commit id(版本号)用处后面讲解，是十六进制的表示方法，这是因为Git是分布式的版本控制系统，所以每一个人的ID 肯定不一样，就像身份一样。
在修改日志中，我们可以看到我们修改的次数是三次，也就是提交的次数，最近一次是"third edit ,add three",我们可以看到修改的次数，作者，和修改日期。


- 简化参数

![Clip_20230328_170039.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281700063.png)



**2.退回上一次编辑的内容**

现在我们把 textfile.txt 的文本内容退回到上一个版本。也就是 “第二次编辑...”.

Git 用 HEAD 表示当前版本，也就是 “第三次编辑...” 

>以此类推，前1000次的应该有1000个 “^”,放心，GIt绝对是人性化的，它可以表示为：HEAD~1000


![Clip_20230328_170050.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281700276.png)



- textfile 已经 发生变化

![Clip_20230328_170059.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281701089.png)


**3.再次查看历史的记录**

![Clip_20230328_170108.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281701085.png)


### 2.4 回到已经删除的位置（redo)


**1.查看历史命令**

![Clip_20230328_170118.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281701940.png)




**2.直接返回 到 dfc8099 编号**


![Clip_20230328_170130.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281701125.png)


- 查看textfile.txt 文件

![Clip_20230328_170138.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281701331.png)


**3.查看历史命令**

![Clip_20230328_170153.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281701482.png)




## 3. 工作区和暂存区

### 3.1.何为工作区（Working Directory）？

 在Git中，工作区就是一个目录，能在本地缓存数据的地方。
 
 ![Clip_20230328_170207.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281702486.png)

 
### 3.2.何为版本库（Repository） ？

在初始化(使用 git init命令初始化)版本库时,生成了一个（.git）文件夹，如上图所示，那是Git的版本库 。

   Git的版本库里面存放了很多东西，不一一剖析，最终要的就是 stage (或者成为index索引)的暂存区，我们创建的第一个分支 maser分支,以及指向master的指针HEAD

 前面我们把文件添加到Git版本库，分两步：

* 第一步：git add,把文件添加进去，实际上是把文件修改，添加到缓存区（stage）。

>备注：此时使用命令 git status ,可以看到本地版本库的状态，可以看到文件修改。

* 第二步：git commit ,提交更改，实际上把暂存的内容，全部提交到本地的master分支上，此时暂存器变空。

>备注：此时使用命令 git status ，可以看到看到提示，暂存器为空，已经把修改提交到master上。

### 3.3 例子：版本库如何运作




我们修改前面的textfile.txt 里面的内容。增加一行内容："add a new line"

![Clip_20230328_170223.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281702931.png)


然后再工作区新添加一个文本文件 NEW.txt

![Clip_20230328_170244.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281702026.png)


我们使用命令：git status ,看看Git的版本库有没有变化

![Clip_20230328_170255.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281703887.png)


提示我们，textfile.txt 被修改，而NEW.txt 没有被添加过，状态显示是 Untracked.

接下来把，textfile.txt 和NEW.txt 全部都 add 到版本库 ，然手再看一下状态,命令：git status

![Clip_20230328_170311.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281703989.png)


看一下现在暂存区的状态：

![Clip_20230328_170326.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281703342.png)


所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

![Clip_20230328_170343.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281703533.png)


提交了以后，工作区就会变空，命令：git status 查看一下

![Clip_20230328_170356.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281704410.png)


那么此时版本库就是这样子：

![Clip_20230328_170407.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281704999.png)


## 4. Git的修改(modify)、管理和删除文件

### 4.1 git的修改

**什么是修改?**

 修改（modiify），在原有文本新加一行、需改一个字符、新建一个文件在Git都是修改。
 
 
**### 为什么说git管理的是修改而不是文件呢？**
 
 * 做个实验，修改textfile.txt文件，新添加一行文字。
 
![Clip_20230328_170421.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281704367.png)

 
 添加到GIt.然后看一下状态：git status
 
![Clip_20230328_170446.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281704302.png)

 
 在同一行上，再次修改textfile.txt 文件：
 
 
![Clip_20230328_170459.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281705513.png)

 
 这次没有git add,直接提交我们看看（并未添加到暂存器，而只有在暂存器的内容才会提交到master分支上）：
 
![Clip_20230328_170508.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281705970.png)

 
 看看当前状态：git status
 
![Clip_20230328_170519.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281705819.png)

 
 可以看见第二第的修改并没有被提交上去，为什么？
 
 回顾一下，我们刚刚的步骤，我们修改一个文件 然后git add,再次修改文件后没有git add,直接git commit 上去，前面我们说过了工作区和版本库的概念， git add命令实际上就是把要提交的所有修改放到暂存区（Stage），而git commit 命令则是一次性把暂存区里面的东西一次性提交到分支（master）,所以 git commit 只是负责把暂存区里面的东西提交，而第二次修改没有git add，也就没有把工作区的修改给添加到暂存区（Stage）,因此就不会被提交。

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：

![Clip_20230328_170529.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281705281.png)


所以确实第二次的修改没有被提交。

**总结：每次修改后没有被git add 到暂存区，在 git add 之后就不会添加到分支（master）去。**

### 4.2 git的撤销修改


#### 4.2.1 撤销修改的例子

是人就是难免会犯错误，在GIt中还有补救的方法，撤销修改。

你现在修改textfile.txt 文件后，你突然不想修改了怎么办？

![Clip_20230328_170541.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281705876.png)


使用命令：**git status** 看一看

![Clip_20230328_170554.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281705932.png)


在你看status 的时候，Git提示你可以用 git checkout --file 可以丢弃工作区的修改 。我们试试：

![Clip_20230328_170603.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281706629.png)


果然回到了原来的状态

![Clip_20230328_170612.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281706736.png)


`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

#### 4.2.2 git checkout -- file 注意事项

`注意`：git checkout -- textfile.txt 的意思是吧textfile.txt 文件的修改全部撤销，有两种情况：

**第一种**：从textfile.txt编辑后就没有被git add（添加到暂存区） 过，现在撤销就和版本库一模一样。
**第二种**：textfile.txt 修改后被添加到暂存区，又做了修改，现在撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。


#### 4.2.3 修改和撤销修改的例子

上面那个是在textfile.txt 修改后，没有添加到暂存区，但是如果修改完还添加到（git add）暂存区怎么办,按照上面的思路我们在看看：

![Clip_20230328_170628.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281706052.png)


Git同样告诉我们，用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

`注意：git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

![Clip_20230328_170642.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281706276.png)


我们在看看状态：git status

![Clip_20230328_170652.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281706898.png)


现在暂存器（stage）是干净的，但是工作区有修改，和我们预想的一样，也确实如此。

还记得我们如何把工作区还原到最近一次吗？ 使用命令：git checkout -- file

![Clip_20230328_170705.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281707443.png)


再看看textfile.txt的内容。又回到最近一次状态

再次看看状态：git status

![Clip_20230328_170718.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281707578.png)


现在工作区没有被修改，暂存区也是空的。

## 4.3 git删除文件

我们说过Git 检测是修改，而不是文件。删除也是一种修改。

我们试一试，新建一个文件 project.txt ,并提交到Git

![Clip_20230328_170818.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281708524.png)



你想删除在Git的project.txt 文件，一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了（删除工作区）：

![Clip_20230328_170836.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281708382.png)


那么，Git马上就会知道，你把project.txt 删除了，检测出版本库和工作区不一致。

![Clip_20230328_170846.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281708719.png)


现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：

![Clip_20230328_170855.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281709659.png)


现在文件就从版本库删除了。工作区同样也删除了（实现了工作区和版本库的同步）。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

使用命令：git checkout -- file

注意：git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

>**总结**：命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。





