---
title: 将直接 I/O 与 DMA 配合使用
description: 将直接 I/O 与 DMA 配合使用
ms.assetid: 0e609613-9023-4f35-a9c5-d68c8b676cfe
keywords:
- 直接 I/O WDK 内核
- 缓冲区 WDK I/O 直接 I/O
- 数据缓冲 WDK I/O，直接 I/O
- I/O WDK 内核，直接 I/O
- DMA 传输 WDK 内核，直接 I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c73882f5ff90bb8f3586040e8017a238b07e94e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381685"
---
# <a name="using-direct-io-with-dma"></a>将直接 I/O 与 DMA 配合使用





下图说明了如何在 I/O 管理器设置[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求 DMA 传输操作中使用直接 I/O。

![说明用户缓冲区对于使用 dma 的设备上的直接 i/o 的关系图](images/3mdldrct.png)

上图阐释了如何驱动程序可以使用 IRP **MdlAddress**将读取请求的数据传输。 图中的驱动程序使用基于数据包的系统或总线 master DMA，并且具有设备对象的或运算**标志**使用\_直接\_IO。

1.  某一范围的用户空间的虚拟地址表示当前线程的缓冲区，该缓冲区的内容可能实际上存储在若干个物理上不连续的页 （在上图中的暗阴影）。 I/O 管理器创建 MDL 来描述此缓冲区。 MDL 是由内存管理器中，将在特定的虚拟地址范围映射到一个或多个基于页面的物理地址范围定义一个不透明的数据结构。 有关详细信息，请参阅[使用 MDLs](using-mdls.md)。

2.  I/O 管理器服务当前线程的读取的请求，为其线程通过一系列用户空间表示缓冲区的虚拟地址。

3.  I/O 管理器或文件系统驱动程序 (FSD) 检查可访问性和调用的用户提供缓冲区[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)使用以前创建的 MDL。 **MmProbeAndLockPages**还会填写 MDL 中相应的物理地址范围。

    上图所示，虚拟范围 MDL 可以有多个相应的基于页面的物理地址条目，和缓冲区的虚拟范围可能开始和结束在一些字节从 MDL 所描述的第一个和最后一页开始偏移量。

4.  I/O 管理器提供一个指针到 MDL (**MdlAddress**) IRP 请求传输操作中。 I/O 管理器或文件系统调用直到[ **MmUnlockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages) MDL 中描述的物理页面 IRP 驱动程序之后，保持锁定，并已分配的缓冲区。 但是，此类 MDL 中的虚拟地址可能会变得不可见 （和无效），甚至之前 IRP 发送到设备驱动程序或任何中间驱动程序，它可能会在设备驱动程序进行分层。

5.  如果驱动程序使用基于数据包的系统或总线 master DMA，其[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)例程调用[ **MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)与IRP **MdlAddress**用于获取 MDL 的基于页面的条目的基的虚拟地址的指针。

6.  *AdapterControl*例程然后调用[ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)使用返回的基址**MmGetMdlVirtualAddress**读取从设备直接插入物理内存的数据。 (有关详细信息，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)。)

驱动程序应始终检查缓冲区长度。 请注意 I/O 管理器不会创建一个零长度缓冲区 MDL。

 

 




