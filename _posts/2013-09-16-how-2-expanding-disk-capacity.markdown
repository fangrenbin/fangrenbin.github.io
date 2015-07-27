---
author: fangrenbin
comments: true
date: 2013-09-16 10:07:23+00:00
layout: post
slug: how-2-expanding-disk-capacity
title: '[翻译]如何扩展硬盘容量'
wordpress_id: 543
categories:
- linux
---

原文：[点击查看
](http://www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_:_Ch27_:_Expanding_Disk_Capacity#Migrating_Data_Over_To_your_New_Partition)
参考：[点击查看](http://vbird.dic.ksu.edu.tw/linux_basic/fedora_4/0230filesystem-fc4.php#fstab)
  

说明：本人能力有限，第一次翻译东西，请多多指教。
**前言**


* * *


对Linux管理员来讲，经常会遇到硬盘容量不足的问题。造成这种情况最常见的就是，数据库中的数据一直在不断的增长，增加更多的用户，还有大量的任务需要去执行。要解决这个问题得增加硬盘容量。
这章内容是介绍如何与Linux系统添加一块硬盘的两种方法。
第一种方法：将数据从已满的硬盘移到另一个有空闲空间的硬盘，然后把两块硬盘链接在一起。(已翻)
第二种方法：合并分区，使用LVM（Linux Logical Volume Manager）。(未翻)

**Debian与Ubuntu的差异**


* * *


本章内容主要是围绕着Fedroa/CentOS/RedHat来进行简单的说明。然而，当遇到命令与Debian/Ubuntu中的不同的时候，我将会标注出来。
就我们平常常见的命令当中，在Fedroa/CentOS/RedHat中使用root用户。使用Debian/Ubuntu的朋友需要使用

    
    
    sudo su -
    


这条命令可以在当前命令中增加你的权限，要使用root权限，使用：

    
    
    sudo <command>
    


下面这条命令可以将当前用户转为root用户登陆：

    
    
    user@ubuntu:~$ sudo su -
    [sudo] password for peter: 
    root@ubuntu:~#
    


下面这个例子是告诉你如何以root权限运行特殊的命令。第一条命令试图去查看目录列表，但是失败了因为没有足够的权限。第二条，当使用sudo的关键字在命令前面的时候命令执行成功了。

    
    
    user@ubuntu:~$  ls -l /var/lib/mysql/mysql
    ls: cannot access /var/lib/mysql/mysql: Permission denied
    user@ubuntu:~$ sudo ls -l /var/lib/mysql/mysql
    [sudo] password for peter: 
    total 964
    -rw-rw---- 1 mysql mysql   8820 2010-12-19 23:09 columns_priv.frm
    -rw-rw---- 1 mysql mysql      0 2010-12-19 23:09 columns_priv.MYD
    -rw-rw---- 1 mysql mysql   4096 2010-12-19 23:09 columns_priv.MYI
    -rw-rw---- 1 mysql mysql   9582 2010-12-19 23:09 db.frm
    ...
    ...
    ...
    user@ubuntu:~$
    


嗯，掌握了这些不同之处，我们可以断续进行讨论了。
  

**给Linux添加硬盘**


* * *


在某些阶段，你必须得面对安装额外的硬盘到你的Linux服务器上面。可能是已存在的设备不工作了，或都没有空间了，需要更多的硬盘空间。这部分就涉及到给硬盘添加一个分区，以及如何从满掉的硬盘里迁移数据到新的硬盘上面。
方案


* * *


事情总是喜欢（不会译了）：尽管你把不想要的数据删除了，/var分区还是满的。你得给系统添加一块硬盘了。你可以使用

    
    
    df -k
    #df -lh 以兆来查看
    


来查看一下当前系统的分区情况，看看哪些分区快没有可用空间来放数据了。

    
    
    [root@bigboy tmp]# df -k
    Filesystem           1K-blocks      Used Available Use% Mounted on
    /dev/hda3               505636    118224    361307  25% /
    /dev/hda1               101089     14281     81589  15% /boot
    none                     63028         0     63028   0% /dev/shm
    /dev/hda5               248895      6613    229432   3% /tmp
    /dev/hda7              3304768   2720332    416560  87% /usr
    /dev/hda2              3304768   3300536      4232  99% /var
    [root@bigboy tmp]#
    


一块新硬盘根据产品说明，已经放进去了。但你得知道如何进行。
确认硬盘的类型


* * *


Linux将所有的的硬盘分区信息存储在/proc/partitions文件当中。整个硬盘使用0来标识，其它分区是按照递增来表示。例如：整个系统有两块硬盘，硬盘/dev/hda已经分好区了，但是第二块硬盘/dev/hdb需要分区。

    
    
    [root@bigboy tmp]# cat /proc/partitions
    major minor  #blocks  name
     
       3     0    7334145 hda
       3     1     104391 hda1
       3     2    1052257 hda2
       3     3    2040255 hda3
       3     4          1 hda4
       3     5    3582463 hda5
       3     6     554211 hda6
      22     0   78150744 hdb
    [root@bigboy tmp]#
    


**NOTE:**Linux硬盘名称遵循特殊的规定，SCSI硬盘都是以sd开头，IDE硬盘以hd开头。然后在后面加一个字母来做为独立的标识。例如：第一块硬盘后面会跟a，第二块硬盘后会跟b，第三块是c，依此类推。最后，还需要使用使用两位数来表示分区号，使用这种约定，系统中的第四块硬盘，第五分区，IDE硬盘，那硬盘将会表示为/dev/hdd5。
  

**准备给新硬盘分区**


* * *


Linux的分区准备很像Windows环境，因为他们都使用fdisk来分区。下面是分区步骤：
1)第一步，将新添加的硬盘分区，添加文件系统。输入fdisk命令，后面跟上你要分区的硬盘。如果你想使用fdisk来分割/dev/hdb这块硬盘。命令就是：

    
    
    [root@bigboy tmp]# fdisk /dev/hdb
     
    The number of cylinders for this disk is set to 9729.
    There is nothing wrong with that, but this is larger than 1024,
    and could in certain setups cause problems with:
    1) software that runs at boot time (e.g., old versions of LILO)
    2) booting and partitioning software from other OSs
       (e.g., DOS FDISK, OS/2 FDISK)
     
    Command (m for help): 
    


