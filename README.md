- 👋 Hi, I’m @renjianqinhuan
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
renjianqinhuan/renjianqinhuan is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# 第一阶段

------





------

## 第一天（关于基本命令1）



------

## 第二天（关于基本命令2）



------

## 第三天 （关于基本命令3）



### 一、Linux操作：

#### 1、快捷键：

​	CTRL   +   U： 从光标处清空至行尾；

​	CTRL   +   L  ：清空屏幕；

​	CTRL   +    c：结束进程

​	reboot：重启 

​	poweroff ：     关机

​	CTR L   +   ：  放大屏幕字体

​	CTRL       SHIFT   -   ：  缩小字体

#### 2、操作命令：

**（1）、基本操作命令：**

​	[Linux 常用操作命令大全（最后更新时间：2022年1月）_linux常用命令_Engineer-Yao的博客-CSDN博客](https://blog.csdn.net/m0_46422300/article/details/104645072)

**（2）、特殊命令：**

​	**ifconfig:**   查看网卡信息；

​	**hostname:**  临时修改虚拟机名字；

​	**hostnamectl  set_hostname   :**修改名字；

​	**mount :** 让目录成为设备的访问点；

​	**umount：**卸载已挂载设备；

**（3）、对数据的操作:**

​	**cd  ~ root：**去往家目录

**ls相关操作：**

​	**ls  -ld :**   显示目录具体信息（本身属性）；

​	**ls  -d:**    显示目录本身属性；

​	**ls -lh :**    显示文件大小；（有单位）

​	**ls  -A:**显示所有信息（包含隐藏数据）；

​    **ls  -R：**递归显示（显示目录本身的内容）；

**通配符(*)：**

​	**ls  /root/a*:**表示以a开头的所有文件显示出来；

​	**注意：**如果是目录，则显示目录里面的内容；

​	**对虚拟机起一个别名：**alias   别名=‘hostname’;

​	**删除别名：**unalias  ;

​	**删除数据：**rm;

​	**文件移动：**mv（重命名）;

​	**拷贝文件 ：**cp(-r  复制目录时需要添加);

​	**grep：**过滤文件内容默认不支持通配符（^root：以root开头的行；bash$：以bash结尾的行）；

​	**^$：**表示空行；

​	**grep  -v  ^$  :**  过滤空行的内容；



------

## 第四天（文档，文件处理）



### 一、文件的归档及压缩

归档：将零散的数据归档起来，方便操作；

压缩：把数据用新的算法减少文件所需要的内存；

#### 1、归档压缩

【tar】

tar  + 【选项】    +       压缩包名字         +             被归档压缩的数据

```Linux
[root@tw /]# tar -zcf tianwei.tar.gz /etc/passwd  /boot/
tar: 从成员名中删除开头的“/”
tar: 从硬连接目标中删除开头的“/”
```

【高级用法】

tar  【选项】   压缩包名字    -C （指定路径）  /路径【空格】 文件名字；

只有文件没有路径。

```Linux
[root@tw /]# tar -zcf /tw1.tar.gz  -C /etc/ passwd /boot
tar: 从成员名中删除开头的“/”
tar: 从硬连接目标中删除开头的“/”
```

```Linux
[root@tw /]# tar -tf tw1.tar.gz 
passwd
boot/
boot/efi/
```

#### 2、tar工具选项

**-C：**指定释放位置；

**-c：**创建一个压缩包；

**-x：**释放包

**-f：**指定tar的名字；（必须放在所有选项最后）

**-Z,-j,-J：**（Z：gzip：-j：bzip2；-J：xz）

​	压缩速度最快的是：Z

​	压缩比例最高，速度最慢：-J；

​	平平常常：-j；

**-t：**检测查阅tar包内容；（tar  -tf ）

```Linux
[root@tw /]# tar -tf  /tianwei.tar.gz -C /tw
etc/passwd
boot/
boot/efi/
boot/efi/EFI/
boot/efi/EFI/rocky/
```

#### 3、文件备份与恢复

**（1）、解包**

​	tar   【选项】  /路径/压缩包名字      【选项】    释放的位置

​	tar   -xf    

```Linux
[root@tw tw]# tar -xf  /tianwei.tar.gz -C /tw
[root@tw tw]# cd /tw/
[root@tw tw]# ll
总用量 4
dr-xr-xr-x. 5 root root 4096 6月  30 11:39 boot
drwxr-xr-x. 2 root root   20 7月   4 10:17 etc
```

**（2）、【案例】**

**创建一个归档文件，名为/root/backup.tar,bz2**，**其中包含/usr/local目录中的内容**，**tar归档必须使用bzip2进行压缩。**

```Linux
[root@tw /]# tar -jcf /root/backup.tar.bz2  /usr/local/
tar: 从成员名中删除开头的“/”
[root@tw /]# tar -tf /root/backup.tar.bz2 
usr/local/
usr/local/bin/
usr/local/etc/
usr/local/games/
usr/local/include/
usr/local/lib/
```

### 二、重定向及管道

定义：重新定向命令的输出；将前面命令的输出，写在全新的文件；

#### 1、覆盖重定向

```Linux
[root@tw /]# head -2 /etc/passwd >/opt/a.txt
[root@tw /]# cat /opt/a.txt 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
```

删除原有的，创建一个新的；

#### 2、追加重定向

```Linux
[root@tw /]# hostname >> /opt/a.txt 
[root@tw /]# cat /opt/a.txt 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
tw
```

在原有基础上追加一个重定向；

echo  123456 >>  /opt/a.txt(追加123456到文件到a.txt)；

#### 3、echo的使用

```Linux
[root@tw /]# echo 123456 >> /opt/a.txt 
[root@tw /]# cat /opt/a.txt 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
tw
123456
```

#### 4、管道操作（|）

**作用：**将前面命令的输出，传递给后面命令，作为后面命令的参数；

**注意：**双参数以及以上的命令无法使用管道；

```Linux
[root@tw /]# head -5 /etc/passwd |tail -1          //显示前五行的最后一行（第五行）
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
[root@tw /]# head -5 /etc/passwd |tail -2          //前五行的最后两行（第四五行）
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

**显示8~12行的内容：**

```Linux
[root@tw /]# cat -n /etc/passwd | head -12 |tail -5
     8	halt:x:7:0:halt:/sbin:/sbin/halt
     9	mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
    10	operator:x:11:0:operator:/root:/sbin/nologin
    11	games:x:12:100:games:/usr/games:/sbin/nologin
    12	ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
```

**grep加管道用法：**

**【案例】：**

Linux中大多数配置文件内容，以#开头，过滤#，显示配置文件有效信息，除去空行；

```Linux
[root@tw /]# grep -v ^# /etc/login.defs |grep -v ^$ >/opt/b.txt
[root@tw /]# cat opt/b.txt 
MAIL_DIR	/var/spool/mail
UMASK		022
HOME_MODE	0700
PASS_MAX_DAYS	99999
PASS_MIN_DAYS	0
PASS_MIN_LEN	5
PASS_WARN_AGE	7
```

#### 4、wc命令

统计文件内容；

```Linux
[root@tw /]# wc /etc/passwd
  45  103 2501 /etc/passwd
```

管道与wc配合使用：



### 三、高级命令

#### 1、find基本使用

**格式：**find  【目录】  【查找类型】  【文件格式】

**功能：**无法查找文件内容，查询文件路径；

find执行原理：查找一个传递一个；

**d：**目录；

```linux
[root@tw /]# find /boot/  -type d
/boot/
/boot/efi
/boot/efi/EFI
/boot/efi/EFI/rocky
```

**f：**文件；

```linux
[root@tw /]# find /boot/  -type f
/boot/grub2/device.map
/boot/grub2/i386-pc/gcry_dsa.mod
/boot/grub2/i386-pc/acpi.mod
/boot/grub2/i386-pc/gcry_idea.mod
/boot/grub2/i386-pc/adler32.mod
```

**l：**快捷方式；

```linux
[root@tw /]# find /sbin -type l
/sbin
```

**【注意】：**使用-name时若用到通配符，要用引号将查找内容括起来；

**（1）、-type：**查找类型；

**（2）、-name：**查找名字；

> *两个条件之间加入-o，表示或者，两个条件满足其中一个；*

**（3）、-iname：**忽略大小写；

**（4）、统计个数：**用管道符与wc配合使用；

**（5）、-size：**查找大于或者小于的文件；（单位：k  M  G）

​		 -size  +10m：大于 10；

   	  -size  -10m：小于10；

```LINUX
[root@tw etc]# find /etc  -size  +5M
/etc/selinux/targeted/policy/policy.31
/etc/udev/hwdb.bin
```

**（6）、-user：**数据的所有者；

find  /路径  -user  用户名；（表示该用户创建哎u你的所有数据）

```Linux
[root@tw etc]# find /home -user abc
/home/abc
/home/abc/.mozilla
/home/abc/.mozilla/extensions
/home/abc/.mozilla/plugins
/home/abc/.bash_logout
/home/abc/.bash_profile
/home/abc/.bashrc
```

**（7）、-mtime：**按修改时间进行查找；

-mtime    +90   ：90天之前的数据；

+mtime   -10    ：最近10天的数据；

```Linux
[root@tw etc]# find /var/log  -mtime +90
/var/log/samba/old
/var/log/glusterfs
/var/log/chrony
/var/log/speech-dispatcher
```

#### 2、find的高级使用

处理查找到的内容：-exec

```Linux
[root@tw /]# find /boot -size +10M -exec cp {} /opt \;    “\;”：表示额外操作的结束；
[root@tw /]# cd /opt
[root@tw opt]# ls
a.txt
b.txt
c.txt
initramfs-0-rescue-54cdfccf6038470fb0d096dac6bd6a0c.img
initramfs-4.18.0-372.9.1.el8.x86_64.img
initramfs-4.18.0-372.9.1.el8.x86_64kdump.img
```

将大于10M 的文件拷贝到opt目录下。

**【案例】**

利用find查找，数据所有者为student，并且必须是文件，把他们拷贝到/root/findfiles文件夹中；

```Linux
[root@tw opt]# useradd student
[root@tw opt]# mkdir /root/findfiles
[root@tw opt]# find / -user student -type f -exec cp {} /root/findfiles \;
find: ‘/proc/14383/task/14383/fdinfo/7’: 没有那个文件或目录
find: ‘/proc/14383/fdinfo/8’: 没有那个文件或目录
[root@tw opt]# ls -a /root/findfiles/
.  ..  .bash_logout  .bash_profile  .bashrc  student
```

#### 3、vim（续）

**（1）、命令模式：**

i/o：进入插入模式；

G：跳到文件最后一行；

gg：返回到第一行；

数字+gg：跳转到第几行；

home/end：home跳转到行首；end跳转到行尾；

dd：删除光标所在行；

delete：删除光标所在字符；

D：删除光标之后所有的字符；

u：撤销命令；

数字+dd：删除光标后面的几行；

yy：复制光标所在行；

数字+yy：复制光标后几行；

p：粘贴；

/关键字：全文搜索关键字；

n：跳转；

U：撤销当前行所有的操作；

zz：保存并退出；

**（2）、插入模式：**

**（3）、末行模式：**

r  /路径/文件名  ：读入其他文件的内容；

set  nu/nonu ：显示行号或者关闭行号；

set   ai/noai：启动自动缩进或者关闭自动缩进；

永久设置：行号和自动缩进

```
vim  /root/.vimrc

set nu

set ai
```

vimdisff：同时更改多个文件；命令模式下CTRL +w切换；

末行模式wqa全部保存退出；



------

## 第五天（软件包相关操作）

### 一、rpm软件包管理

扩展名为.rpm，叫rpm软件包。

#### 1、rpm 基本用法命令

**（1）rpm -qa ：**当前 系统中所有已安装的软件；

```Linux
[root@localhost /]# rpm -qa
libreport-cli-2.9.5-15.el8.rocky.6.3.x86_64
libnftnl-1.1.5-5.el8.x86_64
perl-DBI-1.641-4.module+el8.6.0+891+677074cb.x86_64
gnutls-3.6.16-4.el8.x86_64
biosdevname-0.7.3-2.el8.x86_64
liberation-fonts-common-2.00.3-7.el8.noarc
```

**（2）rpm -q ：**查看是否安装；

```Linux
[root@localhost /]# rpm -q httpd
未安装软件包 httpd 
```

**（3）rpm -qpi ：**查询软件包信息；

```Linux
[root@localhost /]# rpm -qpi /mnt/AppStream/Packages/v/vsftpd-3.0.3-35.el8.x86_64.rpm 
警告：/mnt/AppStream/Packages/v/vsftpd-3.0.3-35.el8.x86_64.rpm: 头V4 RSA/SHA256 Signature, 密钥 ID 6d745a60: NOKEY
Name        : vsftpd
Version     : 3.0.3
Release     : 35.el8
Architecture: x86_64
Install Date: (not installed)
```

 输入--import 可以导入红帽签名名信息；

```Linux
[root@localhost /]# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-rockyofficial 
[root@localhost /]# rpm -qpi /mnt/AppStream/Packages/v/vsftpd-3.0.3-35.el8.x86_64.rpm 
Name        : vsftpd
Version     : 3.0.3
Release     : 35.el8
Architecture: x86_64
Install Date: (not installed)
Group       : System Environment/Daemons
```

**（4）rpm -qpl ：**查询软件包；

```Linux
[root@localhost /]# rpm -qpl /mnt/AppStream/Packages/v/vsftpd-3.0.3-35.el8.x86_64.rpm 
警告：/mnt/AppStream/Packages/v/vsftpd-3.0.3-35.el8.x86_64.rpm: 头V4 RSA/SHA256 Signature, 密钥 ID 6d745a60: NOKEY
/etc/logrotate.d/vsftpd
/etc/pam.d/vsftpd
/etc/vsftpd
/etc/vsftpd/ftpusers
/etc/vsftpd/user_list
```

#### 2、rpm ivh

"rpm ivh"是一种使用RPM包管理器的命令行选项，用于安装RPM软件包并显示安装过程中的详细信息。这个命令的完整格式如下：

```linux
rpm ivh <package.rpm>
```

其中，`<package.rpm>` 是要安装的RPM软件包的文件名。通过执行该命令，系统将会安装指定的RPM包，并在安装过程中显示详细信息，包括安装的文件列表、依赖关系等。

#### 3、chatai搜索基本命令

RPM（RPM Package Manager）是用于在Linux系统上管理软件包的命令行工具。以下是一些常用的RPM命令：

（1）、安装软件包：

```
rpm -i <package-file.rpm>                 // 安装指定的RPM软件包
```

（2）、查询软件包信息：

```
rpm -q <package-name>                     // 查询软件包是否已安装
rpm -qi <package-name>                    // 显示软件包的详细信息
rpm -ql <package-name>                    // 列出软件包中的文件列表
rpm -qf <file-path>                       // 查询指定文件所属的软件包
```

（3）、更新软件包：

```
rpm -U <package-file.rpm>                 // 更新已安装的RPM软件包
```

（4）、升级软件包：

```
rpm -F <package-file.rpm>                 // 升级已安装的RPM软件包（仅升级比已安装的软件包版本新的软件包）
```

（5）、删除软件包：

```
rpm -e <package-name>                     // 删除指定的RPM软件包
```

（6）、列出已安装的软件包：

```
rpm -qa                                   // 列出所有已安装的RPM软件包
```

（7）、查询软件包依赖关系：

```
rpm -qR <package-name>                    // 查询软件包的运行时依赖关系
rpm -qpR <package-file.rpm>               // 查询RPM软件包的运行时依赖关系
```

这些命令提供了基本的RPM软件包管理功能，并且还有更多高级选项可供使用。你可以通过运行`man rpm`命令查看完整的RPM命令手册。

### 二、yum软件包仓库

yum 命令的使用，能自定解决依赖关系安装软件；

####  1、构建软件仓库

软件包 （路径：/mnt/AppStream） +     仓库清单 （）

 配置文件仓库： /etc/yum.repos.d/*.repo      /mnt/BaseOS（必须保证文件全部正确）；

```Linux
[root@localhost yum.repos.d]# cat tw.repo 
[tw]
name=tw
baseurl=file://mnt/AppStream
enabled=1                        #  是否启用  ，1表示启用
gpgcheck=0                       #  是否检查测软件包红帽签名
```

使用yum  repoinfo查看仓库信息：

```Linux
[root@localhost yum.repos.d]# yum repoinfo
tw                          4.2 MB/s | 4.3 kB     00:00    
tw1                          83 MB/s | 2.6 MB     00:00    
仓库ID            : tw
仓库名称          : tw
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L,
                      : R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月16日 星期一 05时01分50秒
Repo-pkgs          : 6,549
Repo-available-pkgs: 5,339
Repo-size          : 8.3 G
Repo-baseurl       : file:///mnt/AppStream
Repo-expire        : 172,800 秒 （最近 2023年07月05日 星期三  : 14时30分32秒）
```

#### 2、yum安装软件

**（1）、安装httpd：（-y：不 询问直接安装）**

```Linux
[root@localhost /]# yum -y install httpd
上次元数据过期检查：0:10:24 前，执行于 2023年07月05日 星期三 14时34分03秒。
依赖关系解决。
============================================================
 软件包            架构   版本                    仓库     大小
============================================================
安装:
 httpd             x86_64 2.4.37-47.module+el8.6.0+823+f143cee1.1
安装  9 软件包
总计：2.0 M
安装大小：5.4 M
下载软件包：
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
已安装:
  apr-1.6.3-12.el8.x86_64                                   
  apr-util-1.6.1-6.el8.1.x86_64                             
  apr-util-bdb-1.6.1-6.el8.1.x86_64                         
  apr-util-openssl-1.6.1-6.el8.1.x86_64                     
  httpd-2.4.37-47.module+el8.6.0+823+f143cee1.1.x86_64      
  httpd-filesystem-2.4.37-47.module+el8.6.0+823+f143cee1.1.noarch
  httpd-tools-2.4.37-47.module+el8.6.0+823+f143cee1.1.x86_64
  mod_http2-1.15.7-5.module+el8.6.0+823+f143cee1.x86_64     
  rocky-logos-httpd-85.0-4.el8.noarch                       

完毕！
```

**（2）、卸载软件**

```Linux
[root@localhost /]# yum remove gcc
依赖关系解决。
============================================================
 软件包           架构    版本                  仓库   大小
============================================================
移除:
 gcc              x86_64  8.5.0-10.el8          @tw    59 M
清除未被使用的依赖关系:
 cpp              x86_64  8.5.0-10.el8          @tw    28 M
 glibc-devel      x86_64  2.28-189.1.el8        @tw1  234 k
 glibc-headers    x86_64  2.28-189.1.el8        @tw1  1.9 M
事务概要
============================================================
移除  7 软件包
将会释放空间：98 M
确定吗？[y/N]： y
运行事务
  准备中  :                                             1/1 
  运行脚本: gcc-8.5.0-10.el8.x86_64                     1/7 
  删除    : gcc-8.5.0-10.el8.x86_64                     1/7 
  运行脚本: glibc-devel-2.28-189.1.el8.x86_64           2/7 
  删除    : glibc-devel-2.28-189.1.el8.x86_64           2/7 
  删除    : libxcrypt-devel-4.1.1-6.el8.x86_64          3/7 
  删除    : glibc-headers-2.28-189.1.el8.x86_64         4/7 
已移除:
  cpp-8.5.0-10.el8.x86_64                                   
  gcc-8.5.0-10.el8.x86_64                                   
  glibc-devel-2.28-189.1.el8.x86_64                                                
完毕！
```

### 三、命令的补充

#### 1、yum特殊操作命令

（1）、yum list 列出已安装的软件包

```Linux
[root@localhost /]# yum list
上次元数据过期检查：0:20:59 前，执行于 2023年07月05日 星期三 14时56分46秒。
已安装的软件包
GConf2.x86_64                   3.2.6-22.el8      @AppStream
ModemManager.x86_64             1.18.2-1.el8      @anaconda 
ModemManager-glib.x86_64        1.18.2-1.el8      @anaconda 
NetworkManager.x86_64           1:1.36.0-4.el8    @anaconda 
NetworkManager-adsl.x86_64      1:1.36.0-4.el8    @anaconda 
```

（2）、yum search 查找安装包

```Linux
[root@localhost /]# yum search ftp
上次元数据过期检查：0:31:11 前，执行于 2023年07月05日 星期三 14时56分46秒。
================== 名称 和 概况 匹配：ftp ==================
ftp.x86_64 : The standard UNIX FTP (File Transfer Protocol)    : client
lftp-scripts.noarch : Scripts for lftp
python3-requests-ftp.noarch : FTP transport adapter for  : python3-requests
```

（3）、yum provides  查看命令产生的包，然后通过yum下载安装包；

```Linux
[root@localhost /]# yum provides cd 
上次元数据过期检查：0:30:03 前，执行于 2023年07月05日 星期三 14时56分46秒。
bash-4.4.20-3.el8.x86_64 : The GNU Bourne Again shell
仓库        ：@System
匹配来源：
文件名    ：/usr/bin/cd
bash-4.4.20-3.el8.x86_64 : The GNU Bourne Again shell
仓库        ：tw1
匹配来源：
文件名    ：/usr/bin/cd
```

（4）、yum update <package_name>  升级特定的软件包（yum update 升级所有可升级的包）

#### 2、清理缓存

（1）、yum clean packages           // 清除已下载的软件包缓存 



（2）、yum clean metadata           // 清除软件包元数据 

（3）、yum clean all                // 清除所有缓存（包括软件包和元数据）

#### 3、升级软件包

（1）、yum upgrade <package-name>  // 升级指定软件包

#### 4、获取命令的帮助信息

（1）、--help列出较为常用的

（2）、man（man  yum  最权威的帮助命令）

#### 5、关于历史命令的操作

在Linux中，你可以使用如下命令来管理和操作历史命令：

（1）、`history`：显示执行过的命令历史列表，包括命令编号和相应的命令内容。

（2）、`!!`：执行上一条命令。

（3）、`!n`：执行第n条命令，其中n为命令编号。

（4）`!string`：执行最近的以string开头的命令。比如`!ls`将执行最近的以"ls"开始的命令。

（5）`!$`：引用上一条命令的最后一个参数。

（6）`!-n`：引用倒数第n条命令的第一个参数。

（7）`Ctrl+R`：在命令提示符下按下Ctrl+R，然后输入关键字，将搜索并执行最近的匹配命令。

（8）`history -c`：清除命令历史记录。

这些命令和快捷键可以帮助你在Linux系统中更方便地管理和操作历史命令。

#### 6、查看修改时间

（1）date

```
[root@localhost /]# date
2023年 07月 05日 星期三 16:33:07 CST
```

（2）date  -s

```
[root@localhost /]# date -s '2000-7-5 16:37:00'
2000年 07月 05日 星期三 16:37:00 CST
```

在Linux中，`date` 是一个用于显示和设置系统日期和时间的命令。以下是一些常用的 `date` 命令用法示例：

（3）显示当前日期和时间：

```
date
```

（4）显示当前日期：

```
date +"%Y-%m-%d"
```

（5）显示当前时间：

```
date +"%H:%M:%S"
```

（6）显示当前星期几：

```
date +"%A"
```

（7）显示完整的日期和时间信息：

```
date +"%Y-%m-%d %H:%M:%S"
```

（8）自定义日期和时间格式，例如将日期和时间输出为 "年-月-日 时:分:秒" 格式：

```
date +"%Y-%m-%d %T"
```

（9）设置系统日期和时间：

```
sudo date -s "YYYY-MM-DD HH:MM:SS"
```

注意：上述命令中的"YYYY-MM-DD"是指定的日期，"HH:MM:SS"是指定的时间。

（10）通过指定不同的时区显示时间：

```
TZ="Asia/Shanghai" date
```

将使用 "Asia/Shanghai" 时区显示时间。

这些是常见的 `date` 命令用法示例。`date` 命令还有更多选项和用法，你可以通过 `man date` 命令查看完整的文档以获取详细信息。

#### 7、zip压缩释放归档文件

（1）zip压缩

```
[root@localhost /]# zip -r /opt/abc.zip /etc/passwd /home
  adding: etc/passwd (deflated 61%)
  adding: home/ (stored 0%)
  adding: home/tw/ (stored 0%)
  adding: home/tw/.mozilla/ (stored 0%)
  adding: home/tw/.mozilla/extensions/ (stored 0%)
  adding: home/tw/.mozilla/plugins/ (stored 0%)
  adding: home/tw/.bash_logout (stored 0%)
  adding: home/tw/.bash_profile (deflated 20%)
  adding: home/tw/.bashrc (deflated 35%)
```

（2）释放

```
[root@localhost opt]# unzip -l /opt/abc.zip 
Archive:  /opt/abc.zip
  Length      Date    Time    Name
```

     2596  07-05-2023 15:09   etc/passwd
        0  06-30-2023 11:36   home/
        0  06-30-2023 11:36   home/tw/
        0  06-30-2023 11:25   home/tw/.mozilla/
        0  04-24-2022 07:44   home/tw/.mozilla/extensions/
        0  04-24-2022 07:44   home/tw/.mozilla/plugins/
       18  04-12-2022 15:03   home/tw/.bash_logout
      141  04-12-2022 15:03   home/tw/.bash_profile
      376  04-12-2022 15:03   home/tw/.bashrc
     3131                     9 files

#### 8、制作快捷方式

（1）、ln   -s  /路径    /快捷方式名字 ：针对目录/文件做快捷方式（软链接）；ln  /路径    /快捷方式的名字（硬链接）；

（2）、ls   -l   查看快捷方式详细属性；

**软链接：**原数据消失，快捷方式就不可以使用，这种方式叫做软链接； 

**硬链接：**原数据消失，快捷方式还可以使用；不能跨分区，只针对文件；



------

## 第六天（关于用户身份）



### 一、用户管理

**总述：**基于账户身份对资源进行访问控制；识别方式：uid，gid；

#### 1、基于账号的访问控制

（1）、超级用户（uid 0）

（2）、系统用户(uid 1-999)

（3）、普通用户(uid  1000以上)

（4）、组账号（gid：由0开始，最大60000唯一标识）

​	基本组（私有组）：一个用户必须有基本组，基本组只能有一个，一般与用户同名；

​	附加组（从属组）：一个用户可以有多个，也可以没有；

**创建用户：**

```Linux
[root@localhost ~]# head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
[root@localhost ~]# useradd tianwei  
[root@localhost ~]# id tianwei 
uid=1001(tianwei) gid=1001(tianwei) 组=1001(tianwei)
[root@localhost ~]# ls /home/
tianwei  tw
```

**在/etc/passwd文件查找：**

```Linux
[root@localhost ~]# grep tianwei /etc/passwd
tianwei:x:1001:1001::/home/tianwei:/bin/bash
```

#### 2、useradd创建用户选项

（1）指定uid:   -u

```Linux
[root@localhost ~]# useradd   -u  1314 tw1
[root@localhost ~]# id tw1
uid=1314(tw1) gid=1314(tw1) 组=1314(tw1)
[root@localhost ~]# grep tw1 /etc/passwd
tw1:x:1314:1314::/home/tw1:/bin/bash
```

（2）指定用户家目录：-d

​	注意：不能自己提前创建目录；无法创建多层目录；

```Linux
[root@localhost ~]# useradd -d /opt/home1 tw2
[root@localhost ~]# grep tw2 /etc/passwd
tw2:x:1315:1315::/opt/home1:/bin/bash
[root@localhost ~]# ls /opt/
home1
```

（3）指定组：-G  （使用-g可以改变用户的基本组）

```Linux
[root@localhost ~]# groupadd stud1
[root@localhost ~]# groupadd stud2
[root@localhost ~]# useradd -G stud1 tw3
[root@localhost ~]# useradd -G stud1,stud2 tw4
[root@localhost ~]# id tw3
uid=1316(tw3) gid=1318(tw3) 组=1318(tw3),1316(stud1)
[root@localhost ~]# id tw4
uid=1317(tw4) gid=1319(tw4) 组=1319(tw4),1316(stud1),1317(stud2)
```

（4）指定登录系统的解释器：-s  默认/bin/bash； /sbin/nologin：禁止用户登录操作系统；

```Linux
[root@localhost ~]# useradd -s /sbin/nologin tw5
[root@localhost ~]# grep tw5 /etc/passwd
tw5:x:1318:1320::/home/tw5:/sbin/nologin
[root@localhost ~]# passwd tw5
```

  <img src="C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230706104656103.png" alt="image-20230706104656103" style="zoom:40%;" />

（5）总结

在Linux系统执行`useradd`命令时，会完成以下操作：

A、创建用户账户：

- 在`/etc/passwd`文件中添加一个新的用户记录。
- 在`/etc/shadow`文件中为用户设置初始密码（如果指定了密码）。
- 分配一个唯一的用户ID（UID）给新用户。
- 分配一个初始的组ID（GID），通常与用户名相同的组将被创建。
- 创建一个与用户名相同的主目录（如果指定了`-m`选项）。
- 为用户设置默认的登录shell（如果指定了`-s`选项）。

B、设置用户账户的其它属性（如果指定了相应选项）：

- 指定用户所属的附加组（使用`-G`选项）。
- 指定用户的家目录路径（使用`-d`选项）。
- 指定用户的邮件地址（使用`-m`选项）。
- 指定用户的登录shell（使用`-s`选项）。

请注意，执行`useradd`命令时可能会涉及到系统的其他配置文件和操作。用户账户的创建涉及许多系统级和文件层面的操作，以确保用户的正确创建和配置。

#### 3、usermod用法

（1）修改名字：-l

```linux
[root@localhost /]# usermod -l haha tw5
[root@localhost /]# id haha
uid=1318(haha) gid=1320(tw5) 组=1320(tw5)
```

（2）修改uid：-u

```linux
[root@localhost /]# usermod -u 1900 haha 
[root@localhost /]# id haha
uid=1900(haha) gid=1320(tw5) 组=1320(tw5)
```

（3）修改登录解释器：-s

```linux 
@localhost /]# usermod -s /bin/bash haha 
[root@localhost /]# grep haha /etc/passwd
haha:x:1900:1320::/home/tw5:/bin/bash
```

（4）修改用户家目录

注意：本次修改并不会重新创建家目录；

```Linux
[root@localhost /]# useradd tw6
[root@localhost /]# usermod -md /mnt/abc16 tw6
[root@localhost /]# grep tw6 /etc/passwd
tw6:x:1901:1901::/mnt/abc16:/bin/bash
```

（5）修改用户的附加组：-G

```Linux
[root@localhost /]# id tw4
uid=1317(tw4) gid=1319(tw4) 组=1319(tw4),1316(stud1),1317(stud2)
[root@localhost /]# groupadd stud3
[root@localhost /]# usermod -G stud1,stud3 tw4
[root@localhost /]# id tw4
uid=1317(tw4) gid=1319(tw4) 组=1319(tw4),1316(stud1),1902(stud3)
```

passwd命令支持非交互式设置密码；

（5）删除目录：userdel   -r

连同家目录一起删除

#### 4、配置文件介绍

【**.bashrc**】

（1）定义永久的别名

在家目录下修改.bashrc里面的内容，完成定义。

注意在家文件写的文件优先级更高；

------

#### 5、【总结】

用户管理是在Linux系统中管理用户账户的过程。以下是一些常见的用户管理操作：

（1）创建用户账户：

```
sudo useradd <username>
```

通过使用`useradd`命令并指定`<username>`创建一个新的用户账户。可以使用额外的选项来指定用户的参数，例如用户组、主目录等。

（2）删除用户账户：

```
sudo userdel <username>
```

使用`userdel`命令并指定`<username>`来删除一个现有的用户账户。可以使用额外的选项来控制删除操作的行为，例如是否删除用户的主目录。

（3）修改用户账户：

```
sudo usermod <options> <username>
```

使用`usermod`命令并指定`<username>`以及要修改的选项来修改现有的用户账户。可以使用各种选项来更改用户的用户名、用户组、主目录、默认shell等。

（4）用户密码管理：

```
passwd <username>
```

使用`passwd`命令并指定`<username>`来更改用户账户的密码。在执行命令后，您将被提示输入新的密码。管理员可以使用`sudo`命令与`passwd`结合使用来更改其他用户账户的密码。

（5）列出用户账户：

```
sudo cat /etc/passwd
```

使用`cat`命令和`/etc/passwd`文件来列出系统中的所有用户账户信息。

（6）切换用户账户：

```
su <username>
```

使用`su`命令并指定`<username>`来切换到其他用户账户。在切换后，您将被要求输入目标用户的密码才能成功切换。

（7）查看当前登录的用户账户信息：

```
whoami
```

使用`whoami`命令来查看当前登录的用户账户。

请注意，上述命令需要管理员权限（使用`sudo`）来执行某些操作。在进行用户管理操作时，务必小心谨慎，并确保了解操作的影响。

### 二、组账号管理

#### 1、gpasswd操作

（1）重置用户组信息（gpasswd -M）

```Linux
[root@localhost /]# grep stud1 /etc/group
stud1:x:1316:kenji
[root@localhost /]# gpasswd -M nb,kaka stud1
[root@localhost /]# grep stud1 /etc/group
stud1:x:1316:nb,kaka
```

会将原来的用户组信息删除，加入新的组信息；

（2）将用户加入到组：gpasswd  -a 

```llinux
[root@localhost /]# gpasswd -a kenji stud1
正在将用户“kenji”加入到“stud1”组中
root@localhost /]# grep stud1 /etc/group
stud1:x:1316:kenji
```

#### 2、组操作

（1）设置组管理员（-A）

```
[root@localhost /]# gpasswd -A nb stud1
[root@localhost /]# su -nb
su: 不适用的选项 -- n
Try 'su --help' for more information.
[root@localhost /]# su - nb
b@localhost ~]$ gpasswd -a kaka stud1
正在将用户“kaka”加入到“stud1”组中
```

（2）组管理信息配置文件【/etc/gshadow】

```
[root@localhost /]# grep stud1 /etc/gshadow
stud1:!:nb:nb,kaka
```

**注意：**基本组无法被删除；

#### 3、【总结】：

在Linux中，您可以使用以下命令来执行创建、删除和修改用户和组的操作：

（1）创建用户：

```
sudo useradd <username>
```

这会创建一个新的用户，并使用指定的用户名(`<username>`)。

可选参数：

- `-m`：在/home目录下为用户创建用户目录。
- `-s <shell>`：指定用户的默认shell。
- `-G <group>`：将用户添加到附加组(`<group>`)。

（2）删除用户：

```
sudo userdel <username>
```

这会删除指定的用户(`<username>`)。

可选参数：

- `-r`：同时删除用户的用户目录。

（3）修改用户：

```
sudo usermod <options> <username>
```

这会修改指定用户(`<username>`)的属性。

常用参数：

- `-l <newusername>`：更改用户名。
- `-s <shell>`：更改用户的默认shell。
- `-G <group>`：更改用户的附加组。

（4）创建组：

```
sudo groupadd <groupname>
```

这会创建一个新的用户组，并使用指定的组名(`<groupname>`)。

（5）删除组：

```
sudo groupdel <groupname>
```

这会删除指定的用户组(`<groupname>`)。

（6）修改组：

```
sudo groupmod <options> <groupname>
```

这会修改指定用户组(`<groupname>`)的属性。

常用参数：

- `-n <newgroupname>`：更改组名。

请注意，上述命令需要管理员权限（使用sudo）。在执行任何用户或组相关的操作时，确保理解其影响并小心操作。

### 三、计划任务

#### 1、cron任务概述

（1）用途：按照设置时间间隔为用户反复执行某一项固定的系统任务；

（2）系统服务：crond；默认运行

（2）日志文件：/var/log/cron；

```
//文件包
[root@localhost /]# tail /var/log/cron 
Jul  6 11:01:01 localhost run-parts[6521]: (/etc/cron.hourly) finished 0anacron
Jul  6 14:01:01 localhost CROND[7265]: (root) CMD (run-parts /etc/cron.hourly)
```

```
//计划任务包
[root@localhost /]# rpm -qa |grep cron
crontabs-1.11-17.20190603git.el8.noarch
cronie-anacron-1.5.2-6.el8.x86_64
cronie-1.5.2-6.el8.x86_64
```

#### 2、管理计划任务策略

分   时    日     月    周

【每分钟记录当前的系统时间】

```
[root@localhost /]# date >> /opt/time.txt
[root@localhost /]# cat /opt/time.txt 
2023年 07月 06日 星期四 17:18:23 CST
[root@localhost /]# crontab -e
no crontab for root - using an empty one
crontab: installing new crontab
[root@localhost /]# crontab -l
*	*	*	*	* 	date >> /opt/time.txt
50  20	*   *   *	poweroff
```

#### 3、如何编写crontab任务记录

编写crontab任务记录相当简单。下面是编写crontab任务记录的步骤：

（1）打开终端或命令行界面。

（2）输入命令 `crontab -e` 来编辑当前用户的crontab文件。

（3）在打开的编辑器中，每一行代表一个crontab任务记录。每行的格式是由分、时、日、月、周几和要执行的命令组成。

例如，要在每天的午夜执行一个任务，可以写成：

```
0 0 * * * command
```

这表示在每天的0时0分执行命令。

（4）如果只想要记录一个任务的输出而不关心它的执行结果，可以将输出重定向到一个文件。例如：

```
0 0 * * * command >> /path/to/logfile.log
```

这将把命令的输出追加到 `logfile.log` 文件中。

（5）编写完crontab任务记录后，保存并关闭文件。编辑器会提示保存修改并退出。

（6）crontab会在下一次计划执行时间达到时开始执行任务。你可以使用 `crontab -l` 命令来查看当前用户的crontab任务记录。

注意事项：

- 在编辑crontab文件时，确保按照正确的格式编写任务记录。如果格式错误，任务记录将不会被执行。
- 可以使用 `*` 通配符表示任意值。例如，使用 `*` 表示每分钟执行。
- 如果需要执行的命令过于复杂或需要特定的环境设置，请将命令写入一个脚本文件，然后在crontab任务记录中调用该脚本。





------

## 第七天（关于权限问题）



### 一、基本权限和归属、附加权限

#### 1、权限和归属概述

（1）访问权限

​	读取：允许查看文件；

​	写入：允许修改文件；

​	可执行：允许运行和切换；

（2）归属关系

​	所有者：拥有此文件/目录的用户；

​	所属组：拥有此文件/目录的组；

​	其他用户：除所有者，所属者以外的用户

```Linux
root@localhost ~]# ls -l /etc/passwd
-rw-r--r--. 1 root root 2501 6月  30 11:36 /etc/passwd
```

#### 2、权限控制

**（1）修改数据权限：chmod**

```Linux
[root@localhost /]# mkdir /nsd01
[root@localhost /]# ls -ld /nsd01/
drwxr-xr-x. 2 root root 6 7月   7 10:08 /nsd01/
[root@localhost /]# chmod u-w /nsd01
[root@localhost /]# ls -ld /nsd01/
dr-xr-xr-x. 2 root root 6 7月   7 10:08 /nsd01/
[root@localhost /]# chmod u+w /nsd01
[root@localhost /]# ls -ld /nsd01/
drwxr-xr-x. 2 root root 6 7月   7 10:08 /nsd01/
```

**（2）递归设置是目录下的所有权限**

```Linux
[root@localhost /]# mkdir -p /opt/yy/uu/ii
[root@localhost /]# chmod -R o=---  /opt/yy
[root@localhost /]# ls -ld /opt/yy
drwxr-x---. 3 root root 16 7月   7 10:23 /opt/yy
[root@localhost /]# ls -ld /opt/yy/uu/
drwxr-x---. 3 root root 16 7月   7 10:23 /opt/yy/uu/
[root@localhost /]# ls -ld /opt/yy/uu/ii
drwxr-x---. 2 root root 6 7月   7 10:23 /opt/yy/uu/ii
```

r=4  w=2  x=1

**（3）案例：设置基本权限**
	1)、 以 root 身份新建/dir 目录，在此目录下新建 readme.txt 文件

```
[root@localhost ~]# mkdir/dir
[root@localhost ~]# echo 123456 > /dir/readme.txt
[root@localhost ~]# cat /dir/readme.txt
```

​	2)、使用户 zhangsan 能够修改readme.txt文件内容

```
[root@localhost ~]# chmod o+w /dir/readme.txt
```

​	3)、使用户 zhangsan不可以修改readme.txt 文件内容

```
[root@localhost~]#chmod o-w /dir/readme.txt
```

​	4)、使用户 zhangsan 能够在此目录下创建/删除子目录

```
[root@localhost~]# chmod o+W /dir/
```

​	5)、调整此目录的权限，使任何用户都不能进入，然后测试用户 zhangsan是否还能查看readme.txt 内容(测试结果是不能，对父目录没有权限)

```
[root@localhost~]# chmod a-x /dir/

