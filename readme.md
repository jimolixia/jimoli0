[TOC]
# 代码
## git init 初始化 
+ `git init` 将当前文件夹变为git版本库，    
+ windows可以左键，选择`git bash here` 完成

## git add 将工作目录的某项目提交到暂存区 
+ `git add [xxxx.xxx]` 提交一个文件到缓存区
+ `git add .` 提交工作目录

## git commit 将暂存区文件保存到本地仓库
+ `git commit -m "[备注]" [xxxx.xxx]`
+ `git commit [xxxx.xxx]`
  + 不推荐这种方法，但如果一不小心点错了，此时会出现一个编译器，要求程序员增加注释:
  + 如何退出：
    + 按i键-> 在cmd上编辑内容-> :wq-> Enter

## 查看信息
### git status 查看当前本地仓库状态
+ `git status`
  + 会出现四个信息，不同情况信息出现不同：
    + 位于分支：显示当前所在的分支名称。
    + 工作目录状态：显示未暂存的修改、新增或删除的文件等工作目录中的变更。
    + 暂存区状态：显示已经添加到暂存区但尚未提交的文件变更。
    + 提示信息：根据当前状态提供一些建议和下一步的操作建议。

### git log 显示提交过的文件版本
+ `git log` 显示提交过的文件与每个版本的编码，可以复制这个编码，然后回退。
+ `git log --pretty=oneline` 更清晰的信息
    + 按q退出

### git differ 查看不同版本区别
+ `git differ`
  > 会出现：
  > 1. 第一行：正在比较的两个文件名 
  >     + 例子：`diff --git a/readme.md b/readme.md`
  > 2. 第二行：两个版本的检索信息
  >     + 例子：`index 92ee4e7..c05d9e2 100644`
  > 3. 三、四行：两个版本的路径
  >     + 例子：`--- a/readme.md。+++ b/readme.md`

### git reflog 查看进行过的操作
+ `git reflog`（reflog == reference log）查看日进行过的操作(包含注释)

## git rm 删除文件
+ `git rm -- catch [xxxx.xxx]` 删除本地库里的某个文件，一般用这个就好
+ `git reset` 本来不是干这个的,但
+ `git chekout`

## git reset 切换版本号
+ `git reset [4b9f42a]`
  + `git reset [4b9f42a]`:       Mixed模式 重置本地仓库的HEAD指针和暂存区（Staging Area）到指定的提交，但不会更改工作区的文件。这会取消暂存的更改，但保留更改的文件
  + `git reset --hard [4b9f42a]` Hard模式：重置本地仓库的HEAD指针、暂存区和工作区都回滚到指定的提交
  + `git reset --soft [4b9f42a]` Soft模式：重置本地仓库的HEAD指针到指定的提交，但不会更改工作区的文件。<br><br>

+ `git reset --hard Head`用Head方式回退<br>
  > 在Git中用HEAD表示当前版本，也就是最新的提交1094adb。    
  > 上一个版本就是HEAD\^，上上一个版本就是HEAD\^\^，当然往上100个版本写100个\^比较容易数不过来，所以写成HEAD~100

+ 原理——指针：   
    ```
    ┌────┐
    │HEAD│
    └────┘
    │
    └──> ○ append GPL
            │
            ○ add distributed
            │
            ○ wrote a readme file
    --------------------------------------
    # 改为指向 add distributed 

    ┌────┐
    │HEAD│
    └────┘
    │
    │    ○ append GPL
    │    │
    └──> ○ add distributed
            │
            ○ wrote a readme file
    ```


## git branch 分支

### 创建分支 
+ `git branch [分支名]`

### 改名
+ `git branch -M [新名字]`

### 查看所有分支
+ `git branch -v`
  > 显示所有分支名、分支编号、备注  
  > 绿色名为所有信息

### 切换分支
+ `git checkout [分支名]`

