---
title: 虚拟地址空间
description: 虚拟地址空间
ms.assetid: 5A3E1918-E5A4-4129-B0C2-45B6EEB7EFB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f945bd59b717c7e242ce46398ea33f2ae76f1582
ms.sourcegitcommit: 8fce8b22c7437f0aa322c40625d5163e8812ea01
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77146509"
---
# <a name="virtual-address-spaces"></a>虚拟地址空间


当处理器读取或写入内存位置时，它会使用虚拟地址。 在读取或写入操作过程中，处理器会将虚拟地址转换为物理地址。 通过虚拟地址访问内存有以下优势：

-   程序可以使用一系列连续的虚拟地址来访问物理内存中不连续的大内存缓冲区。

-   程序可以使用一系列虚拟地址来访问大于可用物理内存的内存缓冲区。 当物理内存的供应量变小时，内存管理器会将物理内存页（通常大小为 4 KB）保存到磁盘文件。 数据或代码页会根据需要在物理内存与磁盘之间移动。

-   不同进程使用的虚拟地址彼此隔离。 一个进程中的代码无法更改正在由另一进程或操作系统使用的物理内存。

进程可用的虚拟地址范围称为该进程的“虚拟地址空间”  。 每个用户模式进程都有其各自的专用虚拟地址空间。 对于 32 位进程，虚拟地址空间通常为 2 GB，范围从 0x00000000 至 0x7FFFFFFF。 对于 64 位 Windows 上的 64 位进程，虚拟地址空间为 128 TB，范围从 0x000'00000000 至 0x7FFF'FFFFFFFF。 一系列虚拟地址有时称为一系列“虚拟内存”  。 有关详细信息，请参阅[内存和地址空间限制](https://docs.microsoft.com/windows/win32/memory/memory-limits-for-windows-releases#memory-and-address-space-limits)。

此图说明了虚拟地址空间的一些重要功能。

![图：两个进程的虚拟地址空间](images/virtualaddressspace01.png)

该图显示了两个 64 位进程的虚拟地址空间：Notepad.exe 和 MyApp.exe。 每个进程都有其各自的虚拟地址空间，范围从 0x000'0000000 至 0x7FF'FFFFFFFF。 每个阴影块都表示虚拟内存或物理内存的一个页（大小为 4 KB）。 注意，Notepad 进程使用从 0x7F7'93950000 开始的虚拟地址的三个连续页面。 但虚拟地址的这三个连续页面会映射到物理内存中的非连续页面。 另请注意，两个进程都使用从 0x7F7'93950000 开始的虚拟内存页面，但这些虚拟页面映射到物理内存的不同页面。

## <a name="span-iduser_space_and_system_spacespanspan-iduser_space_and_system_spacespanspan-iduser_space_and_system_spacespanuser-space-and-system-space"></a><span id="User_space_and_system_space"></span><span id="user_space_and_system_space"></span><span id="USER_SPACE_AND_SYSTEM_SPACE"></span>用户空间和系统空间


诸如 Notepad.exe 和 MyApp.exe 的进程在用户模式下运行。 核心操作系统组件和多个驱动程序在更有特权的内核模式下运行。 有关处理器模式的详细信息，请参阅[用户模式和内核模式](user-mode-and-kernel-mode.md)。 每个用户模式进程都有其各自的专用虚拟地址空间，但在内核模式下运行的所有代码都共享称为“系统空间”  的单个虚拟地址空间。 用户模式进程的虚拟地址空间称为“用户空间”  。

在 32 位 Windows 中，可用的虚拟地址空间共计为 2^32 字节（4 GB）。 通常，较低的 2 GB 用于用户空间，较高的 2 GB 用于系统空间。

![图：系统空间](images/virtualaddressspace02.png)

在 32 位 Windows 中，可以选择指定（在启动时）超过 2 GB 可用于用户空间。 其结果是系统空间可用的虚拟地址更少。 可以将用户空间的大小增加到 3 GB，在这种情况下，系统空间只有1 GB 可用。 若要增大用户空间的大小，请使用 [**BCDEdit /set increaseuserva**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)。

在 64 位 Windows 中，虚拟地址空间的理论大小为 2^64 字节（16 艾字节），但实际上仅使用 16 艾字节范围的一小部分。 范围从 0x000'00000000 至 0x7FF'FFFFFFFF 的 8 TB 用于用户空间，范围从 0xFFFF0800'00000000 至 0xFFFFFFFF'FFFFFFFF 的 248 TB 的部分用于系统空间。

![图：分页缓冲池和非分页缓冲池](images/virtualaddressspace03.png)

用户模式下运行的代码可以访问用户空间，但不能访问系统空间。 此限制可防止用户模式代码读取或更改受保护的操作系统数据结构。 内核模式下运行的代码既可以访问用户空间，也可以访问系统空间。 即，内核模式下运行的代码可以访问系统空间和当前用户模式进程的虚拟地址空间。

内核模式下运行的驱动程序必须在直接从用户空间地址中读取或写入这些地址时非常小心。 此方案说明了原因。

1.  用户模式程序发起从设备读取某些数据的请求。 程序提供缓冲区的起始地址以接收数据。

2.  内核模式下运行的设备驱动程序例程启动读取操作并将控制权返回给其调用程序。

3.  稍后，设备中断了当前正在运行的任何线程以显示读取操作完成。 中断由此任意线程（属于任意进程）上运行的内核模式驱动程序例程进行处理。
4.  此时，驱动程序不得将数据写入用户模式程序在步骤 1 中提供的开始地址。 此地址位于发起请求的进程的虚拟地址空间中，该进程很可能与当前进程不同。

## <a name="span-idpaged_pool_and_nonpaged_poolspanspan-idpaged_pool_and_nonpaged_poolspanspan-idpaged_pool_and_nonpaged_poolspanpaged-pool-and-nonpaged-pool"></a><span id="Paged_pool_and_Nonpaged_pool"></span><span id="paged_pool_and_nonpaged_pool"></span><span id="PAGED_POOL_AND_NONPAGED_POOL"></span>分页缓冲池和非分页缓冲池


在用户空间中，所有物理内存页面都可以根据需要调出到磁盘文件。 在系统空间中，某些物理页面可以调出，而其他物理页面则不能。 系统空间具有用于动态分配内存的两个区域：分页缓冲池和非分页缓冲池。 

分页缓冲池中分配的内存可以根据需要调出到磁盘文件。 非分页缓冲池中分配的内存永远无法调出到磁盘文件。

![图：比较分页缓冲池中的内存分配与非分页缓冲池中的内存分配](images/virtualaddressspace04.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[用户模式和内核模式](user-mode-and-kernel-mode.md)

 

 