```

​	6) 、为此目录及其下所有文档设置权限 TWxr-x---

```
[root@localhost~]# chmod -R U=rwx,g=rx,0=--- /dir
```

#### 3、归属控制

（1）修改所属组的操作

```
[root@localhost /]# mkdir /nsd15
[root@localhost /]# Is-ld /nsd15
drwxr-xr-x. 2 root root 6 7月   7 11:34 /nsd15
[root@localhost /]# groupadd tmooc   #创建组tmooc
[root@localhost /]# useradd lisi #创建用户 lisi
[root@localhost /]# chown lisi:tmooc /nsd15 #修改所有者与所属组
[root@localhost /]#Is -ld/nsd15
drwxr-xr-x. 2 lisi tmooc 6 7月   7 11:34 /nsd15/
[root@localhost /]#chown zhangsan /nsd15 #仅修改所有者
[root@localhost /]#-ld /nsd15
drwxr-xr-x. 2 zhangsan tmooc 6 7月   7 11:34 /nsd15/
[root@localhost /]# chown :root /nsd15 #仅修改所属组
[root@localhost /]# Is -ld /nsd15
drwxr-xr-x. 2 zhangsan root 6 7月   7 11:34 /nsd15/
```

（2）更改所有者：

- `chown`命令：用于更改文件和目录的所有者。例如，`chown user1 file.txt`将文件"file.txt"的所有者更改为"user1"。

（3）更改所属组：

- `chown`命令：用于更改文件和目录的所属组。例如，`chown :group1 file.txt`将文件"file.txt"的所属组更改为"group1"。
- `chgrp`命令：用于更改文件和目录的所属组。例如，`chgrp group1 file.txt`将文件"file.txt"的所属组更改为"group1"。

（4）添加辅助组：

- `usermod`命令：用于将用户添加到或从辅助组中。例如，`usermod -aG group1 user1`将用户"user1"添加到"group1"辅助组。

（5）查看文件和目录的归属信息：

- `ls -l`命令：以长格式显示文件和目录的详细信息，包括所有者和所属组。

正确的归属控制是保护文件和目录安全的重要步骤。通过为文件和目录设置适当的所有者和所属组，以及限制访问和修改权限，可以确保只有授权的用户和组能够访问和操作文件。定期检查和更新归属信息也是保持系统安全性的重要措施之一。

### 二、acl控制

#### 1、acl策略

ACL（Access Control Lists）是一种高级的权限控制机制，它允许对文件和目录的权限进行更详细的定义。通过ACL，可以对单个用户或组设置特定的权限，以覆盖默认的权限设置。

在Linux系统中，使用`setfacl`命令可以设置ACL策略。下面是一些常见的ACL策略示例：

（1）添加ACL策略：

- 设置用户的读取和写入权限：`setfacl -m u:user1:rw file.txt`
- 设置组的读取和执行权限：`setfacl -m g:group1:r-x directory`
- 设置特定用户和组的权限：`setfacl -m u:user1:rwx,g:group1:rx file.txt`

（2）修改ACL策略：

- 修改用户的权限：`setfacl -m u:user1:rx file.txt`
- 修改组的权限：`setfacl -m g:group1:w file.txt`
- 修改特定用户和组的权限：`setfacl -m u:user1:w,g:group1:r file.txt`

（3）删除ACL策略：

- 删除指定用户的ACL策略：`setfacl -x u:user1 file.txt`
- 删除指定组的ACL策略：`setfacl -x g:group1 file.txt`
- 删除全部ACL策略：`setfacl -b file.txt`

（4）查看ACL策略：

- 查看文件的ACL策略：`getfacl file.txt`
- 查看目录的ACL策略：`getfacl directory`

请注意，为了使用ACL，文件系统需要以支持ACL的方式挂载（通常需要在`/etc/fstab`中进行配置）。

使用ACL策略可以更精确地控制用户和组对文件和目录的访问权限。通过ACL，您可以针对具体用户或组设定需要的权限，并实现更细粒度的权限控制。但请谨慎使用ACL，确保正确设置ACL策略，以免导致混乱或安全漏洞。

#### 2、单独赋予一个人权限

（1）黑名单的使用

```
[root@localhost ~]# mkdir /public
[root@localhost ~]# chmod 777 /public
[root@localhost ~]# ls -ld /public/
drwxrwxrwx. 2 root root 6 7月   7 15:14 /public/
[root@localhost ~]# useradd tom
[root@localhost ~]# setfacl -m u:tom:---  /public/
[root@localhost ~]# getfacl tom
[root@localhost ~]# getfacl /public/
getfacl: Removing leading '/' from absolute path names
file: public/
owner: root
group: root
user::rwx
user:tom:---
group::rwx
mask::rwx
other::rwx
```

（2）案例

请实现lisi用户可以读取/etc/shadow文件内容，您有几种办法？
	1）、开放其他人权限
	chmod o+r /etc/shadow
	2）、利用所属组
	chown :lisi  /etc/shadow
	chmod  g+r /etc/shadow

​	3）、利用所有者
​	chown lisi  /etc/shadow
​	chmod u+r  /etc/shadow
​	4）、利用 ACL 策略
​	setfacl -m u:lisi:r  /etc/shadow

#### 3、附加权限

（1）Sticky Bit权限（附加）

占用其他人的x位，在设置了t权限下，即使用户有写入权限，也不能删除或改名其他用户数据；

```
[root@localhost /]# mkdir /nsd26
[root@localhost /]# chmod 777 /nsd26
[root@localhost /]# ls -ld /nsd26
drwxrwxrwx. 2 root root 6 7月   7 16:19 /nsd26
[root@localhost /]# chmod o+t /nsd26
[root@localhost /]# ls -ld /nsd26
drwxrwxrwt. 2 root root 6 7月   7 16:19 /nsd26
```

（2）Set GID权限（附加）

占用所属组的x位；

显示为s或S取决于属组是否有x权限；

对目录有效；

在一个具有SGID权限的目录下，新建的数据会自动继承所属组的身份；

```Linux
[root@localhost /]# mkdir /nsd27
[root@localhost /]# chmod :tmooc /nsd27
[root@localhost /]# chown  :tmooc /nsd27
[root@localhost /]# ls -ld /nsd27
drwxr-xr-x. 2 root tmooc 6 7月   7 16:28 /nsd27
[root@localhost /]# chmod g+s /nsd27
[root@localhost /]# ls  -ld /nsd27
drwxr-sr-x. 2 root tmooc 6 7月   7 16:28 /nsd27
[root@localhost /]# mkdir /nsd27/abc
[root@localhost /]# touch /nsd27/a.txt
[root@localhost /]# ls -l /nsd27
drwxr-sr-x. 2 root tmooc 6 7月   7 16:30 abc
-rw-r--r--. 1 root tmooc 0 7月   7 16:30 a.txt
```

（3）Set UID权限（附加）

​		Set UID（Set User ID）权限是一种特殊权限位，适用于可执行文件。当可执行文件具有Set UID权限时，当普通用户执行该文件时，该进程会以可执行文件的所有者的身份（而不是当前用户的身份）运行。

​		Set UID权限常用于需要特权访问或执行操作的程序，例如`passwd`命令，该命令需要访问密码文件，但普通用户无法直接访问该文件。

​		使用Set UID权限要小心，因为它可以使普通用户获得特权访问，如果使用不当，可能导致系统安全问题。

在Linux系统中，设置Set UID权限可以使用以下步骤：

​		1）、设置可执行文件的所有者为特权用户：

```
sudo chown root:root executable_file
```

其中，`executable_file` 是可执行文件的路径。

​		2）、设置Set UID权限：

```
sudo chmod u+s executable_file
```

​		这将将Set UID权限设置为可执行文件的所有者。

​		可以使用以下命令来验证是否成功设置了Set UID权限：

```
ls -l executable_file
```

​		在结果中，Set UID权限将显示为`-rwsr-xr-x`，其中`s`代表Set UID权限。

​		请注意，只有特定可执行文件的所有者才可以设置Set UID权限。此外，Set UID权限仅在可执行文件上有效，不适用于脚本文件或其他类型的文件。

​		确保仅将Set UID权限应用于必要的程序，并且对可执行文件进行严格的权限控制，以确保系统的安全性。



------

## 第八天（关于硬盘操作）



### 一、识别硬盘

在Linux中，您可以使用以下命令来识别和查看已连接的硬盘和存储设备：

#### 1、lsblk`命令：

显示块设备（包括硬盘和分区）的列表以及它们的挂载点。

```
lsblk
```

#### 2、fdisk`命令：

显示硬盘的分区表信息。

```
sudo fdisk -l
```

#### 3、parted`命令：

显示硬盘的分区表及其详细信息。

```
sudo parted -l
```

#### 4、df`命令：

显示文件系统的磁盘空间使用情况，包括分区、挂载点和可用空间。

```
df -h
```

#### 5、mount`命令：

显示已挂载的文件系统列表，包括硬盘和网络共享。

```
mount
```

#### 6、blkid`命令：

显示硬盘及其分区的UUID以及文件系统类型。

```
sudo blkid
```

#### 7、/proc/partitions`文件：

直接查看此文件，以获取关于已连接硬盘和分区的简单信息。

```
cat /proc/partitions
```

这些命令将提供硬盘、分区、文件系统类型、挂载点等相关信息，帮助您识别和了解系统中的硬盘设备。请注意，在使用这些命令时需要具有管理员权限（或使用`sudo`命令）。

### 二、分区规划

#### 1、分区模式：MBR与GPT；

**【MBR】：**

​		MBR（Master Boot Record）是一种磁盘分区布局方案，可跟踪计算机硬盘上的各个分区。这是一种旧的分区方案，最初用于BIOS（Basic Input/Output System）系统。

MBR方案使用512字节的引导扇区，包含一组固定的数据结构和引导代码。它将硬盘分为四个主分区，每个分区都有自己的标识符和分区表条目。其中一个主分区可以被指定为扩展分区，允许在其中创建多个逻辑分区。

下面是MBR分区的一些特点和限制：

1. 分区类型：MBR方案支持多种分区类型，包括主分区、扩展分区和逻辑分区。

2. 分区标识符：每个分区都有一个标识符，用于指示分区的类型。常见的标识符包括FAT32、NTFS等。

3. 分区表：MBR包含一个分区表，记录了硬盘上各个分区的位置和大小信息。

4. 分区限制：MBR方案最多支持四个主分区，或三个主分区加一个扩展分区。扩展分区可以包含多个逻辑分区。

5. 容量限制：MBR方案对硬盘容量有一定限制，最大支持到2TB（2,048GB）的硬盘。

6. 启动引导：MBR中的引导代码负责加载操作系统，引导扇区的代码将会被读取和运行。

需要注意的是，MBR方案有一些限制，对于现代大容量硬盘或需要更多分区的情况，建议考虑使用GPT（GUID Partition Table）方案，它是一种更先进的分区方案，支持更大的硬盘容量和更多的分区数量。

2、文件系统

Windows：NTFS，FAT；

Linux：

ext4（6）：【单个数据较小】；

xfs（7）：【单个数据较大】；

FAT：【最基本的存储方式】；

#### 2、分区配置

（1）、MBR分区模式

在Linux中，有许多命令可以用于对硬盘进行操作。以下是一些常用的命令：

​	1）lsblk：显示系统上的所有块设备信息，包括硬盘和分区。

​	2）fdisk：用于分区和管理磁盘，可以创建、删除、调整分区等操作。例如，使用"fdisk /dev/sda"来分区/dev/sda硬盘。

​	3）parted：是一个更高级的磁盘分区工具，支持GUID Partition Table（GPT）和MBR分区方案。可以使用"parted /dev/sda"来进入交互模式。

​	4）mkfs：用于创建文件系统。常见的命令是mkfs.ext4（创建ext4文件系统），mkfs.ntfs（创建NTFS文件系统）等。

​	5）mount：将文件系统挂载到指定的挂载点，以便访问其中的文件。例如，使用"mount /dev/sdb1 /mnt"将/dev/sdb1分区挂载到/mnt目录。

​	6）umount：卸载已挂载的文件系统，使其不再可访问。例如，使用"umount /mnt"将/mnt目录下的文件系统卸载。

​	7）mkswap：创建交换分区，用于系统的交换空间。使用"mkswap /dev/sdc1"来创建/dev/sdc1交换分区。

​	8）swapon：启用交换分区，使其可用。例如，使用"swapon /dev/sdc1"来启用/dev/sdc1交换分区。

​	9）sync：将所有未写入的缓冲区数据立即写入硬盘，确保数据持久化存储。

（2）、GPT分区模式

与MBR大致相同，使用命令后，输入g切换到GPT；

#### 3、交换空间

交换空间（Swap Space）是Linux系统中用于辅助内存管理的一种特殊分区。当系统的物理内存不足时，交换空间允许将一部分内存数据暂时存储到硬盘上，以释放物理内存供其他程序使用。以下是在Linux系统中创建和管理交换空间的一般步骤：

（1）检查当前系统是否已经存在交换空间。运行以下命令：

```
sudo swapon --show
```

如果没有任何输出，则表示当前系统没有已启用的交换空间。

（2）确定您要创建交换空间的方法。可以选择以下两种方式之一：

- **创建交换文件（Swap File）**：这是在文件系统中创建一个特定大小的文件，作为交换空间的存储。这是一种比较灵活的方式，可以根据需要随时更改交换空间的大小。
- **创建交换分区（Swap Partition）**：这是在硬盘上创建一个专门的分区来用作交换空间。这是一种较为固定的方式，分区大小和位置将在创建时确定。

（3）创建交换文件：

- 运行以下命令以创建指定大小（例如4GB）的交换文件：

  ```
  sudo fallocate -l 4G /swapfile
  ```

- 授予交换文件适当的权限：

  ```
  sudo chmod 600 /swapfile
  ```

- 格式化交换文件：

  ```
  sudo mkswap /swapfile
  ```

（4）创建交换分区：

- 使用适当的分区工具（如`gdisk`、`parted`或`fdisk`）创建一个空闲分区，并将其类型设置为Linux交换（Hex代码为82）。

- 使用以下命令格式化交换分区：

  ```
  sudo mkswap /dev/sdX1
  ```

其中，`/dev/sdX1` 是您的交换分区设备。

（5）启用交换空间：

- 启用交换文件：

  ```
  sudo swapon /swapfile
  ```

- 启用交换分区：

  ```
  sudo swapon /dev/sdX1
  ```

在此之后，您可以再次运行 `sudo swapon --show` 命令来确认交换空间是否已启用。

（6）更新 `/etc/fstab` 文件（可选）：

- 打开 `/etc/fstab` 文件以进行编辑：

  ```
  sudo nano /etc/fstab
  ```

- 在文件的末尾添加以下行：

  ```
  /swapfile none swap sw 0 0
  ```

  或

  ```
  UUID=<swap_partition_uuid> none swap sw 0 0
  ```

  对于交换文件，请使用第一种方式；对于交换分区，请使用第二种方式，将 `<swap_partition_uuid>` 替换为实际交换分区的UUID。这样系统会在每次启动时自动启用交换空间。

请注意，交换空间的大小通常建议设置为物理内存大小的一半，但具体大小取决于系统配置和需求。如果您发现系统频繁使用交换空间，则可能需要考虑增加物理内存以改善性能。

