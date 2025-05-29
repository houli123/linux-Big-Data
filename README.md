<p align="center"> 
  <a href="https://jaywcjlove.github.io/linux-command">
    <img src="./template/img/banner.svg?sanitize=true">
  </a>
  <h1>Linux Command</h1>
</p>

预览搜索：**https://git.io/linux**

[![Linux 命令大全](https://user-images.githubusercontent.com/1680273/123261829-ce830300-d529-11eb-8cea-a39059b972dd.gif)](https://jaywcjlove.github.io/linux-command/)


**推荐使用的镜像 web 版本**

[**`linuxsearch.largeinfo.cc`**](http://linuxsearch.largeinfo.cc)，[**`srebro.cn`**](https://linux.srebro.cn/)，[**`getaifun.com`**](https://getaifun.com/linux)，[**`linux.devonline.net`**](http://linux.devonline.net/)，[**`man.zch.ooo`**](https://man.zch.ooo/)，[**`linux.mmoke.com`**](https://linux.mmoke.com)，[**`bqrdh.com`**](https://tools.bqrdh.com/linux-command/)，[**`linux.zyimm.com`**](http://linux.zyimm.com/)，[**`linux.vovuo.com`**](https://linux.vovuo.com/)，[`linux.liguiying.cn`](https://linux.liguiying.cn/), [`renye.net`](https://renye.net/), [`diqi.org`](https://diqi.org/)，[`linux.alistnas.top`](https://linux.alistnas.top/)，[`nenufm.com`](https://www.nenufm.com/linux-command/)

**其它 web 版本**

[`linux.ftqq.com`](https://linux.ftqq.com/)，[`linux.gaomeluo.com`](https://linux.gaomeluo.com)，[`atoolbox.net`](http://www.atoolbox.net/Tool.php?Id=826)，[`xiaoshanseo.com`](https://tools.xiaoshanseo.com/Tools/linux-command/)，[`262235.xyz`](https://262235.xyz/linux-command/)，[`cmsblogs.cn`](https://linux.cmsblogs.cn/)，[`loquy.cn`](https://www.loquy.cn/linux-command/)，[`buyao.vip`](https://demo.buyao.vip/linux/)，[`hezhiqiang.gitbook.io`](https://hezhiqiang.gitbook.io/linux/)，[`utils.fun`](https://linux.utils.fun/), [`51tools.info`](https://51tools.info/linux/)

## Docker

[![Docker Image Version (latest by date)](https://img.shields.io/docker/v/wcjiang/linux-command?logo=docker)](https://hub.docker.com/r/wcjiang/linux-command) [![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/wcjiang/linux-command?logo=docker)](https://hub.docker.com/r/wcjiang/linux-command) [![Docker Pulls](https://img.shields.io/docker/pulls/wcjiang/linux-command?logo=docker)](https://hub.docker.com/r/wcjiang/linux-command)

轻松通过 docker 部署 linux-command 网站。

```bash
docker pull wcjiang/linux-command
# Or
docker pull ghcr.io/jaywcjlove/linux-command:latest
```

```bash
docker run --name linux-command --rm -d -p 9665:3000 wcjiang/linux-command:latest
# Or
docker run --name linux-command -itd -p 9665:3000 wcjiang/linux-command:latest
# Or
docker run --name linux-command -itd -p 9665:3000 ghcr.io/jaywcjlove/linux-command:latest
```

在浏览器中访问以下 URL

```bash
http://localhost:9665/
```

## Vercel

可以点击下面按钮一键部署至 [Vercel](https://vercel.com):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/jaywcjlove/linux-command)

<details>
<summary>部署结果</summary>

![](./assets/vercel.png)

</details>

通过 Vercel 分配的域名访问，或者自行在设置中绑定域名。

## 宝塔面板

可通过宝塔面板应用商店快速部署 linux-command

<details>
<summary>部署步骤</summary>

### 前提

* 仅适用于宝塔面板 9.2.0 及以上版本
* 安装宝塔面板，前往[宝塔面板](https://www.bt.cn/new/download.html)官网，选择正式版的脚本下载安装

### 部署

1. 登录宝塔面板，在左侧菜单栏中点击 `Docker`
2. 首次会提示安装`Docker`和`Docker Compose`服务，点击立即安装，若已安装请忽略。
3. 安装完成后在`Docker-应用商店-实用工具`中找到 `linux-command`，点击`安装`，也可以在搜索框直接搜索`linux`。
4. 设置域名等基本信息，点击`确定`
* 说明：
  * 名称：应用名称，默认`linuxcommand_随机字符`
  * 版本选择：默认`latest`
  * 域名：如您需要通过域名访问，请在此处填写您的域名
  * 允许外部访问：如您需通过`IP+Port`直接访问，请勾选，如您已经设置了域名，请不要勾选此处
  * 端口：默认`3000`，可自行修改
  * CPU 限制：0 为不限制，根据实际需要设置
  * 内存限制：0 为不限制，根据实际需要设置
5. 提交后面板会自动进行应用初始化，大概需要`1-3`分钟，初始化完成后即可访问。

### 访问 linux-command

* 如果您填写域名，请在浏览器输入您的域名访问，如`http://demo.linux-command`，即可访问 `linux-command` 页面。
* 如您选择`IP+端口访问`请在浏览器地址栏中输入域名访问 `http://<宝塔面板IP>:6806`，即可访问 `linux-command` 页面。

</details>

## Linux命令分类

*这里存放Linux 命令大全并不全，你可以通过[linux-command](https://jaywcjlove.github.io/linux-command/)来搜索，它是把 [command](./assets/command) 目录里面搜集的命令，生成了静态HTML并提供预览以及索引搜索。*

### 文件传输

bye、ftp、ftpcount、ftpshut、ftpwho、ncftp、tftp、uucico、uucp、uupick、uuto、scp

### 备份压缩

ar、bunzip2、bzip2、bzip2recover、compress、cpio、dump、gunzip、gzexe、gzip、lha、restore、tar、unarj、unzip、zip、zipinfo

### 文件管理

diff、diffstat、file、find、git、gitview、ln、locate、lsattr、mattrib、mc、mcopy、mdel、mdir、mktemp、mmove、mread、mren、mshowfat、mtools、mtoolstest、mv、od、paste、patch、rcp、rhmask、rm、slocate、split、tee、tmpwatch、touch、umask、whereis、which、cat、chattr、chgrp、chmod、chown、cksum、cmp、cp、cut、indent

### 磁盘管理

cd、df、dirs、du、edquota、eject、lndir、ls、mcd、mdeltree、mdu、mkdir、mlabel、mmd、mmount、mrd、mzip、pwd、quota、quotacheck、quotaoff、quotaon、repquota、rmdir、rmt、stat、tree、umount

### 磁盘维护

badblocks、cfdisk、dd、e2fsck、ext2ed、fdisk、fsck.ext2、fsck、fsck.minix、fsconf、hdparm、losetup、mbadblocks、mformat、mkbootdisk、mkdosfs、mke2fs、mkfs.ext2、mkfs、mkfs.minix、mkfs.msdos、mkinitrd、mkisofs、mkswap、mpartition、sfdisk、swapoff、swapon、symlinks、sync

### 系统设置

alias、apmd、aumix、bind、chkconfig、chroot、clock、crontab、declare、depmod、dircolors、dmesg、enable、eval、export、fbset、grpconv、grpunconv、hwclock、insmod、kbdconfig、lilo、liloconfig、lsmod、minfo、mkkickstart、modinfo、modprobe、mouseconfig、ntsysv、passwd、pwconv、pwunconv、rdate、resize、rmmod、rpm、set、setconsole、setenv、setup、sndconfig、SVGAText Mode、timeconfig、ulimit、unalias、unset

### 系统管理

adduser、chfn、chsh、date、exit、finger、free、fwhois、gitps、groupdel、groupmod、halt、id、kill、last、lastb、login、logname、logout、logrotate、newgrp、nice、procinfo、ps、pstree、reboot、renice、rlogin、rsh、rwho、screen、shutdown、sliplogin、su、sudo、suspend、swatch、tload、top、uname、useradd、userconf、userdel、usermod、vlock、w、who、whoami、whois

### 文本处理

awk、col、colrm、comm、csplit、ed、egrep、ex、fgrep、fmt、fold、grep、ispell、jed、joe、join、look、mtype、pico、rgrep、sed、sort、spell、tr、uniq、vi、wc

### 网络通讯

dip、getty、mingetty、ppp-off、smbd(samba daemon)、telnet、uulog、uustat、uux、cu、dnsconf、efax、httpd、ip、ifconfig、mesg、minicom、nc、netconf、netconfig、netstat、ping、ping6、pppstats、samba、setserial、shapecfg(shaper configuration)、smbd(samba daemon)、statserial(status ofserial port)、talk、tcpdump、testparm(test parameter)、traceroute、tty(teletypewriter)、uuname、wall(write all)、write、ytalk、arpwatch、apachectl、smbclient(samba client)、pppsetup

### 设备管理

dumpkeys、loadkeys、MAKEDEV、rdev、setleds

### 电子邮件与新闻组

archive、ctlinnd、elm、getlist、inncheck、mail、mailconf、mailq、messages、metamail、mutt、nntpget、pine、slrn、X WINDOWS SYSTEM、reconfig、startx(start X Window)、Xconfigurator、XF86Setup、xlsatoms、xlsclients、xlsfonts

### 其他命令

yes


## 开发使用

可以通过 `npm` 安装 [`linux-command`](https://www.npmjs.com/package/linux-command) 包，包含所有命令的 markdown 文本，和一个[索引文件](dist/data.json)。

```bash
npm install linux-command
```

```js
var comm = require("linux-command");
console.log("---->", comm.ls);

var alias = require("linux-command/command/alias.md");
console.log("---->", alias); // markdown string
```

你也可以通过 CDN 来访问索引数据，和对应的命令详细内容，我将更新内容定期发布版本，提供大家使用，[UNPKG](https://unpkg.com/linux-command/) 带上版本号，将锁定版本访问，删除版本号请求数据，将会自动重定向最新版本。

```shell
# 命令索引 JSON 数据
https://unpkg.com/linux-command/dist/data.json
# 对应命令详情（Markdown）数据
https://unpkg.com/linux-command/command/<命令名称>.md
```

你也可以通过 Github 的 Raw 来，获取最新的内容

```shell
# 命令索引 JSON 数据
https://raw.githubusercontent.com/jaywcjlove/linux-command/master/dist/data.json
# 对应命令详情（Markdown）数据
https://raw.githubusercontent.com/jaywcjlove/linux-command/master/command/<命令名称>.md 
```

## Linux学习资源整理


### 社区网站

- [Linux中国](https://linux.cn/) - 各种资讯、文章、技术
- [实验楼](https://www.shiyanlou.com/) - 免费提供了Linux在线环境，不用在自己机子上装系统也可以学习Linux，超方便实用。
- [鸟哥的linux私房菜](http://linux.vbird.org/) - 非常适合Linux入门初学者看的教程。
- [Linux公社](http://www.linuxidc.com/) - Linux相关的新闻、教程、主题、壁纸都有。
- [Linux Today](http://www.linuxde.net) - Linux新闻资讯发布，Linux职业技术学习！。
- [X-CMD](https://www.x-cmd.com/) - Shell + AWK 为核心增强原生命令输出以及交互体验，各种命令以及现代化软件包的介绍和使用教程，每日科技新闻资讯，欢迎浏览关注！

### 知识相关

- [Linux思维导图整理](http://www.jianshu.com/p/59f759207862)
- [Linux初学者进阶学习资源整理](http://www.jianshu.com/p/fe2a790b41eb)
- [Linux 基础入门（新版）](https://www.shiyanlou.com/courses/1)
- [【译】Linux概念架构的理解](http://www.jianshu.com/p/c5ae8f061cfe) [En](http://oss.org.cn/ossdocs/linux/kernel/a1/index.html)
- [Linux 守护进程的启动方法](http://www.ruanyifeng.com/blog/2016/02/linux-daemon.html)
- [Linux编程之内存映射](https://www.shiyanlou.com/questions/2992)
- [Linux知识点小结](https://blog.huachao.me/2016/1/Linux%E7%9F%A5%E8%AF%86%E7%82%B9%E5%B0%8F%E7%BB%93/)
- [10大白帽黑客专用的 Linux 操作系统](https://linux.cn/article-6971-1.html)

### 软件工具

- [超赞的Linux软件](https://www.gitbook.com/book/alim0x/awesome-linux-software-zh_cn/details) Github仓库[Zh](https://github.com/alim0x/Awesome-Linux-Software-zh_CN) [En](https://github.com/VoLuong/Awesome-Linux-Software)

Adobe软件的最佳替代品 [原文在这里](https://linux.cn/article-8928-1.html)

- [Evince (Adobe Acrobat Reader)](https://wiki.gnome.org/Apps/Evince) 一个“支持多种文档格式的文档查看器”，可以查看PDF，还支持各种漫画书格式
- [Pixlr (Adobe Photoshop)](https://pixlr.com/) 一个强大的图像编辑工具
- [Inkscape (Adobe Illustrator)](https://inkscape.org/zh/) 一个专业的矢量图形编辑器
- [Pinegrow Web Editor (Adobe Dreamweaver)](https://pinegrow.com/) 一个可视化编辑制作 HTML 网站
- [Scribus (Adobe InDesign)](https://www.scribus.net/) 一个开源电子杂志制作软件
- [Webflow (Adobe Muse)](https://webflow.com/) 一款可以帮助用户不用编码就可以快速创建网站的谷歌浏览器插件。
- [Tupi (Adobe Animate)](http://www.maefloresta.com/portal/) 一款可以创建HTML5动画的工具。
- [Black Magic Fusion (Adobe After Effects)](https://www.blackmagicdesign.com) 一款先进的合成软件，广泛应用于视觉特效、广电影视设计以及3D动画设计等领域。

### 中国开源镜像站点

- 阿里云开源镜像站：http://mirrors.aliyun.com/
- 网易开源镜像站：http://mirrors.163.com/
- 搜狐开源镜像站：http://mirrors.sohu.com/
- 北京交通大学：http://mirror.bjtu.edu.cn/ \<教育网荐\>
- 兰州大学：http://mirror.lzu.edu.cn/ \<西北高校FTP搜索引擎\>
- 上海交通大学：http://ftp.sjtu.edu.cn/
- 清华大学：http://mirrors.tuna.tsinghua.edu.cn/
  - http://mirrors4.tuna.tsinghua.edu.cn/
- 中国科学技术大学：http://mirrors.ustc.edu.cn/ 
  - http://ipv6.ustc.edu.cn/ \<IPv6 only\>
- 东北大学：http://mirror.neu.edu.cn/
- 浙江大学：http://mirrors.zju.edu.cn/
- 东软信息学院：http://mirrors.neusoft.edu.cn/

### 游戏玩家发行版

*面向游戏玩家的八款最佳 Linux 发行版，本文由开源中国整理，[原文在这里](https://my.oschina.net/editorial-story/blog/888795)*。

- [SteamOS](http://store.steampowered.com/livingroom/SteamOS/) [官方文档](http://store.steampowered.com/steamos/buildyourown) [镜像下载](http://repo.steampowered.com/download/)
- [Ubuntu GamePack](https://ualinux.com/en/ubuntu-gamepack) [下载地址](https://ualinux.com/en/ubuntu-gamepack)
- [Fedora – Games Spin](https://www.oschina.net/p/fedora_linux) [下载地址](https://labs.fedoraproject.org/en/games/)
- [SparkyLinux – GameOver Edition](https://www.oschina.net/p/sparkylinux) [下载地址](https://sparkylinux.org/download/#special)
- [Lakka](http://www.lakka.tv/) [下载地址](http://www.lakka.tv/disclaimer/)
- [Game Drift Linux](http://gamedrift.org/) [下载地址](http://gamedrift.org/Download.html)
- [Solus](https://solus-project.com) [下载地址](https://solus-project.com/download/)
- [Manjaro Gaming Edition (mGAMe)](https://sourceforge.net/projects/mgame/) [下载地址](https://sourceforge.net/projects/mgame/)