2)一定要确保你的硬盘是你想要分区硬盘，使用p命令可以打印出所有在这块硬盘上的分区。下面这种情况是没有任何分区：

    
    
    Command (m for help): p
     
    Disk /dev/hdb: 80.0 GB, 80026361856 bytes
    255 heads, 63 sectors/track, 9729 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
     
       Device Boot      Start         End      Blocks   Id   System
     
    Command (m for help):
    


3)使用m命令可以打印出可以使用的命令和命令注解。当你输入m后，你会看到命令n是添加新的分区。添加一个主分区，代号为1，使用默认值，这个分区将会用掉所有的硬盘空间。

    
    
    Command (m for help): n
    Command action
       e   extended
       p   primary partition (1-4)
    
    Partition number (1-4): 1
    First cylinder (1-9729, default 1):<return>
    Using default value 1
    Last cylinder or +size or +sizeM or +sizeK (1-9729, default 9729):
    


4)运行p命令，看看刚才创建的分区成功了没。

    
    
    Command (m for help): p
     
    Disk /dev/hdb: 80.0 GB, 80026361856 bytes
    255 heads, 63 sectors/track, 9729 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
     
       Device Boot      Start         End      Blocks   Id   System
    /dev/hdb1               1        9726    78148161   83  Linux
     
    Command (m for help):
    