```Linux
[root@localhost /]# mkswap /dev/sdc1
mkswap: /dev/sdc1：警告，不要擦除 bootbits 扇区
        (检测到 dos 分区表)。使用 -f 选项强制执行。
正在设置交换空间版本 1，大小 = 2 GiB (2147479552  个字节)
无标签，UUID=04129d16-8760-4e8e-b8bf-16b2b2f71d52
[root@localhost /]# blkid /dev/sdc1
/dev/sdc1: UUID="04129d16-8760-4e8e-b8bf-16b2b2f71d52" TYPE="swap" PTTYPE="dos" PARTUUID="bf52295b-01"
[root@localhost /]# swap
swaplabel  swapoff    swapon        
[root@localhost /]# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition   2G 7.5M   -2
[root@localhost /]# swapon /dev/sdc1
[root@localhost /]# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition   2G 7.5M   -2
/dev/sdc1 partition   2G   0B   -3
[root@localhost /]# free -h
              total        used        free      shared  buff/cache   available
Mem:          1.7Gi       1.0Gi        83Mi        12Mi       674Mi       592Mi
Swap:         4.0Gi       7.0Mi       4.0Gi
[root@localhost /]# swapoff /dev/sdc1
[root@localhost /]# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition   2G   7M   -2
[root@localhost /]# free -h
              total        used        free      shared  buff/cache   available
Mem:          1.7Gi       1.0Gi        85Mi        12Mi       674Mi       593Mi
Swap:         2.0Gi       7.0Mi       2.0Gi
[root@localhost /]# 
```

#### 4、设置开机自动挂载

**（1）对磁盘进行分区**

```
[root@localhost /]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.32.1)。
更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。
设备不包含可识别的分区表。
创建了一个磁盘标识符为 0xa1a0e471 的新 DOS 磁盘标签。
命令(输入 m 获取帮助)：n
分区类型
   p   主分区 (0个主分区，0个扩展分区，4空闲)
   e   扩展分区 (逻辑分区容器)
选择 (默认 p)：
将使用默认回应 p。
分区号 (1-4, 默认  1): 
第一个扇区 (2048-41943039, 默认 2048): 
上个扇区，+sectors 或 +size{K,M,G,T,P} (2048-41943039, 默认 41943039): +2G
创建了一个新分区 1，类型为“Linux”，大小为 2 GiB。
命令(输入 m 获取帮助)：n
分区类型
   p   主分区 (1个主分区，0个扩展分区，3空闲)
   e   扩展分区 (逻辑分区容器)
选择 (默认 p)：
将使用默认回应 p。
分区号 (2-4, 默认  2): 
第一个扇区 (4196352-41943039, 默认 4196352): 
上个扇区，+sectors 或 +size{K,M,G,T,P} (4196352-41943039, 默认 41943039): +2G

创建了一个新分区 2，类型为“Linux”，大小为 2 GiB。
命令(输入 m 获取帮助)：w
分区表已调整。
将调用 ioctl() 来重新读分区表。
正在同步磁盘。
```

（2）创建自动挂载目录

```
[root@localhost /]# mkdir /mypart1
[root@localhost /]# mkdir /mypart2
[root@localhost /]# vim /etc/fstab 
```

（3）、格式化磁盘

```Linux
[root@localhost /]# mkfs.ext4 /dev/sdb1
mke2fs 1.45.6 (20-Mar-2020)
创建含有 524288 个块（每块 4k）和 131072 个inode的文件系统
文件系统UUID：0709fe96-1efb-410c-948c-9a6316c6a60b
超级块的备份存储于下列块： 
	32768, 98304, 163840, 229376, 294912
正在分配组表： 完成                            
正在写入inode表： 完成                            
创建日志（16384 个块）完成
写入超级块和文件系统账户统计信息： 已完成
[root@localhost /]# mkfs.xfs /dev/sdb2
meta-data=/dev/sdb2              isize=512    agcount=4, agsize=131072 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=0 inobtcount=0
data     =                       bsize=4096   blocks=524288, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[root@localhost /]# blkid
/dev/sda1: UUID="1ff79664-8a84-4adf-9361-3412987f5124" BLOCK_SIZE="512" TYPE="xfs" PARTUUID="662da033-01"
/dev/sda2: UUID="n0F0AA-UjvW-d5qV-NUir-dUEd-kPvT-RxQevZ" TYPE="LVM2_member" PARTUUID="662da033-02"
/dev/sdb1: UUID="0709fe96-1efb-410c-948c-9a6316c6a60b" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="a1a0e471-01"
/dev/sdb2: UUID="6bcfd897-fdec-4fb7-ad0f-ac4c2eda683f" BLOCK_SIZE="512" TYPE="xfs" PARTUUID="a1a0e471-02"
/dev/sr0: BLOCK_SIZE="2048" UUID="2022-05-15-21-06-44-00" LABEL="Rocky-8-6-x86_64-dvd" TYPE="iso9660" PTUUID="6b8b4567" PTTYPE="dos"
/dev/mapper/rl-root: UUID="11b644c5-3d58-4d6b-927a-4267e4444c69" BLOCK_SIZE="512" TYPE="xfs"
/dev/mapper/rl-swap: UUID="6ea1b15a-cd9f-44d8-b878-48d30b82fa7e" TYPE="swap"
mount: xfs: mount point does not exist.
```

（4）、修改自动挂载文件

```Linux
[root@localhost /]# cat /etc/fstab 
/dev/mapper/rl-root     /                       xfs     defaults        0 0
UUID=1ff79664-8a84-4adf-9361-3412987f5124 /boot                   xfs     defaults        0 0
/dev/mapper/rl-swap     none                    swap    defaults        0 0
/dev/sdb1 /mypart1 ext4  defaults 0 0
/dev/sdb2          xfs   defaults 0 0
```

（5）、自动挂载

```Linux
[root@localhost /]# mount /dev/cdrom /mypart1
mount: /mypart1: WARNING: device write-protected, mounted read-only.
[root@localhost /]# mount /dev/cdrom /mypart2
mount: /mypart2: WARNING: device write-protected, mounted read-only.
```

### 三、总结

在Linux系统中，硬盘是用于存储数据的重要物理设备。它是计算机中的非易失性存储介质，用于存储操作系统、应用程序、文件和其他数据。以下是关于Linux中硬盘的一些概述：

#### 1、**设备文件**：

​		在Linux中，硬盘通常通过设备文件进行访问。每个硬盘设备都被映射到一个特定的设备文件，这些设备文件位于`/dev`目录下。例如，第一个SATA硬盘通常被映射为`/dev/sda`，第二个硬盘为`/dev/sdb`，依此类推。

#### 2、**分区**：

​		硬盘可以被分成一个或多个分区，每个分区都被视为独立的逻辑单元。分区是为了更好地组织和管理硬盘上的数据。在Linux中，可以使用工具如`fdisk`、`parted`等来创建、修改和删除分区。

#### 3、**分区表**：

​		硬盘的分区信息以分区表的形式存储。在早期的系统中，使用的主要分区表是MBR（Master Boot Record）。但是在较新的系统和大容量硬盘上，通常使用的是GPT（GUID Partition Table）分区表，它提供了更大的分区范围和更多的特性。

#### 4、**文件系统**：

​		硬盘上的分区或整个硬盘可以被格式化为一个特定的文件系统。文件系统定义了用于组织和管理文件的规则和结构。在Linux中，常见的文件系统类型包括ext4、XFS、Btrfs等。使用工具如`mkfs`可以在已创建的分区上创建文件系统。

#### 5、**挂载**：

​		在Linux中，文件系统不会自动加载，需要手动将其挂载到系统的目录树中才能访问。通过挂载，文件系统中的文件和目录将在指定的挂载点上变得可见和可操作。可以使用`mount`命令来挂载文件系统，并使用`/etc/fstab`配置文件来进行挂载设置。

#### 6、**管理和监测**：

​		在Linux中，可以使用多个命令和工具来管理和监测硬盘。例如，可以使用`fdisk`和`parted`等命令来进行分区操作，使用`df`、`du`和`lsblk`来查看磁盘空间使用情况，使用`smartctl`来监测硬盘的健康状态等。

​		请注意，硬盘是一种机械电子设备，有限的使用寿命，因此备份重要数据非常重要，以防止数据丢失。此外，对硬盘进行任何修改或操作时，请谨慎进行，并遵循准确的操作步骤以避免数据损坏或丢失。建议定期检查硬盘的健康状况，并及时更换有问题的硬盘。



------

## 第九天（关于卷组以及进程的操作）

### 一、逻辑卷操作

#### 1、简单了解逻辑卷

参与逻辑卷制作的成员，必须是没有使用的分区或者硬盘；

**优点：**

- [x] 整合分散空间；

- [x] 可以变大；

**原理：**将众多的物理卷（pv）组建成卷组（vg），再从卷组中划分逻辑卷（lv）；

#### 2、逻辑卷

**（1）、建立卷组**

```
[root@localhost ~]# man vgcreate
[root@localhost ~]# vgcreate systemvg /dev/sdb[1-2]
  Physical volume "/dev/sdb1" successfully created.
  Physical volume "/dev/sdb2" successfully created.
  Volume group "systemvg" successfully created
[root@localhost ~]# pvs
  PV         VG       Fmt  Attr PSize   PFree
  /dev/sda2  rl       lvm2 a--  <19.00g      0
  /dev/sdb1  systemvg lvm2 a--  <10.00g <10.00g
  /dev/sdb2  systemvg lvm2 a--  <10.00g <10.00g
[root@localhost ~]# vgs
  VG       #PV #LV #SN Attr   VSize   VFree
  rl         1   2   0 wz--n- <19.00g     0
  systemvg   2   0   0 wz--n-  19.99g 19.99g
[root@localhost ~]#lvcreate -L 16G -n vo  systemvg
  Logical volume "vo" created.
[root@localhost ~]# mkfs.xfs /dev/systemvg/vo 
meta-data=/dev/systemvg/vo       isize=512    agcount=4, agsize=1048576 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=0 inobtcount=0
data     =                       bsize=4096   blocks=4194304, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```

**（2）、设置自动挂载**

```Linux
[root@localhost ~]# vim /etc/fstab 
[root@localhost ~]# mount -a
[root@localhost ~]# lsblk 
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    0   20G  0 disk 
├─sda1        8:1    0    1G  0 part /boot
└─sda2        8:2    0   19G  0 part 
  ├─rl-root 253:0    0   17G  0 lvm  /
  └─rl-swap 253:1    0    2G  0 lvm  [SWAP]
sdb           8:16   0   80G  0 disk 
├─sdb1        8:17   0   10G  0 part 
│ └─systemvg-vo
│           253:2    0   16G  0 lvm  /mylv
├─sdb2        8:18   0   10G  0 part 
│ └─systemvg-vo
│           253:2    0   16G  0 lvm  /mylv
├─sdb3        8:19   0   10G  0 part 
├─sdb4        8:20   0    1K  0 part 
├─sdb5        8:21   0   20G  0 part 
└─sdb6        8:22   0   20G  0 part 
sr0          11:0    1 10.5G  0 rom  /run/media/root/Rocky-8
[root@localhost ~]# 
```

**（3）、扩展逻辑卷 空间：**

```Linux
[root@localhost ~]# lvextend -L 18G /dev/systemvg/vo 
  Size of logical volume systemvg/vo changed from 16.00 GiB (4096 extents) to 18.00 GiB (4608 extents).
  Logical volume systemvg/vo successfully resized.
[root@localhost ~]# vgs
  VG       #PV #LV #SN Attr   VSize   VFree
  rl         1   2   0 wz--n- <19.00g    0 
  systemvg   2   1   0 wz--n-  19.99g 1.99g
[root@localhost ~]# lvs
  LV   VG       Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rl       -wi-ao---- <17.00g                                                    
  swap rl       -wi-ao----   2.00g                                                    
  vo   systemvg -wi-ao----  18.00g  
```

**（4）、扩展文件系统**

```Linux
[root@localhost ~]# xfs_growfs /dev/systemvg/vo 
meta-data=/dev/mapper/systemvg-vo isize=512    agcount=4, agsize=1048576 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=0 inobtcount=0
data     =                       bsize=4096   blocks=4194304, imaxpct=25
[root@localhost ~]# df -h | grep vo
/dev/mapper/systemvg-vo   18G  161M   18G    1% /mylv
[root@localhost ~]# lvs
  LV   VG       Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rl       -wi-ao---- <17.00g                                                  

  swap rl       -wi-ao----   2.00g                                                   

  vo   systemvg -wi-ao----  18.00g                 
```

**（5）扩展卷组空间**

```Linux
[root@localhost ~]# vgextend systemvg /dev/sdb{3,5,6}
  Physical volume "/dev/sdb3" successfully created.
  Physical volume "/dev/sdb5" successfully created.
  Physical volume "/dev/sdb6" successfully created.
  Volume group "systemvg" successfully extended
[root@localhost ~]# vgs
  VG       #PV #LV #SN Attr   VSize   VFree 
  rl         1   2   0 wz--n- <19.00g     0 
  systemvg   5   1   0 wz--n-  69.98g 51.98g  
```

**（6）删除逻辑卷**

```
[root@localhost ~]# lvremove /dev/systemvg/vo 
  Logical volume systemvg/vo contains a filesystem in use.
[root@localhost ~]# umount
umount          umount.nfs4     
umount.nfs      umount.udisks2  
[root@localhost ~]# umount /mylv 
[root@localhost ~]# lvremove /dev/systemvg/vo 
Do you really want to remove active logical volume systemvg/vo? [y/n]: y
  Logical volume "vo" successfully removed.
[root@localhost ~]# lvs
  LV   VG Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rl -wi-ao---- <17.00g                                                    
  swap rl -wi-ao----   2.00g                                                    
[root@localhost ~]# vim /etc/fstab 
```

**（7）删除卷组**

```
[root@localhost ~]# vgremove systemvg 
  Volume group "systemvg" successfully removed
```

 3、卷组细小操作

（1）、注意pe值，系统默认为4：可以用vgchange   -s  大小  systemvg修改；

（2）、vgdisplay：查看卷组详细信息，主要查看pe大小；                  

### 二、程序与进程

程序：静态没有执行 的代码    硬盘

进程：内存中正在执行的代码    内存与cpu

#### 1、关于进程的命令

```
[root@localhost ~]# pstree -p tw
bash(6295)───vim(6378)
[root@localhost ~]# pstree -a tw
bash
  └─vim /opt/1.txt 
```

#### 2、关于查询进程命令

**（1）：ps**

```
[root@localhost ~]# ps aux  | wc -l
241
[root@localhost ~]# ps -elf |  wc -l 
241
```

**（2）：top**

```
[root@localhost ~]# top -d 1 
top - 15:12:18 up  2:20,  1 user,  load average: 0.05, 0.05,
Tasks: 239 total,   1 running, 238 sleeping,   0 stopped,   
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 h
MiB Mem :   1785.4 total,     87.6 free,    945.0 used,    7
MiB Swap:   2048.0 total,   1712.0 free,    335.9 used.    6
PID USER      PR  NI    VIRT    RES    SHR S  %CPU 
934 root      20   0  402416   3440   3016 S   0.0 
935 root      20   0   50280   2104   1200 S   0.0 
936 root      20   0  556292   7208   5064 S   0.0 
937 dbus      20   0   94432   5096   2244 S   0.0 
938 root      20   0  296252   3548   2240 S   0.0 
939 root      20   0  652064   5708   4112 S   0.0 
940 root      20   0   17788   1100    932 S   0.0 
941 rtkit     21   1  202868   1656   1304 S   0.0 
942 polkitd   20   0 1639660   6568   5164 S   0.0 
943 root      20   0  125024   2092   1456 S   0.0 
[root@localhost ~]# 
```

**（3）：pgrep**

```
[root@tw /]# pgrep -x crond 
1376
[root@tw /]# pgrep -lx  crond 
1376 crond
```

#### 3、休眠进程

```
[root@tw /]# sleep 2000
^Z                              //暂时放入后台
[1]+  已停止               sleep 2000
[root@tw /]# jobs 
[1]+  已停止               sleep 2000           //查看后台进程cheng
[root@tw /]# bg 1
[1]+ sleep 2000 &
[root@tw /]# jobs 
[1]+  运行中               sleep 2000 &            //后台运行
[root@tw /]# fg 1
sleep 2000
^C
```

### 三、总结

下面是关于Linux中卷组和进程操作的总结：

#### 1、卷组操作：

（1）创建卷组：使用`vgcreate`命令创建卷组，并将一个或多个物理卷添加到该卷组中。

（2）显示卷组信息：使用`vgdisplay`命令显示卷组的详细信息，包括物理卷、逻辑卷等。

（3）扩展卷组：使用`vgextend`命令将新的物理卷添加到已存在的卷组中，并扩展卷组的容量。

（4）缩小卷组：使用`vgsreduce`命令减少卷组的容量，将物理卷从卷组中移除。

#### 2、逻辑卷操作：

（1）创建逻辑卷：使用`lvcreate`命令在卷组中创建逻辑卷，并指定逻辑卷的大小。

（2）扩展逻辑卷：使用`lvextend`命令扩展逻辑卷的大小。

（3）调整逻辑卷大小：使用`lvresize`命令调整逻辑卷的大小。

（4）删除逻辑卷：使用`lvremove`命令删除逻辑卷。

#### 3、文件系统操作：

（1）创建文件系统：使用`mkfs`命令在逻辑卷上创建文件系统。

（2）挂载文件系统：使用`mount`命令将文件系统挂载到指定的挂载点。

（3）卸载文件系统：使用`umount`命令卸载已挂载的文件系统。

#### 4、进程操作：

（1）查看进程：使用`ps`命令查看当前运行的进程信息。

（2）杀死进程：使用`kill`命令向进程发送信号，终止指定的进程。

（3）后台运行进程：使用`&`符号在命令行将进程放入后台运行。

这是关于Linux中卷组和进程操作的简要总结。请注意，这只是一些常用的操作，Linux提供了更多操作和命令以满足不同需求。你可以查阅相关文档和手册获取更详细的信息。



------

## 第十天（网卡、网络地址以及远程管理）

### 一、配置基础环境

#### 1、搭建yum仓库

```
[root@localhost /]# mkdir  /mydvd
[root@localhost /]# ls
bin   dev  home  lib64  mnt    opt   root  sbin  sys  usr
boot  etc  lib   media  mydvd  proc  run   srv   tmp  var
[root@localhost /]# mount /dev/cdrom /mydvd
mount: /mydvd: WARNING: device write-protected, mounted read-only.
[root@localhost /]# ls /mydvd/
AppStream  EFI     isolinux  media.repo
BaseOS     images  LICENSE   TRANS.TBL
[root@localhost /]# rm -rf /etc/yum.repos.d/*
[root@localhost /]# vim /etc/yum.repos.d/mydvd.repo
[root@localhost /]# yum -y install tftp-server
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
app                         255 MB/s | 7.8 MB     00:00    
base                        209 MB/s | 2.6 MB     00:00    
依赖关系解决。
 软件包          架构       版本              仓库     大小
安装:
 tftp-server     x86_64     5.2-24.el8        app      49 k
事务概要
安装  1 软件包
总计：49 k
安装大小：65 k
下载软件包：
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                             1/1 
  安装    : tftp-server-5.2-24.el8.x86_64               1/1 
  运行脚本: tftp-server-5.2-24.el8.x86_64               1/1 
  验证    : tftp-server-5.2-24.el8.x86_64               1/1 
已安装:
  tftp-server-5.2-24.el8.x86_64                             
完毕！
### 
```

#### 2、设置开机自动挂载。

```
[root@localhost /]# ls /dev/cdrom
/dev/cdrom
[root@localhost /]# blkid /dev/cdrom
/dev/cdrom: BLOCK_SIZE="2048" UUID="2022-05-15-21-06-44-00" LABEL="Rocky-8-6-x86_64-dvd" TYPE="iso9660" PTUUID="6b8b4567" PTTYPE="dos"
[root@localhost /]# vim /etc/fstab 
[root@localhost /]# umount /mydvd 
[root@localhost /]# cat /etc/fstab 
#
/etc/fstab
Created by anaconda on Fri Jun 30 03:05:52 2023
#
Accessible filesystems, by reference, are maintained under '/dev/disk/'.
See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
#
After editing this file, run 'systemctl daemon-reload' to update systemd
units generated from this file.
#
/dev/mapper/rl-root     /  xfs     defaults        0 0
UUID=1ff79664-8a84-4adf-9361-3412987f5124 /boot                   xfs     defaults        0 0
/dev/mapper/rl-swap     none  swap    defaults      0 0
/dev/cdrom  /mydvd  iso9660 defaults 0 0   
[root@localhost /]# mount -a
mount: /mydvd: WARNING: device write-protected, mounted read-only.
```

#### 3、关于网卡配置

**（1）修改网卡命名**

```linux 
[root@nsd2306 ~]# cat /etc/default/grub 
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=auto resume=/dev/mapper/rl-swap rd.lvm.lv=rl/root rd.lvm.lv=rl/swap rhgb quiet net.ifnames=0 biosdevname=0"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
[root@nsd2306 ~]# reboot
[root@nsd2306 ~]# ifconfig | head -2
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        ether 00:0c:29:59:ac:86  txqueuelen 1000  (Ethernet)
[root@nsd2306 ~]# nmcli dev connect eth0   //   链接网卡设备
```

**（2）nmcli：**

删除服务器自己取的外号：

```Linux
[root@nsd2306 ~]# nmcli connection delete ens33 
成功删除连接 "ens33" (08d75bba-75e8-4971-8264-ea9ba6c0f805)。
[root@nsd2306 ~]# nmcli connection delete virbr0 
成功删除连接 "virbr0" (aa4a248c-1959-4689-88cb-0c36f5272a91)。
[root@nsd2306 ~]# nmcli connection show
NAME  UUID                                  TYPE      DEVIC>
eth0  396dd3ed-2761-43c6-9844-b13519c35321  ethernet  eth0 >
```

添加新的网络命名：

```Linux
[root@nsd2306 ~]# nmcli connection add type ethernet ifname eth0 con-name eth0
连接 "eth0" (9611161e-bc21-446a-934d-377d4ecd21cc) 已成功添加。
[root@nsd2306 ~]# nmcli connection show
NAME  UUID                                  TYPE      DEVIC>
eth0  9611161e-bc21-446a-934d-377d4ecd21cc  ethernet  eth0 >
[root@nsd2306 ~]# ping baidu.com
```

修改IP地址：

```Linux
[root@nsd2306 ~]# nmcli connection modify eth0 ipv4.method manual ipv4.addresses 192.168.88.77/24 ipv4.gateway 192.168.88.200 autoconnect yes 
[root@nsd2306 ~]# nmcli connection up eth0   //  激活网卡
连接已成功激活（D-Bus 活动路径：/org/freedesktop/NetworkManager/ActiveConnection/4）
[root@nsd2306 ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:59:ac:86 brd ff:ff:ff:ff:ff:ff
    inet 192.168.88.77/24 brd 192.168.88.255 scope global noprefixroute eth0
[root@nsd2306 ~]route -n         //查看网关地址信息
	Kernel IP routing table
	Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
	0.0.0.0         192.168.88.200  0.0.0.0         UG    100    0        0 eth0
	192.168.88.0    0.0.0.0         255.255.255.0   U     100    0        0 eth0
```

**（3）nmtui：**

![image-20230712114948862](C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230712114948862.png)

**（4）修改网卡配置文件：**



### 二、配置Linux网络

#### 1、克隆三台机器（A，B，C）进行基本修改

```
[root@nsd2306 ~]# hostnamectl set-hostname pc2.tedu.cn
[root@nsd2306 ~]# bash
[root@pc2 ~]# nmcli connection modify eth0 ipv4.method manual ipv4.addresses 192.168.88.2/24 autoconnect yes
[root@pc2 ~]# nmcli connection up eth0 
连接已成功激活（D-Bus 活动路径：/org/freedesktop/NetworkManager/ActiveConnection/3）
[root@pc2 ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:cd:57:5c brd ff:ff:ff:ff:ff:ff
    inet 192.168.88.2/24 brd 192.168.88.255 scope global noprefixroute eth0 
```

#### 2、配置虚拟网卡

使真机与虚拟机之间可以相互联通。

#### 3、远程管理

（1）安装实现远程管理的软件包

```linux 
[root@pc1 ~]# rpm  -qa | grep openssh
openssh-askpass-8.0p1-13.el8.x86_64
openssh-8.0p1-13.el8.x86_64
openssh-clients-8.0p1-13.el8.x86_64
openssh-server-8.0p1-13.el8.x86_64
```

实现被远程管理；

（2）远程管理其他主机

```Linux
[root@pc1 ~]# ssh root@192.168.88.2
The authenticity of host '192.168.88.2 (192.168.88.2)' can't be established.
ECDSA key fingerprint is SHA256:Wrz5d+9MSkj7nQLa84lvIZJ+FpCpsVq0orD82NOUhxA.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.88.2' (ECDSA) to the list of known hosts.
root@192.168.88.2's password: 
Activate the web console with: systemctl enable --now cockpit.socket
Last login: Wed Jul 12 16:12:49 2023
[root@pc2 ~]# ll
总用量 8
drwxr-xr-x. 2 root root    6 6月  30 11:41 公共
```

（3）将对方的东西下载到本地

```
[root@pc2 ~]# scp /opt/my.txt root@192.168.88.240:/opt/
The authenticity of host '192.168.88.240 (192.168.88.240)' can't be established.
ECDSA key fingerprint is SHA256:Wrz5d+9MSkj7nQLa84lvIZJ+FpCpsVq0orD82NOUhxA.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.88.240' (ECDSA) to the list of known hosts.
root@192.168.88.240's password: 
my.txt                    100%    7     4.7KB/s   00:00 
```

```
[root@pc1 ~]# cat /opt/my.txt 
123456
```

（4）无密码远程管理

```Linux
[root@pc1 /]# ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:U9xI98LMAQNPppEPMr3hEV2cb+Q22d/TWf7sQ0ckL20 root@pc1.tedu.cn
The key's randomart image is:
+---[RSA 3072]----+
|       .+=*++.   |
|      o *O.Oooo .|
|       +.*= *+.B |
|        o..  .O E|
|        S    o **|
|         .     +*|
|              ..+|
|               .o|
|               .o|
+----[SHA256]-----+
[root@pc1 /]# ls /root/.ssh/
id_rsa  id_rsa.pub  known_hosts
[root@pc1 /]# ssh-copy-id root@192.168.88.2
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@192.168.88.2's password: 
Number of key(s) added: 1
Now try logging into the machine, with:   "ssh 'root@192.168.88.2'"
and check to make sure that only the key(s) you wanted were added.
[root@pc1 /]# ssh root@192.168.88.2
Activate the web console with: systemctl enable --now cockpit.socket
Last login: Wed Jul 12 16:56:31 2023 from 192.168.88.240
```

### 三、日志管理

1、实时跟踪日志消息



### 四、总结

## 第十一天（网络 常用工具）

### 一、常用的网络工具

#### 1、ip命令

（1）ip   address   show

查看当前网卡信息

```
[root@pc3 ~]# ip address show 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq
```

（2）ip   address   add 

添加一个临时网卡

```
[root@pc3 ~]# ip address add 192.168.88.2/24  dev eth0 
[root@pc3 ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:70:68:91 brd ff:ff:ff:ff:ff:ff
    inet 192.168.88.3/24 brd 192.168.88.255 scope global noprefixroute eth0
       valid_lft forever preferred_lft forever
    inet 192.168.88.2/24 scope global secondary eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::2471:6a06:7946:6b17/64 scope link noprefixroute 
```

（3）ip   address    del

删除临时网卡；

#### 2、ping命令

ping -c  测试联通性；

### 二、用户登录分析

#### 1、查看用户登录信息

（1）users

（2）who

（3）w命令

#### 2、产看最近登录成功或失败的用户信息

（1）last

（2）lastb

### 二、sel inux 服务

#### 1、sel inux的运行模式

（1）enforcing【强制】：

（2）permissive【宽松】：

（3）disabled【彻底禁用】：

#### 2、切换运行模式

（1）临时切换：setenforce    1|0

```
[root@pc1 ~]# getenforce 
Enforcing
[root@pc1 ~]# setenforce 0
[root@pc1 ~]# getenforce 
Permissive
```

（2）固定配置：/etc/sel inux/config文件

```
[root@pc1 ~]# vim /etc/selinux/config
[root@pc1 ~]# cat /etc/selinux/config 

This file controls the state of SELinux on the system.

SELINUX= can take one of these three values:

enforcing - SELinux security policy is enforced.

permissive - SELinux prints warnings instead of enforcing.

disabled - No SELinux policy is loaded.

SELINUX=permissive

SELINUXTYPE= can take one of these three values:

targeted - Targeted processes are protected,

minimum - Modification of targeted policy. Only selected processes are protected. 

mls - Multi Level Security protection.

SELINUXTYPE=targeted
```

