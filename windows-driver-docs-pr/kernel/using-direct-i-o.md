---
title: 使用直接 I/O
description: 使用直接 I/O
ms.assetid: e40b4657-833f-404c-8472-2e33564129a5
keywords:
- 直接 i/o WDK 内核
- 缓冲 WDK i/o，直接 i/o
- 数据缓冲区 WDK i/o，直接 i/o
- I/o WDK 内核，直接 i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd0cdd534837fe343fc3f7fcc711920b5a007a7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838360"
---
# <a name="using-direct-io"></a>使用直接 I/O





对于可以一次传输大量数据的设备，其驱动程序应将直接 i/o 用于这些传输。 将直接 i/o 用于大容量传输可提高驱动程序的性能，方法是降低中断开销，消除缓冲 i/o 固有的内存分配和复制操作。

通常情况下，大容量存储设备驱动程序请求传输请求的直接 i/o，包括使用直接内存访问（DMA）或程控 i/o （PIO）的最低级别驱动程序，以及其上链式的任何中间驱动程序。

I/o 管理器按如下方式确定 i/o 操作使用的是直接 i/o：

-   对于[**IRP\_mj\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)和[**IRP\_mj\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求，请在设备的**Flags**成员[ **\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构中设置\_直接\_IO。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

-   对于[**IRP\_mj\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)和[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求，IOCTL 代码的值包含\_直接或方法\_OUT 中的方法\_\_直接作为 IOCTL 值中的*TransferType*值。 有关详细信息，请参阅[定义 I/o 控制代码](defining-i-o-control-codes.md)。

使用直接 i/o 的驱动程序有时也会使用缓冲 i/o 来处理某些 Irp。 具体而言，驱动程序通常对**IRP\_\_\_MJ**的某些 i/o 控制代码使用缓冲 i/o，而不考虑驱动程序是否将直接 i/o 用于读取和写入操作。

设置直接 i/o 传输会略有不同，具体取决于是否使用 DMA 或 PIO。 有关详细信息，请参阅：

[将直接 i/o 用于 DMA](using-direct-i-o-with-dma.md)

[使用带有 PIO 的直接 i/o](using-direct-i-o-with-pio.md)

驱动程序必须采取措施来维护 DMA 和 PIO 传输过程中的缓存一致性。 有关详细信息，请参阅[维护缓存一致性](maintaining-cache-coherency.md)。

 

 




