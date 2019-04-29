---
title: 将直接 I/O 与 PIO 配合使用
description: 将直接 I/O 与 PIO 配合使用
ms.assetid: 84d36567-c8c6-4576-91a0-829c8819de4d
keywords:
- 直接 I/O WDK 内核
- 缓冲区 WDK I/O 直接 I/O
- 数据缓冲 WDK I/O，直接 I/O
- I/O WDK 内核，直接 I/O
- PIO 传输操作 WDK 内核
- 编程 I/O 传输 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e3565137cd214292717595d8d32c5f932648b46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383209"
---
# <a name="using-direct-io-with-pio"></a>将直接 I/O 与 PIO 配合使用





使用的驱动程序进行编程 I/O (PIO)，而不是 DMA 双向必须将用户空间缓冲区映射到系统空间地址范围。 下图说明了如何在 I/O 管理器设置[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)请求 PIO 传输操作中使用直接 I/O。

![说明使用 pio 的设备的直接 i/o 的关系图](images/3mdlpio.png)

下图显示如何使用 PIO 设备处理相同的任务。

1.  某一范围的用户空间的虚拟地址表示当前线程的缓冲区，该缓冲区的内容可能实际上存储在若干个物理上不连续的页。 如果缓冲区长度为零，I/O 管理器创建 MDL 来描述此缓冲区。

2.  I/O 管理器服务当前线程的读取的请求，为其线程通过一系列用户空间表示缓冲区的虚拟地址。

3.  I/O 管理器或 FSD 检查可访问性的用户提供缓冲区。 如果 I/O 管理器已创建 MDL，则会调用[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664) MDL 与指定的虚拟用户缓冲区的地址范围。 **MmProbeAndLockPages**还会填写 MDL 中相应的物理地址范围。

4.  I/O 管理器提供一个指针到 MDL (**MdlAddress**) IRP 请求传输操作中。 I/O 管理器或文件系统调用直到[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381) MDL 中描述的物理页面 IRP 驱动程序之后，保持锁定，并已分配的缓冲区。 但是，此类 MDL 中的虚拟地址可能会变得不可见 （和无效），甚至之前 IRP 发送到设备驱动程序或任何中间驱动程序，它可能会在设备驱动程序进行分层。

5.  如果驱动程序需要系统 （虚拟） 地址，该驱动程序会调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)与 IRP **MdlAddress**指针双向映射用户空间 MDL 到系统空间地址范围中的虚拟地址。 在上图中，AliasBuff 表示 MDL 描述的双向映射的地址。

6.  驱动程序使用系统空间的虚拟地址范围内的双向映射 MDL (AliasBuff) 若要将数据读入内存。

当驱动程序将通过调用完成 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)，I/O 管理器或文件系统发布 MDL 的双向映射的系统空间范围，如果该驱动程序调用**MmGetSystemAddressForMdlSafe**。 I/O 管理器或文件系统解除锁定 MDL 和驱动程序的代表会释放 MDL 和 IRP 中所述的页面。 为了更好的性能，驱动程序应避免双向 MDL 物理地址映射到系统空间中所述步骤 3 中，除非它们必须使用虚拟地址。 执行此操作不必要地使用系统页表项，并可以减少驱动程序性能和可伸缩性。 此外，系统可能会崩溃如果占满页表项，因为大多数旧驱动程序无法处理这种情况。

当前用户线程的缓冲区以及该线程本身保证该线程是最新时才可驻留在物理内存。 为在上图中所示的线程，其用户缓冲区的内容可能出页到辅助存储时运行另一个进程的线程。 运行另一个进程的线程时，可以覆盖请求线程的缓冲区的系统物理内存，除非内存管理器已锁定，并保留那些包含原始线程的缓冲区的相应物理页。

但是，原始线程的虚拟地址其缓冲区不保持不可见时另一个线程是最新，即使内存管理器保留缓冲区的物理页。 因此，驱动程序不能使用返回的虚拟地址[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)访问内存。 此例程的调用方必须传递到其结果[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402) (以及 IRP **MdlAddress**指针) 才能使用基于数据包的系统的数据传输或主总线 DMA。

 

 