### 三、Linux密码破解

#### 1、重启操作系统

按上下键停留在此界面：



![image-20230713113721092](C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230713113721092.png)

找到Linux开头的一行，将ro修改为rw，空格，写入rd.break:

![image-20230713113956791](C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230713113956791.png)

#### 2、进入救援模式

（1）、进入救援模式

（2）、切换到硬盘操作系统

（3）、重设root密码

（4）、如果selinux是强制模式，才需要selinux失忆，其他模式不需要让selinux进行失忆、

sh-4.2#touch  /.autorelablel            #让selinux失忆

或者修改运行配置文件

（5）、强制重启系统修复完成

![image-20230713115508921](C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230713115508921.png)





------

## 第十二天（关于网页服务）



### 一、web服务

#### 1、web服务操作

**（1）搭建服务**

```
[root@pc1 ~]# yum -y install httpd
上次元数据过期检查：1 day, 19:09:25 前，执行于 2023年07月12日 星期三 14时13分33秒。
依赖关系解决。
============================================================
 软件包            架构   版本                   仓库  大小
============================================================
安装:
 httpd             x86_64 2.4.37-47.module+el8.6.0+823+f143cee1.1
                                                 app  1.4 M
安装依赖关系:
 apr               x86_64 1.6.3-12.el8           app  128 k
 apr-util          x86_64 1.6.1-6.el8.1          app  104 k
 httpd-filesystem  noarch 2.4.37-47.module+el8.6.0+823+f143cee1.1
                                                 app   40 k
 httpd-tools       x86_64 2.4.37-47.module+el8.6.0+823+f143cee1.1
                                                 app  107 k
 mod_http2         x86_64 1.15.7-5.module+el8.6.0+823+f143cee1
                                                 app  153 k
 rocky-logos-httpd noarch 85.0-4.el8             base  22 k
安装弱的依赖:
 apr-util-bdb      x86_64 1.6.1-6.el8.1          app   23 k
 apr-util-openssl  x86_64 1.6.1-6.el8.1          app   26 k
启用模块流:
 httpd                    2.4                              
事务概要
============================================================
安装  9 软件包
总计：2.0 M
安装大小：5.4 M
下载软件包：
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                             1/1 
  安装    : apr-1.6.3-12.el8.x86_64                     1/9 
  运行脚本: apr-1.6.3-12.el8.x86_64                     1/9 
  安装    : apr-util-bdb-1.6.1-6.el8.1.x86_64           2/9 
  安装    : apr-util-openssl-1.6.1-6.el8.1.x86_64       3/9 
  安装    : apr-util-1.6.1-6.el8.1.x86_64               4/9 
  运行脚本: apr-util-1.6.1-6.el8.1.x86_64               4/9 
  安装    : httpd-tools-2.4.37-47.module+el8.6.0+823+   5/9 
  安装    : rocky-logos-httpd-85.0-4.el8.noarch         6/9 
  运行脚本: httpd-filesystem-2.4.37-47.module+el8.6.0   7/9 
  安装    : httpd-filesystem-2.4.37-47.module+el8.6.0   7/9 
  安装    : mod_http2-1.15.7-5.module+el8.6.0+823+f14   8/9 
  安装    : httpd-2.4.37-47.module+el8.6.0+823+f143ce   9/9 
  运行脚本: httpd-2.4.37-47.module+el8.6.0+823+f143ce   9/9 
  验证    : apr-1.6.3-12.el8.x86_64                     1/9 
  验证    : apr-util-1.6.1-6.el8.1.x86_64               2/9 
  验证    : apr-util-bdb-1.6.1-6.el8.1.x86_64           3/9 
  验证    : apr-util-openssl-1.6.1-6.el8.1.x86_64       4/9 
  验证    : httpd-2.4.37-47.module+el8.6.0+823+f143ce   5/9 
  验证    : httpd-filesystem-2.4.37-47.module+el8.6.0   6/9 
  验证    : httpd-tools-2.4.37-47.module+el8.6.0+823+   7/9 
  验证    : mod_http2-1.15.7-5.module+el8.6.0+823+f14   8/9 
  验证    : rocky-logos-httpd-85.0-4.el8.noarch         9/9 
已安装:
  apr-1.6.3-12.el8.x86_64                                   
  apr-util-1.6.1-6.el8.1.x86_64                             
  apr-util-bdb-1.6.1-6.el8.1.x86_64                         
  apr-util-openssl-1.6.1-6.el8.1.x86_64                     
  httpd-2.4.37-47.module+el8.6.0+823+f143cee1.1.x86_64      
  httpd-filesystem-2.4.37-47.module+el8.6.0+823+f143cee1.1.noarch
  httpd-tools-2.4.37-47.module+el8.6.0+823+f143cee1.1.x86_64
  mod_http2-1.15.7-5.module+el8.6.0+823+f143cee1.x86_64     
  rocky-logos-httpd-85.0-4.el8.noarch                       
完毕！
[root@pc1 ~]# echo NSD Web Server > /var/www/html/index.html 
[root@pc1 ~]# systemctl restart httpd
[root@pc1 ~]# curl 192.168.88.240
NSD Web Server
```

#### 2、关于服务的操作

​	DocumentRoot：指定存放网页文件的路径，默认路径为：/var/www/html

**（1）apache自己访问自己的规则**

自动继承父目录

/var/www/html    # 允许所有客户端访问

/var/                      # 拒绝所有客户访问

###注意在配置文件写入相关目录的标签；

**（2）测试页面出现发的原因：**

没有网页文件；

selinux没有关闭或设置为宽松；

httpd没有访问规则；

网页文件名称不是index.html；

**（3）网络路径与实际路径**

网路路径：http：//192.168.88.1（IP地址）/webroot/abc；

实际路径：网页配置文件写入的路径（/webroot/webroot/abc）；

**关于网络路径与实际路径的区别：**

```
[root@pc1 webroot]# mkdir /webroot/abc
[root@pc1 webroot]# echo wo shi abc > /webroot/abc/index.html
[root@pc1 webroot]# curl 192.168.88.240/abc/
wo shi abc
[root@pc1 webroot]# curl 192.168.88.240/abc
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://192.168.88.240/abc/">here</a>.</p>
</body></html>
[root@pc1 webroot]# curl 192.168.88.240/abc/
wo shi abc
[root@pc1 webroot]#  
```

<img src="C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230714114534923.png" alt="image-20230714114534923" style="zoom: 25%;" />



网页界面会自动补全abc/；

**（4）配置文件操作**

```
[root@pc1 /]# vim /etc/httpd/conf.d/haha.conf
[root@pc1 /]# cat /var/www/cbd/index.html 
wo shi cbd
[root@pc1 /]# mkdir /var/www/cbd
[root@pc1 /]# echo wo shi cbd > /var/www/cbd/indec.html
[root@pc1 /]# systemctl restart httpd.s
httpd.service  httpd.socket   
[root@pc1 /]# systemctl restart httpd.s
httpd.service  httpd.socket   
[root@pc1 /]# systemctl restart httpd
[root@pc1 /]# curl 192.168.88.240
root@pc1 /]# curl 192.168.88.240
wo shi cbd
```

#### 3、listen 监听ip地址

```
[root@pc1 /]# vim /etc/httpd/conf.d/haha.conf 
[root@pc1 /]# cat /etc/httpd/conf.d/haha.conf 
DocumentRoot  /var/www/cbd
Listen 8000
[root@pc1 /]# systemctl restart httpd
[root@pc1 /]# curl 192.168.88.240:8000
wo shi cbd
[root@pc1 /]# curl 192.168.88.240
wo shi cbd
```

### 二、虚拟web主机

#### 1、虚拟web主机操作

**（1）基于域名**

```
[root@pc1 /]# vim /etc/httpd/conf.d/xixi.conf
[root@pc1 /]# cat /etc/httpd/conf.d/xixi.conf
<VirtualHost>
  ServerName www.qq.com
  DocumentRoot /var/www/qq 
</VirtualHost>
<VirtualHost *:80>
  ServerName www.lol.com
  DocumentRoot /var/www/lol 
</VirtualHost>
[root@pc1 /]# mkdir /var/www/qq /var/www/lol
[root@pc1 /]# echo wo shi qq > /var/www/qq/index.html
[root@pc1 /]# echo wo shi lol > /var/www/lol/index.html
[root@pc1 /]# systemctl restart httpd
```

/etc/hosts文件实现域名解析；

```Linux
[root@pc1 /]# vim /etc/hosts
[root@pc1 /]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.88.240  www.qq.com  www.lol.com[root@pc1 /]# curl www.qq.com
wo shi qq
[root@pc1 /]# curl www.lol.com
wo shi lol
[root@pc1 /]# 
```

**（2）基于端口号**

```Linux
[root@pc1 /]# vim /etc/httpd/conf.d/xixi.conf 
[root@pc1 /]# cat  /etc/httpd/conf.d/xixi.conf 
<VirtualHost *:80>
  ServerName www.qq.com
  DocumentRoot /var/www/qq 
</VirtualHost>
listen 8080
<VirtualHost *:8080>
  ServerName www.qq.com
  DocumentRoot /var/www/lol 
</VirtualHost>
[root@pc1 /]# systemctl restart httpd
[root@pc1 /]# curl www.qq.com:8080
wo shi lol
[root@pc1 /]# curl www.qq.com
wo shi qq
```

### 三、NFS服务

#### 1、定义：

用途：为客户机提供共享使用的文件夹；

协议：NFS，RPC；

所需的协议：nfs-utils；

系统服务：nfs-server；

#### 2、搭建服务（主配置文件;/etc/exports）

**（1）创建共享文件夹**

```
[root@pc1 /]# mkdir /abc
[root@pc1 /]# echo haha > /abc/h.txt
[root@pc1 /]# echo xixi > /abc/x.txt
```

**（2）编辑配置文件**

```
[root@pc1 /]# vim /etc/exports
[root@pc1 /]# systemctl restart nfs-server
[root@pc1 /]# cat /etc/exports
/abc  *(ro)
```

**（3）在b服务器上查看共享文件**

```
[root@pc2 ~]# showmount -e 192.168.88.240
Export list for 192.168.88.240:
/abc *
```

**（4）访问**

```Linux
[root@pc2 ~]# mount  192.168.88.240:/abc /mnt
[root@pc2 ~]# ls /mnt/
h.txt  x.txt

[root@pc1 /]# ls /abc/            //注意文件共享，新建文件时，pc2上也能看到；
gg.txt  h.txt  x.txt

[root@pc2 ~]# ls /mnt/
gg.txt  h.txt  x.txt
```

**（5）实现开机自动挂载共享目录**

```Linux
[root@pc2 ~]# vim /etc/fstab 
[root@pc2 ~]# sed -n '16p'  /etc/fstab 
192.168.88.240:/abc /mnt nfs  _netdev 0 0 
[root@pc2 ~]# umount /mnt 
[root@pc2 ~]# ls /mnt/
hgfs
[root@pc2 ~]# mount -a
[root@pc2 ~]# ls /mnt/
gg.txt  h.txt  x.txt
```

### 四、触发挂载

#### 1、相关内容

（1）由autofs服务提供的“按需访问”机制

—只要访问挂载点，就会触发响应，自动挂载指定设备；

—闲置超过时限后，会自动卸载；

#### 2、操作

```
[root@pc2 ~]# yum -y install autofs
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
上次元数据过期检查：2:30:30 前，执行于 2023年07月14日 星期五 14时49分16秒。
依赖关系解决。
============================================================
 软件包     架构       版本                  仓库      大小
============================================================
安装:
 autofs     x86_64     1:5.1.4-82.el8        base     706 k
事务概要
============================================================
安装  1 软件包
总计：706 k
安装大小：2.8 M
下载软件包：
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                             1/1 
  安装    : autofs-1:5.1.4-82.el8.x86_64                1/1 
  运行脚本: autofs-1:5.1.4-82.el8.x86_64                1/1 
  验证    : autofs-1:5.1.4-82.el8.x86_64                1/1 
已安装:
  autofs-1:5.1.4-82.el8.x86_64                              
完毕！
[root@pc2 ~]# systemctl restart autofs
[root@pc2 ~]# ls /misc/
[root@pc2 ~]# ls /misc/cd
AppStream  EFI     isolinux  media.repo
BaseOS     images  LICENSE   TRANS.TBL
[root@pc2 ~]# 
```

##：注意：只能在misc目录下触发挂载；



------

## 第十三天（自建仓库）



### 一、构建新的软件仓库

#### 1、从真机上传相关文件

<img src="C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230717105949228.png" alt="image-20230717105949228" style="zoom:33%;" />

#### 2、解压文件

```Linux
[root@pc1 ~]# tar -tf /root/tools.tar.gz 
tools/
tools/other/
tools/other/ntfs-3g-2014.2.15-6.el6.x86_64.rpm
tools/other/boxes-1.1.1-4.el7.x86_64.rpm
tools/other/sl-5.02-1.el7.x86_64.rpm
tools/other/oneko-1.2-19.fc24.x86_64.rpm
tools/other/cmatrix-1.2a-1.i386.rpm
tools/inotify-tools-3.13.tar.gz
tools/xcowsay-1.6.tar.gz
tools/typespeed_0.6.5.orig.tar.gz
[root@pc1 ~]# tar -xf /root/tools.tar.gz -C /
[root@pc1 ~]# ls /tools/
inotify-tools-3.13.tar.gz  typespeed_0.6.5.orig.tar.gz
other                      xcowsay-1.6.tar.gz
[root@pc1 ~]# ls /tools/other/
boxes-1.1.1-4.el7.x86_64.rpm
cmatrix-1.2a-1.i386.rpm
ntfs-3g-2014.2.15-6.el6.x86_64.rpm
oneko-1.2-19.fc24.x86_64.rpm
sl-5.02-1.el7.x86_64.rpm
```

#### 3、生成文件数据

**（1）生成数据文件**


 * ```
   * [root@pc1 ~]# createrepo /tools/other
     bash: createrepo: 未找到命令...
     安装软件包“createrepo_c”以提供命令“createrepo”？ [N/y] y              //安装命令
   ```


     * 正在队列中等待... 
     * 装入软件包列表... 
       下列软件包必须安装：
        createrepo_c-0.17.7-5.el8.x86_64	Creates a common metadata repository
        createrepo_c-libs-0.17.7-5.el8.x86_64	Library for repodata manipulation
        drpm-0.4.1-3.el8.x86_64	A library for making, reading and applying deltarpm packages
       继续更改？ [N/y] y


     * 正在队列中等待... 
     * 正在等待认证... 
     * 正在队列中等待... 
     * 装入软件包列表... 
     * 正在请求数据... 
     * 正在测试更改... 
     * 正在安装软件包...                            //生成数据文件
       Directory walk started
       Directory walk done - 5 packages
       Temporary output repo path: /tools/other/.repodata/
       Preparing sqlite DBs
       Pool started (with 5 workers)
       Pool finished


**（2）、修改配置文件**

```
[root@pc1 yum.repos.d]# vim mydvd.repo 
[root@pc1 yum.repos.d]# cd /
[root@pc1 /]# yum repoinfo
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
app                         4.2 MB/s | 4.3 kB     00:00    
base                        3.8 MB/s | 3.9 kB     00:00    
myrpm                       716 kB/s | 3.7 kB     00:00    
仓库ID            : app
仓库名称          : app
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L,
                      : R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月16日 星期一 05时01分50秒
Repo-pkgs          : 6,549
Repo-available-pkgs: 5,339
Repo-size          : 8.3 G
Repo-baseurl       : file:///mydvd/AppStream
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 09时40分47秒）
```





#### 4、自建仓库的更新

```
[root@pc1 /]# mv /tools/other/sl-5.02-1.el7.x86_64.rpm /root
[root@pc1 /]# ls /root
公共  图片  音乐             initial-setup-ks.cfg
模板  文档  桌面             sl-5.02-1.el7.x86_64.rpm
视频  下载  anaconda-ks.cfg  tools.tar.gz
[root@pc1 /]# yum repoinfo
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
上次元数据过期检查：0:36:33 前，执行于 2023年07月17日 星期一 09时47分23秒。
仓库ID            : app
仓库名称          : app
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L,
                      : R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月16日 星期一 05时01分50秒
Repo-pkgs          : 6,549
Repo-available-pkgs: 5,339
Repo-size          : 8.3 G
Repo-baseurl       : file:///mydvd/AppStream
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 09时47分23秒）
仓库文件名      : /etc/yum.repos.d/mydvd.repo

仓库ID            : base
仓库名称          : base
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L,
                      : R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月16日 星期一 04时59分01秒
Repo-pkgs          : 1,716
Repo-available-pkgs: 1,714
Repo-size          : 1.3 G
Repo-baseurl       : file:///mydvd/BaseOS
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 09时47分23秒）
仓库文件名      : /etc/yum.repos.d/mydvd.repo

仓库ID            : myrpm
仓库名称          : myrpm
Repo-revision      : 1689558057
Repo-updated       : 2023年07月17日 星期一 09时40分57秒
Repo-pkgs          : 5
Repo-available-pkgs: 5
Repo-size          : 413 k
Repo-baseurl       : file:///tools/other
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 09时47分23秒）
仓库文件名      : /etc/yum.repos.d/mydvd.repo
软件包总数：8,270

[root@pc1 /]# createrepo --update /tools/other/     //更新仓库数据文件
Directory walk started
Directory walk done - 4 packages
Loaded information about 4 packages
Temporary output repo path: /tools/other/.repodata/
Preparing sqlite DBs
Pool started (with 5 workers)
Pool finished
[root@pc1 /]# yum makecache                                    ////   更新yum源仓库
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
app                         4.2 MB/s | 4.3 kB     00:00    
base                        3.8 MB/s | 3.9 kB     00:00    
myrpm                       2.9 MB/s | 3.0 kB     00:00    
myrpm                       950 kB/s | 3.3 kB     00:00    
元数据缓存已建立。
[root@pc1 /]# yum repoinfo
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
上次元数据过期检查：0:00:12 前，执行于 2023年07月17日 星期一 10时24分39秒。
仓库ID            : app
仓库名称          : app
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L,
                      : R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月16日 星期一 05时01分50秒
Repo-pkgs          : 6,549
Repo-available-pkgs: 5,339
Repo-size          : 8.3 G
Repo-baseurl       : file:///mydvd/AppStream
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 10时24分38秒）
仓库文件名      : /etc/yum.repos.d/mydvd.repo

仓库ID            : base
仓库名称          : base
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L,
                      : R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月16日 星期一 04时59分01秒
Repo-pkgs          : 1,716
Repo-available-pkgs: 1,714
Repo-size          : 1.3 G
Repo-baseurl       : file:///mydvd/BaseOS
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 10时24分39秒）
仓库文件名      : /etc/yum.repos.d/mydvd.repo

仓库ID            : myrpm
仓库名称          : myrpm
Repo-revision      : 1689560662
Repo-updated       : 2023年07月17日 星期一 10时24分22秒
Repo-pkgs          : 4
Repo-available-pkgs: 4
Repo-size          : 399 k
Repo-baseurl       : file:///tools/other
Repo-expire        : 172,800 秒 （最近 2023年07月17日 星期一
                   : 10时24分39秒）
仓库文件名      : /etc/yum.repos.d/mydvd.repo
软件包总数：8,269
```





### 二、服务

#### 1、构建网络服务

网络服务：ftp、web、nfs

构建ftp服务，提供仓库内容：

**（1）、修改配置文件：**

```
[root@pc1 /]# vim /etc/vsftpd/vsftpd.conf 
[root@pc1 /]# cat /etc/vsftpd/vsftpd.conf     
ymous_enable=YES                             //找到这行，将no改为yes
[root@pc1 /]# systemctl restart vsftpd.
vsftpd.service  vsftpd.target   
[root@pc1 /]# systemctl restart vsftpd.
vsftpd.service  vsftpd.target   
[root@pc1 /]# systemctl restart vsftpd
[root@pc1 /]# systemctl enable vsftpd
Created symlink /etc/systemd/system/multi-user.target.wants/vsftpd.service → /usr/lib/systemd/system/vsftpd.service
```

**（2）、拷贝文件**

```
[root@pc1 /]# cp -r /tools/other/ /var/ftp/rpms
[root@pc1 /]# ls /var/ftp/
pub  rpms
[root@pc1 /]# curl ftp://192.168.88.240/rpms/
-rwxr-xr-x    1 0        0           67452 Jul 17 02:54 boxes-1.1.1-4.el7.x86_64.rpm
-rwxr-xr-x    1 0        0           31940 Jul 17 02:54 cmatrix-1.2a-1.i386.rpm
-rwxr-xr-x    1 0        0          263956 Jul 17 02:54 ntfs-3g-2014.2.15-6.el6.x86_64.rpm
-rwxr-xr-x    1 0        0           45526 Jul 17 02:54 oneko-1.2-19.fc24.x86_64.rpm
drwxr-xr-x    2 0        0            4096 Jul 17 02:54 repodata
-rwxr-xr-x    1 0        0           14244 Jul 17 02:54 sl-5.02-1.el7.x86_64.rpm


```



#### 2、虚拟机B修改配置文件

​		修改配置文件路径，将本机路径改为ftp://192.168.88.240/rpms/

然后重新加载yum源仓库

yum repoinfo

【注意】：可以用同样的方法将yum源仓库使用起来；

【注意】：ftp服务要设置为开机自启动；

【注意】：要关闭防火墙；

#### 3、wget基于网络服务

（1）、在pc1上创建一个文档

```
[root@pc1 ftp]# ls
1.txt  dvd  pub  rpms
```


（2）、在pc2上通过wget命令下载

```
[root@pc2 ~]# wget ftp://192.168.88.240/1.txt
--2023-07-17 14:09:39--  ftp://192.168.88.240/1.txt
           => “1.txt”
正在连接 192.168.88.240:21... 已连接。
正在以 anonymous 登录 ... 登录成功！
==> SYST ... 完成。   ==> PWD ... 完成。
==> TYPE I ... 完成。 ==> 不需要 CWD。
==> SIZE 1.txt ... 完成。

==> PASV ... 完成。   ==> RETR 1.txt ... 完成。

1.txt              [ <=> ]       0  --.-KB/s  用时 0s      

2023-07-17 14:09:39 (0.00 B/s) - “1.txt” 已保存 [0]

[root@pc2 ~]# ll
总用量 8
-rw-r--r--. 1 root root    0 7月  17 14:09 1.txt
drwxr-xr-x. 2 root root    6 6月  30 11:41 公共
drwxr-xr-x. 2 root root    6 6月  30 11:41 桌面
-rw-------. 1 root root 1259 6月  30 11:36 anaconda-ks.cfg
-rw-r--r--. 1 root root 1550 6月  30 11:40 initial-setup-ks.cfg
[root@pc2 ~]# 
```





#### 3、使用web服务用于网络仓库搭建

（1）装载httpd

（2）创建挂载点：/var/www/html/dvd/

（3）指定仓库位置，修改配置文件；

#### 4、DNS服务

**（1）工作原理**

dns系统存在的意义，方便记忆；

**正向解析：**DNS正向解析是指将域名转换为IP地址的过程。当用户在浏览器中输入一个域名时，系统会通过DNS解析器向DNS服务器发送查询请求，以获得与该域名相关的IP地址。这个过程就是DNS正向解析。

**反向解析：**DNS反向解析是指根据IP地址查找对应的域名的过程。与DNS正向解析相反，DNS反向解析是根据IP地址来获取域名信息。

**（2）服务分析**

**（3）单区域DNS服务**

#### 5、BIND域名服务

官方网点：

**（1）安装包（两个工具包）**

bind：

bind-chroot：提供牢笼政策

```
[root@pc1 /]# yum -y install bind bind-chroot
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
上次元数据过期检查：0:21:00 前，执行于 2023年07月17日 星期一 15时00分23秒。

依赖关系解决。
============================================================

 软件包         架构      版本                 仓库    大小
============================================================

安装:
 bind           x86_64    32:9.11.36-3.el8     app    2.1 M
 bind-chroot    x86_64    32:9.11.36-3.el8     app    104 k

事务概要
============================================================

安装  2 软件包
总下载：2.2 M
安装大小：4.6 M
下载软件包：
(1/2): bind-chroot-9.11.36- 162 kB/s | 104 kB     00:00    

(2/2): bind-9.11.36-3.el8.x 2.1 MB/s | 2.1 MB     00:01    
------------------------------------------------------------

总计                        2.2 MB/s | 2.2 MB     00:01     
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                             1/1 
  运行脚本: bind-32:9.11.36-3.el8.x86_64                1/2 
  安装    : bind-32:9.11.36-3.el8.x86_64                1/2 
  运行脚本: bind-32:9.11.36-3.el8.x86_64                1/2 
  安装    : bind-chroot-32:9.11.36-3.el8.x86_64         2/2 
  运行脚本: bind-chroot-32:9.11.36-3.el8.x86_64         2/2 
  验证    : bind-32:9.11.36-3.el8.x86_64                1/2 
  验证    : bind-chroot-32:9.11.36-3.el8.x86_64         2/2 
已安装:
  bind-32:9.11.36-3.el8.x86_64                              
  bind-chroot-32:9.11.36-3.el8.x86_64                       
完毕！
```






**（2）配置文件**

主配置文件路径：/etc/named.conf

地址库文件：/var/named                     //完全合格的域名与IP地址对应关系；

默认端口号：53

为了安全起见，可以先对配置文件进行备份，cp -p    ；

**编辑主配置文件：**

```Linux
[root@pc1 /]# vim  /etc/named.conf
[root@pc1 /]# cat  /etc/named.conf
options {
	directory 	"/var/named";
};
zone "." IN {                              //定义负责解析的域名为“.”,可修改，比如：“tedu.cn”
	type master;
	file "named.ca";
};
```

**编写地址库文件：**

```
[root@pc1 named]# cat tedu.cn.zone 
$TTL 1D
@	IN SOA	@ rname.invalid. (
					0	; serial
					1D	; refresh
					1H	; retry
					1W	; expire
					3H )	; minimum
tedu.cn 	        NS	nsd2306.tedu.cn
nsd2306.tedu.cn 	A	192.168.88.240
www.tedu.cn             A       1.1.1.1
ftp.tedu.cn             A       2.2.2.2
tts                     A       3.3.3.3        
```

**查看解析结果：**

```
[root@pc1 named]# vim tedu.cn.zone 
[root@pc1 named]# systemctl restart named
[root@pc1 named]# nslookup pc1.tedu.cn
Server:		127.0.0.1
Address:	127.0.0.1#53
Name:	pc1.tedu.cn
Address: 192.168.88.240
[root@pc1 named]# nslookup www.tedu.cn
Server:		127.0.0.1
Address:	127.0.0.1#53
Name:	www.tedu.cn
Address: 1.1.1.1
```

**（3）、特殊解析记录：**

```
[root@pc1 named]# vim tedu.cn.zone
[root@pc1 named]# cat tedu.cn.zone 
$TTL 1D
@	IN SOA	@ rname.invalid. (
					0	; serial
					1D	; refresh
					1H	; retry
					1W	; expire
					3H )	; minimum
 	        NS	pc1
pc1 	A	192.168.88.240
www  A       1.1.1.1
ftp     A       2.2.2.2
tts             A       3.3.3.3      

*      A     4.4.4.4                                  //：未知域名解析为4.4.4.4
[root@pc1 named]# systemctl restart named
[root@pc1 named]# nslookup wwdwdew.tedu.cn
Server:		192.168.88.240
Address:	192.168.88.240#53
Name:	wwdwdew.tedu.cn
Address: 4.4.4.4
```

**（4）、有规律的解析记录（内置函数）：**

```Linux
[root@pc1 named]# vim tedu.cn.zone 
[root@pc1 named]# cat tedu.cn.zone 
$TTL 1D
@	IN SOA	@ rname.invalid. (
					0	; serial
					1D	; refresh
					1H	; retry
					1W	; expire
					3H )	; minimum
 	        NS	pc1
pc1 	A	192.168.88.240
www  A       1.1.1.1
ftp     A       2.2.2.2
tts             A       3.3.3.3      

*      A     4.4.4.4 
       $GENERATE 1-50 stu$ A  192.168.1.$                //：加入函数
[root@pc1 named]# systemctl restart named
[root@pc1 named]# nslookup stu33.tedu.cn
Server:		192.168.88.240
Address:	192.168.88.240#53

Name:	stu33.tedu.cn
Address: 192.168.1.33
[root@pc1 named]# nslookup stu34.tedu.cn
Server:		192.168.88.240
Address:	192.168.88.240#53
Name:	stu34.tedu.cn
Address: 192.168.1.34
```