小帖示:如果你分区的时候分错了，你可以使用d命令来删除分错的区，然后重新分区。使用t命令可以将你的分区类型由默认的83改为其它的类型，如82用于交换分区。不过这也没有必要，默认的已经够我们使用了。
注意：当你在创建分区的时候，你也许会注意到使用fdisk时候，是否将分区设为主分区或第二分区。Linux允许一块硬盘有四个主分区。如果你需要更多，你可以将一个分区转换为一个扩展分区。下面这个例子展示了一块硬盘的分区，其中包括一个扩展分区，扩展分区下面有两个分区。

    
    
    Command (m for help): p
     
    Disk /dev/hda: 7510 MB, 7510164480 bytes
    255 heads, 63 sectors/track, 913 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
     
       Device Boot      Start         End      Blocks   Id   System
    /dev/hda1   *           1          13      104391   83  Linux
    /dev/hda2              14         144     1052257+  83  Linux
    /dev/hda3             145         398     2040255   82  Linux swap
    /dev/hda4             399         913     4136737+   5  Extended
    /dev/hda5             399         844     3582463+  83  Linux
    /dev/hda6             845         913      554211   83  Linux
     
    Command (m for help):
    


添加更多的分区只需要重复前面的步骤。在有些阶段你需要硬多的分区，你需要添加一个扩展分区。
5)当操作了以上的命令进行分区之后，你的分区信息并未写入硬盘，得输入w命令才能够保存。保存完分区信息以后，使用q命令退出。

    
    
    Command (m for help): w
    Command (m for help): q
    


分完区以后需要验证一下你刚才的分区，准备迁移数据到新的硬盘上。下面我们开始吧。
验证你的新分区
  

可以在你的系统中查看/proc/partitions文件，也可以使用fdisk -l命令来查看你刚才分出来的区的信息。

    
    
    [root@bigboy tmp]# cat /proc/partitions
    major minor  #blocks  name
    ...
    ...
    ...
      22     0   78150744 hdb
      22     1   78150744 hdb1
    [root@bigboy tmp]#
     
     
    [root@bigboy tmp]# fdisk -l
    ...
    ...
    ...
    Disk /dev/hdb: 80.0 GB, 80026361856 bytes
    255 heads, 63 sectors/track, 9729 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
     
       Device Boot      Start         End      Blocks   Id  System
    /dev/hdb1              1         9729    76051710   83  Linux
    [root@bigboy tmp]#
    


  

**挂载目录到新分区**


* * *


现在我们来格式化分区，用mkfs命令来给定文件系统类型，Fedora安装程序默认使用的是ext3，我们在这儿也用这种类型。

    
    
    [root@bigboy tmp]# mkfs -t ext3 /dev/hdb1
    


接下来，你得创建一个目录作为挂载点，就是新分区要挂载的目录。创建目录/mnt/hdb1

    
    
    [root@bigboy tmp]# mkdir /mnt/hdb1
    


当Linux启动的时候，系统会搜索/etc/fstab文件中的分区信息列表，然后自动将它们挂载起来。你需要添加一条挂载信息，如下：

    
    
    #
    # File: /etc/fstab
    #
    /dev/hdb1  /mnt/hdb1  ext3  defaults 1 2
    


有六列内容，第一列/dev/hdb1表示要挂载的分区，第二列/mnt/hdb1挂载点，第三列系统文件类型，第四列挂载选项，使用defaults可以适用于大部分情况，第五列是否使用dump系统备份0代表不要做dump备份，1代表要进行dump动作。最后一项是当系统启动检验分区的文件系统的完整性，0是不要检验，1是要检验，2也是要检验，不过1比2要早检验。一般来说根目录设为1，其它设为2就可以了。 如果你不熟悉/etc/fstab文件，使用man fstab命令来查看完整的说明文档，里面有所有选项的说明。你不需要等机器重启来挂载你的分区，可以使用-a选项来重新读取/etc/fstab文件中的新分区信息。

    
    
    [root@bigboy tmp]# mount -a
    


