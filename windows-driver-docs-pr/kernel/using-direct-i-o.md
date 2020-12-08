---
title: 使用直接 I/O
description: 使用直接 I/O
keywords:
- 直接 i/o WDK 内核
- 缓冲 WDK i/o，直接 i/o
- 数据缓冲区 WDK i/o，直接 i/o
- I/o WDK 内核，直接 i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef131e5219386d24dc1350a8a40403a7b5dcee66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830381"
---
# <a name="using-direct-io"></a>使用直接 I/O





对于可以一次传输大量数据的设备，其驱动程序应将直接 i/o 用于这些传输。 将直接 i/o 用于大容量传输可提高驱动程序的性能，方法是降低中断开销，消除缓冲 i/o 固有的内存分配和复制操作。

通常情况下，大容量存储设备驱动程序请求传输请求的直接 i/o，其中包括使用直接内存访问的最低级别驱动程序 (DMA) 或程控 i/o (PIO) ，以及其上链式的任何中间驱动程序。

I/o 管理器按如下方式确定 i/o 操作使用的是直接 i/o：

-   对于 [**IRP \_ mj \_ 读取**](./irp-mj-read.md)和 [**irp \_ Mj \_ 写入**](./irp-mj-write.md)请求，请 \_ \_ 在 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的 **Flags** 成员中设置直接 IO。 有关详细信息，请参阅 [初始化设备对象](initializing-a-device-object.md)。

-   对于 [**IRP \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 和 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求，ioctl 代码的值将直接包含 \_ 方法 \_ 或方法 \_ OUT \_ 作为 IOCTL 值中的 *TransferType* 值。 有关详细信息，请参阅 [定义 I/o 控制代码](defining-i-o-control-codes.md)。

使用直接 i/o 的驱动程序有时也会使用缓冲 i/o 来处理某些 Irp。 具体而言，对于某些 i/o 控制代码，驱动程序通常使用缓冲 i/o 来处理需要数据传输的 **IRP \_ MJ \_ 设备 \_ 控制** 请求，而不考虑驱动程序是否使用直接 i/o 进行读写操作。

设置直接 i/o 传输会略有不同，具体取决于是否使用 DMA 或 PIO。 有关详细信息，请参阅：

[将直接 I/O 与 DMA 配合使用](using-direct-i-o-with-dma.md)

[将直接 I/O 与 PIO 配合使用](using-direct-i-o-with-pio.md)

驱动程序必须采取措施来维护 DMA 和 PIO 传输过程中的缓存一致性。 有关详细信息，请参阅 [维护缓存一致性](maintaining-cache-coherency.md)。

 