**（5）、递归解析**

递归查询：客户端发送请求给首选DNS服务器，首选DNS服务器与其他的DNS服务器交流，最终将解析结果带回来；

迭代查询：与递归不同的是请求发给首选DNS服务器，首选DNS服务器告知下一个DNS服务器；





------

## 第十四天（同步以及数据库）

### 一 、rsync本地同步

#### 1、基本用法

**（1）同步操作**

— rsync  【选项】   源目录    目标目录

与复制是差异：

复制：完全拷贝到源数据；

同步：增量拷贝，只传输变化过的数据；

**（2）同步控制**

-n：测试同步过程；

-a：归档模式 ，相当于-rlptgoD；

-v：显示详细操作信息；

-z：传输过程中启用压缩；（默认启用）

-X：保证acl策略不变；

#### 2、配置操作

（1）创建同步目录

```
[root@pc1 ~]# mkdir /mydir
[root@pc1 ~]# mkdir /todir
[root@pc1 ~]# echo 123 > /mydir/1.txt
[root@pc1 ~]# cp /etc/shells /mydir/
[root@pc1 ~]# ls /mydir/
1.txt  shells
[root@pc1 ~]# ls /todir/
[root@pc1 ~]# 
```

（2）同步操作

```
[root@pc1 ~]# rsync -avX /mydir/ /todir/
sending incremental file list
./
1.txt
shells

sent 301 bytes  received 60 bytes  722.00 bytes/sec
total size is 48  speedup is 0.13
[root@pc1 ~]# ls /todir/
1.txt  shells
```

【注意】：目录路径后面是否有“/”;

#### 3、远程同步

rsync  +    ssh ：远程同步；

**（1）操作**

```
[root@pc1 ~]# rsync -avX --delete /mydir/ root@192.168.88.2:/mnt
The authenticity of host '192.168.88.2 (192.168.88.2)' can't be established.
ECDSA key fingerprint is SHA256:Wrz5d+9MSkj7nQLa84lvIZJ+FpCpsVq0orD82NOUhxA.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.88.2' (ECDSA) to the list of known hosts.
root@192.168.88.2's password: 
sending incremental file list
deleting hgfs/
./
1.txt
shells

sent 306 bytes  received 70 bytes  44.24 bytes/sec
total size is 48  speedup is 0.13
```

**（2）实现ssh无密钥验证（实现只要数据有变化，就同步）**

```
[root@pc1 ~]# ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:F1phFFoH7T5oMuDiIr8eP7ArfbESSx2jXavrb/8eyzE root@pc1.tedu.cn
The key's randomart image is:
+---[RSA 3072]----+
|         .B+.    |
|         + o.    |
|        . o.     |
|    o o  o ..    |
|   + = oS .o     |
|  = = o o.o o    |
| o.* =   +E  .   |
|o *o* .  . =     |
| ==B+=...o=      |
+----[SHA256]-----+
[root@pc1 ~]# ls /root/.ssh/
id_rsa  id_rsa.pub  known_hosts

[root@pc1 .ssh]# ssh-copy-id root@192.168.88.2
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@192.168.88.2's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@192.168.88.2'"
and check to make sure that only the key(s) you wanted were added.

[root@pc1 .ssh]# rsync -avX --delete /mydir/ root@192.168.88.2:/mnt
sending incremental file list

sent 125 bytes  received 12 bytes  91.33 bytes/sec
total size is 48  speedup is 0.35

```

### 二、源代码软件的安装

#### 1、RPM源码包

目的：数据实时同步；

（1）、操作：监控目录变化 【inotify-tools】

#### 2、安装make与gcc开发工具

```
[root@pc1 .ssh]# yum -y install make gcc
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
上次元数据过期检查：1:24:06 前，执行于 2023年07月18日 星期二 09时28分53秒。
依赖关系解决。
============================================================
 软件包           架构    版本                  仓库   大小
============================================================
安装:
 gcc              x86_64  8.5.0-10.el8          app    23 M
 make             x86_64  1:4.2.1-11.el8        base  497 k
安装依赖关系:
 cpp              x86_64  8.5.0-10.el8          app    10 M
 glibc-devel      x86_64  2.28-189.1.el8        base   78 k
 glibc-headers    x86_64  2.28-189.1.el8        base  482 k
 isl              x86_64  0.16.1-6.el8          app   834 k
 kernel-headers   x86_64  4.18.0-372.9.1.el8    base  9.3 M
 libxcrypt-devel  x86_64  4.1.1-6.el8           base   24 k
事务概要
============================================================
安装  8 软件包
总下载：45 M
安装大小：99 M
下载软件包：
(1/8): isl-0.16.1-6.el8.x86 635 kB/s | 834 kB     00:01    
(2/8): glibc-devel-2.28-189  47 kB/s |  78 kB     00:01    
(3/8): glibc-headers-2.28-1 1.5 MB/s | 482 kB     00:00    
(4/8): cpp-8.5.0-10.el8.x86 2.0 MB/s |  10 MB     00:05    
(5/8): libxcrypt-devel-4.1. 9.6 kB/s |  24 kB     00:02    
(6/8): make-4.2.1-11.el8.x8 792 kB/s | 497 kB     00:00    
(7/8): kernel-headers-4.18. 1.8 MB/s | 9.3 MB     00:05    
(8/8): gcc-8.5.0-10.el8.x86 2.2 MB/s |  23 MB     00:10    
------------------------------------------------------------
总计                        4.1 MB/s |  45 MB     00:10     
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                             1/1 
  安装    : kernel-headers-4.18.0-372.9.1.el8.x86_64    1/8 
  运行脚本: glibc-headers-2.28-189.1.el8.x86_64         2/8 
  安装    : glibc-headers-2.28-189.1.el8.x86_64         2/8 
  安装    : libxcrypt-devel-4.1.1-6.el8.x86_64          3/8 
  安装    : glibc-devel-2.28-189.1.el8.x86_64           4/8 
  运行脚本: glibc-devel-2.28-189.1.el8.x86_64           4/8 
  安装    : isl-0.16.1-6.el8.x86_64                     5/8 
  运行脚本: isl-0.16.1-6.el8.x86_64                     5/8 
  安装    : cpp-8.5.0-10.el8.x86_64                     6/8 
  运行脚本: cpp-8.5.0-10.el8.x86_64                     6/8 
  安装    : gcc-8.5.0-10.el8.x86_64                     7/8 
  运行脚本: gcc-8.5.0-10.el8.x86_64                     7/8 
  安装    : make-1:4.2.1-11.el8.x86_64                  8/8 
  运行脚本: make-1:4.2.1-11.el8.x86_64                  8/8 
  验证    : cpp-8.5.0-10.el8.x86_64                     1/8 
  验证    : gcc-8.5.0-10.el8.x86_64                     2/8 
  验证    : isl-0.16.1-6.el8.x86_64                     3/8 
  验证    : glibc-devel-2.28-189.1.el8.x86_64           4/8 
  验证    : glibc-headers-2.28-189.1.el8.x86_64         5/8 
  验证    : kernel-headers-4.18.0-372.9.1.el8.x86_64    6/8 
  验证    : libxcrypt-devel-4.1.1-6.el8.x86_64          7/8 
  验证    : make-1:4.2.1-11.el8.x86_64                  8/8 
已安装:
  cpp-8.5.0-10.el8.x86_64                                   
  gcc-8.5.0-10.el8.x86_64                                   
  glibc-devel-2.28-189.1.el8.x86_64                         
  glibc-headers-2.28-189.1.el8.x86_64                       
  isl-0.16.1-6.el8.x86_64                                   
  kernel-headers-4.18.0-372.9.1.el8.x86_64                  
  libxcrypt-devel-4.1.1-6.el8.x86_64                        
  make-1:4.2.1-11.el8.x86_64                                
完毕！
[root@pc1 .ssh]# rpm  -q gcc
gcc-8.5.0-10.el8.x86_64
[root@pc1 .ssh]# rpm  -q make 
make-4.2.1-11.el8.x86_64
```

#### 3、准备源码包

```
[root@pc1 /]# tar -xf /tools/inotify-tools-3.13.tar.gz -C /usr/local/
[root@pc1 /]# ls /usr/l
lib/     lib64/   libexec/ local/   
[root@pc1 /]# ls /usr/l
lib/     lib64/   libexec/ local/   
[root@pc1 /]# ls /usr/local/
bin  games    inotify-tools-3.13  lib64    sbin   src
etc  include  lib                 libexec  share
[root@pc1 /]# 
[root@pc1 /]# cd /usr/local/inotify-tools-3.13/
[root@pc1 inotify-tools-3.13]# ls
aclocal.m4    configure     libinotifytools  NEWS
AUTHORS       configure.ac  ltmain.sh        README
ChangeLog     COPYING       Makefile.am      src
config.guess  depcomp       Makefile.in
config.h.in   INSTALL       man
config.sub    install-sh    missing
```

#### 4、编译安装

```
[root@pc1 inotify-tools-3.13]# ./configure --prefix=/opt/myrpm
```

安装到指定路径，；不会新建路径 ；

```
[root@pc1 /]# cd /usr/local/inotify-tools-3.13/

[root@pc1 inotify-tools-3.13]# make
make  all-recursive
PATH="$PATH:/sbin" ldconfig -n /opt/myrpm/lib
----------------------------------------------------------------------
Libraries have been installed in:
   /opt/myrpm/lib
----------------------------------------------------------------------
s/src”

[root@pc1 inotify-tools-3.13]# make install
Making install in libinotifytools
make[1]: 进入目录“/usr/local/inotify-tools-3.13/libinotifytools”
Making install in src
make[2]: 进入目录“/usr/local/inotify-tools-3.13/libinotifytools/src”
Making install in inotifytools
make[3]: 进入目录“/usr/local/inotify-tools-3.13/libinotifytools/src/inotifytools”


[root@pc1 inotify-tools-3.13]# ls /opt/
myrpm
[root@pc1 inotify-tools-3.13]# ls /opt/myrpm/
bin  include  lib  share
[root@pc1 inotify-tools-3.13]# ls /opt/myrpm/bin/
inotifywait  inotifywatch
```

#### 5、编写监控实时跟新脚本

（1）创建脚本文件

```
[root@pc1 /]# touch /etc/rsync.sh 
[root@pc1 /]# chmod +x /etc/rsync.sh        //为脚本文件添加执行权限
```

（2）编写脚本内容

```
[root@pc1 mydir]# cat /etc/rsync.sh 
#bin/bash
while /opt/myrpm/bin/inotifywait  -rqq /mydir/
do
	rsync -ax --delete /mydir/ root@192.168.88.2:/mnt
done
```

（3）执行脚本

```
[root@pc1 mydir]# ls
1.txt  2.txt  haha  shells
```

```
[root@pc2 mnt]# ls
1.txt  2.txt  haha  shells
```

```
[root@pc1 mydir]# touch  3.txt
[root@pc1 mydir]# ls
1.txt  2.txt  3.txt  haha  shells
```

```
[root@pc2 mnt]# ls
1.txt  2.txt  3.txt  haha  shells
```

```
[root@pc1 mydir]# jobs 
[1]+  运行中               /etc/rsync.sh &  (工作目录: /)
```

### 三、数据库

#### 1、安装数据库软件

```
[root@pc1 mydir]# yum -y install mariadb-server
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
上次元数据过期检查：1:51:23 前，执行于 2023年07月18日 星期二 12时53分52秒。
依赖关系解决。
============================================================
 软件包                     架构   版本           仓库
                                                        大小
============================================================
安装:
 mariadb-server             x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app  16 M
安装依赖关系:
 mariadb                    x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app 6.0 M
 mariadb-common             x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app  63 k
 mariadb-connector-c        x86_64 3.1.11-2.el8_3 app 199 k
 mariadb-connector-c-config noarch 3.1.11-2.el8_3 app  14 k
 mariadb-errmsg             x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app 233 k
 perl-DBD-MySQL             x86_64 4.046-3.module+el8.6.0+904+ef468285
                                                  app 155 k
安装弱的依赖:
 mariadb-backup             x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app 6.1 M
 mariadb-gssapi-server      x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app  50 k
 mariadb-server-utils       x86_64 3:10.3.32-2.module+el8.5.0+777+18007c86
                                                  app 1.1 M
启用模块流:
 mariadb                           10.3                    
 perl-DBD-MySQL                    4.046                   
事务概要
============================================================
安装  10 软件包
总下载：30 M
安装大小：154 M
下载软件包：
(1/10): mariadb-common-10.3 209 kB/s |  63 kB     00:00    
(2/10): mariadb-connector-c 2.4 MB/s | 199 kB     00:00    
(3/10): mariadb-connector-c 185 kB/s |  14 kB     00:00    
(4/10): mariadb-errmsg-10.3 3.9 MB/s | 233 kB     00:00    
(5/10): mariadb-gssapi-serv 751 kB/s |  50 kB     00:00    
(6/10): mariadb-10.3.32-2.m 2.7 MB/s | 6.0 MB     00:02    
(7/10): mariadb-backup-10.3 2.7 MB/s | 6.1 MB     00:02    
(8/10): mariadb-server-util 2.0 MB/s | 1.1 MB     00:00    
(9/10): mariadb-server-10.3 2.8 MB/s |  16 MB     00:05    
(10/10): perl-DBD-MySQL-4.0  23 kB/s | 155 kB     00:06    
------------------------------------------------------------
总计                        3.4 MB/s |  30 MB     00:08     
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                             1/1 
  安装    : mariadb-connector-c-config-3.1.11-2.el8    1/10 
  安装    : mariadb-common-3:10.3.32-2.module+el8.5    2/10 
  安装    : mariadb-errmsg-3:10.3.32-2.module+el8.5    3/10 
  安装    : perl-DBD-MySQL-4.046-3.module+el8.6.0+9    4/10 
  安装    : mariadb-connector-c-3.1.11-2.el8_3.x86_    5/10 
  安装    : mariadb-backup-3:10.3.32-2.module+el8.5    6/10 
  安装    : mariadb-gssapi-server-3:10.3.32-2.modul    7/10 
  安装    : mariadb-server-utils-3:10.3.32-2.module    8/10 
  运行脚本: mariadb-server-3:10.3.32-2.module+el8.5    9/10 
  安装    : mariadb-server-3:10.3.32-2.module+el8.5    9/10 
  运行脚本: mariadb-server-3:10.3.32-2.module+el8.5    9/10 
  安装    : mariadb-3:10.3.32-2.module+el8.5.0+777+   10/10 
  运行脚本: mariadb-3:10.3.32-2.module+el8.5.0+777+   10/10 
  验证    : mariadb-3:10.3.32-2.module+el8.5.0+777+    1/10 
  验证    : mariadb-backup-3:10.3.32-2.module+el8.5    2/10 
  验证    : mariadb-common-3:10.3.32-2.module+el8.5    3/10 
  验证    : mariadb-connector-c-3.1.11-2.el8_3.x86_    4/10 
  验证    : mariadb-connector-c-config-3.1.11-2.el8    5/10 
  验证    : mariadb-errmsg-3:10.3.32-2.module+el8.5    6/10 
  验证    : mariadb-gssapi-server-3:10.3.32-2.modul    7/10 
  验证    : mariadb-server-3:10.3.32-2.module+el8.5    8/10 
  验证    : mariadb-server-utils-3:10.3.32-2.module    9/10 
  验证    : perl-DBD-MySQL-4.046-3.module+el8.6.0+9   10/10 
已安装:
  mariadb-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64    
  mariadb-backup-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64
  mariadb-common-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64
  mariadb-connector-c-3.1.11-2.el8_3.x86_64                 
  mariadb-connector-c-config-3.1.11-2.el8_3.noarch          
  mariadb-errmsg-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64
  mariadb-gssapi-server-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64
  mariadb-server-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64
  mariadb-server-utils-3:10.3.32-2.module+el8.5.0+777+18007c86.x86_64
  perl-DBD-MySQL-4.046-3.module+el8.6.0+904+ef468285.x86_64 
完毕！
```

#### 2、启动服务

```
[root@pc1 mydir]# systemctl restart  mariadb
[root@pc1 mydir]# systemctl status  mariadb
● mariadb.service - MariaDB 10.3 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service;>
   Active: active (running) since Tue 2023-07-18 14:48:41 C>
     Docs: man:mysqld(8)
           https://mariadb.com/kb/en/library/systemd/
  Process: 14696 ExecStartPost=/usr/libexec/mysql-check-upg>
  Process: 14562 ExecStartPre=/usr/libexec/mysql-prepare-db>
  Process: 14537 ExecStartPre=/usr/libexec/mysql-check-sock>
 Main PID: 14665 (mysqld)
   Status: "Taking your SQL requests now..."
    Tasks: 30 (limit: 11046)
   Memory: 76.9M
   CGroup: /system.slice/mariadb.service
           └─14665 /usr/libexec/mysqld --basedir=/usr

7月 18 14:48:37 pc1.tedu.cn systemd[1]: Starting MariaDB 10>
7月 18 14:48:38 pc1.tedu.cn mysql-prepare-db-dir[14562]: In>
7月 18 14:48:41 pc1.tedu.cn mysqld[14665]: 2023-07-18 14:48>
lines 1-18/19 94%
```

#### 3、什么是数据库

**（1）、定义**

存放数据的仓库；

**（2）、数据库的基本操**

```mysql
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.001 sec)

MariaDB [(none)]> create database haha
    -> ;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| haha               |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.001 sec)
```

**（3）建立一个test数据库，使用数据库恢复恢复表格**

```mysql
MariaDB [(none)]> use test;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [test]> show tables;
+----------------+
| Tables_in_test |
+----------------+
| base           |
| location       |
+----------------+
2 rows in set (0.001 sec)

MariaDB [test]> 
```

**增：insert；**

```mysql
——insert      【表名】    values   【相关插入的数据 】  ；
```

**删：delete；**

```mysql
——delete    from   【表名】   where    【条件】；
```

**改：update；**

```mysql
——update       【表名】    set    【字段】     where   【条件】；
```

**查：select；**  

```mysql
—— select    【表字段】   from    【表名】{基本用法}；

——select     【表字段】   from    【表面】   where   【条件】    and/or   【另外条件】{带条件的查询}；
```



### 四、NTP时间同步

#### 1、装包

```
[root@pc1 ~]# yum -y install chrony
仓库 'app' 在配置中缺少名称，将使用 id。
仓库 'base' 在配置中缺少名称，将使用 id。
仓库 'myrpm' 在配置中缺少名称，将使用 id。
上次元数据过期检查：0:07:11 前，执行于 2023年07月18日 星期二 17时23分52秒。
软件包 chrony-4.1-1.el8.x86_64 已安装。
依赖关系解决。
无需任何处理。
完毕！
```

#### 2、修改配置文件

```Linux
[root@pc1 ~]# vim /etc/chrony.conf 、
[root@pc1 ~]# cat  /etc/chrony.conf 
# Use public servers from the pool.ntp.org project.
# Please consider joining the pool (http://www.pool.ntp.org/join.html).
#pool 2.pool.ntp.org iburst
# Record the rate at which the system clock gains/losses time.
driftfile /var/lib/chrony/drift
# Allow the system clock to be stepped in the first three updates
# if its offset is larger than 1 second.
makestep 1.0 3
# Enable kernel synchronization of the real-time clock (RTC).
rtcsync
# Enable hardware timestamping on all interfaces that support it.
#hwtimestamp *
# Increase the minimum number of selectable sources required to adjust
# the system clock.
#minsources 2
# Allow NTP client access from local network.
allow all
# Serve time even if not synchronized to a time source.
local stratum 10
# Specify file containing keys for NTP authentication.
keyfile /etc/chrony.keys
# Get TAI-UTC offset and leap seconds from the system tz database.
leapsectz right/UTC
# Specify directory for log files.
logdir /var/log/chrony
# Select which information is logged.
#log measurements statistics tracking
```



#### 3、重启服务

```stylus
[root@pc1 ~]# systemctl restart chrony
chronyd.service      chrony-wait.service
[root@pc1 ~]# systemctl restart chronyd
[root@pc1 ~]# systemctl status chronyd
● chronyd.service - NTP client/server
   Loaded: loaded (/usr/lib/systemd/system/chronyd.service;>
   Active: active (running) since Tue 2023-07-18 17:40:43 C>
     Docs: man:chronyd(8)
           man:chrony.conf(5)
  Process: 17032 ExecStartPost=/usr/libexec/chrony-helper u>
  Process: 17029 ExecStart=/usr/sbin/chronyd $OPTIONS (code>
 Main PID: 17031 (chronyd)
    Tasks: 1 (limit: 11046)
   Memory: 1.1M
   CGroup: /system.slice/chronyd.service
           └─17031 /usr/sbin/chronyd
7月 18 17:40:43 pc1.tedu.cn systemd[1]: Starting NTP client>
7月 18 17:40:43 pc1.tedu.cn chronyd[17031]: chronyd version>
7月 18 17:40:43 pc1.tedu.cn chronyd[17031]: Using right/UTC>
7月 18 17:40:43 pc1.tedu.cn systemd[1]: Started NTP client/>
...skipping...
● chronyd.service - NTP client/server
   Loaded: loaded (/usr/lib/systemd/system/chronyd.service;>
   Active: active (running) since Tue 2023-07-18 17:40:43 C>
     Docs: man:chronyd(8)
           man:chrony.conf(5)
  Process: 17032 ExecStartPost=/usr/libexec/chrony-helper u>
  Process: 17029 ExecStart=/usr/sbin/chronyd $OPTIONS (code>
 Main PID: 17031 (chronyd)
    Tasks: 1 (limit: 11046)
   Memory: 1.1M
   CGroup: /system.slice/chronyd.service
           └─17031 /usr/sbin/chronyd
7月 18 17:40:43 pc1.tedu.cn systemd[1]: Starting NTP client>
7月 18 17:40:43 pc1.tedu.cn chronyd[17031]: chronyd version>
7月 18 17:40:43 pc1.tedu.cn chronyd[17031]: Using right/UTC>
7月 18 17:40:43 pc1.tedu.cn systemd[1]: Started NTP client/>
lines 1-17/17 (END)
```



------

## 第十五天（容器基本）



### 一、Linux容器

#### 1、容器的分类

Linux 容器是一种轻量级的虚拟化技术，允许在单个 Linux 操作系统内运行多个独立的容器。它们提供了一种隔离和封装应用程序及其依赖项的方式，使得应用程序可以在独立的、相互隔离的环境中运行，而不会互相干扰。

以下是一些与 Linux 容器相关的关键技术和工具：

（1）Namespace（命名空间）：Linux 命名空间是一种隔离机制，用于隔离容器内的资源。常见的命名空间类型包括进程、网络、挂载点、用户等。命名空间允许容器中的进程只能看到和操作特定的资源，而不会影响到其他容器或主机系统。

（2）cgroups（控制组）：cgroups 是一种资源限制和优先级管理的机制，用于限制容器对系统资源的访问。通过 cgroups，可以为容器分配 CPU、内存、磁盘和网络等资源的配额，以确保容器之间资源的公平共享和隔离。

（3）Docker：Docker 是一个流行的容器化平台，使用 Linux 容器技术来简化应用程序的打包、分发和部署过程。它提供了一个高级的容器管理接口，使得创建、启动、停止和删除容器变得更加简单。同时，Docker 还提供了容器镜像的构建和共享功能。

（4）Podman：Podman 是一个与 Docker 类似的容器运行时工具，但它不依赖于守护进程。Podman 提供了与 Docker 兼容的命令行接口，可以用于管理容器和镜像。与 Docker 不同，Podman 运行容器时不需要运行守护进程，并且容器和镜像的管理是以用户权限直接进行的。

（5）Kubernetes：Kubernetes 是一个用于自动化部署、扩展和管理容器化应用程序的开源平台。它提供了一组高级功能，如自动容器编排、负载均衡、故障恢复和服务发现等，使得在大规模容器集群中运行和管理应用程序变得更加简单和可靠。

2、容器的

### 二、Linux容器管理

在Linux中管理容器，可以使用一些常见的工具和技术来实现。以下是一些常用的Linux容器管理工具和技术：

#### 1、Docker：

​		Docker是一个流行的容器化平台，提供了用于创建、管理和部署容器的工具和接口。使用Docker，可以构建和打包应用程序的镜像，并使用容器来运行镜像。Docker提供了命令行工具和API，用于管理容器的创建、启动、停止和删除，以及镜像的构建、推送和拉取等操作。

#### 2、Podman：

​		Podman是另一个常用的Linux容器运行时工具，与Docker类似。与Docker不同，Podman不需要运行守护进程，而是以用户权限直接管理容器。Podman提供了与Docker兼容的命令行接口，可以用于创建、启动、停止和删除容器，以及管理容器的存储卷、网络配置等。

#### 3、Kubernetes：

​		Kubernetes是一个开源的容器编排平台，用于自动化部署、扩展和管理容器化应用程序。它提供了丰富的功能，如容器编排、负载均衡、自动伸缩、故障恢复等。Kubernetes使用yaml文件来定义和管理应用程序的部署、服务和网络，可以通过kubectl命令行工具或者Kubernetes API进行管理。

#### 4、LXC / LXD：

​		LXC（Linux Containers）和LXD是用于管理和运行系统级容器的工具。LXC提供了对Linux内核命名空间和cgroups的封装，用于创建和管理容器。LXD是建立在LXC之上的高级容器管理器，提供了易于使用的命令行接口和API，用于管理容器的创建、启动、停止和删除等操作。

#### 5、systemd-nspawn：

​		systemd-nspawn是Systemd初始化系统的一部分，它提供了一种轻量级的容器管理机制。通过systemd-nspawn，可以在Linux系统中创建和管理容器，并提供与操作系统一致的启动和管理接口。

​		这些工具和技术能够帮助简化容器的创建、部署和管理，提供了高度的灵活性和可扩展性，从而使得在Linux上运行和管理容器更加方便和高效。具体选择哪种工具和技术取决于你的需求和偏好。

### 三、podman命令行 

Podman 是一个与 Docker 类似的容器运行时工具，提供了一组与 Docker 兼容的命令行接口。下面是一些常用的 Podman 命令行操作：

#### 1、显示容器列表：

```
podman ps
```

#### 2、创建并启动容器：

```
podman run --name my_container -d my_image:tag
```

#### 3、启动已创建的容器：

```
podman start my_container
```

#### 4、停止运行中的容器：

```
podman stop my_container
```

#### 5、进入容器内部：

```
podman exec -it my_container bash
```

#### 6、查看容器日志：

```
podman logs my_container
```

#### 7、删除容器：

```
podman rm my_container
```

#### 8、构建容器镜像：

```
podman build -t my_image:tag .
```

#### 9、导出容器为镜像：

```
podman export my_container -o my_image.tar
```

#### 10、导入镜像为容器：

```
podman import my_image.tar my_image:tag
```

#### 11、列出容器镜像列表：

```
podman images
```

除了上述命令，Podman 还提供了其他功能，如容器网络配置、数据卷管理、镜像推送和拉取、容器和镜像的保存与加载等。你可以通过 `podman --help` 命令来查看更多的命令和选项，或参考 Podman 的官方文档进行更详细的了解。

### 四、管理容器进阶

#### 1、自动创建容器镜像脚本

（1）创建脚本文件：

```
[root@pc2 ~]# cat yum.sh 
#/bin/bash
rm -rf /etc/yum.repos.d/*
echo '
[app]
baseurl=ftp://10.88.0.1/dvd/AppStream
gpgcheck=0

[base]
baseurl=ftp://10.88.0.1/dvd/BaseOS
gpgcheck=0' > /etc/yum.repos.d/dvd.repo
yum -y install net-tools vim bash-completion


```

（2）、创建Containerfile文件

```
[root@pc2 ~]# cat Containerfile 
FROM  localhost/rockylinux:8.6
COPY  yum.sh /opt
RUN   /opt/yum.sh
```

（3）、启动脚本

```
podman build -t myos:2.0 /root
```

#### 2、端口网页同时绑定