哈哈，现在可以使用你访问你刚挂载的分区了/mnt/hdb1。
  

**迁移数据到新的分区**


* * *


应该还记df -k命令吧，/var分区几乎就要满了。 

    
    
    [root@bigboy tmp]# df -k
    Filesystem           1K-blocks      Used Available Use% Mounted on
    /dev/hda3               505636    118224    361307  25% /
    /dev/hda1               101089     14281     81589  15% /boot
    none                     63028         0     63028   0% /dev/shm
    /dev/hda5               248895      6613    229432   3% /tmp
    /dev/hda7              3304768   2720332    416560  87% /usr
    /dev/hda2              3304768   3300536      4232  99% /var
    [root@bigboy tmp]#
    


du -sk *命令可以查看目录下面的所有文件以及文件夹的使用情况。切到/var目录下面，递归当前目录下面的文件和文件夹，查看到底哪个文件最大，最耗空间。使用了这个命令最后发现/var/transactions目录是罪魁祸首。

    
    
    [root@bigboy tmp]# cd /var
    [root@bigboy var]# du -sk *
    2036    cache
    4       db
    8       empty
    ...
    ...
    133784  transactions
    ...
    ...
    [root@bigboy var]#
    


就上面的情况，使用挂载在/mnt/hdb1的/dev/hdb1分区来扩展/var分区。迁移数据，步骤：
1)备份数据到你将要使用的分区
2)用who命令来看看谁登进来了。如果当前还有其它用户在，使用wall命令来告诉他们要关掉了。

    
    
    [root@bigboy tmp]# who
    root     pts/0        Nov  6 14:46 (192-168-1-242.my-site.com)
    bob      pts/0        Nov  6 12:01 (192-168-1-248.my-site.com)
    bunny    pts/0        Nov  6 16:25 (192-168-1-250.my-site.com)
    [root@bigboy tmp]# wall The system is shutting down now!
     
    Broadcast message from root (pts/0) (Sun Nov  7 15:04:27 2004):
     
    The system is shutting down now!
    [root@bigboy tmp]#
    


3)进入VGA控制台，使用单用户模式登陆。

    
    
    [root@bigboy tmp]# init 1
    


4)重命名 /var/transactions为/var/transactions-save，可以很方便的恢复备份的数据。

    
    
    sh-2.05b# mv /var/transactions /var/transactions-save
    


5)创建一个新的空间的文件夹/var/transactions，等一下做为挂载点

    
    
    sh-2.05b# mkdir /var/transactions
    


6)复制/var/transactions-save directory里面的内容到/dev/hdb1分区，实际上就是/mnt/hdb1目录

    
    
    sh-2.05b# cp -a /var/transactions-save/* /mnt/hdb1
    


7)卸载/dev/hdb1分区

    
    
    sh-2.05b# umount /mnt/hdb1
    


8)编辑/etc/fstab文件，将之前的/dev/hdb1挂载点换成新的挂载点（/var/transactions）

    
    
    #
    # File: /etc/fstab
    #
     
    #/dev/hdb1  /mnt/hdb1  ext3  defaults 1 2
     
    /dev/hdb1  /var/transactions  ext3  defaults 1 2
    


9)使用mount -a命令重新挂载/dev/hdb1，其实就是重新载/etc/fstab自动挂载没有挂载的分区。

    
    
    sh-2.05b# mount -a
    


10)看看新挂载的/var/transactions目录是否与/var/transactions-save目录下的文件完全相同。
11)输入exit返回到多用户模式。系统将会进入正常的运行级别。

    
    
    sh-2.05b# exit
    


12)看看你的程序能不能正确运行在当前的目录，然后删除/var/transactions-save目录和/mnt/hsdb1挂载点。
通过上面这个小例子，给大家展示了如何整个目录下面的数据迁移到新的硬盘上。
