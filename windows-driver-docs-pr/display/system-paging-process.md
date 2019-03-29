---
title: 系统分页进程
description: 大多数分页操作发生在系统分页进程的上下文中。 唯一的例外是从 UpdateGpuVirtualAddress 回调，它在特殊随附上下文中出现且出现同步呈现的页表更新。
ms.assetid: B010C7E5-6B67-43D2-92A6-5258B132FB5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd53b3081a0d0fa329f4cd4adf380b9f01214b0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576303"
---
# <a name="system-paging-process"></a>系统分页进程


大多数分页操作发生在系统分页进程的上下文中。 唯一的例外是从页面表更新[ *UpdateGpuVirtualAddress 回调*](https://msdn.microsoft.com/library/windows/hardware/dn906365)，这发生在特殊的配套的上下文中，发生呈现的同步。

Microsoft DirectX 图形内核使用系统分页进程来执行分页操作，如：

-   系统和本地的图形处理单元 (GPU) 内存之间传输分配
-   填充分配，则使用模式
-   更新页表
-   映射分配到 aperture 段
-   刷新转换旁视缓冲

分页进程都有其自己的 GPU 虚拟地址空间、 GPU 上下文和直接内存访问 (DMA) 缓冲区 （称为分页）。 它具有其自己固定在物理内存并仅在电源转换过程中逐出的页表。

分页进程虚拟地址空间具有预定义的布局，适配器初始化和内存内容丢失由于电源转换后的每个时间期间进行初始化。

![虚拟和物理地址空间](images/system-paging-process.1.png)

DirectX 图形内核初始化足够的页表和根页表，将覆盖的 1 GB 虚拟地址空间中的页表项。 暂存区域是用于临时映射分配到分页进程虚拟地址空间的传输和填充操作过程。 如果分配不会不适合的虚拟地址暂存区域，在传输操作将完成块区中。

为分页进程创建系统根页表分配。 在初始化和永远不会更改 （除非 power 转换后） 过程中设置其内容。

系统进程的页表分为两个部分：

一个*系统页表*将创建一个反映*暂存区域中的页表*到系统进程的地址空间。 这允许系统过程来修改暂存区域页表和地图/取消映射从暂存区域根据需要的内存。 页表的内容在适配器初始化过程中设置并永远不会更改。
*暂存区域中的页表*页表项用于将分配映射到分页进程的虚拟地址空间。 它们初始化为*无效*在初始化过程中，更高版本用于分页操作。
通过初始化都分页进程的页表[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)适配器初始化和事件加电过程分页操作。 对于这些操作， **PageTableUpdateMode**都强制发往**CPU\_虚拟**，并且必须使用的 CPU （不应使用分页缓冲区） 立即完成。

完成更新的页表条目的所有其他进程使用**PageTableUpdateMode**指定驱动程序。 在分页过程的上下文中完成这些更新。

下面是如何完成安装程序：

1.  创建根页表分配和较低级别的页表分配以涵盖 1 GB 的地址空间。
2.  分配是提交到一个内存段。
3.  多个[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)分页操作颁发给驱动程序来初始化页表项。

作为分页进程虚拟地址空间初始化的示例，让我们考虑使用以下参数的情况：

-   页面大小为 4096 个字节
-   分页进程虚拟地址空间为 1 GB
-   页表条目大小为 4 个字节

在这种情况下，我们需要 2 级翻译方案组成：

-   一个系统根页表
-   一个系统页表
-   255 暂存区域页表

下图显示了如何将初始化页表基于在根页表和在物理内存中的页表的位置。 请注意，仅作为图给出的物理地址。
页表包含了 4 MB 的地址空间。 因此系统页表涵盖了所有的暂存区域页表。 从 4 MB 的虚拟地址开始的暂存区域。

正如您看到的虚拟地址范围从 0 到 4095 将无效。

![页表初始化](images/system-paging-process.2.png)

 

 





