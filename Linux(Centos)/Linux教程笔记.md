[toc]

# 环境准备

## 共享文件夹 - vmtools

1. 可以通过vmtools这个工具实现：

   - 可以直接粘贴命令在Windows和Linux之间
   - 可以设置Windows和Linux的共享文件夹

2. **安装**

   - 点击 VMwareStation 上的虚拟机 -> install vmware tools

   - centos 会有一个安装包，将其中的压缩文件解压就会得到一个安装文件

     `解压命令：tar -zxvf xxx.tar.gz`

     **注意：如果要将压缩包复制到别的目录下，要注意权限问题，一般用root账户登录就能避免**

   - 进入解压的目录，安装 `./vmware-install.pl`

   - 全部使用默认设置即可

   - 需要重启系统

3. **设置共享文件夹**

   - 在实际的开发中，文件的上传和下载是用远程方式操作的
   - Windows端：虚拟机 -> 设置 -> 选项 -> 共享文件夹 -> 总是启用 -> 添加Windows的文件夹路径
   - Linux端：根目录下的mnt -> hgfs -> 这里就是共享的文件夹

# Linux目录结构

## 基本介绍

- Linux中，`/`即代表根目录，不同于Windows的C、D、E盘结构，Linux只有一个根目录，然后在此目录下创建其他目录，是**树结构**
- Linux的文件系统采用级层式的树状目录结构，最上层目录就是根目录，有且只有一个
- ==Linux世界里，一切皆为文件==，即使是硬件，也会被映射成相应的文件
- ==**Linux开机流程**：开机 => BIOS => /boot => init进程 => 运行级别 => 运行级别对应的服务==

## 根目录

```shell
/bin   这个目录存放着最经常使用的命令，主要有cat、chmod、chown、date、mv、mkdir、cp、bash等

/sbin   存放着系统管理员使用的系统管理程序，包括开机过程所需要的开机、修复、还原系统所需要的命令

/home  存放普通用户的主目录，每个用户都有一个自己的目录，一般目录名以用户账号命名，主文件夹有两种代号：～代表当前这个用户的主文件夹

/root   超级权限者的用户主目录，系统管理员的主文件夹

/lib  放置的是系统开机所需要最基本的动态链接共享库，类似于Windows的DLL文件，包括开机时会用到的数据库，以及在/bin和/sbin下命令会调用的函数库

/lost+found  一般情况下是空的，系统非法关机后，系统就会存放一些文件

/etc   所有系统管理员所需要的配置文件和子目录，例如人员的帐号密码文件，各种服务的起始文件等。一般来说，这个目录下面的各文件属性时可以让一般的用户查阅的，但是只有root用户有权先修改。FHS建议不要放置可执行的文件在这个目录下

/usr  这里面放置的数据属于可分享的与不可变动的（shareable，static），其实usr是UNIX SOFTWARE RESOURCE的缩写，而非user的缩写，也就是unix操作系统软件放置的位置而非用户的数据

/boot  这个目录主要放置开机能够使用到的文件，包括linux内核文件和开机菜单与开机所以需要的配置文件
====================================================================================================
一下三个目录跟Linux内核有关，一般不要动
/proc  这个目录本身是一个虚拟文件系统，它放置的数据都是在内存当中，不占用硬盘的容量

/src  src可以视作service的缩写，是一些网络服务启动后，这些服务需要取用的数据目录，常见的服务例如www,ftp等

/sys  这个目录其实跟/proc非常的相似，也是一个虚拟的文件系统主要也是记录与内核相关的信息，不占用硬盘容量
====================================================================================================
/tmp  这是让一般的用户或者是正在执行的程序暂时放置文件的地方

/dev   在linux中任何的设备和接口设备都是以文件的形式存在于这个目录当中。你只要到通过访问这个目录下的某个文件就相当于访问某个设备，类似于Windows的设备管理器

/media  放置的就是可以删除的设备。包括软盘，光盘，dvd等都临时挂放在此。

/mnt  系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将外部的存储挂载在该目录下，然后进入该目录就能看见了，例如vmtools的共享文件夹

/opt  这个是给第三方软件放置的目录。不过，在以前的linux下我们喜欢放置在/usr/local下面，一般是通过编译源码方式安装的程序。

/var  这个目录下面主要放置常态性变动的文件，包括cache,logfile以及某些软夹运营所产生的文件。例如MYSQL数据库文件等

/selinux SeLinux是一种安全子系统他能控制程序只能访问特定文件
```

## 小结

- Linux有且只有一个根目录
- Linux的各个目录存放的内容是预先规划好的，不要乱放文件
- Linux是以文件的形式来管理设备，因此Linux中一切皆为文件
- Linux的各个文件目录下存放什么内容必须有一个认识，最好能指哪个说哪个
- 学习后脑子里应该有一颗目录树

# 远程登录到Linux服务器

## 为什么要远程登陆呢？

1. 如果是实际的开发，Linux服务器一般是在第三方服务商的机房里，那么要控制Linux服务器，就要同构远程登陆的方式来操作
2. 还有文件的上传和下载，也要通过远程登录的方式
3. 可以用termius / XShell 远程登陆 / Xftp 远程文件上传下载
4. 安装之前要先开启Linux的远程监听服务，然后开启服务来供远程终端连接，一般云服务器会用一个密钥来连接，**该服务监听22号端口**
5. `setup -> 系统服务 -> sshd` 查看是否开启远程监听服务（SSHD），`*` 代表已经开启；`service sshd status` 也可以检查

## 连接Linux

1. 通过XShell连接到Linux服务器

   ```shell	
   ifconfig    查看IP地址
   ```

   **默认nat模式下，linux的IP与虚拟的网卡IP不一样，要设置端口转发，才能确保正常连接！**

2. **Linux虚拟机的三种网络连接形式**

   - 桥接模式：与主机在同一网段，Linux可以和其他系统通信，但是如果Linux虚拟机数量多可能造成ip冲突
   - NAT模式：网络地址转换方式，即母机代理通讯，再创建子网供虚拟机使用，其中一个和Linux无法和本局域网中的其他真实主机进行通讯
   - 仅主机模式：即单机模式，是一个独立的主机，不能访问外网

   ==一般选择NAT模式==

## 远程下载和上传文件

可以使用Xftp软件进行文件的传输，直接安装即可，然后输入Linux主机的IP地址，选择SFTP协议（22号端口），再输入账号密码即可

如果出现中文乱码问题，可以在主机的属性中的选项中选择使用**UTF-8编码**即可

直接拖拉文件即可

# Vi和Vim编辑器

## 基本介绍

1. 所有Linux系统都会内建vi文本编辑器
2. Vim具有程序编辑的能力，可以当作是vi的增强版，可以主动的以字体颜色辨别语法的正确性，方便程序设计。代码补全、编译及错误跳转等方便编程的功能特别丰富，被广泛使用。

## vi和vim的三种常见模式

1. 正常模式

   **一般默认就是正常模式**，在该模式下，我们**可以使用快捷键**。

   以 vim 打开一个档案就直接进入一般模式了(这是默认的模式)。在这个模式中，你可以使用『上下左右』按键来移动光标，你可以使用『删除字符』或『删除整行』来处理档案内容，也可以使用『复制、粘贴』来处理你的文件数据。

2. 插入模式（编辑模式）

   在模式下，程序员可以**输入内容**。

   按下` i, I, o, O, a, A, r, R` 等任何一个字母之后才会进入编辑模式, **一般来说按` i `即可**

3. 命令行模式

   在这个模式当中， 可以提供你相关指令，完成读取、存盘、替换、离开 vim 、显示行号等的动作则是在此模式中操作的

## 快速入门案例

- 写一个hello world的 java 代码文件

```java
ll  查看目录下的文件
vim Hello.java  用vim打开一个java文件
输入 i 进入编辑模式
输入代码:
public class Hello{
    public static void main(String args[]){
        System.out.println("Hello World");
    }
}
输入完成后按ESC按键，从编辑模式切换到正常模式
输入 :或者/ 后即可从正常模式切换到命令行模式
输入 wq (w是写入的意思 q是退出的意思) 保存 
    q 是退出，如果有修改，就会提示加上 ! 强制执行，这样修改的内容就会消失
```

## 快捷键使用案例

> 要先从进入正常模式才可以使用快捷键

