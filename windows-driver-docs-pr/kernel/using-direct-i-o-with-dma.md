---
title: 将直接 I/O 与 DMA 配合使用
description: 将直接 I/O 与 DMA 配合使用
ms.assetid: 0e609613-9023-4f35-a9c5-d68c8b676cfe
keywords:
- 直接 i/o WDK 内核
- 缓冲 WDK i/o，直接 i/o
- 数据缓冲区 WDK i/o，直接 i/o
- I/o WDK 内核，直接 i/o
- DMA 传输 WDK 内核，直接 i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b00803099ee0ad2690bb477c78428716c05c609
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189269"
---
# <a name="using-direct-io-with-dma"></a>将直接 I/O 与 DMA 配合使用





下图说明了 i/o 管理器如何为使用直接 i/o 的 DMA 传输操作设置 [**IRP \_ MJ \_ 读取**](./irp-mj-read.md) 请求。

![说明使用 dma 的设备的用户缓冲区上的直接 i/o 的示意图](images/3mdldrct.png)

上图说明了驱动程序如何使用 IRP 的 **MdlAddress** 来传输读取请求的数据。 该图中的驱动程序使用基于数据包的系统或 bus 主机 DMA，并通过 DO DIRECT IO 运算设备**Flags**对象的标志 \_ \_ 。

1.  某些范围的用户空间虚拟地址表示当前线程的缓冲区，该缓冲区的内容实际上可能存储在与上图)  (深色底纹相同的部分中。 I/o 管理器会创建一个 MDL 来描述此缓冲区。 MDL 是一种不透明的数据结构，由内存管理器定义，将特定的虚拟地址范围映射到一个或多个基于页面的物理地址范围。 有关详细信息，请参阅[使用 MDL](using-mdls.md)。

2.  I/o 管理器为当前线程的读取请求提供服务，该请求为其传递了一个表示缓冲区的用户空间虚拟地址范围。

3.  I/o 管理器或文件系统驱动程序 (FSD) 检查用户提供的缓冲区的可访问性，并与以前创建的 MDL 调用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 。 **MmProbeAndLockPages** 还会在 MDL 中填充相应的物理地址范围。

    如上图所示，一个虚拟范围的 MDL 可以有多个相应的基于页面的物理地址条目，并且缓冲区的虚拟范围可能会以与 MDL 描述的第一页和最后一页开头的某个字节偏移量开始和结束。

4.  I/o 管理器提供指向 MDL (**MdlAddress**) 的指针，该 MDL 请求传输操作。 在驱动程序完成 IRP 后，在 i/o 管理器或文件系统调用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 之前，MDL 中描述的物理页面将保持锁定状态并分配给缓冲区。 但是，即使在将 IRP 发送到设备驱动程序或可能会分层到设备驱动程序的任何中间驱动程序之前，此类 MDL 中的虚拟地址也会变得不可见 (和无效) 。

5.  如果驱动程序使用基于数据包的系统或 bus 主机 DMA，则其[*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程将使用 IRP 的**MdlAddress**指针调用[**MmGetMdlVirtualAddress**](./mm-bad-pointer.md) ，以获取 MDL 基于页面的条目的基本虚拟地址。

6.  然后， *AdapterControl*例程使用**MmGetMdlVirtualAddress**返回的基址调用[**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) ，以将数据从设备直接读入物理内存。  (有关详细信息，请参阅 [适配器对象和 DMA](./introduction-to-adapter-objects.md)。 ) 

驱动程序应始终检查缓冲区长度。 请注意，i/o 管理器不会为长度为零的缓冲区创建 MDL。

 