### 合并分支
步骤：
1. 切换到接收修改的分支上
2. `git merge [被合并的分支名]`
   > **如果有改变**：         
   > 第一行：`updating [接收修改的分支]..[被合并的分支]`        
   > 第二行：`Fast-forward` 表示这是一个快速合并操作，没有产生新的提交，只是将当前分支直接指向了"e2719ed"的提交。       
   > 第三行：`readme.md | 4 ++--` 表示更新涉及到了"readme.md"文件，并且显示了文件的修改情况。   
   > 第四行：`1 file changed, 2 insertions(+), 2 deletions(-)`表示"readme.md"文件的修改包括了2处插入和2处删除的操作。     
   >      
   > **如果没改变**：   
   > `Already up to date.`

### 解决分支冲突
+ 我也不会，遇到再说

### 删除分支
+ `git branch -D [分支名]`删除已经被合并的分支，如果没被别的分支合并，则操作会失败，并报错
+ `git branch -D [分支名]`强制删除分支，就算它没被合并

## 远程
### 设置信息
+ 更改名字：
+ `git config --global user.name "[Git账号]"`
+ 更改邮箱
+ `git config --global user.email "[Git邮箱]"`

### git remote add 连接远程仓库
+ `git remote add [origin] [xxx@xxxxxx/xxxx]`
> `origin` 是给远程仓库起的名称     
>

### 查看远程仓库
+ `git remote -v`
  >**若存在仓库**，每一个关联的仓库出现两行：   
  > `[本地对远程仓库的代称，一般是origin] [仓库名] (fetch)` 表示可以从远程仓库获取数据  
  > `[本地对远程仓库的代称，一般是origin] [仓库名] (push)` 可以将本地更改推送到远程仓库中。 
  >**若未关联**，则无信息

### git push 从本地推送分支
+ `git push -u origin main` 第一次，写这个
  > -u 或 --set-upstream：将本地分支与远程分支进行关联
+ `git push` 关联后，写这个就好

### git pull 从远程拉(更新)代码
+ `git pull`

### git clone 从远程克隆代码
+ `git clone [xxxx]`该命令会在本地主机生成一个目录，与远程主机的版本库同名。如果要指定不同的目录名，可以将目录名作为git clone命令的第二个参数
  
### 删除远程仓库
+ `git remote rm [origin]`

## 解决分支冲突
+ `git config pull.rebase false`使用合并（merge）方式解决冲突
+ `git config pull.rebase true`使用变基（rebase）方式解决冲突

# git 基础知识
>![](2023-05-15-20-05-08.png)

## 概念
> **1.工作区（工作目录）**：工作区是您在计算机上实际编辑和修改文件的地方。
>
> **2.暂存区**：暂存区也称为索引（Index），它是一个介于工作目录和本地仓库之间的中间区域。在提交更改之前，您需要将要提交的文件或更改添加到暂存区。暂存区相当于一个缓冲区，它允许您选择要包含在下一次提交中的文件，并构建一个待提交的快照。
>
> **3.本地仓库**：本地仓库是Git用来存储您的项目历史记录和版本信息的地方。它包含了完整的版本控制历史，以及所有文件的各个版本。本地仓库通常位于您项目根目录下的一个名为.git的隐藏文件夹中。
>
> **4.分支**：分支是在版本控制过程中，使用多条线同时推进多个任务。git分支就是在版本控制过程中，使用多条线同时推进多个任务。一个项目里，主分支master分为几部分分支feature，处理不同的部分。如，一个游戏项目，可以分出搞图像的、搞运算的、操作的等分支。在公司里，每个团队处理属于自己的分支，不同部门分支互不干扰，也不影响主分支，假如某个分支出现严重错误，只需要删除这个分支重新来过，其他分支没影响。当一个分支开发完成，就把他合并到主干中，全部分支开发完后，最终形成整个项目。然而，主干master也可能出现bug，这个时候就有一个host_fix分支（临时分支，用来修复bug，修复完及时合并为主干）
> ![](2023-05-17-20-00-00.png)