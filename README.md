# Git环境配置

[TOC]



## 一、生成SSH密钥对

[仓库地址](https://github.com/pthuang/git-tutorial)

### 1. 下载并安装git

+   下载git: [Git-Downloads(git-scm.com)](https://git-scm.com/downloads)
+   安装：具体安装过程不再赘述，有需要可以参考[Git详细安装教程(详解 Git 安装过程的每一个步骤)](https://blog.csdn.net/mukes/article/details/115693833)

### 2. 运行git bash

### 3. 配置姓名和邮箱地址

```shell
git config --global user.name "firstname lastname"
git config --global user.email "xxx@163.com"
```

配置完成之后，win系统下会在*C:/Users/Administrator/*路径下生成**".gitconfig"**文件，后续也可通过直接编辑此文件修改姓名和邮箱地址；

### 4. 生成密钥（公钥和私钥）

```shell
ssh-keygen -t rsa -C "xxx@163.com"
```

keygen是秘钥生成(key generate)的意思，-t(type)是指加密类型是rsa，-C是指账户(Count)为"xxx@163.com"，用户在github上面提交仓库时，会显示该账户；

执行指令过程中，根据提示需要输入*"yes"*和设置*“私钥密码”*；==私钥密码不设置的话可以直接回车，会有安全风险，若设置则每次访问远程服务器都需要输入密码对私钥进行校验，比较麻烦，建议用户自行选择==

以下是笔者生成的整个过程：

```shell
$ ssh-keygen -t rsa -C "xxx@163.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/Administrator/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/Administrator/.ssh/id_rsa
Your public key has been saved in /c/Users/Administrator/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx xx_xxx@163.com
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|             .   |
|       .    . E  |
|        S =. . . |
|       o Oo+.    |
|       oB+*o.o  .|
|      ++*O+o..*oo|
|     o++*O= o+oB*|
+----[SHA256]-----+

```

运行完成之后，win系统中会在*C:/Users/Administrator/.ssh/*路径下生成两个文件：==id_rsa（私钥）==和==id_rsa.pub==（公钥）；

想了解更多SSH和私钥、公钥相关内容可以参考这两篇文章[什么是SSH?](https://info.support.huawei.com/info-finder/encyclopedia/zh/SSH.html)和[id_rsa与id_rsa.pub文件详解](https://www.cnblogs.com/linuxAndMcu/p/14487989.html#_label0)；

## 二、github添加公钥

### 1. 复制公钥内容

+   添加公钥时，注意不要直接用编辑器打开==id_rsa.pub==文件，可以在git bash中运行指令进行复制：

+   windows:

    ```shell
    clip < ~/.ssh/id_rsa.pub
    ```

+    macos:

     ```shell
     pbcopy < ~/.ssh/id_rsa.pub
     ```

+    linux:

     ```shell
     xclip -sel clip < ~/.ssh/id_rsa.pub
     ```

### 2. 添加到github

+   步骤

    GitHub --> setting --> SSH and GPG --> New SSH key
    title: 随便取个名字

    key:直接粘贴





## 三、连接测试

### 1. start git bash

+   run

    ```shell
    ssh -T git@github.com
    ```

+   运行过程：

    ```shell
    $ ssh -T git@github.com
    Hi user_name! You've successfully authenticated, but GitHub does not provide ell access.
    ```

​	出现上述打印信息说明访问成功！

​	另外，若生成私钥的时候设置了密码，这里会要求你输入私钥密码进行校验，以后每次访问都需要进行校验；

​	如果失败的话根据具体报错信息进行解决。

### 2. 其他参考文章

[GitHub常见操作：生成ssh公钥，clone，push_github使用秘钥push项目](https://blog.csdn.net/weixin_43923436/article/details/120821770)

[解决git@github.com: Permission denied (publickey). Could not read from remote repository](https://blog.csdn.net/ywl470812087/article/details/104459288)

[Git下载、安装及环境配置(超详细)](https://blog.csdn.net/weixin_43951315/article/details/104921428?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-104921428-blog-83032408.235^v27^pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-104921428-blog-83032408.235^v27^pc_relevant_multi_platform_whitelistv3&utm_relevant_index=1)





## 四、git指令学习

### 1. 基本操作

+   新建路径(文件夹)

    ```shell
    mkdir repo_name
    ```

+   切换路径

    ```shell
    cd ./repo_name
    ```

+   初始化本地仓库

    ```shell
    git init 
    ```

+   查看仓库状态

    ```shell
    git status 
    ```

+   创建文件 查看文件/路径的时间属性，不存在则创建空白文件

    ```shell
    touch readme.md
    ```

+   向暂存区添加文件 

    ```shell
    git add readme.md
    ```

+   提交，即记录工作树中所有文件的当前状态

    ```shell
    git commit -m "add new file readme.md"
    ```

+   查看日志

    ```shell
    git log 
    ```

+   只显示第一行日志

    ```shell
    git log --pretty=short
    ```

+   只显示指定目录/文件的日志

    ```shell
    git log readme.md 
    ```

+   只显示指定文件提交带来的改动

    ```shell
    git log -p readme.md
    ```

+   查看工作树和暂存区的差别

    ```shell
    git diff
    ```

+   查看工作树和最新提交的差别，HEAD指的是当前分支最新一次提交的指针

    ```shell
    git diff HEAD 
    ```

    +   一个好习惯：

        **在执行git commit之前，先执行git diff HEAD命令，查看本次提交与上次提交之间有什么差别，确认完毕之后再进行提交。**



### 2. 分支操作

+   显示分支预览

    ```shell
    git branch
    ```

+   新建分支

    ```shell
    git branch branch_name
    ```

+   切换分支

    ```shell
    git checkout branch_name
    ```

+   新建并切换分支

    ```shell
    git checkout -b branch_name 
    ```

+   合并分支branch_name到当前分支

    ```shell
    git merge --no-ff branch_name
    ```

+   以图表形式查看日志

    ```shell
    git log --graph
    ```



### 3. 更改提交

+   查看当前仓库相关操作日志（获取哈希值）

    ```shell
    git reflog s
    ```

+   回溯到某一版本

    ```shell
    git reset --hard hash_valuesh
    ```

+   消除修改冲突

    手动修改，然后提交修改；

+   修改“提交信息” : 须学会vim操作

    ```shell
    git commit --amend 
    ```

+   压缩历史(将两次修改合并)

    ```shell
    # 1.先提交修改
    git commit -am "modify log0"
    # 2.再次修改后提交
    git commit -am "modify log1"
    # 3.更改历史, 选择包含HEAD(最新提交)在内的两个最新历史记录为对象
    git rebase -i HEAD~2
    ```

    +   在编辑器中将最新的历史记录改为fixup

        ```markdown
        pick 7a34294 modify log0
        pick 6fba227 modify log1
        ```

        改为：

        ```markdown
        pick 7a34294 modify log0
        fixup 6fba227 modify log1
        ```

    +   保存并关闭编辑器（ESC + ZZ）

    +   查看最新的哈希值

        ```shell
        git log --graph
        ```

        

### 4. 推送

+   新建github仓库
    +   仓库名与本地仓库名保持一致；
    +   不要勾选Initialize the repostory with a README选项；

+   添加远程仓库

    ```shell
    git remote add origin git@github.com:user_name/repostory_name.git
    ```

+   推送至master分支

    ```shell
    git push -u origin master 
    ```

+   推送其他分支

    ```shell
    # 切换分支
    git checkout branch-A
    # 推送至github 同名分支
    git push -u origin branch-A

​	

### 5. 获取

1.   以第二开发者角度理解

+   获取远程仓库(本地不存在仓库)

    ```shell
    git clone git@github.com:user_name/repostory_name.git

+   获取远程分支

    ```shell
    # 在本地仓库中新建branch_name分支，来源是github中的branch_name分支
    git checkout -b branch_name origin/branch_name
    ```

+   修改并提交分支

    ```shell
    # 修改后提交
    git commit -am "modify log"
    ```

+   推送分支

    ```shell
    git push 
    ```

2.   以第一开发者角度理解

+   获取最新的远程仓库分支

    ```shell
    git pull 
    ```

### 6.Ubuntu建立远程仓库

1.   切换到仓库路径

     ```
     cd ./home/server
     ```

2.   建立并初始化仓库

     ```shell
     git init --bare repo_name
     ```

     

3.   客户端克隆远程仓库

     ```shell
     # user_name@ip:directory/repo_name
     git clone git@152.168.7.303:/home/server/repo_name.git
     ```

     

### 6. 删除分支

+   删除本地分支

    ```shell
    # 该分支必须完全和它的上游分支merge完成,如果没有上游分支,必须要和HEAD完全merge
    git branch --delete branch_name
    git branch -d branch_name
    # 下面两个等效,在不检查merge状态的情况下删除分支
    git branch --delete --force branch_name
    git branch -D branch_name
    ```

+   删除远程分支

    ```shell
    # 同时也会删除追踪分支
    git push origin --delete branch_name
    ```

+   单独删除跟踪分支

    跟踪分支：与远程分支有直接关系的本地分支；

    ```shell
    git fetch origin --prune branch_name
    git fetch origin -p branch_name
    ```

+   查看本地分支与远程分支的跟踪关系

    ```shell
    git branch -vv
    ```



## 五、电子书

上述不少内容来自/doc/路径中的电子书；





未完待续......