1. **拷贝当前行** `yy` , 拷贝当前行向下的 5 行 `5yy`，并粘贴  `p` 
2. **删除当前行** `dd` , 删除当前行向下的 5 行 `5dd`
3. 在文件中查**找某个单词**：命令行下 `/` 关键字 ， 回车 查找 , 输入 `n` 就是查找下一个
4. 设**置文件的行号**，**取消文件的行号**：命令行下`:set nu` 和 `:set nonu`
5.  编辑 /etc/profile 文件，使用快捷键到底文档的**最末行**`G`和**最首行**`gg`，注意这些都是在==正常模式==下执行的
6.  在一个文件中输入 "hello" ,然后又**撤销这个动作**，在正常模式下输入 `u`
7. **取消着色标记**操作是  `:noh`
8.  编辑 /etc/profile 文件，并将**光标移动到 第 20 行** `shift+g`
   - 第一步：显示行号 :set nu 
     - 输入20，直接按回车的话，是从当前位置前进20行
     - 数字+Enter 可以到 光标当前位置+数字 的那一行
   - 第二步：输入 20 这个数
   - 第三步: 输入 shift+g
9. 单行注释 `# 后面写注释`
10. 多行注释：`:<<!   中间的代码   !`

## vim键盘图

![](https://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch1.gif)

![](https://www.linuxidc.com/upload/2016_08/160826064815403.png)

# 开机、重启和用户登录注销

## 关机和重启

```shell
shutdown
	shutdown -h now 立即关机
	shutdown -h 1 表示一分钟过后就关机
	shutdown -r now 立即重启
halt 停机指令 直接使用即可 效果等同于关机
reboot 就是重启系统
sync 代表把内存的数据同步到磁盘上
```

- **不管是重启还是关机，都应该先执行以下 sync 指令，把内存的数据写入磁盘，防止数据丢失**

## 用户登录和注销

- 登录时**尽量少用 root 帐号登录**，因为它是系统管理员，拥有最大的权限，**避免操作失误**。可以利用普通用户登录，登录后再用`su - 用户名` 命令来切换成系统管理员身份
- 在提示符下输入` logout `即可注销用户

> logout 注销指令在图形运行级别无效即在虚拟机上操作时无效，在 运行级别 3 下有效，例如远程连接时使用

# 用户管理

## 基本介绍

- Linux 系统是一个多用户多任务的操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统
- 用户组：Linux下有很多地用户组，这是Linux对用户管理地一种管理，每一个用户至少属于一个组，例如 root 用户属于 root 组
- 家目录：`/home/` 目录下有各个创建的用户对应的家目录，当用户登录时会自动地进入到自己地家目录

## 添加用户

- 基本语法：`useradd [选项] 用户名`

- 例如：添加用户小明 ==> 添加完成后发生的变化：

  - 有一个组被创建了(系统会默认创建一个**同名用户组**，当然也可以指定加入一个组)； 
  - `/home/` 目录下有一个 `xiaoming` 的目录

  ```shell
  useradd xiaoming
  useradd -d /home/tiger xiaohong    给新创建的用户xiaohong指定家目录所在位置
  useradd -g groupname username   将新创建的用户添加到指定用户组
  ```

## 给用户指定/修改密码

使用命令 `passwd 用户名` 

```shell
passwd [-k] [-l] [-u [-f]] [-d] [-S] [username]
-d 删除密码
-f 强制执行
-k 更新只能发送在过期之后
-l 停止账号使用
-S 显示密码信息
-u 启用已被停止的账户
-x 设置密码的有效期
-g 修改群组密码
-i 过期后停止用户账号
```

## 删除用户

使用命令`userdel username`

```shell
userdel xiaoming   删除用户 xiaoming 但是要保留家目录
userdel -r xiaoming    删除用户 xiaoming 以及用户主目录
```

- 实际开发工作中，删除用户时一般不会将家目录删除，以免一些文件被误删

## 查询用户

使用命令 `id username`

系统会显示：**用户id号；所在组id号；组名**

如果不存在该用户，会显示 **无此用户**

## 切换用户

- 在操作 Linux 中，如果当前用户的权限不够，可以通过 su - 指令，切换到高权限用户，比如 root
- 使用命令：`切换：su - username  返回原来的用户：exit`
- **高权限用户切换到低权限用户时不需要输入密码，反之需要**

## 用户组

- 用户组：类似于角色，系统可以对有共性的多个用户进行统一的管理
- 增加组： `groupadd groupname`

```shell
useradd -g groupname username   将新创建的用户添加到指定用户组
usermod -g groupname username   修改某个用户的用户组
usermod -d 目录名 用户名         改变该用户登录的初始目录
```

## 用户和组的相关文件

### /etc/passwd 文件

- 用户（user）的配置文件，**记录用户的各种信息**
- 每行的含义：`用户名:密码:用户id:组id:注释性描述::家目录:登录 Shell`

### /etc/group 文件

- 组(group)的配置文件，**记录 Linux 包含的组的信息**
- 每行含义：`组名:口令:组标识号:组内用户列表`

### /etc/shadow 文件

- 口令的配置文件（密码和登录信息，是加密的）

- 每行的含义：

  `登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志`

# 实用指令

## 指定运行级别

- **七大运行级别**

  ```shell
  0 ：关机
  1 ：单用户【找回丢失密码】
  2：多用户状态没有网络服务
  3：多用户状态有网络服务
  4：系统未使用保留给用户 一般不使用
  5：图形界面
  6：系统重启
  常用运行级别是 3 和 5 ，要修改默认的运行级别可改文件
  系统的运行级别配置文件 /etc/inittab
  /etc/inittab 中的 id:5:initdefault: 这一行中的数字就代表着当前运行级别
  切换运行级别 init [0|1|2|3|5|6]
  也可以编辑文件中的那一行，然后reboot即可
  ```

- `systemctl get-default` 查看当前运行级别

- centos7中，这个文件在`/lib/systemd/system`

- 找回root用户的密码：可以进入单用户模式之后再使用passwd命令修改

## 帮助指令

当我们对某个指令不熟悉的时候，我们可以使用Linux提供的帮助指令来了解这个指令的使用方法

1. 通过man指令获得帮助信息：`man [命令或配置文件]`
2. 通过help指令获得 shell 内置命令的帮助信息：`help [命令]`
3. 当然，更推荐直接百度

> 按J或K滚动翻看

## 文件目录类指令

> 斜杠在前表示绝对路径，没有斜杠表示相对路径，斜杠在后表示某文件夹下的一个文件

1. **pwd 命令**( print woking dictionary )，显示当前工作目录的绝对路径

   ```shell
   使用方法：pwd
   ```

2. **ls 命令** ，显示当前目录的所有文件和目录，包括隐藏的

   ```shell
   使用方法：ls [选项] [目录或是文件]
   -a 显示当前目录所有的文件和目录，包括隐藏的
   -l 以列表的方式显示信息
   -h 显示文件大小
   ```

3. **cd 命令**（change directory），切换到指定的目录

   ```shell
   cd [绝对路径|相对路径]
   cd~ 或者 cd: 回到自己家目录
   cd .. 回到当前目录的上一级目录
   . 代表当前目录
   .. 代表上一级目录
   ```
   
4. **mkdir 命令**（make directory），用于创建目录

   ```shell
   mkdir [选项] 要创建的目录
   -p 创建多级目录，多级目录即创建一个目录后然后在这个目录下再创建一个目录，相当于创建两个目录
   ```

5. **rmdir 命令**（remove directory），用于删除==空目录==

   ```shell
   rmdir [选项] 要删除的空目录
   rm -rf 要删除的非空目录
   注意！rm -rf /* 是删除根目录下的所有内容，不要乱听别人说
   ```

6. **touch 命令**，用于创建空文件

   ```shell
   touch 文件名称
   也可以一次创建多个文件，空格分开即可
   ```

7. **cp 命令**（copy），拷贝文件到指定目录

   ```shell
   cp [选项] 要拷贝的文件 要粘贴的目录
   -r  递归复制整个文件夹
   例1：cp a.txt /home/b/ 将a.txt文件拷贝到/home/b目录下
   例2：cp -r /home/a/ /home/b/ 将/home/a/目录下的所有文件递归拷贝到/home/b/下，当有重复文件的时候会提示是否覆盖
   例3：cp -r /home/a/ /home/b/ 这样就能强制覆盖系统不会提示，这样就不用一个一个文件的操作
   ```

8. **rm 命令**，删除文件或目录

   ```shell
   rm [选项] 要删除的文件或目录
   -r  递归删除整个文件夹
   -f  强制删除不提示
   ```

9. **mv 命令**，移动文件与目录，或重命名

   ```shell
   mv 旧文件名 新文件名     重命名
   mv 源文件路径 目标文件路径   移动文件
   例1：mv a.txt b.txt
   例2：mv a.txt /home/    如果移动到的文件夹内存在同名的文件会提示是否覆盖,也可以重命名
   ```

10. **cat 命令**，查看文件内容，以只读的方式打开

    ```shell
    cat [选项] 要查看的文件
    -n ：显示行号
    例1：cat -n /etc/profile 这样直接打开文件会一下走到最后一行然后退出到命令行
    	因此一般会加上 | more 来分页显示
    cat 只能浏览文件，而不能修改文件，为了浏览方便，一般会带上 管道命令 | more
    cat 文件名 | more [分页浏览]
    回车翻页
    ```

11. **more 命令**

    more 指令是一个基于 VI 编辑器的文本过滤器，它以==全屏幕的方式按页显示文本文件的内容==

    more 指令中内置了若干快捷键，详见操作文档

    ```shell
    more 要查看的文件
    
    常用快捷键：
    一行一行的看就按 Enter 键
    一页一页的看就按 空格 键
    Ctrl+B 回到上一页
    Ctrl+F 下一页
    q 立即离开more，不再显示文本内容
    = 输出当前行的行号
    :f 输出文件名和当前行的行号
    ```

12. **less 命令**

    less 命令用来==分屏查看文件内容==，它的功能与 more 命令类似，但是**更强大**，支持各种显示终端

    less 指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是**根据显示需要加载内容**，==对于显示大型文件具有较高的效率==

    ```shell
    less 要查看的文件
    
    常用快捷键
    空格键    向下翻一页
    pagedown  向下翻一页
    pageup    向上翻一页
    /字符串   向下搜索字符串，n：向下查找 N：向上查找
    ?字符串   向上搜索字符串，n：向上查找 N：向下查找
    q  离开less这个程序
    ```

13. `> 命令`和`>> 命令`

    `> 命令` **输出重定向** : 会将原来的文件的内容覆盖

    `>> 命令` **追加**： 不会覆盖原来文件的内容，而是追加到文件的尾部

    ```shell
    ls -l >文件   将ls -l 显示的内容写入文件 a.txt 中（覆盖写）如果该文件不存在，就创建该文件
    ls -al >>文件 将ls -al 显示的内容追加到文件 a.txt 的末尾
    cat 文件 1 > 文件 2   将文件1的内容覆盖到文件2
    echo "str">>文件  将字符串内容追加到文件中
    echo "str">文件   将字符串的内容覆盖到文件中，原来的内容全都没了
    ```

14. **echo 命令**，输出内容到控制台

    ```shell
    echo [选项] [输出内容]
    例1  使用 echo 指令输出环境变量,输出当前的环境路径 ==> echo $PATH
    例2  使用 echo 指令输出"hello world" ==> echo "hello world"
    ```

15. **head 命令**，用于显示文件的开头部分内容，默认情况下 head 指令显示文件的前 10 行内容

    ```shell
    head 文件 
    head -n 5 文件    查看文件头 5 行内容，5 可以是任意行数
    ```

16. **tail 命令**，用于输出文件中尾部的内容，默认情况下 tail 指令显示文件的后 10 行内容

    ```shell
    tail 文件
    tail -n 5 文件    查看文件后 5 行内容，5 可以是任意行数
    tail -f 文件    实时追踪该文档的所有更新，实际开发工作中会经常使用，Ctrl+C退出追踪
    如果你是用的vim修改，因为vim实际上是删除本文件，生成了新的同名文件，所以无法进行监控
    ```

17. **ln 命令**，给原文件创建一个链接  

    软链接也叫符号链接，类似于 windows 里的快捷方式，主要存放了链接其他文件的路径

    硬连接指通过索引节点来进行链接

    [ 关于硬连接和软连接的详细介绍 ](https://www.cnblogs.com/songgj/p/9115954.html)

    ```shell
    ln [参数] [原文件或目录] [目标文件或目录]  
    -i 交互模式，文件存在则提示用户是否覆盖。
    -s 软链接(符号链接)。
    -d 允许超级用户制作目录的硬链接。
    -b 删除，覆盖以前建立的链接
    
    在默认不带参数情况下，ln命令创建的是硬链接
    
    例： ln -s /root linkToRoot   在当前目录下创建一个软链接，链接指向root目录
    当 cd linkToRoot 时，就会跳转到root目录，但是用pwd查看路径时，还是会显示原来目录的linkToRoot的路径
    ```

18. **history 命令**，查看已经执行过历史命令,也可以执行历史指令

    ```shell
    history [数字]
    不加数字则显示所有的历史命令
    加数字则显示最近使用的n条命令
    !10  执行历史编号为10的命令
    history -c 清除历史记录
    ```

## 时间日期类指令

1. **cal 命令**，显示当前日历信息

   ```shell
   cal [选项]
   不加选项，显示本月日历
   cal 2020  显示2020年一整年的日历
   ```

2. **date 命令**，显示当前日期 / 设置当前日期

   ```shell
   date 显示当前时间
   date +%Y   显示当前年份
   date +%m   显示当前月份
   date +%d   显示当前是哪一天
   date "+%Y-%m-%d %H:%M:%S"   显示年月日时分秒
   
   date -s 字符串时间  设置系统当前时间
   例：date -s "2020-11-11 11:11:11"
   设置回原来的时间
   ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
   ```

## 搜索查找类指令

1. **find 命令**，将从指定目录向下递归地遍历其各个子目录，将满足条件的文件或者目录显示在终端

   ```shell
   find [搜索范围] [选项]
   -name<查询方式> 按照指定的文件名查找模式查找文件  例：find /home -name hello.txt 
   -user<用户名>  查找属于指定用户名所有文件  例： find /root -user root
   -size<文件大小>  按照指定的文件大小查找文件 [+n大于 -n小于 n等于]  例：find /root -size +20M
   使用文件名查找时可以使用通配符，例：find /home -name *.txt
   ```

2. **locate 命令**，快速定位文件路径

   locate 指令利用==事先建立的系统中所有文件名称及路径的 locate 数据库==实现快速定位给定的文件

   Locate 指令无需遍历整个文件系统，查询速度较快

   为了保证查询结果的准确度，管理员**必须定期更新** locate 时刻

   由于 locate 指令基于数据库进行查询，所以==第一次运行前，必须使用 updatedb 指令创建 locate 数据库==。

   ```shell
   locate 搜索文件
   例：locate hello.txt
   ```

3. **grep 指令和 管道符号 |**

   grep 过滤查找 ， 管道符`|`，表示**将前一个命令的处理结果输出传递给后面的命令处理**

   ```shell
   grep [选项] 查找内容 源文件
   -n 显示匹配行及行号
   -i 忽略字母大小写
   
   例：cat hello.txt | grep -n yes  在 hello.txt 文件中，查找 "yes" 所在行，并且显示行号
   ```

## 压缩和解压缩类指令

1. **gzip / gunzip 指令**

   gzip 用于==压缩文件==， gunzip 用于==解压缩==

   压缩完成后，原来的文件就没了，取而代之的是对应的压缩文件，不会保留原来的文件

   ```shell
   gzip 文件        压缩文件，只能将文件压缩为 *.gz 文件
   gunzip 文件.gz   解压缩文件命令
   ```

2. **zip / unzip 指令**

   zip 用于==压缩文件==， unzip 用于==解压缩==，这个在项目打包发布中很有用的

   ```shell
   zip [选项] XXX.zip 将要压缩的内容    压缩文件和目录的命令
   unzip [选项] XXX.zip         解压缩文件
   zip ==>  -r：递归压缩，即压缩目录
   unzip ==>  -d<目录> ：指定解压后文件的存放目录
   例： zip -r home.zip /home/   ==>   将 /home 下的 所有文件进行压缩成 home.zip
   例： unzip -d /home/ home.zip   ==>   将 mypackge.zip 解压到 /home 目录下
   ```

3. **tar 指令**，打包指令

   最后打包后的文件是` .tar.gz `的文件

   ```shell
   tar [选项] XXX.tar.gz 打包的内容     打包目录，压缩后的文件格式.tar.gz
   -c 产生 .tar 打包文件
   -v 显示详细信息
   -f 指定压缩后的文件名
   -z 打包同时压缩
   -x 解包 .tar 文件
   
   -c create -t list -x extract -z gzip -j bzip2 -J xz -f filename
   
   例1 -> tar -zcvf a.tar.gz a1.txt a2.txt   ==>  将 a1.txt 和 a2.txt 压缩成 a.tar.gz
   例2 -> tar -zcvf myhome.tar.gz /home/   ==>  将 /home/ 目录下所有文件打包压缩成 myhome.tar.gz
   例3 -> tar -zxvf a.tar.gz   ==>  将 a.tar.gz 解压到当前目录
   例4 -> tar -zxvf myhome.tar.gz -C /home/   ==>  将 myhome.tar.gz 解压到 /home/ 目录下
   
   -C 应该是change，改变目录
   ```

   - 指定解压缩的目标目录一定要事先存在

# 组管理

## 基本介绍

- 在 linux 中的每个用户必须属于一个组，不能独立于组外
- 在 linux 中每个文件有所有者、所在组、其它组的概念
  1. 所有者：一般为文件的创建者，谁创建了该文件，就自然的成为该文件的所有者
  2. 所在组：文件也会归属于一个组，一般默认是所有者所在的组
  3. 其他组：除文件的所有者和所在组的用户外，系统的其它用户都是文件的其它组.

## 文件 / 目录 所有者

**一般为文件的创建者**，谁创建了该文件，就自然的成为该文件的所有者

1. 查看文件所有者

   ```shell
   ls -ahl 即可查看文件的所有者和所在组
   ```

2. 修改文件所有者 ==> change owner

   ```shell
   chown [参数] 用户名 文件名
   chown newowner:newgroup file 改变用户的所有者和所有组
   -R 如果是目录 则使其下所有子文件或目录递归生效 递归的修改文件、目录的所有者
   ```

## 文件 / 目录 所在组

当某个用户创建了一个文件后，**默认这个文件的所在组就是该用户所在的组**

1. 查看文件所在组

   ```shell
   ls -ahl
   ```

2. 修改文件所在组  ==> change group

   ```bash
   chgrp [参数] 组名 文件名
   -R 如果是目录 则使其下所有子文件或目录递归生效 递归的修改文件、目录的所在组
   ```

# 权限管理

## 基本介绍

- ls -l 中显示的内容如下：

  ​	`-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc`

- 0-9 位说明

  1. 第 0 位确定文件类型(d 目录，- 普通文件， l 连接，c 字符设备，b 块文件例如硬盘)
  2. 第 1-3 位确定**所有者**（该文件的所有者）拥有该文件的权限。---User
  3. 第 4-6 位确定**所属组**（同用户组的）拥有该文件的权限，---Group
  4. 第 7-9 位确定**其他组的用户**拥有该文件的权限 ---Other
  5. 这里的权限也**可用数字**表示为: r=4，w=2，x=1 因此 rwx=4+2+1=7

- `1` 的意思是：如果是文件，表示**硬连接的数**；如果是目录，则表示**该目录下有多少个子目录**

- 所有者名称

- 所在组名称

- 文件大小，1213个字节，如果是目录会统一显示4096

- 文件最后的修改时间

- 文件名

## rwx 权限详解

1. **rwx 作用到文件**
   1.  [ r ]代表可读(read)：可以读取，查看
   2.  [ w ]代表可写(write)：可以修改，==但是不代表可以删除该文件==，删除一个文件的前提条件是==对该文件所在的目录有写权限，才能删除该文件==
   3.  [ x ]代表可执行(execute)：可以被执行
2. **rwx 作用到目录**
   1. [ r ] 代表可读(read)：可以读取，ls 查看目录内容
   2. [ w ] 代表可写(write)：可以修改，目录内创建+删除+重命名目录
   3. [ x ] 代表可执行(execute)：可以进入该目录

## 修改权限 -- chmod

- 通过 chmod 指令，可以修改文件或者目录的权限

**第一种方式：通过+ 、-、= 变更权限**

- u：所有者 g：所在组 o：其他人 a：所有人(u、g、o 的总和)
- chmod u=rwx,g=rx,o=x 文件目录名   ==>   给所有者读写操作的权限，给所在组读写权限，给其他人执行的权限
- chmod o+w 文件目录名   ==>   给其他人增加写权限
- chmod a-x 文件目录名   ==>   给所有人减少写权限

**第二种方式：通过数字变更权限，其实就是二进制来表示，三个位分别用0和1表示权限的无和有**

- 规则：r=4 w=2 x=1 ，rwx=4+2+1=7 ，rx=4+1=5
- chmod u=rwx,g=rx,o=x 文件目录名         相当于      chmod 751 文件目录名

注意：对于目录，要拥有执行的权限才能进入目录

# 定时任务调度

## 基本介绍

- crond 定时任务调度
- 在我们写了一个脚本或代码，能够完成某个任务，但是需要定时完成，就能够使用一种机制，去定时的调度我们写好的脚本或代码
- 可以通过crontab进行定时任务设置

## 基本语法

- 任务调度：是指系统在某个时间执行的特定的命令或程序

- 任务调度分类：

  1. 系统工作：有些重要的工作必须周而复始地执行，如病毒扫描等
  2. 个别用户工作：个别用户可能希望执行某些程序，比如对mysql数据库的备份

  ```bash
  crontab [选项]
  -e 编辑crontab定时任务
  -l 查询crontab任务
  -r 删除当前用户所有的crontab任务
  ```

- 对于一些简单的任务，可以不用写脚本，直接在crontab中加入任务即可

- 对于复杂的任务，就需要写脚本来完成（shell脚本）

## 快速入门

任务要求：

- 设置任务调度文件：/etc/crontab
- 设置个人任务调度
- 执行 crontab –e 命令
- 接着输入任务到调度文件   如：`*/1 * * * * ls –l /etc/ > /tmp/to.txt `  
- 语句的意思说每小时的每分钟执行` ls –l /etc/ > /tmp/to.txt `命令

具体步骤：

- crontab -e 进入编辑模式
- 输入代码：`*/1 * * * * ls –l /etc/ > /tmp/to.txt`
- 按esc，再按i/a/o，就进入输入模式。按esc再按：进入末行，按esc，按R进入替换模式
- 当保存退出后就程序
- 在每一分钟都会自动的调用 ls -l /etc >> /tmp/to.txt

参数说明：

1. 五个占位符
   1. 第一个 `*`  => 一小时的第几分钟  0-59
   2. 第二个 `*`  => 一天的第几小时 0-23
   3. 第三个`*`  => 一个月当中的第几天 1-31
   4. 第四个 `*`  => 一年当中的第几月  1-12
   5. 第五个 `*`  => 一周当中的星期几  0-7（0和7都代表星期日）
2. 特殊符号的说明
   1. `*` 号代表任何时间
   2. `,` 号代表不连续的时间
   3. `-`号代表连续的时间范围
   4. `*/n`号代表没隔多久就执行一次
3. 表达式例子：

```bash
45 22 * * * 命令   ==>  在22点45分执行命令
0 17 * * 1 命令   ==>  在每周一的17点0分执行命令
0 5 1,15 * * 命令   ==>  在每月的1号和15号的凌晨5点0分执行命令
40 4 * * 1-5 命令   ==>  每周一到周五的凌晨4点40分执行命令
*/10 4 * * * 命令   ==>  每天的凌晨4点，每个10分钟执行一次命令
0 0 1,15 * 1 命令   ==>  每月的1号和15号，每周一的0点0分都会执行命令
注意:星期几和几号最好不要同时出现，因为他们定义的都是天，很容易产生混乱
```

## 任务调度的几个应用实例

### 第一个案例：每隔1 分钟，就将当前的日期信息，追加到 /tmp/mydate 文件

1. 先编写一个文件 mytask1.sh

   ```shell
   date >> /tmp/mydate
   ```

2. 给 mytask1.sh 一个可以执行权限

   ```bash
   chmod 744 mytask1.sh
   ```

3. 执行命令 `crontab -e`

4. 执行 `*/1 * * * * mytask1.sh` 代码

### 第二个案例：每隔1 分钟， 将当前日期和日历都追加到 /home/mycal 文件中

1. 先编写一个文件 /home/mytask2.sh

   ```bash
   date >> /tmp/mycal 
   cal >> /tmp/mycal
   ```

2. 给 mytask1.sh 一个可以执行权限

   ```bash
   chmod 744 /home/mytask2.sh
   ```

3. `crontab -e` 进入定时任务调度

4.  `*/1 * * * * /home/mytask2.sh` 

### 第三个案例：每天凌晨2:00 将mysql 数据库 testdb ，备份到文件中

1. 先编写一个文件 /home/mytask3.sh

   ```shell
   /usr/local/mysql/bin/mysqldump -u root -proot testdb > /tmp/mydb.bak
   ```

2. 给 mytask3.sh 一个可以执行权限

   ```shell
   chmod 744 /home/mytask3.sh
   ```

3. `crontab -e`

4. `0 2 * * * /home/mytask3.sh` 

## crond相关指令

```bash
conrtab –r  ==>  终止任务调度
crontab –l  ==>  列出当前有那些任务调度
service crond restart [重启任务调度]
```



# Linux磁盘分区和挂载

## 分区基础知识

**分区的两种方式：**

1. MBR分区（主引导记录）
   1. 最多支持四个主分区
   2. 系统只能安装在主分区
   3. 扩展分区要占一个主分区
   4. MBR 最大只支持 2TB，但拥有最好的兼容性
2. GPT 分区（GUID Partition Table 全局唯一标识磁盘分区表）
   1. 支持无限多个主分区（但操作系统可能限制，比如 windows 下最多 128 个分区）
   2. 最大支持 18EB 的大容量（1EB=1024 PB，1PB=1024 TB ）
   3. windows7 64 位以后支持 gpt

**Windows下的分区**

- 分为主分区和扩展分区（扩展分区下面可再分逻辑分区）

## Linux分区

- **原理介绍：**
  - Linux 来说无论有几个分区，分给哪一目录使用，它**归根结底就只有一个根目录**，**一个独立且唯一的文件结构** , Linux 中每个分区都是用来组成整个文件系统的一部分。
  - Linux 采用了一种叫==“载入”==的处理方法，它的整个文件系统中包含了一整套的文件和目录， 且将一个分区和一个目录联系起来。这时要载入的一个分区将使它的存储空间在一个目录下获得。
  - 通俗来说，就是硬盘下的分区会映射成根目录下的某个目录
- 硬盘说明
  - Linux 硬盘分 IDE 硬盘和 SCSI 硬盘，目前基本上是 SCSI 硬盘
  - 对于 IDE 硬盘，驱动器标识符为`hdx~`,其中`hd`表明分区所在设备的类型，这里是指 IDE 硬盘了。`x`为盘号（**a 为基本盘，b 为基本从属盘，c 为辅助主盘，d 为辅助从属盘**）,`~`代表分区，**前四个分区用数字 1 到 4 表示**，它们是主分区或扩展分区，**从 5 开始就是逻辑分区**。例如：hda3 表示为第一个 IDE 硬盘上的第三个主分区或扩展分区,hdb2 表示为第二个 IDE 硬盘上的第二个主分区或扩展分区
  - 对于 SCSI 硬盘则标识为`sdx~`，SCSI 硬盘是用`sd`来表示分区所在设备的类型的，其余则和 IDE 硬盘的表示方法一样。
- 使用`lsblk 命令`查看当前系统的分区和挂载情况
  - List block 显示分区
  - 输入`lsblk -f` 即可查看到当前系统的分区情况和相对应的挂载目录
  - 显示的内容为：
    - 分区情况、分区类型、UUID（universal unique id）唯一标识分区的40位不重复的字符串、挂载点
  - 如果想看大小，可以直接输入`lsblk`查看

## 新增硬盘并挂载的详细步骤

案例：给 Linux 系统增加一个新的硬盘，并且挂载到 `/home/newdisk`

1. **虚拟机添加硬盘**

   ```bash
   虚拟机  ->  设置  ->  硬件  ->  添加  ->  选择硬盘，下一步  ->  SCSI虚拟磁盘类型  ->  分配空间  -> 完成
   系统重启，再使用 lsblk -f 查看硬盘分区情况，可以查看到一个没有分区的硬盘sdb
   ```

2. **分区**

   ```bash
   fdisk /dev/sdb  进入分区引导
   m  寻求帮助
   n  添加一个新的分区
   p  设置为主分区  e是扩展分区
   选择主分区编号
   回车 + 回车，两次回车默认剩余全部空间
   w 分区信息写入硬盘并退出
   再使用 lsblk -f 查看分区情况可以发现只有分区sdb1但是没有对应的信息，这就是因为还没有格式化
   ```

3. **格式化**（MakeFileSystem）-- 创建文件系统

   ```bash
   msfs -t ext4 /dev/sdb1   
   意思就是：把 sdb1 格式化成 ext4 这种分区类型
   ```

4. **挂载**，将一个分区和一个目录联系起来

   ```bash
   先创建一个目录 /home/newdisk
   mount /dev/sdb1 /home/newdisk   ->     挂载
   但是这样的设置挂载，当你重启机器的时候，硬盘和目录的挂载关系就会没有了，这个只是临时挂载
   
   如果想不挂载了，就使用umount 设备名称 或者 挂载目录
   例如： umount /dev/sdb1 或 者 umount /newdisk
   要想设置永久，就需要设置一个文件
   ```

5. **设置可以自动挂载**（永久挂载），当你重启系统，仍然可以挂载到 /home/newdisk

   ```bash
   编辑一个文件 vim /etc/fstab  这个文件就记录着分区和挂载点的情况
   -----------------------------------------------------------------------
   编辑其中的内容
   添加一行映射关系代码
   /dev/sdb1                      /home/newdisk ext4 default 0 0
   保存退出
   -----------------------------------------------------------------------
   编辑完成后
   mount -a 
   -a 就是自动挂载
   重启过后就能发现是永久挂载了
   ```

## 查看磁盘情况

```bash
df [选项]   ->  查询系统整体磁盘使用情况
-l   列表显示

du [选项] [目录]  ->  查询指定目录的磁盘占用情况，默认为当前目录
-s   指定目录占用大小汇总
-h   带计量单位
-a   含文件
--max-depth=1   子目录深度
-c   列出明细的同时，增加汇总值

例1 -> 查询 /opt 目录的磁盘占用情况，深度为 1  ->  du -ach --max-depth=1 /opt
例2 -> 统计/home 文件夹下文件的个数  ->  ls -l /home | grep "^-" | wc -l
例3 -> 统计/home 文件夹下目录的个数  ->  ls -l /home | grep "^d" | wc -l
例4 -> 统计/home 文件夹下文件的个数，包括子文件夹里的  ->  ls -lR /home | grep "^-" | wc -l
例5 -> 统计文件夹下目录的个数，包括子文件夹里的  ->  ls -lR /home | grep "^d" | wc -l
例6 -> 以树状显示目录结构  ->  先yum install tree，再tree

解析：
用了管道符分隔，先列出来，再过滤，再统计
"^-"中 ^ 是定位符，表示开头   -表示以-开头的
ls参数是区分大小写的  -> 大写的R代表递归，小写的r（reverse）代表逆序
```

# 网络配置

## 常用指令

```bash
Windows下查看ip地址  ->  ipconfig
Linux下查看ip地址  ->  ifconfig

测试两个主机之间网路是否联通  ->  ping ip地址
```

## Linux网络环境配置

1. 可以通过**图形化界面**进行设置，设置**自动连接**

   - linux 启动后会自动获取 IP，**缺点是每次自动获取的 ip 地址可能不一样**
   - 这个不适用于做服务器，因为我们的服务器的 ip 需要是固定的

2. 通过**修改配置文件指定固定ip**

   ```bash
   直接修改配置文件来指定IP，并可以连接到外网   ->   /etc/sysconfig/network-scripts/ifcfg-eth0
   第一个显卡就是eth0，第二个就是eth1
   
   例：要将 ip 地址配置成静态的，ip 地址为 192.168.184.130
   vim /etc/sysconfig/network-scripts/ifcfg-eth0    ->  打开配置文件
   Linux会显示文件内容，其中要修改的内容如下 ↓↓↓↓
   DEVICE=eth0   ->接口名（设备，网卡）
   HWADDR=00:0c:2x:6x:0x:xx   ->  MAC地址
   TYPE=Ethernet   ->  网络类型
   UUID=926a57ba-92c6-4231-bacb-f27e5e6a9f44   ->  随机ID
   ONBOOT=yes    ->   系统启动的时候网络接口是否有效  静态，ONBOOT为yes；自动，ONBOOT为no
   BOOTPROTO=static   -> 以静态方式获得ip，还有bootp采用BOOTP协议 dhcp采用DHCP协议 none不使用协议
   IPADDR=192.168.184.130   ->  指定ip
   GATEWAY=192.168.184.2   ->  网关
   DNS1=192.168.184.2   ->  dns和网关保持一致即可
   
   修改后，一定要 重启服务
   service network restart
   或者直接  reboot 重启系统
   ```

   

# 进程管理

## 进程的基本介绍

- 在 LINUX 中，**每个执行的程序（代码）都称为一个进程**。每一个进程都**分配一个 ID 号**
- **每一个进程，都会对应一个父进程，而这个父进程可以复制多个子进程**。例如 www 服务器
- **每个进程都可能以两种方式存在的，前台与后台**。所谓前台进程就是用户目前的屏幕上可以进行操作的。后台进程则是实际在操作（也称为守护进程），但由于屏幕上无法看到的进程，通常使用后台方式执行
- **一般系统的服务都是以后台进程的方式存在，而且都会常驻在系统中**。直到关机才才结束

## 显示系统执行的进程

```bash
查看进行使用的指令是 ps ,一般来说使用的参数是 ps -aux
-a  显示当前终端所有的进程信息
-u  以用户的格式显示进程信息
-x  显示后台进程运行的参数
-e  显示所有进程
-f  全格式

PID   进程识别号
TTY   终端机号
TIME  此进程所消CPU时间
CMD   正在执行的命令或进程名


例1：输入指令 ps -aux | more
USER   PID   %CPU  %MEM   VSZ   RSS   TTY   STAT    START    TIME     COMMAND

详解
System V 展示风格
USER：用户名称
PID：进程号
%CPU：进程占用 CPU 的百分比
%MEM：进程占用物理内存的百分比
VSZ：进程占用的虚拟内存大小（单位：KB）
RSS：进程占用的物理内存大小（单位：KB）
TTY：终端名称
STAT：进程状态，其中 S-睡眠，s-表示该进程是会话的先导进程，N-表示进程拥有比普通优先级更低的优先级，R-正在运行，D-短期等待，Z-僵死进程，T-被跟踪或者被停止等等
STARTED：进程的启动时间
TIME：CPU 时间，即进程使用 CPU 的总时间
COMMAND：启动进程所用的命令和参数，如果过长会被截断显示


例2：输入指令 ps -ef | more
UID  PID  PPID   C  STIME  TTY   TIME   CMD

详解：
UID：用户 ID
PID：进程 ID
PPID：父进程 ID
C：CPU 用于计算执行优先级的因子。数值越大，表明进程是 CPU 密集型运算，执行优先级会降低；数值越小，表明进程是 I/O 密集型运算，执行优先级会提高
STIME：进程启动的时间
TTY：完整的终端名称
TIME：CPU 时间
CMD：启动进程所用的命令和参数
```

## 终止进程 kill 和 killall

- 若是某个进程执行一半需要停止时，或是已消了很大的系统资源时，此时可以考虑停止该进程
- 可使用 kill 命令来完成此项任务

```bash
kill [选项] 进程号    ->   通过进程号杀死进程
-9  表示强迫进程立即停止

killall 进程名称      ->   通过进程名称杀死进程，也支持通配符，这在系统因负载过大而变得很慢时很有用

例子：
踢掉某个用户  ->  ps -aux | grep sshd  ->  查看进程号  ->  kill 4010
终止多个 gedit 编辑器  ->  killall gedit
强制杀掉一个终端  ->  kill -9 4090
```

## 查看进程树

```bash
pstree [选项] 
-p :显示进程的 PID
-u :显示进程的所属用户

例子：请你树状的形式显示进程的 pid
pstree -p
```

## 服务管理

- **服务(service) 本质就是进程**，但是是运行在后台的，通常都会监听某个端口，等待其它程序的请求，比如（mysql , sshd 防火墙等），因此我们又称为**守护进程**，是 Linux 中非常重要的知识点。

```bash
service 服务名 [start | stop | restart | reload | status]
CentOS7.0 后 不再使用 service ,而是 systemctl

查看服务名：
1.使用setup->系统服务查看   CentOS7是nmtui   使用tab切换到[确定]和[取消]
2.查看目录 ls -l /etc/init.d/    CentOS7使用 systemctl list-unit-files 可以列出所有的服务
```

## 查看防火墙

```bash
查看当前防火墙的状况   ->    service iptables status  CentOS7改为  systemctl status firewalld
关闭防火墙    ->    service iptables stop  CentOS7改为  systemctl stop firewalld
开启防火墙    ->    service iptables start  CentOS7改为  systemctl start firewalld

检查Linux的某个端口是否在监听并且可以访问    ->    telnet ip 端口号  例如 telnet 192.168.1.30 22
yum list telnet*   yum install telnet-server  yum install telnet.*   按照这三条指令先安装亲测有效

注意！
1. 关闭或者启用防火墙后，立即生效
2. 这种方式只是临时生效，当重启系统后，还是回归以前对服务的设置
3. 如果希望设置某个服务自启动或关闭永久生效，要使用 chkconfig 指令
```

## **chkconfig 指令**

- 通过`chkconfig` 命令可以**给每个服务的各个运行级别设置自启动/关闭**
- 但是这个指令只能在CentOS中使用

```bash
chkconfig --list|grep xxx     ->  查看服务 
chkconfig 服务名 --list        ->  查看服务 
chkconfig --level 5 服务名 on/off   ->  修改服务在某个运行级别下的自启动

例子：
案例 1： 请显示当前系统所有服务的各个运行级别的运行状态  ->   chkconfig --list
案例 2：请查看 sshd 服务的运行状态  ->   service sshd status
案例 3： 将 sshd 服务在运行级别 5 下设置为不自动启动，看看有什么效果？  ->   chkconfig --level 5 sshd off
案例 4： 当运行级别为 5 时，关闭防火墙  ->   chkconfig --level 5 iptables off
案例 5： 在所有运行级别下，关闭防火墙  ->   chkconfig iptables off
案例 6： 在所有运行级别下，开启防火墙  ->   chkconfig iptables on3
```

- chkconfig 重新设置服务后自启动或关闭，==需要重启机器 reboot 才能生效==

## 动态监控进程

- top 与 ps 命令很相似，它们都用来显示正在执行的进程

- Top 与 ps 最大的不同之处，在于 top 在执行一段时间可以更新正在运行的的进程
- 有点类似于Windows下的任务管理器

```bash
top [选项]
选项说明：
-d 秒数  ->  指定top命令每隔几秒更新，默认是3秒在top命令的交互模式当中可以执行的命令
-i   ->   使top不显示任何进闲置或僵死进程
-p   ->   通过指定监控进程ID来仅仅监控某个进程的状态
交互操作说明
P  ->  以CPU使用率排序
M  ->  以内存使用率排序
N  ->  以PID排序
q  ->  退出top
输入u后输入某个用户名  ->  查看该用户名的服务
输入k，回车，再输入一个进程ID号  ->  终止指定的进程
```

## 查看系统网路情况 netstat

```bash
net [选项]
-an  ->  按一定顺序排列输出
-p  ->  显示哪个进程在调用

案例1:查看系统所有的网络服务  ->  netstat -anp | more
案例2:查看系统某一个网络服务  ->  netstat -anp | grep sshd
```



# RPM

## 基本介绍

RPM是一种用于互联网下载包的打包及安装工具，它包含在某些 Linux 分发版中，生成具有`.RPM `扩展名的文件

RPM 是 `RedHat Package Manager`（RedHat 软件包管理工具）的缩写，类似 windows 的 setup.exe，这一文件格式名称虽然打上了 RedHat 的标志，但理念是通用的

Linux 的分发版本都有采用（suse,redhat, centos 等等），可以算是公认的行业标准了。

## 查询RPM包

```bash
rpm -qa  ->  查询所安装的所有rpm 软件包
rpm -qa | more   ->  分页显示
rpm -qa | grep X [rpm -qa | grep firefox]  ->  指定查找某个软件
rpm -qi 软件包名  ->  查询软件包信息
rpm -ql 软件包名  ->   查询软件包中的文件
rpm -qf 文件全路径名   ->  查询文件所属的软件包


基本格式：
一个 rpm 包名：firefox-45.0.1-1.el6.centos.x86_64.rpm 
名称:firefox
版本号：45.0.1-1
适用操作系统: el6.centos.x86_64
表示 centos6.x 的 64 位系统
如果是 i686、i386 表示 32 位系统，noarch 表示通用
```

## 安装RPM包

```bash
rpm -ivh RPM包的全路径名称
i=install 安装
v=verbose 提示
h=hash  进度条

```

## 卸载RPM包

```bash
rpm -e RPM包名

注意事项：
1. 如果其它软件包依赖于您要卸载的软件包，卸载时则会产生错误信息。如：
$ rpm -e foo
removing these packages would break dependencies:foo is needed by bar-1.0-1
2. 如果我们就是要删除 foo 这个 rpm 包，可以增加参数 --nodeps ，就可以强制删除，但是一般不推荐这样做，因为依赖于该软件包的程序可能无法运行
如：$ rpm -e --nodeps foo
带上 --nodeps 就是强制删除。
```

# YUM

## 基本介绍

- Yum 是一个 **Shell 前端软件包管理器**
- YUM 基于 RPM 包管理，**能够从指定的服务器自动下载 RPM 包并且安装**，可以自动处理依赖性关系，并且一次安装所有依赖的软件包。**使用 yum 的前提是已经联网**。

```bash
基本指令：
查询 yum 服务器是否有需要安装的软件  ->  yum list|grep xx 软件列表
下载安装指定的 yum 包  ->  yum install xxx 
```

## 安装YUM包

```bash
先查询软件列表  ->   yum list|grep jdk
安装包  yum install java-1.8.0-openjdk.i686

一般会默认安装最新的，你也可以指定安装某个包
安装完成过后会删除安装包
```

如果需要卸载，直接通过RPM包管理卸载即可

# JAVAEE环境安装

## 需要安装jdk

- 这里安装 Java8 版本，而且是通过官网下载的压缩包进行解压，再配置

```bash
先将软件通过 xftp5 上传到 /opt 下
解压缩到 /opt  ->   tar -zxvf jdk-8u181-linux-x64.tar.gz
配置环境变量的配置文件 vim /etc/profile
	JAVA_HOME=/opt/jdk1.7.0_79    ->  JavaHome
	PATH=/opt/jdk1.7.0_79/bin:$PATH   ->  路径
	export JAVA_HOME PATH   ->   输出变量，环境变量生效
需要注销用户，环境变量才能生效  ->  运行级别3就logout，运行级别5就重启
输入 java -version  和  javac -version  查看是否配置成功
```



## 需要安装tomcat

- 一般spring boot项目会自带tomcat，就不需要安装，传统的SSM和SSH就需要tomcat服务器

```bash
上传文件过后解压缩到/opt
启 动 tomcat ./startup.sh	
	进入bin目录  ->  cd apache-tomcat-7.0.70/bin/
	ls 查看目录内文件
	执行脚本文件  ->  ./startup.sh
开放端口 8080 这样外网才能访问到 tomcat
	vim /etc/sysconfig/iptables
	将开放22号端口的哪一行代码复制粘贴，将22改成8080即可开放8080端口
	Centos7 -> firewall-cmd --permanent --add-port=8080/tcp  ->  firewall-cmd --reload
	centos8 -> firewall-cmd --add-port=8080/tcp --permanent
```

- CentOS7 安装tomcat9可以查看教程 ：https://blog.csdn.net/mmmbox/article/details/89461518

## 需要安装数据库，这里安装MySQL

- 可查看教程：https://www.cnblogs.com/nicknailo/articles/8563737.html
- 初始密码的要求参数：https://www.cnblogs.com/newbest/p/9753706.html

## 如果是图形界面，还需要安装一款ide

- 这个可以直接在图形界面的软件商店中安装

# Shell编程

## 为什么要学Shell编程

1. Linux 运维工程师在进行服务器集群管理时，需要**编写 Shell 程序来进行服务器管理**。
2. 对于 JavaEE 和 Python 程序员来说，工作的需要，你的老大会要求你编写一些**Shell 脚本**进行程序或者是服务器的维护，比如编写一个定时备份数据库的脚本。
3. 对于大数据程序员来说，需要编写 Shell 程序来**管理集群**。

## Shell是什么

- Shell 是一个命令行解释器，它为用户提供了一个向Linux 内核发送请求以便运行程序的界面系统级程序，用户可以用 Shell 来启动、挂起、停止甚至是编写一些程序
- 在我们使用的过程中，应用程序调用shell或者我们直接执行shell脚本，然后shell操作Linux内核，内核再驱动硬件
- <font color=red>shell主要是对我们的指令进行解析，解析指令给Linux内核。反馈结果在通过内核运行出结果，通过shell解析给用户</font>
- ==shell是外壳程序的统称，bash 是具体的一种shell==

![](http://c.biancheng.net/uploads/allimg/190417/1-1Z41G31T3628.gif)

- Shell编程开发原理

![](https://img-blog.csdn.net/20180911114843294?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ExNTkyOTc0ODUwMg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## Shell脚本执行方式

1. **格式要求**：

   - 脚本以`#!/bin/bash` 开头
   - 脚本需要有可执行权限

2. **快速写一个 输出 helloworld 的脚本** `hello.sh`

   ```bash
   #!/bin/bash    ->  表示shell脚本用bash来解析
   echo "hello world"
   ```

3. **常用执行方式**：

   1. **输入脚本的绝对路径或相对路径**，即可执行

      ```bash
      chmod 744 hello.sh   ->  给所有者一个执行权限
      ./hello.sh   ->   相对路径
      /root/shell/hello.sh   ->   绝对路径
      ```

   2. **输入指令**：`sh 脚本路径`   这样可以不用赋予脚本执行权限，直接执行，但是==不推荐==

      ```bash
      sh ./hello.sh   ->   通过相对路径
      sh /root/shell/hello/sh   ->   通过绝对路径
      ```

## Shell的变量

### Shell变量的介绍

- Linux Shell 中的变量分为，==系统变量==和==用户自定义变量==。

```shell
系统变量：$HOME、$PWD、$SHELL、$USER 等   比如： echo "path=$PATH"
显示当前 shell 中所有变量：set
```

### Shell变量的定义

```shell
定义变量：变量=值
撤销变量：unset 变量
声明静态变量：readonly 变量，  注意：不能unset!
把变量提升为全局环境变量，可供其他 shell 程序使用   --> 详情见下一节 设置环境变量

例：
A=100
readonly B=99
echo "A=$A"
unset A
```

### 定义变量的规则

1. 变量名称可以由**字母、数字和下划线**组成，但是**不能以数字**开头。
2. **等号两侧不能有空格**
3. 变量名称一般习惯为**大写**

### 将命令的返回值赋给变量（重点）

```shell
A=`ls -la`   用反引号将命令括起来 -> 运行里面的命令并把结果返回给变量 A
A=$(ls -la)  等价于反引号
```

## 设置环境变量

### 基本语法

```bash
export 变量名=变量值  ->  将 shell 变量输出为环境变量
source 配置文件   ->  让修改后的配置信息立即生效
echo $变量名   ->  查询环境变量的值
```

- 例如，在 /etc/profile 中设置一个环境变量`$TOMCAT_HOME` ，在我们自己写得shell脚本中引用，但是在配置过后，为了让 /etc/profile 中的环境变量生效，需要使用 `source /etc/profile` 或者重启系统/注销用户才能生效，类似于一个全局变量

### 快速入门

```shell
# vim /etc/profile 
# 定义一个环境变量 
TOMCAT_HOME='helloworld'
export TOMCAT_HOME

# 要使用 source /etc/profile 指令重新加载，不然使用不了

# vim ./hello.sh
#!/bin/bash
echo "$TOMCAT_HOME"
```

## 位置参数变量

### 介绍

当我们执行一个 shell 脚本时，如果希望**获取到命令行的参数信息**，就可以使用到位置参数变量

比如 ：

`./myshell.sh 100 200` , 这个就是一个执行 shell 的命令行，可以在 myshell 脚本中获取到参数信息

### 基本语法

```shell
$n   -> n 为数字，$0 代表命令本身，$1-$9 代表第一到第九个参数，十以上的参数，十以上的参数需要用大括号包含，如${10}

$*   ->   这个变量代表命令行中所有的参数，$*把所有的参数看成一个整体
$@   ->   这个变量也代表命令行中所有的参数，不过$@把每个参数区分对待
===> 这两者的区别可以到循环语句的for循环语句存中查看区别

$#   ->   这个变量代表命令行中所有参数的个数
```

### 17.6.3 应用实例

- 编写一个 shell 脚本 positionPara.sh ， 在脚本中获取到命令行的各个参数信息

```shell
#!/bin/bash
#获取各个参数
echo $0 $1 $2
echo $*
echo $@
echo "参数个数=$#"

输入 ./positionPara.sh 100 200 300 后的输出效果
./positionPara.sh 100 200
100 200 300
100 200 300 
参数个数=3
```

## 预定义变量

1. 基本介绍

   - 预定义变量就是 shell 设计者事先已经定义好的变量，可以直接在 shell 脚本中使用

2. 基本语法

   ```shell
   $$  ->  当前进程的进程号（PID）
   $!  ->  后台运行的最后一个进程的进程号（PID）
   $？ ->  最后一次执行的命令的返回状态。如果这个变量的值为 0，证明上一个命令正确执行；如果这个变量的值为非 0（具体是哪个数，由命令自己来决定），则证明上一个命令执行不正确了。
   ```

3. 应用实例

   ```shell
   编写脚本 test.sh
   #!/bin/bash
   echo "当前的进程号=$$"
   # 后台的方式运行 ./myshell.sh 这个脚本
   ./myshell.sh &
   echo "最后的进程号=$!"
   echo "最后一次执行的命令的返回状态：$?"
   
   
   输出效果：
   当前的进程号=22083
   最后的进程号=22084
   最后一次执行的命令的返回状态：0
   ```

## 运算符

1. **基本介绍**

   - 可以在 shell 中进行各种运算操作

2. **基本语法**

   ```bash
   "$((运算式))"或"$[运算式]"   ->   推荐使用 $[运算式]
   expr m + n   ->  注意 expr 运算符间要有空格
   expr m - n
   expr \*, /, %   -> 乘，除，取余
   ```

3. 应用案例

   ```shell
   计算（2+3）X4 的值
       $((运算式))  ->  RESULT1=$(((2+3)*4))
       $[运算式]  ->  RESULT2=$[(2+3)*4]
       expr  ->   TEMP=`expr 2 + 3`
   			  RESULT3=`expr $TEMP \* 4`
   请求出命令行的两个参数[整数]的和
   	SUM=$[$1+$2]
   	echo "SUM=$SUM"
   	输入指令 ./shelltest.sh 100 200 即可看到输出结果为 SUM=300
   ```

## 条件判断

1. 基本语法

   ```shell
   [ condition ] （注意 condition 前后要有空格）#非空返回 true，可使用$?验证（0 为 true，>1 为 false）
   
   一些案例：
   [ string ]   ->   返回true
   [ ]   ->   返回false
   [ condition ] && echo OK || echo notok   ->  类似于问号表达式，条件为真走前，假走后
   ```

2. 常用判断条件

   ```shell
   1. 两个整数比较
       = 字符串比较
       -lt 小 于
       -le 小于等于
       -eq 等 于
       -gt 大 于
       -ge 大于等于
       -ne 不等于
   2. 按照文件权限进行判断
       -r 有读的权限 [ -r 文件 ]
       -w 有写的权限
       -x 有执行的权限
   3. 按照文件类型进行判断
       -f 文件存在并且是一个常规的文件
       -e 文件存在
       -d 文件存在并是一个目录
   ```

3. 应用实例

   ```shell
   案例1："ok"是否等于"ok"   ->   [ "ok" = "ok" ] && echo equal || echo notEqual
   案例2：23 是否大于等于 22   ->   [ 23 -gt 22 ] && echo yes || echo no
   案例3：/root/install.log 目录中的文件是否存在   ->  [ -e /root/install.log ] && echo have || echo nothave  
   ```

## 循环和分支

1. if 判断

   ```shell
   if [ 条件判断式 ];then
   	程序
   fi
   或者
   if [ 条件判断式 ]
   then
   	程序
   elif [条件判断式]
   then
   	程序
   fi
   注意事项：
   1. [ 条件判断式 ]  中括号和条件判断式之间必须有空格 
   2. 推荐使用第二种方式
   
   案例：请编写一个 shell 程序，如果输入的参数，大于等于 60，则输出 "及格了"，如果小于 60,则输出 "不及格"
   if [ $1 -ge 60 ]
   then
           echo "及格了"
   elif [ $1 -lt 60 ]
   then
           echo "不及格"
   fi
   输出结果：
   [root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./test2.sh 60
   及格了
   [root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./test2.sh 59
   不及格
   ```

2. case 语句

   ```shell
   case $变量名 in
   "值 1"）
   	如果变量的值等于值 1，则执行程序 1
   ;;
   "值 2"）
   	如果变量的值等于值 2，则执行程序 2
   ;;
   …省略其他分支…
   *）
   	如果变量的值都不是以上的值，则执行此程序
   ;;
   esac
   案例1：当命令行参数是 1 时，输出 "周一", 是 2 时，就输出"周二"， 其它情况输出 "other"
   case $1 in
   "1")
           echo "周一"
   ;;
   "2")
           echo "周二"
   ;;
   *)
           echo "other"
   esac
   
   输出结果：
   [root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./case.sh 1
   周一
   [root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./case.sh 2
   周二
   [root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./case.sh 3
   other
   ```

3. for 循环

   ```shell
   第一种方式：
   for 变量 in 值1 值2 值3…
   do
     程序
   done
   第二种方式：
   for (( 初始值;循环控制条件;变量变化 ))
   do
   	程序
   done
   
   案例1：打印命令行输入的参数 -> 顺便讲解一下 $* 和 $@ 的区别
   	代码：
   	#!/bin/bash
       for i in "$*"
       do
               echo "the num is $i"
       done
       echo "=============="
       for j in "$@"
       do
               echo "the num is $j"
       done
   	输出效果：
   	[root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./for.sh 1 2 3 4 5 6
       the num is 1 2 3 4 5 6
       ==============
       the num is 1
       the num is 2
       the num is 3
       the num is 4
       the num is 5
       the num is 6
   案例2：从 1 加到 100 的值输出显示
   	代码：
   	SUM=0
       for ((i=1;i<=100;i++))
       do
               SUM=$[SUM+$i]
       done
       echo "SUM=$SUM"
   	输出效果：
   	SUM=5050
   ```

4. while 循环

   ```shell
   while [ 条件判断式 ]    ->  注意空格，while后面是有空格的
   do
   	程序
   done
   案例1：从命令行输入一个数 n，统计从 1+..+ n 的值
   	代码：
   	SUM=0
       i=0
       while [ $i -le $1 ]
       do
               SUM=$[$SUM+$i]
               i=$[$i+1]
       done    
       echo "sum=$SUM"
       输入指令：
       ./while.sh 100
       输出效果：
       sum=5050
   ```

## read 读取控制台输入

基本语法

```shell
read [选项] [参数] 赋值变量名
-p：指定读取值时的提示符，然后会阻塞等你输入一个值，回车后继续执行
-t：指定读取值时等待的时间（秒），如果没有在指定的时间内输入，就不再等待了
赋值变量名：会将读取到的值赋给该变量

例1：读取控制台输入一个 num 值
read -p "请输入一个num值：" NUM1
echo "num=$NUM1"
例2：读取控制台输入一个 num 值，在 10 秒内输入
read -t 3 -p "请输入一个num值：" NUM2
echo "num2=$NUM2"
```

## 函数

1. 函数介绍

   - shell 编程和其它编程语言一样，有系统函数，也可以自定义函数。系统函数中，我们这里就介绍两个：`basename`和`dirname`

2. 系统函数

   1. basename  =>  返回完整路径最后 / 的部分，常用于获取文件名

      ```shell
      basename [pathname] [suffix]
       basename命令会删掉所有的前缀包括最后一个（‘/’）字符，然后将字符串显示出来
       suffix 为后缀，如果 suffix 被指定了，basename 会将 pathname 或 string 中的 suffix 去掉
      
      例子：请返回 /root/shell/read.sh 的 "read.sh" 部分
          basename /root/shell/read.sh  ->  返回 read.sh
          basename /root/shell/read.sh .sh  ->  如果加上后缀则只返回文件名 read
      ```

   2. dirname  =>  返回完整路径最后 / 的前面的部分，常用于返回路径部分

      ```shell
      dirname 文件绝对路径 
      从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径（目录的部分）
      
      例子：请返回 /root/shell/read.sh 的 /root/shell
      dirname /root/shell/read.sh  ->  返回前面的路径 /root/shell
      ```

3. 自定义函数

   ```shell
   function funname(){
   	Action; 
   	[return int;]
   }
   调用直接写函数名： funname [值]
   
   例子：计算输入两个参数的和（read）， getSum
   	代码：
       #!/bin/bash
       function getSum(){
               SUM=$[$n1+$n2]
               echo "和是:$SUM"
       }
   
       read -p "请输入a:" n1
       read -p "请输入b:" n2
   
       getSum $n1 $n2
       输入指令：
       ./fun.sh
       输出：
       [root@iZwz98zprwjrt7d2pp9g0zZ shell]# ./fun.sh
       请输入a:1
       请输入b:2
       和是:3
   ```

## Shell编程综合案例

- 需求分析：

  - 每天凌晨 2:10 备份 数据库 testDB 到 /data/backup/db
  - 备份开始和备份结束能够给出相应的提示信息
  - 备份后的文件要求以备份时间为文件名，并打包成 .tar.gz 的形式，比如：2018-03-12_230201.tar.gz
  - 在备份的同时，检查是否有 10 天前备份的数据库文件，如果有就将其删除。

- 思路分析：

  - 数据库中有一个 testDB ，要在Linux的 /data/backup/db 下备份数据库
  - 现在在 /usr/sbin 下写一个 mysql_db_bbackup.sh 脚本来实现这个功能
  - 写完脚本后交给crond来做定时任务调度

- 代码实现：

  ```shell
  vim /usr/sbin/mysql_db_bbackup.sh
  
  #!/bin/bash
  # 数据库的备份
  
  # 定义备份的路径
  BACKUP=/data/backup/db
  # 获取当前的时间，作为文件名
  DATETIME=$(data +%Y_%m_%d_%H%M%S)
  # 输出变量查看 以作调试
  echo $DATETIME
  
  echo "======开始备份======"
  echo "======备份的路径是 $BACKUP/$DATETIME.tar.gz======"
  
  # 主机
  HOST=localhost
  # 用户名字
  DB_USER=root
  # 密码
  DB_PASSWD=root
  # 数据库名
  DATABASE=testDB
  # 创建备份的路径  如果备份的路径文件夹存在就使用，没有就创建
  [ ! -d "$BACKUP/$DATETIME" ] && mkdir -p "$BACKUP/$DATETIME"
  # 执行mysql的备份数据库的指令 将备份完后的内容进行压缩，形成一个临时的压缩包文件
  mysqldump -u${DB_USER} -p${DB_PASSWD} --host=$HOST $DATABASE | gzip > $BACKUP/$DATETIME/$DATETIME.sql.gz
  # 打包备份文件
  cd $BACKUP
  tar -zcvf $DATETIME.tar.gz $DATETIME
  # 删除临时目录
  rm -rf $BACKUP/$DATETIME
  # 删除10天前的备份文件
  find $BACKUP -mtime +10 -name "*.tar.gz" -exec rm -rf {} \;
  echo "======备份成功======"
  
  至此shell脚本编写完成
  然后将脚本交给crond定时执行
  crontab -e
  10 2 * * * /usr/sbin/mysql_db_bbackup.sh
  ```

  





















