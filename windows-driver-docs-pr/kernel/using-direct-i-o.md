---
title: 使用直接 I/O
description: 使用直接 I/O
ms.assetid: e40b4657-833f-404c-8472-2e33564129a5
keywords:
- 直接 I/O WDK 内核
- 缓冲区 WDK I/O 直接 I/O
- 数据缓冲 WDK I/O，直接 I/O
- I/O WDK 内核，直接 I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fcff7c2d6f3f2a572593d27198f91d884e1e7c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381658"
---
# <a name="using-direct-io"></a>使用直接 I/O





可以一次传输大量数据的设备的驱动程序应使用这些传输的直接 I/O。 对大型传输使用直接 I/O 可以提高驱动程序的性能，同时通过减少其中断开销，并消除内存分配和复制操作中缓冲的 I/O 固有。

通常情况下，大容量存储设备驱动程序请求的传输请求，包括使用直接内存访问 (DMA) 或编程 I/O (PIO) 的最低级别驱动程序，以及链接在其上方的任何中间驱动程序直接 I/O。

I/O 管理器确定 I/O 操作使用直接 I/O，如下所示：

-   有关[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)并[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求时，执行操作\_直接\_中设置 IO**标志**的成员[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)结构。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

-   有关[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)并[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求时，IOCTL 代码的值包含方法\_IN\_直接访问或通过方法\_出\_直接作为*留空，则*IOCTL 值中的值。 有关详细信息，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

使用直接 I/O 驱动程序有时也将使用缓冲的 I/O 来处理某些 Irp。 具体而言，驱动程序通常使用缓冲的 I/O 有关的某些 I/O 控制代码**IRP\_MJ\_设备\_控制**需要数据传输，无论是否使用该驱动程序的请求直接 I/O 进行读取和写入操作。

设置直接 I/O 传输而异略有不同，具体取决于是否正在使用 DMA 或 PIO。 有关详细信息，请参阅：

[使用 DMA 直接 I/O](using-direct-i-o-with-dma.md)

[使用 PIO 直接 I/O](using-direct-i-o-with-pio.md)

驱动程序必须采取措施来维护缓存一致性 DMA 和 PIO 传输过程。 有关详细信息，请参阅[维护缓存一致性](maintaining-cache-coherency.md)。

 

 




