## 1.上传没有包含大于100M文件的代码

![Clip_20230328_174045.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281740978.png)



### 1.1 上传的步骤

#### -新建一个仓库

![Clip_20230328_174105.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281741050.png)


---

得到

![Clip_20230328_174116.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281741102.png)

```python
echo "# LFS_Test3" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zGuangYuan/LFS_Test3.git
git push -u origin main
```

--- 

```python
git remote add origin https://github.com/zGuangYuan/LFS_Test3.git
git branch -M main
git push -u origin main
```

#### -在需要上传的文件夹进行执行git Bash


![Clip_20230328_174129.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281741300.png)


#### -按步骤添加文件和远程地址

- 初始化

```
git init
```

- 添加所有的文件

```
git add .
```

- 提交改变

```
git commit -m "add files without models"

```

![Clip_20230328_174138.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281741820.png)


- 切换到 main 分支上

```
git branch -M main
```

- 添加远程仓库的地址

```
git remote add origin https://github.com/zGuangYuan/LFS_Test3.git
```

- 推送到远程仓库的主分支上

```
git push -u origin main
```

![Clip_20230328_174147.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281741903.png)



查看github的状态

![Clip_20230328_174204.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281742443.png)


>上传完就可以关闭git Bash了


---

## 2.上传大文件到 LFS_Test3 目录中

![Clip_20230328_174228.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281742463.png)



### 2.1 上传大文件的步骤

#### -在大文件文件夹git Bash

![Clip_20230328_174241.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281742628.png)


#### -步骤


- 初始化

```
git init 
```

![Clip_20230328_174251.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281742015.png)


- 切换到主分支上

```
git branch -M main
```

- 关联远程仓库

```
git remote add origin https://github.com/zGuangYuan/LFS_Test3.git
```

- 拉取仓库的代码并重新设置新的源

```
git pull --rebase origin main
```

![Clip_20230328_174305.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281743968.png)



- 安装添加大文件

```
git lfs install
```

![Clip_20230328_174313.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281743490.png)


- 设置跟踪的大文件

```
git lfs track "rbs_weights.hdf5"
```

![Clip_20230328_174321.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281743804.png)


- 上传 .gitattributes

```
git add .gitattributes
```

- 提交 gitattributes

```
git commit -m "attributes"
```

![Clip_20230328_174330.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281743825.png)


- 推送到远程仓库

```
git push -u origin main
```

![Clip_20230328_174341.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281743834.png)


- 添加大文件

```
git add rbs_weights.hdf5
```

- 提交改变

```
 git commit -m "add model"
```

![Clip_20230328_174350.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744986.png)


- 开始上传大文件

```
git push -u origin main
```

![Clip_20230328_174407.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744010.png)


![Clip_20230328_174415.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744357.png)


---

## 3.把上传的大文件移动到model中


>有一些大文件是不可以直接在github进行移动得到。但是可以通过命令的方式进行一定，配合本地操作。

#### -新建一个新的本地文件夹克隆

![Clip_20230328_174423.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744882.png)

```
git clone https://github.com/zGuangYuan/LFS_Test3.git
```

- 得到和远程仓库相同的目录结构

![Clip_20230328_174432.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744649.png)


#### -在本地移动文件夹

![Clip_20230328_174440.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744088.png)



#### -进入LFS_Test3再git Bash

![Clip_20230328_174450.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281744854.png)


#### -查看状态 git status

```
git status
```

![Clip_20230328_174458.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281745019.png)


#### -add 和commit

- add

```
git add
git status
```

![Clip_20230328_174507.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281745037.png)


- commit

```
git commit -m "move file"
```

![Clip_20230328_174515.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281745594.png)


#### -推送到main分支上

```python
git push -u origin main
```

![Clip_20230328_174527.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281745280.png)


#### -查看远程仓库

![Clip_20230328_174539.png](https://raw.githubusercontent.com/zGuangYuan/pic/main/Ob/pic/202303281745545.png)



## 4.官方教程地址

[Github官网教程](https://docs.github.com/cn/repositories/working-with-files/managing-files/moving-a-file-to-a-new-location "Github官网教程")

