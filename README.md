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





feature-D