```
[root@pc2 /]# podman rm -f  nadweb 
0fd8ff279893de735fba563d69c180aa2d342398e46db4c89346e156d9a33b90
[root@pc2 /]# mkdir /webroot
[root@pc2 /]# echo wo shi niuniu > /webroot/index.html
[root@pc2 /]# podman run --name nadweb -p 80:80 -v /webroot:/var/www/html -itd localhost/
localhost/httpd:latest    localhost/myos:2.0
localhost/myos:1.0        localhost/rockylinux:8.6
[root@pc2 /]# podman run --name nadweb -p 80:80 -v /webroot:/var/www/html -itd localhost/
localhost/httpd:latest    localhost/myos:2.0
localhost/myos:1.0        localhost/rockylinux:8.6
[root@pc2 /]# podman run --name nadweb -p 80:80 -v /webroot:/var/www/html -itd localhost/httpd:latest 
0fb714536f1d38dcf4f8ec7c0a9ef89ab3546f8f75a106ff5a2ab4f5ae134221
[root@pc2 /]# curl 192.168.88.2
wo shi niuniu
```

#### 3、容器之光联系

```stylus
[root@pc2 system]# cd /lib/systemd/system
[root@pc2 system]# podman ps -a 
CONTAINER ID  IMAGE                   COMMAND               CREATED         STATUS             PORTS               NAMES
0fb714536f1d  localhost/httpd:latest  /usr/sbin/httpd -...  28 minutes ago  Up 28 minutes ago  0.0.0.0:80->80/tcp  nadweb
[root@pc2 system]# podman generate systemd --name nadweb --files 
/lib/systemd/system/container-nadweb.service
[root@pc2 system]# vim container-
container-getty@.service  container-nadweb.service
[root@pc2 system]# vim container-nadweb.service 
[root@pc2 system]# systemctl daemon-reload 
[root@pc2 system]# podman stop nadweb 
nadweb
[root@pc2 system]# podman ps -a
CONTAINER ID  IMAGE                   COMMAND               CREATED         STATUS                     PORTS               NAMES
0fb714536f1d  localhost/httpd:latest  /usr/sbin/httpd -...  31 minutes ago  Exited (0) 13 seconds ago  0.0.0.0:80->80/tcp  nadweb
[root@pc2 system]# systemctl enable container-nadweb.service 
Created symlink /etc/systemd/system/default.target.wants/container-nadweb.service → /usr/lib/systemd/system/container-nadweb.service.
[root@pc2]reboot
```





#### 邮件

yum -y install mailx

mail  -s  'test01'   -r   yg    xln

mail    -u   xln

> N  1  yg@server.tedu.cn    Fri   Sep   18  17:24  18/510
>
> &  1  
>
> &  quit

非交互式

echo  123456  |   mail   -s    'test02'    -r    yg   xln

mail    -u     xln







 

------

## 第十六天（关于网络特殊服务器的搭建）

php、apache、lamnp





## 第十七天（关于网络）

### 一、关于网络的基础知识

#### 1、基本知识

​		网络是指将多个独立的计算机系统通过通信链路相互连接起来，以实现数据和信息的交换与共享的系统。网络的基础知识包括以下内容：

（1）、网络拓扑：网络拓扑是指网络中各个节点之间的连接方式和布局。常见的拓扑结构有总线型、星型、环型、树型和网状等。

（2）、网络协议：网络协议是指规定计算机网络中通信实体之间传输数据所遵循的规则和约定。常见的协议有TCP/IP协议套件、HTTP协议、FTP协议等。

（3）、IP地址和子网掩码：IP地址是互联网上的每个设备在网络中的唯一标识符，用于实现不同设备之间的通信。而子网掩码用于划分网络中的子网。

（4）、端口：端口是指网络通信中的进程或应用程序与网络之间进行交互的接口。每个端口都有一个唯一的数字标识，常见的有HTTP端口80、FTP端口21等。

（5）、路由器和交换机：路由器是连接不同网络的设备，负责将数据包从源地址发送到目标地址。而交换机是在局域网内连接多个设备的网络设备，提供更高的数据传输速率。

（6）、DNS：DNS（Domain Name System，域名系统）是用于将域名转换为对应IP地址的系统，实现域名和IP地址之间的映射。

（7）、网络安全：网络安全是指保护网络系统和数据不受非法侵入、破坏、窃取或干扰的技术和管理措施，包括防火墙、加密、访问控制等。

#### 2、tcp/ip主要内容

​		TCP/IP（Transmission Control Protocol/Internet Protocol）是一组用于互联网通信的协议。它由多个协议组成，提供了可靠的、面向连接的通信以及数据在网络中的传输和路由。下面是TCP/IP协议主要的内容：

（1）、IP（Internet Protocol）：IP协议是TCP/IP协议族中的核心协议，用于定义数据在网络中的传输方式和寻址规则。它负责将数据分割成适当的数据包，并通过网络进行传输。IP地址用于标识网络中的每个设备。

（2）、TCP（Transmission Control Protocol）：TCP协议是一种面向连接的、可靠的传输协议。它在数据传输前建立一个连接，确保数据的完整性和可靠性。TCP使用序列号来重新排序数据包，并使用确认和重传机制来处理丢失的数据包。

（3）、UDP（User Datagram Protocol）：UDP协议是一种无连接的传输协议，相比TCP更轻量级。它不提供可靠性保证，因此速度更快，适用于传输实时数据和音频/视频流等不需要保证可靠性的场景。

（4）、DNS（Domain Name System）：DNS协议用于将域名转换为对应的IP地址。它通过分布式的域名服务器层次结构来实现域名和IP地址之间的映射，使用户可以使用便于记忆的域名来访问互联网资源。

（5）、DHCP（Dynamic Host Configuration Protocol）：DHCP协议用于自动分配和管理IP地址和其他网络配置信息。它允许计算机在加入网络时自动获取IP地址、子网掩码、网关等信息，简化了网络配置过程。

（6）、ICMP（Internet Control Message Protocol）：ICMP协议用于在IP网络中传递错误和控制信息。它用于网络故障诊断、错误报告等，常见的应用是ping命令。

（7）、HTTP（Hypertext Transfer Protocol）：HTTP协议是在TCP/IP协议之上的应用层协议，用于在Web浏览器和Web服务器之间传输超文本文档。它定义了客户端和服务器之间的请求和响应的格式。

​		以上是TCP/IP协议的主要内容，它们共同构成了现代互联网的通信基础。这些协议在网络通信中发挥着重要的作用，实现了可靠的数据传输和互联网资源的访问。

#### 3、iso七层模型

​		ISO七层模型（ISO/OSI七层参考模型）是国际标准化组织制定的网络协议体系结构，用于描述计算机网络中不同层级之间的通信和功能。每个层级负责特定的功能，并通过接口与相邻层级进行通信。以下是ISO七层模型的介绍：

（1）、物理层（Physical Layer）：物理层是ISO七层模型的最底层，负责定义电气、物理接口和传输介质等物理特性。它处理比特流的传输，如传输速率、电压等。

（2）、数据链路层（Data Link Layer）：数据链路层建立在物理层之上，提供了可靠的点对点数据传输，以及错误检测和纠正的功能。它将比特流分割为帧，并负责帧的传输。

（3）、网络层（Network Layer）：网络层负责在不同网络之间进行路由选择、转发和分组交换。它使用IP协议确定数据包的传输路径，并处理数据包的寻址和路由。

（4）、传输层（Transport Layer）：传输层提供端到端的可靠数据传输服务。最常用的传输层协议是TCP（Transmission Control Protocol）和UDP（User Datagram Protocol），它们负责分段、重组和数据的传输确认。

（5）、会话层（Session Layer）：会话层负责建立、管理和终止不同计算机之间的会话连接。它处理会话的开始、中断、重启和同步等操作。

（6）、表示层（Presentation Layer）：表示层处理数据的格式和表示，负责数据的编解码、数据压缩、数据加密和解密等操作，以保证应用程序之间的互操作性。

（7）、应用层（Application Layer）：应用层是ISO七层模型的最高层，提供直接面向用户的应用服务。它包括各种应用协议，如HTTP、FTP、SMTP等，用于实现不同的网络应用。

​		ISO七层模型提供了一个通用的框架，用于理解和描述计算机网络中不同层级的功能和通信。不同层级之间的接口和协作使得网络中的各个部分能够互相配合工作，实现可靠的数据传输和网络服务。

### 二、华为模拟器的使用

#### 1、试图的调换

（1）、用户视图：进入系统视图；

```stylus
<Huawei>system-view 
Enter system view, return user view with Ctrl+Z.
[Huawei]
```

（2）、系统视图：进入接口视图；

```stylus
[Huawei]interface Ethernet 0/0/1
[Huawei-Ethernet0/0/1]
```

（3）、接口视图：可以对对应的接口进行配置；

（4）、协议视图：

使用quit可以返回上一层；

#### 2、基本操作

在基本视图：

（1）修改名字：

```stylus
<Huawei>system-view 
Enter system view, return user view with Ctrl+Z.	
[Huawei]sysname sw1
[sw1]
```

（2）关闭日志：

```stylus
[sw1]undo info-center enable
Info: Information center is disabled.
[sw1]
```

（3）查看当前配置：

```stylus
[sw1]display current-configuration 
#
sysname sw1
#
undo info-center enable
#
cluster enable
ntdp enable
ndp enable
#
drop illegal-mac alarm
#
diffserv domain default
#
drop-profile default
#
aaa
 authentication-scheme default
 authorization-scheme default
 accounting-scheme default
 domain default
 domain default_admin
 local-user admin password simple admin
 local-user admin service-type http
#
```

（4）查看版本型号

```stylus
[sw1]display version 
Huawei Versatile Routing Platform Software
VRP (R) software, Version 5.110 (S3700 V200R001C00)
Copyright (c) 2000-2011 HUAWEI TECH CO., LTD
Quidway S3700-26C-HI Routing Switch uptime is 0 week, 0 day, 1 hour, 17 minutes
```

（5）创建用户，修改密码

```stylus
<sw1>system-view 
Enter system view, return user view with Ctrl+Z.
[sw1]aaa	
[sw1-aaa]local-user test01 password simple 123        //创建test01账户，并设置明文密码；
Info: Add a new user.
[sw1-aaa]local-user test01 password cipher 123        //设置隐藏密码；
[sw1-aaa]quit
[sw1]user-interface console 0                            //进入用户控制台接口
[sw1-ui-console0]authentication-mode aaa
[sw1-ui-console0] User interface con0 is available          //激活配置
Please Press ENTER.
Login authentication
Username:test01
Password:
<sw1>
```

（6）save

#### 3、交换机广播、转发

广播：向除数据来源接口之外的所有接口发送寻找目标主机的信息；

转发：通过mac地址表，一对一转发数据；

更新：超过300秒，mac地址表信息会刷新；

查看mac接听转发的过程：

```stylus
<sw1>display mac-address

MAC address table of slot 0:
-------------------------------------------------------------------------------

MAC Address    VLAN/       PEVLAN CEVLAN Port            Type      LSP/LSR-ID  

               VSI/SI                                              MAC-Tunnel  
-------------------------------------------------------------------------------

5489-98aa-6795 1           -      -      Eth0/0/3        dynamic   0/-         

5489-98fd-06da 1           -      -      Eth0/0/1        dynamic   0/-         
-------------------------------------------------------------------------------

Total matching items on slot 0 displayed = 2 
```





## 十七天（关于交换机）



### 一、vlan

#### 1、关于vlan

（1）、vlan作用

广播控制

增加安全

提高带宽利用

降低数据传递延迟

（2）、vlan概念

#### 2、vlan操作

（1）、创建vlan

（2）、vlan划分

（3）、对端口进行Turk处理   （中继链路）

```stylus
[Huawei]interface Ethernet 0/0/7
[Huawei-Ethernet0/0/7]undo shutdown 
[Huawei-Ethernet0/0/7]port link-type trunk 
[Huawei-Ethernet0/0/7]port trunk allow-pass vlan all 
```

(4)、链路聚合 

```stylus
[Huawei]interface Eth-Trunk 1
[Huawei-Eth-Trunk1]trunkport Ethernet 0/0/7 0/0/8
Info: This operation may take a few seconds. Please wait for a moment...done.
[Huawei-Eth-Trunk1]port link-type trunk 
[Huawei-Eth-Trunk1]port trunk allow-pass vlan all 
```

达到的效果：

```stylus
[Huawei]display vlan
The total number of vlans is : 3
--------------------------------------------------------------------------------
U: Up;         D: Down;         TG: Tagged;         UT: Untagged;
MP: Vlan-mapping;               ST: Vlan-stacking;
#: ProtocolTransparent-vlan;    *: Management-vlan;
--------------------------------------------------------------------------------
VID  Type    Ports                                                          
--------------------------------------------------------------------------------
1    common  UT:Eth0/0/1(U)     Eth0/0/2(U)     Eth0/0/9(D)     Eth0/0/10(D)    
                Eth0/0/11(D)    Eth0/0/12(D)    Eth0/0/13(D)    Eth0/0/14(D)    
                Eth0/0/15(D)    Eth0/0/16(D)    Eth0/0/17(D)    Eth0/0/18(D)    
                Eth0/0/19(D)    Eth0/0/20(D)    Eth0/0/21(D)    Eth0/0/22(D)    
                GE0/0/1(D)      GE0/0/2(D)      Eth-Trunk1(U)                   
2    common  UT:Eth0/0/3(U)     Eth0/0/4(U)                                     
             TG:Eth-Trunk1(U)                                                   
3    common  UT:Eth0/0/5(U)     Eth0/0/6(U)                                     
             TG:Eth-Trunk1(U)                                                   
VID  Status  Property      MAC-LRN Statistics Description      
--------------------------------------------------------------------------------
1    enable  default       enable  disable    VLAN 0001                         
2    enable  default       enable  disable    VLAN 0002                         
3    enable  default       enable  disable    VLAN 0003   
```



### 二、ensp基本命令

ENSParadigm（ENSP）是华为企业网络仿真平台，用于设计、配置和模拟企业网络。以下是一些ENSParadigm的基本常用命令：

#### 1、设备管理命令：

- `display current-configuration`：显示当前设备的配置信息。
- `display interface brief`：显示接口的基本信息，如接口状态、IP地址等。
- `display ip interface`：显示接口的IP配置信息。
- `display vlan`：显示VLAN的配置信息。

#### 2、配置命令：

- `system-view`：进入系统视图，开始进行配置。
- `interface <interface>`：进入接口视图，对指定接口进行配置。
- `vlan <vlan-id>`：进入VLAN视图，对指定VLAN进行配置。
- `ip address <ip-address> <subnet-mask>`：配置接口的IP地址和子网掩码。
- `interface <interface> port default vlan <vlan-id>`：配置接口的默认VLAN。

#### 3、保存和恢复配置命令：

- `save`：保存当前配置到设备的配置文件中。
- `startup saved-configuration`：设置设备下次启动时加载的配置文件。
- `reset saved-configuration`：清除设备下次启动时加载的配置文件。

#### 4、模拟器相关命令：

- `router-set password`：设置模拟器启动时的特权密码。
- `router-reset password`：重置模拟器的特权密码。
- `simulate`：启动模拟器并开始仿真。

请注意，以上只是一些常用命令示例，ENSParadigm具有更多的功能和命令，请根据具体的需求和文档结合使用。



### 三、网络层

#### 1、网络层的功能

**（1）、router配置**

添加，为端口配置IP地址；

为计算机配置网关；

实现不同网段互通；

**（2）、路由表**

直连路由：设备开启，配置好IP，自动产生；

静态路由：

IP   router-static   目的网关  子网掩码   下一跳地址；

**查询路由表：**

```stylus
<Huawei>display ip routing-table | include 24
Route Flags: R - relay, D - download to fib
------------------------------------------------------------------------------
Routing Tables: Public
         Destinations : 10       Routes : 10       
Destination/Mask    Proto   Pre  Cost      Flags NextHop         Interface
192.168.1.0/24  Direct  0    0           D   192.168.1.254   GigabitEthernet0/0/0
192.168.2.0/24  Direct  0    0           D   192.168.2.1     GigabitEthernet0/0/1
```

**查询IP：**

```stylus
<Huawei>display ip interface brief 
*down: administratively down
^down: standby
(l): loopback
(s): spoofing
The number of interface that is UP in Physical is 3
The number of interface that is DOWN in Physical is 1
The number of interface that is UP in Protocol is 3
The number of interface that is DOWN in Protocol is 1
Interface                         IP Address/Mask      Physical   Protocol  
GigabitEthernet0/0/0              192.168.1.254/24     up         up        
GigabitEthernet0/0/1              192.168.2.1/24       up         up        
GigabitEthernet0/0/2              unassigned           down       down      
NULL0                             unassigned           up         up(s)     
```

#### 2、网络层协议

ARP协议：



## 第十八天（关于路由）

### 一、三层交换机

#### 1、概述

二层交换机+路由器

#### 2、操作

#### 3、三层交换机配置IP思路

（1）创建vlan；

（2）进入vlan的虚拟接口配置IP；

（3）把打算配置IP的真实接口加入上述vlan；

#### 4、动态路由（ospf）

（1）、概念

基于某种路由协议实现；

自动学习路由；

注意 在路由宣告过程中所加的是反掩码；

### 二、传输层

#### 1、协议

tcp：

udp：

#### 2、端口号

**（1）、tcp传数据**

21   ftp        

22   ssh

25   smtp

53    dns

80     http

443    https

**（2）、udp传数据**

69     tftp

53     dns

123     ntp

### 三、acl控制

#### 1、配置acl策略

拒绝访问设置：

```stylus
[Huawei]acl 2000
[Huawei-acl-basic-2000]rule ?
  INTEGER<0-4294967294>  ID of ACL rule
  deny                   Specify matched packet deny
  permit                 Specify matched packet permit	
[Huawei-acl-basic-2000]rule deny source 192.168.2.1 0.0.0.0
[Huawei-acl-basic-2000]display this 
[V200R003C00]
acl number 2000  
 rule 5 deny source 192.168.2.1 0 
#
return
[Huawei-acl-basic-2000]quit
[Huawei]interface GigabitEthernet 0/0/1t
[Huawei-GigabitEthernet0/0/1]traffic-filter inbound acl 2000
```

放行配置：

```stylus
[Huawei]acl 2001
[Huawei-acl-basic-2001]rule permit source 192.168.2.1 0
[Huawei-acl-basic-2001]
```

（1）创建acl列表；

（2）配置acl 策略；

（3）注意使用反掩码；

（4）注意当反掩码为四个255时，带表所有人；

（5）acl策略配置完成后注意要在端口激活；





## 第十九天（关于acl的高级配置）

### 一、高级acl配置

#### 1、关于ftp

```stylus
[Huawei]acl 3000
[Huawei-acl-adv-3000]rule deny tcp source 192.168.2.1 0 destination 192.168.1.1 
0 destination-port eq 21
```

#### 2、关于dns，禁止192.168.2 网段联通192.168.1.1

```stylus
[Huawei]acl 3000
[Huawei-acl-adv-3000]rule deny tcp source 192.168.2.0 0.0.0.255 destination 192.168.1.1 
0 destination-port eq 53
[Huawei-acl-adv-3000]rule deny udp source 192.168.2.0 0.0.0.255 destination 192.168.1.1 
0 destination-port eq 53
```

### 二、nat

#### 1、nat的作用

通过将

#### 2、静态nat转换  ——一对一双向通信

```stylus
[Huawei]interface GigabitEthernet 0/0/0
[Huawei-GigabitEthernet0/0/0]nat static global 100.0.0.2 inside 192.168.2.1
```

将私有网络地址进行静态nat转换为外网地址；

#### 3、easy  IP——多对一单向通信

同时使用acl和

```stylus
[Huawei]acl 2000	
[Huawei-acl-basic-2000]rule permit source 192.168.2.0 0.0.0.255 
[Huawei-acl-basic-2000]quit
[Huawei]interface GigabitEthernet 0/0/0
[Huawei-GigabitEthernet0/0/0]display this 
[V200R003C00]
interface GigabitEthernet0/0/0
 ip address 100.0.0.1 255.0.0.0 
 nat static global 100.0.0.2 inside 192.168.2.1 netmask 255.255.255.255
 nat static global 100.0.0.3 inside 192.168.2.2 netmask 255.255.255.255
#
return
[Huawei-GigabitEthernet0/0/0]un	
[Huawei-GigabitEthernet0/0/0]undo  nat static global 100.0.0.2 inside 192.168.2.1 netmask 255.255.255.255
[Huawei]interface GigabitEthernet 0/0/0
[Huawei-GigabitEthernet0/0/0]display this 
[V200R003C00]
#
interface GigabitEthernet0/0/0
 ip address 100.0.0.1 255.0.0.0 
 nat static global 100.0.0.3 inside 192.168.2.2 netmask 255.255.255.255
#
return
[Huawei-GigabitEthernet0/0/0]undo  nat static global 100.0.0.3 inside 192.168.2.2 netmask 255.255.255.255
[Huawei-GigabitEthernet0/0/0]nat outbound 2000
```





## 第二十天 （）

### 一、VRRP负载均衡配置

#### 1、在sw1上配置

```stylus
[sw1]interface Vlanif 1	
[sw1-Vlanif1]vrrp vrid 1 virtual-ip 192.168.1.254 	
[sw1-Vlanif1]vrrp vrid 1 priority 105
[sw1-Vlanif1]quit
[sw1]interface Vlanif 2
[sw1-Vlanif2]vrrp vrid 2 virtual-ip 192.168.2.254
```

#### 2、在sw2上配置

```stylus
[sw2]interface Vlanif 1
[sw2-Vlanif1]vrrp vrid 1 virtual-ip 192.168.1.254 
[sw2-Vlanif1]quit
[sw2]interface Vlanif 2
[sw2-Vlanif2]vrrp vrid 2 virtual-ip 192.168.2.254
[sw2-Vlanif2]vrrp vrid 2 priority 105
[sw2-Vlanif2]
```

### 二、子网划分

#### 1、作用

将一个网段划分成多个网段；

#### 2、划分步骤

**（1）准备好要划分的网段；**

192.168.1.0   /24

11111111.11111111.11111111.10000000

​                                 255.255.255.10000000

**（2）根据公式计算**

2 的n次方=要划分的网段

n是借用子网掩码主机位的个数；

**（3）计算网段**

​     192.168.1.00000000                            第一个网段

255.255.255.100000000                 255.255.255.128              子网掩码

192.168.1.0~192.168.1.127       完整范围

192.168.1.1~192.168.1.126       可用范围



​     192.168.1.10000000                            第二个网段

255.255.255.100000000                255.255.255.128       

192.168.1.128~192.168.1.255       完整范围

192.168.1.129~192.168.1.254       可用范围





------

# 第二阶段





## 第一天(脚本基本概念)

### 一、shell脚本

#### 1、概念

注意：在脚本中，不可以使用交互式命令；

交互式：人工干预，智能化程度高，逐条 解释执行，效率低

非交互式：需要提前设计，智能化难度大；批量执行，效率高；方便在后台悄悄执行；

#### 2、bash的基本特性

快捷键、tab键补全；

历史命令；

命令别名；

标准输入输出；

重定向、管道操作；

### 二、shell脚本规范

#### 1、声明解释器

#！/bin/bash

#### 2、编写注释

解释脚本作用；作者信息；变量作用；

#号开头；                     单行注释

/* 注释内容 */              多行注释

#### 3、脚本的执行方式 

（1）使用脚本执行；

（2）使用解释器执行，无需执行权限；    会新开启子进程；

（3）使用source命令执行；                       不会新开子进程；

### 三、脚本练习

#### 1、使用脚本搭建yum源

```stylus
[root@tw /]# vim test02.sh
[root@tw /]# umount /abc
[root@tw /]# bash  test02.sh
mkdir: 无法创建目录 “/abc”: 文件已存在
mount: /abc: WARNING: device write-protected, mounted read-only.
仓库 'a' 在配置中缺少名称，将使用 id。
仓库 'b' 在配置中缺少名称，将使用 id。
a                                                                               76 MB/s | 7.8 MB     00:00
b                                                                               75 MB/s | 2.6 MB     00:00
上次元数据过期检查：0:00:01 前，执行于 2023年07月27日 星期四 23时28分42秒。
仓库ID            : a
仓库名称          : a
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L, R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月15日 星期日 17时01分50秒
Repo-pkgs          : 6,549
Repo-available-pkgs: 5,339
Repo-size          : 8.3 G
Repo-baseurl       : file:///abc/AppStream
Repo-expire        : 172,800 秒 （最近 2023年07月27日 星期四 23时28分41秒）
仓库文件名      : /etc/yum.repos.d/abc.repo
仓库ID            : b
仓库名称          : b
Repo-revision      : 8.6
Repo-distro-tags      : [cpe:/o:rocky:rocky:8]:  ,  , 8, L, R, c, i, k, n, o, u, x, y
Repo-updated       : 2022年05月15日 星期日 16时59分01秒
Repo-pkgs          : 1,716
Repo-available-pkgs: 1,714
Repo-size          : 1.3 G
Repo-baseurl       : file:///abc/BaseOS
Repo-expire        : 172,800 秒 （最近 2023年07月27日 星期四 23时28分42秒）
仓库文件名      : /etc/yum.repos.d/abc.repo
软件包总数：8,265
```

> 脚本内容
>
> ```shell
> [root@tw /]# cat test02.sh
> #!/bin/bash
> #搭建yum源仓库
> rm -rf /etc/yum.repos.d/*.repo
> mkdir /abc
> mount /dev/cdrom /abc
> touch /etc/yum.repos.d/abc.repo
> echo "[a]
> baseurl=file:///abc/AppStream
> gpgcheck=0
> [b]
> baseurl=file:///abc/BaseOS
> gpgcheck=0 " > /etc/yum.repos.d/abc.repo
> yum repoinfo
> ```

#### 2、编写脚本，安装ftp服务，并开启开机自启

```stylus
[root@tw /]# vim test03.sh
[root@tw /]# bash test03.sh
仓库 'a' 在配置中缺少名称，将使用 id。
仓库 'b' 在配置中缺少名称，将使用 id。
上次元数据过期检查：0:08:45 前，执行于 2023年07月27日 星期四 23时28分42秒。
依赖关系解决。
===============================================================================================================
 软件包                   架构                     版本                              仓库                 大小
===============================================================================================================
安装:
 vsftpd                   x86_64                   3.0.3-35.el8                      a                   180 k
事务概要
===============================================================================================================
安装  1 软件包
总计：180 k
安装大小：347 k
下载软件包：
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
  准备中  :                                                                                                1/1
  安装    : vsftpd-3.0.3-35.el8.x86_64                                                                     1/1
  运行脚本: vsftpd-3.0.3-35.el8.x86_64                                                                     1/1
  验证    : vsftpd-3.0.3-35.el8.x86_64                                                                     1/1
已安装:
  vsftpd-3.0.3-35.el8.x86_64
完毕！
Created symlink /etc/systemd/system/multi-user.target.wants/vsftpd.service → /usr/lib/systemd/system/vsftpd.service.
[root@tw /]# systemctl status vsftpd
● vsftpd.service - Vsftpd ftp daemon
   Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2023-07-27 23:37:29 EDT; 31s ago
 Main PID: 7413 (vsftpd)
    Tasks: 1 (limit: 23329)
   Memory: 580.0K
   CGroup: /system.slice/vsftpd.service
           └─7413 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf
7月 27 23:37:29 tw.tedu.cn systemd[1]: Starting Vsftpd ftp daemon...
7月 27 23:37:29 tw.tedu.cn systemd[1]: Started Vsftpd ftp daemon.
```

> 脚本内容
>
> ```shell
> [root@tw /]# cat test03.sh
> #!/bin/bash
> yum -y  install    vsftpd
> systemctl restart  vsftpd
> systemctl  enable  vsftpd
> ```

注意：  >     重定向标准信息；

​             2>     重定向错误信息 ；   （收集错误信息）。

​			 &>    /dev/null     撤销所有输出字符；

#### 3、什么是变量

**（1）、以固定的名称存放**

1）echo $**0**                    #脚本的名称

2）echo $**1**                    #第一个参数

3）echo $**2**                    #第二个参数

4）echo $*****                    #所有参数

5）echo $#                    #所有参数的个数

6）echo $$                    #当前进程的进程号

