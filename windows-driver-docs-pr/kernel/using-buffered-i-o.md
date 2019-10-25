---
title: 使用缓冲 I/O
description: 使用缓冲 I/O
ms.assetid: 69291156-babb-465a-9e80-1766f075768b
keywords:
- 缓冲 i/o WDK 内核
- 缓冲 WDK i/o，缓冲 i/o
- 数据缓冲区 WDK i/o，缓冲 i/o
- 非分页系统缓冲 WDK i/o
- I/o 控制代码 WDK 内核，缓冲 i/o
- I/o WDK 内核，缓冲 i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55676be840c1f446056457cec777459a86c2104b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836032"
---
# <a name="using-buffered-io"></a>使用缓冲 I/O





服务于交互式或慢速设备的驱动程序，或者一次通常传输相对较小数据量的驱动程序时，应使用[缓冲 i/o](methods-for-accessing-data-buffers.md)传输方法。 对小型交互式传输使用缓冲 i/o 可以提高总体物理内存使用量，因为内存管理器不需要为每次传输锁定一整页，因为它对请求直接 i/o 的驱动程序也是如此。 通常，视频、键盘、鼠标、串行和并行驱动程序请求缓冲 i/o。

I/o 管理器按如下方式确定 i/o 操作使用的是缓冲 i/o：

-   对于[**IRP\_mj\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)和[**IRP\_mj\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求，执行\_缓冲\_IO 是在[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的**Flags**成员中设置的。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

-   对于[**IRP\_mj\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)和[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求，IOCTL 代码的值包含作为*TransferType*值缓冲的方法\_在 IOCTL 值中。 有关详细信息，请参阅[定义 I/o 控制代码](defining-i-o-control-codes.md)。

下图说明了 i/o 管理器如何为使用缓冲 i/o 的传输操作设置**IRP\_MJ\_读取**请求。

![说明用户缓冲区的缓冲 i/o 的关系图](images/3mdlbffr.png)

此图显示了驱动程序如何使用 IRP 中的**SystemBuffer**指针来传输读取请求的数据，当驱动程序使用 DO\_缓冲\_IO 来运算设备对象**标志**时：

1.  某些范围的用户空间虚拟地址表示当前线程的缓冲区，该缓冲区的内容可能存储在一系列基于页面的物理地址（上图中的暗阴影）范围内。

2.  I/o 管理器为当前线程的读取请求提供服务，该请求为其传递了一个表示缓冲区的用户空间虚拟地址范围。

3.  I/o 管理器检查用户提供的缓冲区中的可访问性，并调用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)来创建非分页系统空间缓冲区（**SystemBuffer**）用户提供的缓冲区大小。

4.  I/o 管理器提供对它发送到驱动程序的 IRP 中新分配的**SystemBuffer**的访问权限。

    如果该图显示了写入请求，则 i/o 管理器会将数据从用户缓冲区复制到系统缓冲区，然后再将 IRP 发送到驱动程序。

5.  对于上图中显示的读取请求，驱动程序将数据从设备读取到系统空间缓冲区。 此缓冲区的内存未分页，驱动程序可以在不先锁定缓冲区的情况下安全地访问它。 如果已满足读取请求，驱动程序将调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)和 IRP。

6.  当原始线程再次处于活动状态时，i/o 管理器会将数据从系统缓冲区复制到用户缓冲区。 它还会调用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)来释放系统缓冲区。

在 i/o 管理器为驱动程序创建了系统空间缓冲区后，可以交换请求的用户模式线程，并使其物理内存可由另一个线程（可能是属于另一进程的线程）重用。 但是，在此驱动程序通过 IRP 调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)之前，IRP 中提供的系统空间虚拟地址范围始终有效。

一次传输大量数据的驱动程序（特别是执行多页传输的驱动程序）不应尝试使用缓冲 i/o。 当系统运行时，非分页池可能会成为碎片，因此，i/o 管理器无法为这样的驱动程序分配要在 Irp 中发送的较大的连续系统空间缓冲区。

通常，驱动程序对某些类型的 Irp 使用缓冲 i/o，例如[**irp\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，即使它也使用[直接 i/o](methods-for-accessing-data-buffers.md)也是如此。 使用直接 i/o 的驱动程序通常只为[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)和[**IRP\_mj\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求，以及可能的驱动程序定义的[**IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)需要大型数据传输的请求。

每个**IRP\_mj\_设备\_控制**和**IRP\_MJ\_内部\_设备\_控制**请求包括一个 i/o 控制代码。 如果 i/o 控制代码指示 IRP 必须使用缓冲 i/o 来支持，则 i/o 管理器使用单个系统缓冲区来表示用户应用程序的输入和输出缓冲区。 支持此类 i/o 控制代码的驱动程序必须从缓冲区读取输入数据（如果有），然后通过覆盖输入数据提供输出数据（如果有的话）。 有关详细信息，请参阅[定义 I/o 控制代码](defining-i-o-control-codes.md)。

 

 




