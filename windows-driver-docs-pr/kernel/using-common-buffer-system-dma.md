---
title: 使用公用缓冲区系统 DMA
description: 使用公用缓冲区系统 DMA
ms.assetid: ee060aa4-2db4-4bd2-b107-b71acced97fd
keywords:
- 系统 DMA WDK 内核，常见的缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，常见的缓冲区
- AllocateCommonBuffer
- 自动初始化模式 WDK DMA
- 连续 DMA WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aa962faedfdd8fed147bc5910be06237729b95e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361085"
---
# <a name="using-common-buffer-system-dma"></a>使用公用缓冲区系统 DMA





使用系统 DMA 控制器的自动初始化模式的驱动程序必须为传输到其中或从哪些 DMA 可执行的缓冲区分配内存。驱动程序调用[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575)若要获取此缓冲区中，通常从[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)处理例程[**IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 下图显示了如何将驱动程序分配的缓冲区，并将其虚拟地址范围映射到系统的物理内存。

![说明如何将驱动程序为系统 dma 分配常见缓冲区的关系图](images/3hlsysbf.png)

上图所示，驱动程序将采用以下步骤来分配系统 DMA 缓冲区：

1.  驱动程序调用[ **AllocateCommonBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff540575)，将指针传递到该适配器对象，返回的[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)，以及在请求其缓冲区的字节数的长度。 经济方面，使用内存输入*长度*值缓冲区应为小于或等于页面\_大小应为整数倍的页或\_大小。

2.  如果**AllocateCommonBuffer**返回**NULL**指针，该驱动程序应释放它已经占用任何系统资源并返回状态\_不足\_中的资源响应**IRP\_MN\_启动\_设备**请求。

    否则为**AllocateCommonBuffer**分配请求的系统的虚拟地址空间中的内存量并返回到该缓冲区的两种不同类型的指针：

    -   *LogicalAddress*驱动程序必须提供存储，但它之后应忽略的缓冲区 (在上图中的 BufferLogicalAddress)

    -   虚拟地址的驱动程序还必须存储，以便它可以生成描述 DMA 操作其缓冲区 MDL 缓冲区 (在上图中的 BufferVirtualAddress)

    该驱动程序应将这些指针存储在设备扩展或其他驱动程序分配的常驻内存中。

3.  驱动程序调用[ **IoAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548263)分配 MDL 缓冲区。 驱动程序传递*VirtualAddress*返回的缓冲区**AllocateCommonBuffer**并*长度*其缓冲区以分配 MDL。

4.  驱动程序调用[ **MmBuildMdlForNonPagedPool** ](https://msdn.microsoft.com/library/windows/hardware/ff554498)所返回的指针与**IoAllocateMdl**以将其常驻缓冲区的虚拟地址范围映射到系统物理内存。

分配常见缓冲区并映射其虚拟地址范围后, 的从属的设备驱动程序可以开始处理 IRP，请求 DMA 传输。 若要执行此操作，该驱动程序调用支持例程的以下一般规则：

1.  驱动程序编写器根据判断[ **RtlMoveMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562030)数据将从复制锁定的用户缓冲区到驱动程序分配的常见缓冲区传输到设备

2.  **AllocateAdapterChannel**时驱动程序已准备好编程 DMA 其设备，并且需要系统 DMA 控制器

3.  [**MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)，与介绍驱动程序分配常见的缓冲区，若要设置在传输操作的系统 DMA 控制器 MDL

    请注意，该驱动程序调用**MapTransfer**仅一次，以将系统 DMA 控制器设置为使用其常见的缓冲区。 传送期间，驱动程序可以调用[ **ReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff560782)以确定多少个字节保持传输，以及如果有必要，请调用**RtlMoveMemory**复制更多的数据到或从用户缓冲区。

4.  [**FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)时驱动程序已完成其 DMA 传输向/从从属的设备

5.  [**FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)只要已传输的所有请求的数据，或者驱动程序必须由于设备 I/O 错误而失败 IRP

所返回的适配器对象指针**IoGetDmaAdapter**是必需的参数，为每种支持之外例程**RtlMoveMemory**。

单独的驱动程序在不同时间点，具体取决于每个驱动程序的实现来服务其设备的方式调用这一序列的支持例程。 例如，一个驱动程序的[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程可能会使对调用**AllocateAdapterChannel**，另一个驱动程序可能会进行此调用，从删除从 Irp 的例程驱动程序创建互锁队列，和另一个驱动程序可能会进行此调用时其从属 DMA 设备将指示它已准备好将数据传输。

 

 