7）echo $**?**                    #上一个程序的返回状态码

**（2）、特殊符号意义：**

“  ”     界定范围   ；

‘   ’     界定范围，屏蔽特殊符号的功能；

``    反撇号     将命令执行的标准输出作为字符串存储；

#### 4、read

（1）功能

通过键盘 获取变量值；

```stylus
[root@tw /]# vim test05.sh 
[root@tw /]# bash test05.sh 
Please enter the username you want to create:px
please enter your user password:123                     // stty   -echo    屏蔽回显
更改用户 px 的密码 。                                      //  stty   echo    恢复回显
passwd：所有的身份验证令牌已经成功更新。
```

> 简本内容：
>
> ```stylus
> [root@tw /]# cat test05.sh 
> #!/bin/bash
> #创建用户tom配置密码123456
> read -p "Please enter the username you want to create:" x
> useradd  $x
> read -p "please enter your user password:" n
> echo $n | passwd  --stdin  $x
> ```

（2）创建全局变量

**export：**子进程，父进程都可以使用；（注意要在父进程使用）



#### 5、加减乘除求模取余

（1）使用  $[ ]  或者  $((  ))  进行计算：

​      、 +、  -   、  * 、   /     、 %  

（2）let用法

带计算的定义变量：

```stylus
[root@tw ~]# let a=1+1
[root@tw ~]# echo $a
2
```

自增自减操作：

```stylus
[root@tw ~]# a=5
[root@tw ~]# let a+=2
[root@tw ~]# echo $a
7
[root@tw ~]# 
```

**注意：**let、expr只能用于整数；

（3）bc用法

可以用于小数；

scale定义小数点后是位数；

```stylus
[root@tw ~]# echo "scale=3;10/3" | bc
3.333
[root@tw ~]# 
```

​	

------

## 第二天（运算符以及条件判断）



### 一、条件测试

#### 1、格式

test      表达式

[  表达式  ]

#### 2、内容

（1）字符串判断；

== ：等于   

!= ：不等于

```shell
[root@localhost /]# a==1
[root@localhost /]# b==2
[root@localhost /]# [ a == b ]
[root@localhost /]# echo $?
1
[root@localhost /]# [ a != b ]
[root@localhost /]# echo $?
0
```

-z ：判断变量是否为空；为空则表示对；

! -z（-n）：判断变量非空；

```shell
[root@localhost /]# [ -z $a ]
[root@localhost /]# echo $?
0
```

（2）逻辑符

&&：与     a&&b  （a成功则继续执行b，否则不执行）；

||：或       a||b  （a成功，则不许要执行b，表示这项表达式为真）；

```stylus 
[root@localhost opt]# touch a b c
[root@localhost opt]# ls a || ls b || ls c
a
[root@localhost opt]# ls a && ls b && ls c
[1] 6137
a
b
c
```

（3）、数字判断字符

-eq：等于；

-ne：不等于；

-gt：大于；

-ge：大于等于；

-lt：小于；

-le：小于等于；

（4）对文件判断

-e：判断文件是否存在，不关心 类型；

-f：判断文件是否存在，文件必须是普通文件；

-d：判断文件是否存在，文件是目录；

```stylus
[root@localhost opt]# touch a
[root@localhost opt]# mkdir ab
[root@localhost opt]# [ -e /opt/a ]
[root@localhost opt]# echo $?
0
[root@localhost opt]# [ -f /opt/a ]
[root@localhost opt]# echo $?
0
[root@localhost opt]# [ -d /opt/a ]
[root@localhost opt]# echo $?
1
[root@localhost opt]# [ -d /opt/ab ]
[root@localhost opt]# echo $?
0
[root@localhost opt]# [ -f /opt/ab ]
[root@localhost opt]# echo $?
1
```

-r：当前用户是否有读权限；

-w：当 前用户是否有写权限；

-x：当前用户有么执行权限（文件）或者进入权限（目录）；

### 二、基本脚本的实现

#### 1、检测系统，并发送邮件

```shell
[root@localhost opt]# cat youjian.sh 
#!/bin/bash
x=$(cat /etc/passwd | wc -l) 
[ $x -gt 46 ]  && echo "账户新增用户，请注意急时查看！"  | mail -s test root
[root@localhost opt]# 
```

#### 2、if分支语句

**（1）单分支**

if  条件测试；then

指令1

fi

```stylus
[root@localhost opt]# vim test02.sh
[root@localhost opt]# bash test02.sh 
我是管理员
ok
```

```shell
[root@localhost opt]# cat test02.sh 
#!/bin/bash
if [ $UID -eq 0 ];then
	echo "我是管理员"
	echo "ok"
fi
[root@localhost opt]# 
```

练习：

检测/if_test/cdrom目录，若不存在则创建；

```shell
[root@localhost opt]# vim test03.sh
[root@localhost opt]# cat test03.sh 
#!/bin/bash
dir=/if_test/cdrom
if [ ! -d $dir ];then
	mkdir -p  $dir    # 创建多级目录；
fi
[root@localhost opt]# bash test03.sh 
[root@localhost opt]# ls /
bin   dev  home     lib    media  opt   root  sbin  sys  usr
boot  etc  if_test  lib64  mnt    proc  run   srv   tmp  var
```

**（2）双分支**

**结构：**

if  条件测试；then

指令1

else

指令2

fi

```shell
[root@localhost opt]# vim test02.sh 
[root@localhost opt]# bash test02.sh 
我是管理员
ok
[root@localhost opt]# cat test02.sh 
#!/bin/bash
if [ $UID -eq 0 ];then
	echo "我是管理员"
	echo "ok"
else
	echo "我不是管理员"
fi
[root@localhost opt]# su tw
[tw@localhost opt]$ bash test02.sh 
我不是管理员
```

练习：

注意：ping   127.0.0.1 -c   3    -i  1  -W  1：（3为次数，1为1秒，-W表示ping不通时1秒后反馈信息）；

```shell
[root@localhost opt]# vim test04.sh
[root@localhost opt]# cat test04.sh 
#!/bin/bash
ping 192.168.88.5 -c 2 -i 0.2 -W 1 &> /dev/null
if [ $? -eq 0 ];then
	echo "通了"
else
	echo "不通"
fi
[root@localhost opt]# bash test04.sh 
通了
```

**（3）多分支**

结构：

if  条件测试；then

指令1

elif   条件测试；then

指令2

...

fi

```shell
[root@localhost opt]# vim test05.sh
[root@localhost opt]# bash test05.sh 
上次月考多少分：99
优秀！
[root@localhost opt]# bash test05.sh 
上次月考多少分：88
良好！
[root@localhost opt]# bash test05.sh 
上次月考多少分：77
良好！
[root@localhost opt]# bash test05.sh 
上次月考多少分：66
加油！
[root@localhost opt]# bash test05.sh 
上次月考多少分：55
晚上别吃饭了！
[root@localhost opt]# bash test05.sh 
上次月考多少分：1000
你真牛批！！
[root@localhost opt]# bash test05.sh 
上次月考多少分：-2
你真牛批！！
[root@localhost opt]# cat test05.sh 
#!/bin/bash
read -p "上次月考多少分：" a
if [ $a -ge 90 ] && [ $a -le 100 ];then
	echo "优秀！"
elif [ $a -ge 70 ] && [ $a -lt 90 ];then
	echo "良好！"
elif [ $a -ge 60 ] && [ $a -lt 70 ];then
	echo "加油！"
elif [ $a -ge 0 ] && [ $a -lt 60 ];then
	echo "晚上别吃饭了！"
else
	echo  "你真牛批！！"
fi
```

#### 3、循环（while 、for）

（1）、for循环(适合有次数的循环)

for   变量名  in 值

do

任务列表

done

```shell
[root@localhost opt]# cat test06.sh 
#!/bin/bash
for i in 1 2 3 4       //{1..100}表连续;     
	do  
		echo abc
		echo $i
	done
[root@localhost opt]# bash test06.sh 
abc
1
abc
2
abc
3
abc
4
```

（2）while 

while   【条件】

do

执行语句

done

注意：进入死循环时可以用CTRL +  C 结束；

### 三、总结

#### 1、关于运算符号

（1）文件

-e (是否存在，无关类型)      -f（是否存在，文件类型）   -d（是否存在，目录类型）  r（是否有读权限）  w（是否有写入权限）x（是否有执行或进入权限）

（2）字符串

&&  （与，两个都满足为真）    || （或，满足其中一个为真） ==（等于）  ！=（不等于）   -z（判断 是否为空）   ！ -z（是否为非空）

 -n（是否为非空）

（3）数值

  -eq（相等）  -ge（大于等于）  -gt（大于） -le（小于等于）  -lt（小于）  -ne（不等于）

#### 2、关于命令的用法

（1）ping

ping   -c   【指定ping次数】  -i 【指定每次ping的时间】  -W 【ping不通时的反馈时间】   （IP地址）；

（2）判断语法

if（单分支）  if（双分支）  if（多分支）

（3）循环语法

for（for  i   in   字段  do   执行语句  done）

while（死循环结构，满足某个条件，一直循环，知道条件不满足）

#### 3、课后习题

（1）运用条件测试操作，检查当前的用户是否为root。

```shell
[root@localhost opt]# vim  test1.sh
[root@localhost opt]# bash test1.sh 
是root用户
[root@localhost opt]# cat test1.sh 
#!/bin/bash
if [ $UID -eq 0 ];then
	echo "是root用户"
else
	echo “"不是root用户"
fi
```

（2）编写uaddfor.sh脚本，根据用户名列表快速添加用户账号。

> ​      需要添加的账号名称保存在/root/users.txt文件中，每行一个用户名。要求在执行uaddfor.sh脚本后，能够为这些用户名快速添加好系统账号，并将登录密码设置为1234567。

```shell
[root@localhost opt]# bash uaddfor.sh 
更改用户 tw1 的密码 。
passwd：所有的身份验证令牌已经成功更新。
tw1创建完成
更改用户 tw2 的密码 。
passwd：所有的身份验证令牌已经成功更新。
tw2创建完成
更改用户 tw3 的密码 。
passwd：所有的身份验证令牌已经成功更新。
tw3创建完成
[root@localhost opt]# su tw2
[tw2@localhost opt]$ 
[root@localhost opt]# cat uaddfor.sh 
#!/bin/bash
for i in $(cat /opt/user.txt)
do
	useradd $i
	echo 123456 | passwd --stdin $i
	echo "$i创建完成"
done
```

（3）、 编写sumwhile脚本，计算从1-100之间所有整数的和。

```shell
[root@localhost opt]# vim sunwhile.sh
[root@localhost opt]# cat sunwhile.sh 
#!/bin/banh
a=0
b=0
while [ a -le 100 ]
do 
	let b+=$a
	let a+=1
done
echo "1—100的和为$b"
[root@localhost opt]# bash sunwhile.sh 
1—100的和为5050
```



------

## 第三天



### 一、循环的控制

#### 1、中断

#### 2、退出

（1）、exit：

结束循环；也结束整个脚本；

```shell
[root@localhost opt]# vim t3.sh
[root@localhost opt]# bash t3.sh 
abc
[root@localhost opt]# cat vim t3.sh 
#!/bin/bash
for i in {1..5}
do
	echo abc
	exit
done
echo over
```

（2）、break：

只结束循环，继续执行done后面的语句；

```shell
[root@localhost opt]# vim t3.sh
[root@localhost opt]# bash t3.sh 
abc
over
[root@localhost opt]# cat vim t3.sh 
#!/bin/bash
for i in {1..5}
do
	echo abc
	break
done
echo over
```

（3）、continue：

结束当前循环，继续下一次循环；

```shell
[root@localhost opt]# vim t3.sh
[root@localhost opt]# bash t3.sh 
abc
haha
abc
haha
abc
abc
haha
abc
haha
over
[root@localhost opt]# cat vim t3.sh 
#!/bin/bash
for i in {1..5}
do
	echo abc
       [ $i -eq 3 ] && continue
   echo haha
done
echo over
```

练习：

编写脚本，可以为用户进行整数求和；

```shell
[root@localhost opt]# vim t4.sh
[root@localhost opt]# bash t4.sh 
请输入数字求和（0为结束看结果）3
请输入数字求和（0为结束看结果）
请输入数字求和（0为结束看结果）
请输入数字求和（0为结束看结果）
请输入数字求和（0为结束看结果）
请输入数字求和（0为结束看结果）3234
请输入数字求和（0为结束看结果）
请输入数字求和（0为结束看结果）
请输入数字求和（0为结束看结果）0
总和是：3237
[root@localhost opt]# cat t4.sh 
#!/bin/bash
x=0
while true
do
	read -p "请输入数字求和（0为结束看结果）" n
	[ -z $n ] && continue             #结束当前循环；
	[ $n -eq 0 ] && break
	let x+=n
done
echo "总和是：$x"
```

### 二、case分支

#### 1、语法格式：

case   变量   in

模式1）

​			指令1

​			指令2；；

模式2）

​			指令1

​			指令2；；

......

*）

​		指令1

​		指令 2；；

esac

#### 2、案例

（1）案例一：

```shell
[root@localhost opt]# vim t5.sh
[root@localhost opt]# bash t5.sh abc
123
[root@localhost opt]# bash t5.sh xyz
456
[root@localhost opt]# cat t5.sh 
#!/bin/bash
case $1 in
	abc)
		echo 123;;
	xyz)
		echo 456;;
	*)
		echo "请输入abc或者xyz"
esac
```

（2）案例二：

```shell
[root@localhost opt]# bash t6.sh t aa
[root@localhost opt]# ls
aa  t2.sh  t3.sh  t4.sh  t5.sh  t6.sh  test1.sh
[root@localhost opt]# cat t6.sh 
#!/bin/bash
case $1 in
	t)
		touch $2;;
	m)
		mkdir $2;;
	r)
		rm -rf $2;;
	*)
		echo "错误"
esac
```

（3）案例三：（脚本实现，nginx的编译和安装）

```shell
[root@localhost opt]# cat 7.sh 
#!/bin/bash
yum -y install gcc make pcre-devel openssl-devel
tar -xf nginx-1.22.1.tar.gz
cd nginx-1.22.1
./configure
make
make install
[root@localhost opt]# cat 8.sh 
#!/bin/bash
#!/bin/bash
case $1 in
start|kai)
        /usr/local/nginx/sbin/nginx;;
stop|guan)
        /usr/local/nginx/sbin/nginx -s stop;;
restart|cq)
        /usr/local/nginx/sbin/nginx -s stop
        /usr/local/nignx/sbin/nginx;;
status|zt)
        ss -ntulp | grep -q nginx
        [ $? -eq 0 ] && echo "nginx正在运行" || echo "nginx 未开启" ;;
*)
       echo "请输入start、stop"
esac
```



### 三、函数

#### 1、基本概念

使用一个公共存储的语句块，可以实现方便调用，避免代码重复的目的。

格式：

（1）、function   函数名（）{

指令

}

（2）、函数名 （）{

指令

}

```shell
[root@localhost opt]# vim 9.sh
[root@localhost opt]# bash 9.sh 
abc
xyz
abc
xyz
[root@localhost opt]# cat 9.sh 
#!/bin/bash
a(){
echo abc
echo xyz
}
a
a
```

#### 2、案例实现

使用函数脚本，修改输出字体颜色：

```stylus
[root@localhost opt]# chmod u+x 9.sh 
[root@localhost opt]# ls
7.sh  8.sh  9.sh  a.sh  nginx-1.22.1  nginx-1.22.1.tar.gz
[root@localhost opt]# ./9.sh 
abcd
wxyz
abcd
wxyz
[root@localhost opt]# cat 9.sh 
#!/bin/bash
a(){
echo -e "\033[$1m$2\033[0m"
}
a  31  abcd
a  32  wxyz
a  91  abcd
a  92  wxyz
```

<img src="C:\Users\rjyws\AppData\Roaming\Typora\typora-user-images\image-20230801154653694.png" alt="image-20230801154653694" style="zoom: 50%;" />

### 四、字符串处理

#### 1、变量字符串处理

（1）字符串的截取

语法1：${变量名：起始位置：截取长度}

```stylus
[root@localhost opt]# a=abcahbbdjvv
[root@localhost opt]# echo ${a:4:4}
hbbd
[root@localhost opt]# echo ${a:2:4}
cahb
```

（2）获取随机密码的脚本

```shell
[root@localhost opt]# bash 10.sh 
s47m5NCC
[root@localhost opt]# bash 10.sh 
Uuhy76uG
[root@localhost opt]# bash 10.sh 
1ZxUTHB4
[root@localhost opt]# cat 10.sh 
#!/bin/bash
x=abcdefghijklmnopqistuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789
for i in {1..8}
do 
	n=$[RANDOM%62]
    p=${x:n:1} 
	pass+=$p
done
echo $pass
```

（3）字符更换

/：换一个字符；

//：换所有字符；

```stylus
[root@localhost opt]# echo ${a/c/6}
ab6defg
[root@localhost opt]# echo ${a//c/6}
ab6defg
[root@localhost opt]# a=abcdabcd
[root@localhost opt]# echo ${a//c/6}
ab6dab6d
```

（4）字符串删除

