---
layout: post
title:  "VirtualBox 虚拟机磁盘镜像"
categories: Tools
tag: VirtualBox 
---

* content
{:toc}


VirtualBox 支持的虚拟硬盘格式如下：

- VDI
- VMDK
- VHD
- HDD

这几种格式的特性：  

- **动态调整大小：** VDI，VMDK，VHD 都支持动态调整大小。VMDK 具有将村粗的文件分割。其中，VMDK 具有将存储的文件分割为少于 2 GB 文件的附加功能，如果文件系统的文件大小限制较小，那么这个功能非常有用。
- **可以做快照：** 都支持做快照。
- **以较小代价移动到另一个操作系统或者虚拟机：**  
    + VDI 是 VirtualBox 的基本且独有的格式。目前应该还没有支持这种格式的其他软件。  
    + VMDK 是专门为 VMWare 开发，但其他虚机像 Sun xVM，QEMU，VirtualBox，SUSE Studio 和 .NET DiscUtils 也都支持这种格式。 (这种格式应该是最适合题主的，因为您希望在Ubuntu上正常运行虚拟机软件。)    
    + VHD 是 Microsoft Virtual PC 的基本格式。这是在 Microsoft 产品系中受欢迎的格式。  
    + 关于 HDD，从[这个站点](https://www.parallels.com/)来看，Parallels 是 Mac OS X 产品，可能不太适合您，特别是考虑到VirtualBox仅支持旧版本的HDD格式。

- **性能：**  通常格式不会影响性能，或者说至少对性能影响可以忽略不计。影响性能的因素主要有：物理设备限制(磁盘或固态硬盘？)；扩展动态分配的虚拟机磁盘的过程会影响性能，比如说写入操作随着虚拟磁盘扩展而变慢，但一旦它足够大，扩展的影响应该会减少；采用哪种虚拟化技术，看是硬件还是软件，硬件虚拟化技术有助于VirtualBox提高虚拟操作系统的速度；由于是虚拟化过程，性能总是比在主机上直接运行操作系统要慢。

**选择：**
通常使用 VDI，因为它是 VirtualBox 的基本(native)格式;然而，使用 VMDK(VMWare格式) 可以增加与其他虚拟机软件的兼容性。  
VirtualBox 在 Ubuntu 上运行良好，所以如果目标是 Windows /Ubuntu 的互操作性，VDI将是一个很棒的选择。  
另外两个，其中 VHD 是微软系的格式，而 HDD 是苹果系的格式，这些都对跨平台有限制，所以，不太推荐。

**关于虚拟机迁移：**
关于虚拟机迁移，更通用的做法可能是使用 VirtualBox 文件/导出功能，创建一个“开放的虚拟化设备”.ova文件，然后可以导入到 VMware。通过这种方法，您可以将虚拟机移植到支持.ova的任何虚拟化系统，而无需关心您在 VirtualBox 中使用哪种磁盘映像格式。   
如果您已经有一个.vdi文件，您可以试试这个是否有效，而无需创建新的虚拟机：将其导出为.ova，然后尝试使用vmware进行导入。

**参考链接：** [https://vimsky.com/article/3578.html](https://vimsky.com/article/3578.html)

