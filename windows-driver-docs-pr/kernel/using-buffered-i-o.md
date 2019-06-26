---
title: 使用缓冲 I/O
description: 使用缓冲 I/O
ms.assetid: 69291156-babb-465a-9e80-1766f075768b
keywords:
- 缓冲的 I/O WDK 内核
- 缓冲区 WDK I/O 缓冲 I/O
- 数据缓冲区 WDK I/O 缓冲 I/O
- 非分页的系统缓冲 WDK I/O
- I/O 控制代码 WDK 内核，缓冲 I/O
- I/O WDK 内核缓冲 I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e65b280741fac4a942f6f6f26e94634b38b492
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358196"
---
# <a name="using-buffered-io"></a>使用缓冲 I/O





服务是交互式的或速度缓慢的设备，或一个通常一次传输的数据量相对较少的驱动程序应使用[缓冲 I/O](methods-for-accessing-data-buffers.md)传输方法。 对小型的交互式传输使用缓冲的 I/O 可以提高总物理内存使用情况，因为内存管理器不需要完整的物理页锁定为每次传输，因为它请求的驱动程序的直接 I/O。 通常情况下，视频、 键盘、 鼠标、 串行、 并行的驱动程序请求缓冲的 I/O。

I/O 管理器确定 I/O 操作使用缓冲的 I/O，如下所示：

-   有关[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)并[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求时，执行操作\_缓冲\_中设置 IO**标志**的成员[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)结构。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

-   有关[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)并[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求时，IOCTL 代码的值包含方法\_的形式缓冲*留空，则*IOCTL 值中的值。 有关详细信息，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

下图说明了如何在 I/O 管理器设置**IRP\_MJ\_读取**针对传输操作中使用的缓冲 I/O 请求的请求。

![说明用户缓冲区缓冲的 i/o 的关系图](images/3mdlbffr.png)

图显示了如何使用驱动程序的概述**SystemBuffer** IRP 传输数据的读取请求时驱动程序包含或运算的设备对象中的指针**标志**使用\_缓冲\_IO:

1.  某一范围的用户空间的虚拟地址表示当前线程的缓冲区，该缓冲区的内容可能某个位置存储在一系列基于页面的物理地址 （在上图中的暗阴影）。

2.  I/O 管理器服务当前线程的读取的请求，为其线程通过一系列用户空间表示缓冲区的虚拟地址。

3.  I/O 管理器检查可访问性和调用的用户提供缓冲区[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)若要创建非分页的系统空间缓冲区 (**SystemBuffer**)用户提供缓冲区的大小。

4.  I/O 管理器提供对新分配的访问**SystemBuffer** IRP 发送到该驱动程序中。

    如果该图显示了写入请求，I/O 管理器将数据从用户缓冲区复制到系统缓冲区它发送 IRP 到驱动程序之前。

5.  有关在上图中所示的读取请求，该驱动程序读取数据，从设备到系统空间缓冲区。 此缓冲区的内存非分页和驱动程序可以安全地访问缓冲区，而不会第一个锁定。 当已满足读取的请求时，该驱动程序会调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与 IRP。

6.  当原始线程再次处于活动状态时，I/O 管理器中读取数据系统将缓冲区复制到用户缓冲区。 它还调用[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)以释放系统缓冲区。

I/O 管理器已创建该驱动程序的系统空间缓冲区后，请求的用户模式线程可以换出，另一个线程，可能是由属于另一个进程的线程可以重复使用其物理内存。 但是，IRP 中提供的系统空间虚拟地址范围之前将保持有效的驱动程序调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与 IRP。

在某个时间，具体而言，驱动程序执行多页传输，传输的数据量大的驱动程序不应尝试使用缓冲的 I/O。 当系统运行时，非分页缓冲的池可以零碎的以便在 I/O 管理器不能分配大型的连续未分配的系统空间缓冲区以将 Irp 中发送了此类驱动程序。

通常情况下，驱动程序使用缓冲的 I/O 对于某些类型的 Irp，如[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求时，即使它还使用[直接 I/O](methods-for-accessing-data-buffers.md)。 通常使用直接 I/O 驱动程序仅对于这样[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)并[ **IRP\_MJ\_写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求，并可能是驱动程序定义[ **IRP\_MJ\_内部\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求需要传输大量数据。

每个**IRP\_MJ\_设备\_控制**并**IRP\_MJ\_内部\_设备\_控件**请求包括 I/O 控制代码。 如果 I/O 控制代码指示 IRP，必须支持通过使用缓冲的 I/O，I/O 管理器将使用单个系统缓冲区来表示用户应用程序的输入和输出缓冲区。 驱动程序支持此类 I/O 控制代码必须从缓冲区读取输入的数据 （如果有），然后将提供的数据输出 （如果有） 通过覆盖的输入的数据。 有关详细信息，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

 

 