掐头：${变量名#删除内容}；匹配最短

​           ${变量名##*删除内容}；  匹配最长

去尾：${变量名%删除内容}；匹配最短

​			${变量名%%删除内容*}；       匹配最长、

```stylus
[root@localhost opt]# echo ${a#ab}
cdabcd
[root@localhost opt]# echo ${a%bcd}
abcda
```



### 五、总结 

输入身高，符合要求选中，加入文档，不符合未选中，继续进行脚本；

```shell
[root@localhost opt]# bash lianxi.sh 
输入你的身高(cm[整数，去尾])：199
你被选中！！！
输入你的身高(cm[整数，去尾])：198
你被选中！！！
输入你的身高(cm[整数，去尾])：197
你被选中！！！
输入你的身高(cm[整数，去尾])：196
你被选中！！！
输入你的身高(cm[整数，去尾])：195
你被选中！！！
189 199 187 193 196 199 1234 199 198 197 196 195
[root@localhost opt]# cat lianxi.sh 
#!/bin/bash
green(){
	echo -e "\033[$1m$2\033[0m"
}
touch haha.txt
i=0
while :
do
	read -p "输入你的身高(cm[整数，去尾])：" a
	if [ $a -ge 185 ];then
		echo $a >> haha.txt 
	    let	i+=1
		green 92 "你被选中！！！"
		if [ $i -ge 5 ];then
        	break
		else
			continue
		fi
	elif [ $a -eq 0 ];then
		exit
	else
		green 91 "你未被选中！！！"
	fi
done
b=$(cat haha.txt)
echo $b
```



------

## 第四天



### 一、正则表达式概述

#### 1、基本正则格式

![基本正则](C:\Users\rjyws\Pictures\Screenshots\table001.png)

![扩展正则](C:\Users\rjyws\Pictures\Screenshots\table002.png)

#### 2、案例练习

（1）编写脚本，问用户要整数数字，如果用户没按要求则给出提示：

```shell
[root@localhost opt]# bash 2.sh 
输入一个数字1
1
[root@localhost opt]# bash 2.sh 
输入一个数字weqq2r
weqq2r
输入错误，请重新输入！！！
[root@localhost opt]# cat 2.sh 
#!/bin/bash

read -p "输入一个数字" b
echo $b | grep "[^0-9]" 
if [ $? -ne 0 ];then
	echo "$b"
else
	echo "输入错误，请重新输入！！！"
fi
```

### 二、grep

#### 1、测试 ^ $ [] [^]

```shell
grep ^root user                #找以root开头的行
grep bash$ user                #找以bash结尾的行
grep ^$ user                    #找空行
grep -v ^$ user                #显示除了空行的内容
grep "[root]" user            #找r、o、t任意一个字符 
grep "[rot]" user                #效果同上
grep "[^rot]" user            #显示r或o或t以外的内容
grep "[0123456789]" user        #找所有数字
grep "[0-9]" user                #效果同上
grep "[^0-9]" user            #显示数字以外内容
grep "[a-z]" user                #找所有小写字母
grep "[A-Z]" user                #找所有大写字母
grep "[a-Z]" user                #找所有字母
grep "[^0-9a-Z]" user            #找所有符号
```

#### 2、测试 . *

```shell
grep "." user                 #找任意单个字符，文档中每个字符都可以理解为任意字符
grep "r..t" user                #找rt之间有2个任意字符的行
grep "r.t" user                #找rt之间有1个任意字符的行，没有匹配内容，就无输出
grep "*" user                    #错误用法，*号是匹配前一个字符任意次，不能单独使用
grep "ro*t" user                #找rt，中间的o有没有都行，有几次都行
grep ".*" user                #找任意，包括空行 .与*的组合在正则中相当于通配符的效果
```

#### 3、测试 \{n\} \{n,\} \{n,m\} \(\)

```shell
grep "ro\{1,2\}t" user        #找rt，中间的o可以有1~2个
grep "ro\{2,6\}t" user        #找rt，中间的o可以有2~6个
grep "ro\{1,\}t" user            #找rt，中间的o可以有1个以及1个以上
grep "ro\{3\}t" user             #找rt，中间的o必须只有有
```



### 三、sed流式编辑器（逐行处理）

可以对文档进行非交互式增删改查；

前置指令 |  sed  选项  条件   指令

sed  选项    条件  指令   文档

#### **1、选项：**

-n：屏蔽默认输出；

-r：支持扩展正则表达式；

-i：修改原文件；

#### **2、指令：**

p：输出；

```shell
[root@localhost opt]# cat user 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed 'p' user 
root:x:0:0:root:/root:/bin/bash
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin



------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed -n 'p' user                         //输出所有行
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed -n '1p' user                         //输出第一行
root:x:0:0:root:/root:/bin/bash
------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed -n '2,4p' user                       //输出2~4行
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed -n '2p;4p' user                       //第二行和第四行
bin:x:1:1:bin:/bin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed -n '3,+1p' user                       //输出第三行以及后面的一行
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
------------------------------------------------------------------------------------------------------------
[root@localhost opt]# sed -n '1~2p' user                      //    输出奇数行
root:x:0:0:root:/root:/bin/bash
daemon:x:2:2:daemon:/sbin:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

d：删除；

与p的操作大致相同；

s：替换；

```shell
[root@localhost opt]# sed 's/2017/666/' 3.txt 
#!/bin/bash
666 2011 2018
666 2017 2024
666 2017 2017
[root@localhost opt]# sed 's/666/6666/' 3.txt 
#!/bin/bash
2017 2011 2018
2017 2017 2024
2017 2017 2017
[root@localhost opt]# sed 's/2017/6666/' 3.txt 
#!/bin/bash
6666 2011 2018
6666 2017 2024
6666 2017 2017
[root@localhost opt]# sed 's/2017/6666/2' 3.txt 
#!/bin/bash
2017 2011 2018
2017 6666 2024
2017 6666 2017
[root@localhost opt]# sed '2s/2017/6666/2' 3.txt 
#!/bin/bash
2017 2011 2018
2017 2017 2024
2017 2017 2017
[root@localhost opt]# sed '2s/2017/6666/2' 3.txt 
2017 2011 2018
2017 6666 2024
2017 2017 2017
[root@localhost opt]# sed '/2018/s/2017/6666/2' 3.txt 
2017 2011 2018
2017 2017 2024
2017 2017 2017
[root@localhost opt]# sed '/2018/s/2017/6666/' 3.txt 
6666 2011 2018
2017 2017 2024
2017 2017 2017
```

替换的使用技巧：

```shell
[root@localhost opt]# sed -r 's/\/bin\/bash/\/sbin\/sh/' user 
root:x:0:0:root:/root:/sbin/sh
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

[root@localhost opt]# sed -r 's!/bin/bash!/sbin/sh!' user     //注意：只要是三个一样的字符都可以用来替换；
root:x:0:0:root:/root:/sbin/sh
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```



#### **3、条件：**

行号，正则表达式；

#### **4、脚本练习**

> **1、案例：**
>
> sed选项的用法：
>
> ```shell
> [root@localhost opt]# sed -n '/^root/p' user          //    以root开头
> root:x:0:0:root:/root:/bin/bash
> [root@localhost opt]# sed -n '/root/p' user            //    包含root的行
> root:x:0:0:root:/root:/bin/bash
> [root@localhost opt]# sed -n '1!p' user            //输出除了第一行 的内容，！是取反
> bin:x:1:1:bin:/bin:/sbin/nologin
> daemon:x:2:2:daemon:/sbin:/sbin/nologin
> adm:x:3:4:adm:/var/adm:/sbin/nologin
> lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
> 
> 
> [root@localhost opt]# sed -n '$p' user               //输出最后一行
> 
> [root@localhost opt]# sed -n '=' user    //输出行号，如果是$=就是最后一行的行号
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> ```
>
> **2、案例**
>
> 使用脚本装载httpd服务，并修改配置文件，监听端口为82；
>
> ```shell
> [root@localhost opt]# bash 4.sh 
> Created symlink /etc/systemd/system/multi-user.target.wants/httpd.service → /usr/lib/systemd/system/httpd.service.
> [root@localhost opt]# curl 192.168.88.5:82
> sed-test~~~
> [root@localhost opt]# cat 4.sh 
> #!/bin/bash
> yum -y remove httpd  &> /dev/null
> rm -rf /etc/httpd
> yum -y install httpd  &> /dev/null
> sed -i '/^Listen 80/s/0/2/' /etc/httpd/conf/httpd.conf
> setenforce 0
> systemctl restart httpd
> systemctl enable httpd
> echo sed-test~~~ > /var/www/html/index.html
> ```
>
> **3、案例**
>
> （1）、找到使用bash作为登录shell的用户名；
>
> （2）、列出这些用户的密码；
>
> （3）、按每行账户名-->密码记录保存
>
> ```shell
> [root@localhost opt]# vim 5.sh
> [root@localhost opt]# bash 5.sh 
> root ---> $6$MHZCxTv5.ERa3yfO$5TjhOzSgzRyFdDWK1JlDsnjw0czVV09ePD1DM7lL7epvwOitrIQWOYgOtewhSqHoufBM9AsFDgee3QwJf2rs6/
> tw ---> $6$k/kYAnLn9wy3/HIl$lSULOxDcd79/gd/G/sb1nOMsVALsUQbdr5rpp4YKdseuslHDh8qTe2CzDpsq.Z4UjPwrCiQQ7IEZN3.8np77t/
> [root@localhost opt]# cat 5.sh 
> #!/bin/bash
> u=$(sed -n '/bash$/s/:.*//p' /etc/passwd)
> for i in $u
> do
> 	pass=$(grep $i /etc/shadow)
> 	pass=${pass#*:}
> 	pass=${pass%%:*}
> 	echo "$i --->
>  $pass"
> done
> ```
>
> 

### 四、总结

**1 、简述egrep工具的-q选项的含义，并验证其在脚本应用中的价值。**

答：egrep中-p的作用是将输出静默，大概意思与 &>  /dev/null类似；

**2 、正则表达式中的+、？、*分别表示什么含义？**

+：代表最少匹配一次；

？：最多匹配一次；

*：可以匹配任意个；

**3 、如何编写正则表达式匹配11位的手机号？**

```shell
[root@localhost opt]# egrep  '^1[0-9]{10}$' p.txt 
18234567890
19219900584
[root@localhost opt]# cat p.txt 
18234567890
19219900584
23443534
23123123
```

**4 、简述sed定址符的作用及表示方式。**

- 作用：地址符（执行指令的条件）控制sed需要处理文本的范围；不加定址符则逐行处理所有行
- 表示方式：地址符可以使用行号或正则表达式

**5、 如何使用sed提取文本中的偶数行？**

```shell
[root@localhost opt]# cat p.txt | sed -n '2~2p' p.txt 
19219900584
23123123
[root@localhost opt]# 
```

**6、 如何使用sed删除文本中每行的第4个字符？**

```shell
[root@localhost opt]# sed -r 's/3//' p.txt 
1824567890
19219900584
2443534
2123123
[root@localhost opt]# 
```

**7、 提取/etc/passwd文件的第6-10行，另存为pass5.txt文件。**

```shell
[root@localhost opt]# sed -n "6,10p"  /etc/passwd  >> a.txt
[root@localhost opt]# cat a.txt 
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin

```



------

## 第五天



### 一、补充

#### 1、关于正则表达式的补充：

（1）、\w 匹配数字、字母、下划线

```shell
egrep "roo\w" user   #找roo后面必须是数字或字母或下划线的字符串
```

（2）、\s 匹配空格、tab键

```shell
egrep "roo\s" user   #找roo后面是1个空格或者tab键打出来的空格的字符串，如果没有就不输出
```

（3）、\d 匹配数字，和[0-9]等效

```shell
egrep "(25[0-5]\.|2[0-4][0-9]\.|1?[0-9]?[0-9]\.){3}(25[0-5]|2[0-4][0-9]|1?[0-9]?[0-9])"   #匹配ip地址
grep -P "(25[0-5]\.|2[0-4]\d\.|1?\d?\d\.){3}(25[0-5]|2[0-4]\d|1?\d?\d)"   #匹配ip地址
```

#### 2、关于sed补充

（1）、a行下追加 i行上添加 c替换整行

```shell
sed 'a 666' user    #所有行的下面追加666
sed '1a 666' user   #第1行的下面追加666
sed '/^bin/a 666' user   #在以bin开头的行的下面追加666
sed 'i 666' user  #所有行的上面添加666
sed '5i 666' user   #第5行的上面添加666
sed '$i 666' user  #最后1行的上面添加666
sed 'c 666' user   #所有行都替换成666
sed '1c 666' user  #替换第1行为666
```

（2）、替换特殊用法

```shell
cat abc.txt                                #先准备素材100   
laowang98  
gangge59   
laoni
used -r 's/([0-9]+)(\s+)([a-z]+)/\3\2\1/' abc.txt    #使用替换功能更改文本列,此处小括号相当于保留（复制），\1相当于粘贴之前第1个小括号里的内容
```

### 二、使用awk提取文本

#### 1、 问题

本案例要求使用awk工具完成下列过滤任务：

- 练习awk工具的基本用法
- 提取本机系统数据
- 格式化输出信息

#### 2、 步骤

实现此案例需要按照如下步骤进行。

> 步骤一：awk的基本用法

**1）基本操作方法**

格式1：awk [选项] '[条件]{指令}' 文件

格式2：前置指令 | awk [选项] '[条件]{指令}'

其中，print 是最常用的编辑指令；若有多条编辑指令，可用分号分隔。

Awk过滤数据时支持仅打印某一列，如第2列、第5列等。

处理文本时，默认将空格、制表符作为分隔符。

条件可以用/ /的方式，与sed类似

**awk常用内置变量：**

$0 文本当前行的全部内容

$1 文本的第1列

$2 文件的第2列

$3 文件的第3列，依此类推

NR 文件当前行的行号

NF 文件当前行的列数（有几列）

```shell
[root@svr5 ~]# cat abc.txt hello the worldwelcome to beijingawk '{print}' abc.txt                #输出所有awk '/to/{print}' abc.txt            #输出有to的那行awk '{print $2}' abc.txt            #输出所有行的第2列awk '/to/{print $1}' abc.txt        #输出有to的那行的第1列awk '{print $0}' abc.txt            #输出所有行所有列awk '{print $0,$1}' abc.txt        #输出所有行所有列，第1列awk '{print NR}' abc.txt            #输出所有行的行号awk '{print NR,$0}' abc.txt        #输出所有行的行号，所有列awk '{print NR,NF}' abc.txt        #输出所有行的行号，列号(有几列)
```

再使用之前的user文档测试

```shell
awk '/^bin/{print NR}'  user        #找以bin开头的行，显示该行的行号
awk '/^bin/{print NR,$0}'  user    #找以bin开头的行，显示该行的行号，所有列
awk '{print NF}'   user            #输出所有行的列号（每行有几列）
```

**2）选项 -F 可指定分隔符**

```shell
awk -F: '{print $1}'  user         #文档中如果没有空格，可以用F修改分隔符
awk -F: '{print $1,$6}'  user        #使用冒号作为列的分隔符，显示第1、6列
```

awk还识别多种单个的字符，比如以“:”或“/”分隔

```shell
awk -F [:/] '/^root/{print $1,$10}' user
```

awk的print指令不仅可以打印变量，还可以打印常量

```shell
awk -F: '{print $1" 的家目录是 "$6}'  user    #输出常量，加双引号即可
awk -F: '{print $1" 的解释器是 "$7}'  user
```

> 步骤二：利用awk提取本机系统数据

**1）收集根分区剩余容量**

```shell
df -h | awk  '/\/$/{print  $4}'    #使用df  -h 作为前置指令交给awk处理找到以/结尾的行，并输出第4列
df -h | awk  '/\/$/{print  "根分区剩余容量是"$4}'   #然后加常量输出
```

**2）收集网卡流量信息**

RX为接收的数据量，TX为发送的数据量。packets以数据包的数量为单位，bytes以字节为单位：

```shell
ifconfig eth0 | awk '/RX p/{print "eth0网卡接收的数据量是"$5"字节"}'
ifconfig eth0 | awk '/TX p/{print "eth0网卡发送的数据量是"$5"字节"}'
```

> 步骤三：格式化输出信息

**1）awk处理的时机**

awk会逐行处理文本，支持在处理第一行之前做一些准备工作，以及在处理完最后一行之后做一些总结性质的工作。在命令格式上分别体现如下：

```shell
awk  [选项]  '[条件]{指令}'  文件awk  [选项]  'BEGIN{指令} {指令} END{指令}'  文件
```

- BEGIN{ } 行前处理，读取文件内容前执行，指令执行1次
- { } 逐行处理，读取文件过程中执行，指令执行n次
- END{ } 行后处理，读取文件结束后执行，指令执行1次

```shell
awk -F: 'BEGIN{print "start"}{print $1}END{print "over"}' userawk 'BEGIN{print NR}{print NR}END{print NR}' user
```

**2）格式化输出/etc/passwd文件**

要求: 格式化输出passwd文件内容时，要求第一行为列表标题，中间打印用户的名称、UID、家目录信息，最后一行提示一共已处理文本的总行数，效果如图-1所示。

<img src="C:\Users\rjyws\Pictures\Screenshots\image001.png" style="zoom: 200%;" />

**3）根据实现思路编写、验证awk过滤语句**

输出信息时，可以使用“\t”显示Tab制表位：

```shell
awk 'BEGIN{print "User\tUID\tHome"}'            #第1步输出表头信息
awk -F: '{print $1"\t"$3"\t"$6}' user            #第2步输出内容
awk 'END{print "总计"NR"行" }' user                #第3步输出结尾
awk -F: 'BEGIN{print "User\tUID\tHome"}{print $1"\t"$3"\t"$6}END{print "总计"NR"行"}' user   #合在一起写
```



### 三、awk处理条件

#### 1 、问题

- 本案例要求使用awk工具熟悉各种条件，以达到更精确查找某行的目的

#### 2、 步骤

实现此案例需要按照如下步骤进行。

> 步骤一：认识awk处理条件的设置

使用正则设置条件

**1）/正则/ ~ 包含 !~不包含**

```shell
awk -F: '$6~/root/{print}'  user  #输出第6列包含root的行
awk -F: '$6~/bin/{print}'  user   #输出第6列包含bin的行
awk -F: '$6!~/bin/{print}'  user  #输出第6列不包含bin的行
```

**2）使用数值/字符串比较设置条件**

比较符号：==(等于) !=（不等于） >（大于）

\>=（大于等于） <（小于） <=（小于等于）

```shell
awk -F: '$3<3{print}' user            #输出第3列小于3的行
awk -F: '$3<=3{print}' user        #输出第3列小于等于3的行
awk -F: 'NR==2{print}' user        #输出第2行
awk -F: 'NR>2{print}' user            #输出行号大于2的行
```

**3）逻辑测试条件**

```shell
awk -F: 'NR>=3&&NR<=5{print}' user            #找行号是3~5行
awk -F: 'NR==2||NR==4{print}' user            #找行号是2或者4的行
awk -F: 'NR==2||NR==40{print}' user        #如果只有一个条件满足就显示一个
```

当定义了条件且指令就是print时可以省略指令不写

```shell
awk -F: '$7~/bash/&&$3<=500' user        #找第7列包含bash并且第3列小于等于500的行
awk 'NR==2&&NR==4' user                #找行号既是2又是4的行，不存在，无输出
awk -F: '$7~/bash/&&NR<=3' user        #找第7列包含bash并且行号是1~3的
awk -F: '$7~/bash/||NR<=3' user        #找第7列包含bash或者行号是1~3的
```

**4）数学运算**

```shell
awk 'NR%2==0{print NR,$0}' user   #在条件中使用运算，找到将行号除以2余数等于0的行，然后输出该行的行号和所有列，相当于输出偶数行
```



### 四、使用awk统计网站访问量

使用awk统计网站访问量

```shell
setenforce 0                         #关闭
selinuxsystemctl stop firewalld            #关闭防火墙
systemctl restart httpd            #开启网站服务
```

使用浏览器多访问几次网站，包括本机用curl

```shell
curl  192.168.88.2:82                #如果端口没改过就不用敲:82
awk  '{print $1}'  /var/log/httpd/access_log   #初步统计，不完美
```



### 五、案例3：awk数组

#### 1、 问题

本案例要求了解awk数组的使用

> 步骤一：awk数组

**1）数组的语法格式**

数组是一个可以存储多个值的变量，具体使用的格式如下：

定义数组的格式：数组名[下标]=元素值

调用数组的格式：数组名[下标]

```shell
awk 'BEGIN{a=10;a=20;print a}'                 #首先测试普通变量
awk 'BEGIN{a[1]=10;a[2]=20;print a[2],a[1]}'    #使用awk测试数组，创建数组a，下标1对应值是10，下标2对应值是20，然后输出下标是2与下标是1的值
```

注意，awk数组的下标除了可以使用数字，也可以使用字符串，字符串需要使用双引号：

```shell
awk 'BEGIN{a["abc"]="abcabc";a["xyz"]="xyzxyz";print a["xyz"]}'   
```

以上信息是手工输入，还可以从文档收集

准备一个测试文档，里面有6行，每行分别是abc、xyz、abc、opq、xyz、abc 然后按照awk逐行处理的工作特点使用awk '{a[$1]++}' shu.txt 走完每一行得到下列结果，但不会输出到屏幕

逐行任务 每行实际执行 执行结果

a[$1]++ a[abc]++ a[abc]=1

a[$1]++ a[xyz]++ a[xyz]=1

a[$1]++ a[abc]++ a[abc]=2

a[$1]++ a[opq]++ a[opq]=1

a[$1]++ a[xyz]++ a[xyz]=2

a[$1]++ a[abc]++ a[abc]=3

```shell
awk  '{a[$1]++}END{print a["abc"]}'  shu.txt        #如果要看值，可以输出数组名[下标]，由于数组下标不确定，逐行任务运算前可以不用BEGIN任务定义
```

根据上述操作了解数组可以收集信息，但收集完了之后查看确不方便，可以用for循环实现。方法如下：

for(变量名 in 数组名){print 变量名} #这个格式可以查看数组的所有下标

```shell
awk '{a[$1]++}END{for(i in a){print i,a[i]}}' shu.txt   #使用逐行任务与数组收集文档shu.txt中的信息，然后在END任务中使用for循环显示所有数组a的下标与值
```



### 六、案例4：awk扩展应用

#### 1、 问题

本案例要求使用awk工具完成下列两个任务：

分析Web日志的访问量排名，要求获得客户机的地址、访问次数，并且按照访问次数排名

#### 2、 方案

1）awk统计Web访问排名

在分析Web日志文件时，每条访问记录的第一列就是客户机的IP地址，其中会有很多重复的IP地址。因此只用awk提取出这一列是不够的，还需要统计重复记录的数量并且进行排序。

通过awk提取信息时，利用IP地址作为数组下标，每遇到一个重复值就将此数组元素递增1，最终就获得了这个IP地址出现的次数。

针对文本排序输出可以采用sort命令，相关的常见选项为-r、-n、-k。其中-n表示按数字顺序升序排列，而-r表示反序，-k可以指定按第几个字段来排序。

#### 3、 步骤

实现此案例需要按照如下步骤进行。

步骤一：统计Web访问量排名

分步测试、验证效果如下所述。

**1）提取IP地址及访问量**

```shell
awk '{ip[$1]++}END{for(i in ip){print ip[i],i }}' /var/log/httpd/access_log     #数组名称可以自定义其他的，通过awk数组+for循环查看日志中哪个ip来访过以及来访的次数
```

**2）对第1）步的结果根据访问量排名**

```shell
awk '{ip[$1]++}END{for(i in ip){print ip[i],i}}' /var/log/httpd/access_log | sort -nr        #使用sort命令增加排序功能，-n是以数字形式排序，-r是降序
```



### 七、案例5：安全检测

#### 1、 问题

本案例要检测登录者的IP

检测安全日志，登录root且密码错误就输出对方IP

#### 2、步骤

实现此案例需要按照如下步骤进行。

步骤一：准备工作

**1）/var/log/secure是安全日志，如果有人登陆时输入错误密码的话信息会记录下来，这种信息可以用awk抓取出来，方法如下：**

```shell
awk '/Failed password for root/{ip[$11]++}END{for(i in ip){print i,ip[i]}}'  /var/log/secure    #统计安全日志中访问root账户且密码输入错误的ip地址与次数
```



### 八、 案例6：编写监控脚本

#### 1、 问题

本案例要求编写脚本，实现计算机各个性能数据监控的功能，具体监控项目要求如下：

#### 2 、步骤

实现此案例需要按照如下步骤进行。

步骤一：准备工作

**1）部分常用命令**

```shell
[root@svr5 ~]# uptime                            #查看CPU负载
[root@svr5 ~]# ifconfig eth0                    #查看网卡流量
[root@svr5 ~]# free                            #查看内存信息
[root@svr5 ~]# df                                #查看磁盘空间
[root@svr5 ~]# wc -l /etc/passwd                #查看计算机账户数量
[root@svr5 ~]# who |wc -l                        #查看登录账户数量
[root@svr5 ~]# rpm -qa |wc -l                    #查看已安装软件包数量
```

步骤二：编写参考脚本

**1）脚本内容如下：**

```shell
#!/bin/bashwhile :doclear                                    #清屏
free -h | awk  '/^Mem:/{print "剩余内存容量是"$4}'
df -h | awk  '/\/$/{print "根分区剩余容量是"$4}'
awk 'END{print "用户总数是"NR"个"}'  /etc/passwd
who | awk 'END{print "登录用户数量是"NR"个"}'
uptime | awk '{print "cpu的15分钟平均负载是"$NF}'
rpm -qa | awk 'END{print "安装的软件包数量是"NR"个"}'
sleep 3
```



### 九、总结（习题）

#### 1 、简述awk工具的基本语法格式。

参考答案

- 格式1： awk [选项] ‘[条件]{处理动作}’ 文件列表
- 格式2： 命令 | awk [选项] ‘[条件]{处理动作}’

#### 2、 简述awk工具常用的内置变量、各自的作用。

参考答案

- $n：即$1、$2、$3……，表示指定分隔的第几个字段
- $0：保存当前读入的整行文本内容
- NF：记录当前处理行的字段个数（列数）
- NR：记录当前已读入行的数量（行数）

#### 3、 awk处理文本时，读文件前、读取文件内容中、读文件后后这三个环节是如何表示的？

参考答案

- BEGIN{ } 文件前处理：awk没有读入行之前 要执行的动作； 一般对数据作初始化操作，可以单独使用。
- { } 行处理：对awk读入的每一行进行处理，可以单独使用。
- END{ }文件后处理：awk 把所有的行都处理完后要执行的动作，一般输出数据处理的结果。可以单独使用。
- 

#### 4 、提取当前eth0网卡的IPv4地址及掩码信息。

参考答案

查看测试文本：

```shell
[root@svr5 ~]# ip add list eth02: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000    link/ether 00:0c:29:64:88:8e brd ff:ff:ff:ff:ff:ff    inet 192.168.4.55/24 brd 192.168.4.255 scope global eth0    inet 192.168.4.5/24 brd 192.168.4.255 scope global secondary eth0    inet6 fe80::20c:29ff:fe64:888e/64 scope link        valid_lft forever preferred_lft forever
```

提取IPv4地址及掩码信息的操作及效果：

```shell
[root@svr5 ~]# ip add list eth0 | awk '/\<inet\>/{print $2}'192.168.4.55/24192.168.4.5/24
```

#### 5 、找出UID位于10~20之间的用户，输出用户名及对应的UID。

参考答案

```shell
[root@svr5 ~]# awk -F: '$3>=10 && $3<=20{print $1":"$3}' /etc/passwduucp:10operator:11games:12gopher:13ftp:14 
```

#### 6 、利用awk工具统计使用bash作为解释器的用户数量。

参考答案

使用NF内置变量找最后一列的内容，匹配bash即可让x+1：

```shell
[root@svr5 ~]# awk -F/ '$NF=="bash"{x++}END{print x}' /etc/passwd
```

#### 7、 在awk中是否可以使用数组，分别以什么构成？

参考答案

可以使用数组，分别以 数组名、下标、值 三个部分构成

#### 8、 在linux中对文本的排序如何实现？

参考答案

使用sort命令，比如abc.txt文本

另外还可以使用选项-n按数字升序排列 -k：针对指定的列进行排序 -r：反向排序

[root@svr5 ~]# sort -n abc.txt

#### 9 、通过安全日志/var/log/secure，分析是谁登录账户tom且密码输入错误，如果错误次数达到3次以上的话，就输出登陆者的IP

```shell
awk '/Failed password for tom/{ip[$11]++}END{for(i in ip){print ip[i],i}}' /var/log/secure| awk '$1>3{print $2}'
```





------

## 第六天



### 一、案例

#### 1、编写一个查看服务器信息脚本：

```shell
[root@localhost opt]# bash t1.sh 
根分区的剩余内存是：58G
剩余内存是：86Mi
cpu的15分种平均负载是：0.29
服务器账户总数是“46个
服务器已经登陆的账户数量是1个
服务器安装的软件包总数是1386个
[root@localhost opt]# cat t1.sh 
#!/bin/bash
df -h | awk '/\/$/{print "根分区的剩余内存是：" $4}'
free -h | awk '/^Mem:/{print "剩余内存是：" $4}'
uptime | awk '{print "cpu的15分种平均负载是：" $NF}'
awk 'END{print "服务器账户总数是“"NR"个"}' /etc/passwd
who | awk 'END{print "服务器已经登陆的账户数量是"NR"个"}'
rpm -qa | awk  'END{print "服务器安装的软件包总数是"NR"个"}'
```

#### 2、对不同版本服务器配置脚本

需求分析：

（1）永久关闭防火墙服务和selinux

（2）关闭7版本的历史命令记录，修改8版本的命令，历史记录最多保存2000条并加上时间戳

（3）关闭版本系统的交换分区

（4）定义root远程登录系统后 的ssh保存时间为300秒

（5）设置时间同步；

```shell
[root@localhost opt]# cat t2.sh 
#!/bin/bash
#1）判断当前用户身份，再关闭防火墙和selinux
[ $UID -ne 0 ] && echo  "请使用管理员权限" && exit
systemctl stop firewalld
systemctl disable firewalld
setenforce 0
sed -i 's/SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config
#2)判断不同服务器版本，安排不同任务
egrep -q "\s+8\.[0-9]"  /etc/redhat-release 
if [ $? -ne 0 ];then
	sed -ri 's/HISTSIZE=[0-9]+/HISTSIZE=0/'  /etc/profile
else
	sed -ri 's/HISTSIZE=[0-9]+/HISTSIZE=2000/'  /etc/profile
	egrep -q 'HISTTIMEFORMAT="%F %T "' /etc/profile
	if [ $? -eq 0 ];then
		sed -i '/^export/i HISTTIMEFORMAT="%F %T " ' /etc/profile
		fi
	sed -i '/^export/s/$/ HISTTIMEFORMAT/'  /etc/profile
	swap=$(swapon | awk 'NR!=1{print $1}')
	for i in $swap
	do 
		swapoff $i
	done
	sed -i '/swap/s/^/#/'  /etc/fstab
fi
#3)最后所有机器设置ssh超时时间与时间同步
echo "export TMOUT=300" >> ~/.bash_profile
yum -y install chrony
systemctl enable chronyd
sed  -ri  '/^(pool|server).*iburst/s/^/#/'   /etc/chrony.conf
sed  -i  '1i server 192.168.88.240 iburst'   /etc/chrony.conf
systemctl restart chronyd
[root@localhost opt]# 
```

#### 3、创建用户以及密码

（1）查看用户密码

（2）自动生成密码

（2）自动分组

```shell
[root@localhost opt]# cat t3.sh 
#!/bin/bash
x=$(awk  '/^[0-9a-zA-Z]/&&!/已创建/{print NR}'  user.txt )
if [ -z "$x" ];then
	echo "没有新的用户要创建"
	exit
fi
for i in $x
do
	pass=$(tr -cd '_a-zA-Z0-9' < /dev/urandom | head -c 10)
	sed -i "${i}s/$/\t$pass/" user.txt
	read name pass << EOF
	$(sed -n "${i}p" user.txt)
EOF
	useradd $name
	echo $pass | passwd --stdin $name
	sed -i "${i}s/$/\t已创建/" user.txt
done
```

#### 4、自定义一个图形化脚本

```shell
[root@localhost opt]# cat menu 
x=1        #高亮行号，默认1
y=0        #所在第几行
menu(){
	clear 
	for i in  1、安装ftp服务  2、开关ftp服务   3、退出
	do
		echo "-----------------------"
		let y++
		[ $x -eq $y ] && echo -e "\033[44;91m$i\033[0m" && continue
		echo "$i"
	done
	y=0
	echo "-----------------------"
}
```

```shell
[root@localhost opt]# cat ser_manager 
ser_manager(){
	if ! rpm -q vsftpd &> /dev/null ;then
		msg="未安装ftp服务"
		return
	fi
	case $1 in
	start)
		systemctl start vsftpd
		msg="ftp已经启动"
		ser_manager=start;;
	stop)
		systemctl stop vsftpd
		msg="ftp已经关闭"
		ser_manager=stop;;
	esac
}
[root@localhost opt]# 
```

```shell
[root@localhost opt]# cat h.sh 
#!/bin/bash
. menu
. ftp_install
. ser_manager
while :
do
	menu
	echo "$msg"
	read -n 3 c 
	if [ "$c" == $'\033[A' ];then
		[ $x -eq 1 ] && continue 
		let x--
	elif [ "$c" == $'\033[B' ];then
		[ $x -eq 3 ] && continue
		let x++
	elif [ $x -eq 1 ] && [ -z $c ];then
		msg="ftp服务安装中..."
		echo $msg
		ftp_install
	elif [ $x -eq 2 ] && [ -z $c ];then
		[ "$ser_manager" != "start" ] && ser_manager start || ser_manager stop
	elif [ $x -eq 3 ] && [ -z $c ];then
		exit
	fi
done
[root@localhost opt]# 
```

### 二、总结

写一个产看系统信息的图形化脚本：

#### 1、jb.sh文件

```shell
[root@localhost tian]# cat jb.sh 
#!/bin/bash
#1)查看cpu详细信息
. menu
. xunhuan
. mingling
while :
do
	menu
	read -n 3 c
	if [ "$c" == $'\033[A'  ];then
		[ $x -eq 1 ] && continue
		let x--
	elif [ "$c" == $'\033[B' ];then
		[ $x -eq 6 ] && continue
		let x++
	elif [ $x -eq 1 ] && [ -z $c ];then
		echo -e "\033[32m以下是cpu基本信息：\033[0m"
		cpu1
	elif [ $x -eq 2 ] && [ -z $c ];then
		fuzai1			
	elif [ $x -eq 3 ] && [ -z $c ];then
		sum1
	elif [ $x -eq 4 ] && [ -z $c ];then
		f4
	elif [ $x -eq 5 ] && [ -z $c ];then
		g5
	elif [ $x -eq 6 ] && [ -z $c ];then
		exit
	fi
done
```

#### 2、menu文件

```shell
[root@localhost tian]# cat menu 
x=1        #高亮行号，默认1     
y=o  #所在第几行
menu(){
	clear 
	for i in  1、查看cpu基本信息  2、查看15分钟cpu负载   3、查看服务器账户总数  4、查看根分区剩余内存 5、服务器剩余内存 6、退出
	do
		echo "-----------------------"
		let y++
		[ $x -eq $y ] && echo -e "\033[44;91m$i\033[0m" && continue
		echo "$i"
	done
	y=0
	echo "-----------------------"
}


m=1
n=0
menu1(){
        for i in  1、刷新  2、退出
        do
                let n++
                [ $m -eq $n ] &&  echo -e "\033[44;91m$i\033[0m" && continue
                echo $i
        done
        n=0
}
```

#### 3、xunhuan文件（递归）

```shell
[root@localhost tian]# cat xunhuan 
cpu1(){
        while :
        do
            clear
            cpu
            menu1
            read -n 3 b
            if [ "$b" == $'\033[A'  ];then
                [ $m -eq 1 ] && continue
                let m--
            elif [ "$b" == $'\033[B' ];then
                [ $m -eq 2 ] && continue
                let m++
            elif [ $m -eq 1 ] && [ -z $b ];then
                echo -e "\033[32m刷新成功！！！\033[0m"
		sleep 1
		cpu1
		break
            elif [ $m -eq 2 ] && [ -z $b ];then
                break
            fi
        done
}

fuzai1(){
        while :
        do
            clear
            fuzai
            menu1
            read -n 3 b
            if [ "$b" == $'\033[A'  ];then
                [ $m -eq 1 ] && continue
                let m--
            elif [ "$b" == $'\033[B' ];then
                [ $m -eq 2 ] && continue
                let m++
            elif [ $m -eq 1 ] && [ -z $b ];then
                echo -e "\033[32m刷新成功！！！\033[0m"
		sleep 1
		fuzai1
		break
            elif [ $m -eq 2 ] && [ -z $b ];then
                break
            fi
        done
}


sum1(){
        while :
        do
            clear
            sum
            menu1
            read -n 3 b
            if [ "$b" == $'\033[A'  ];then
                [ $m -eq 1 ] && continue
                let m--
            elif [ "$b" == $'\033[B' ];then
                [ $m -eq 2 ] && continue
                let m++
            elif [ $m -eq 1 ] && [ -z $b ];then
                echo -e "\033[32m刷新成功！！！\033[0m"
                sleep 1
                sum1
		break
            elif [ $m -eq 2 ] && [ -z $b ];then
                break 
            fi
        done
}


f4(){
        while :
        do
            clear
            f
            menu1
            read -n 3 b
            if [ "$b" == $'\033[A'  ];then
                [ $m -eq 1 ] && continue
                let m--
            elif [ "$b" == $'\033[B' ];then
                [ $m -eq 2 ] && continue
                let m++
            elif [ $m -eq 1 ] && [ -z $b ];then
                echo -e "\033[32m刷新成功！！！\033[0m"
                sleep 1
                f4
		break
            elif [ $m -eq 2 ] && [ -z $b ];then
                break
            fi
        done
}


g5(){
        while :
        do
            clear
            g
            menu1
            read -n 3 b
            if [ "$b" == $'\033[A'  ];then
                [ $m -eq 1 ] && continue
                let m--
            elif [ "$b" == $'\033[B' ];then
                [ $m -eq 2 ] && continue
                let m++
            elif [ $m -eq 1 ] && [ -z $b ];then
                echo -e "\033[32m刷新成功！！！\033[0m"
                sleep 1
                g5
		break
            elif [ $m -eq 2 ] && [ -z $b ];then
                break
            fi
        done
}
```

#### 4、mingling文件

```shell
[root@localhost tian]# cat mingling 
cpu(){
	a=$(lscpu | awk 'NR==1 || NR==2 || NR==4 || NR==5 || NR==6 || NR==9' )
	echo "$a"
	return
}

sum(){
	a=$(awk 'END{print "服务器账户总数是:"NR"个"}' /etc/passwd)
	echo $a
}

fuzai(){
	a=$(uptime | awk '{print "cpu的15分种平均负载是：" $NF}')
	echo $a
}

f(){
	a=$(free -h | awk '/^Mem:/{print "剩余内存是：" $4}')
	echo $a
}

g(){
	a=$(df -h | awk '/\/$/{print "根分区的剩余内存是：" $4}')
	echo $a
}
```

