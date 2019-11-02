---
layout: post
title:  "VirtualBox Issue"
categories: JavaScript
tag: JavaScript 
---

* content
{:toc}


## Issue 1
**问题：**  
A differencing image of snapshot {1393c164-d036-4ce1-b1ca-adbd3da7394f} could not be found. Could not find an open hard disk with UUID {2548eb10-2ba2-4125-b485-a0b6c97eb5d1}.  
**解决方法：**  
1. 打开虚拟机目录下的 `ubuntu-64.vbox`；在里面搜索 `uuid="{2548eb10-2ba2-4125-b485-a0b6c97eb5d1}"` 的以下 section，然后删掉。

    <AttachedDevice type="HardDisk" hotpluggable="false" port="0" device="0">
        <Image uuid="{2548eb10-2ba2-4125-b485-a0b6c97eb5d1}"/>
    </AttachedDevice>

2. 打开 VirtualBox，点击虚拟机的 设置->存储->控制权：SATA，添加现有的虚拟硬盘。

##Issue 2
**问题：**   
设置共享文件夹  
**解决方法：**  
1. 打开 VirtualBox，虚拟机的 设置->共享文件夹，在固定分配添加，只勾选 `固定分配` ，不勾选 `只读分配` 和 `自动挂载`。   
2. 在 `/mnt/` 目录下面建立相应的目录，例如建立一个 `Blog` 的文件夹，那么在 `/etc/fstab` 文件中添加下面的内容： 

    Blog /mnt/Blog vboxsf rw,gid=samsara,uid=samsara,auto 0 0
3. 可以重启虚拟机后自动挂载，也可以使用 `sudo mount -a` 来挂载。

## Issue 3
**问题：**  
virtualbox 安装增强功能时总是提示 The headers for the current running kernel were not found. If the following .....  
**解决方法：**   
直接升级了 virtualbox 软件后就 ok 了 

## Issue 4
**问题：**  
总是提示未能加载虚拟光盘  
**解决方法：**  
直接右击虚拟光盘弹出就可以了

## Issue 5
**问题：**  
开机时提示：

    welcome to emergency mode！after logging in ，type “journalctl -xb” to view system logs，
    “systemctl   reboot” to reboot ，“systemctl default” to try again to boot into default mode。
    give root password for maintenance
    （or type Control-D to continue）：

**解决方法：**  
**原因是文件 `/etc/fstab` 中添加的自动挂载的信息有错，导致开机时没有自动挂载成功。**  
1. 登陆 root ， 乱码也输入密码；  
2. `vim /etc/fstab` ，检查磁盘挂载信息，修改正确，如果不确定，则可以注释掉或者删除掉；  
3. `reboot` 来重启虚拟机。