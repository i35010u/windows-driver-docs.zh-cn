---
title: 访问数据缓冲区的方法
description: 访问数据缓冲区的方法
ms.assetid: f95a0aec-65f9-44c9-8ae5-11bb4d832752
keywords:
- I/o WDK 内核，数据缓冲区
- 数据缓冲区 WDK i/o
- 缓冲 WDK i/o
- 缓冲 WDK i/o，访问
- 数据缓冲区 WDK i/o，访问
- 数据传输 WDK 内核，数据缓冲区访问
- 传输数据 WDK 内核，数据缓冲区访问
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8770763d0c3f8d6b46ebb01897220d8b590f0d16
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187915"
---
# <a name="methods-for-accessing-data-buffers"></a>访问数据缓冲区的方法


驱动程序堆栈的主要职责之一是在用户模式应用程序和系统设备之间传输数据。 操作系统提供以下三种方法来访问数据缓冲区：

<a href="" id="buffered-i-o"></a>*缓冲 i/o*  
操作系统会创建一个未分页的系统缓冲区，大小等于应用程序的缓冲区。 对于写入操作，i/o 管理器会在调用驱动程序堆栈之前将用户数据复制到系统缓冲区。 对于读取操作，当驱动程序堆栈完成请求的操作后，i/o 管理器会将数据从系统缓冲区复制到应用程序的缓冲区中。

有关详细信息，请参阅 [使用缓冲 i/o](using-buffered-i-o.md)。

<a href="" id="direct-i-o"></a>*直接 i/o*  
操作系统将应用程序缓冲区锁定在内存中。 然后，它创建 (MDL) 的内存描述符列表，该列表标识锁定的内存页，并将 MDL 传递到驱动程序堆栈。 驱动程序通过 MDL 访问锁定的页面。

有关详细信息，请参阅 [使用直接 i/o](using-direct-i-o.md)。

<a href="" id="neither-buffered-nor-direct-i-o"></a>*未缓冲或直接 i/o*  
操作系统将应用程序缓冲区的虚拟起始地址和大小传递给驱动程序堆栈。 只有在应用程序的线程上下文中执行的驱动程序才能访问该缓冲区。

有关详细信息，请参阅 [不使用缓冲和直接 i/o](using-neither-buffered-nor-direct-i-o.md)。

对于 [**IRP \_ mj \_ 读取**](./irp-mj-read.md) 和 [**irp \_ mj \_ 写入**](./irp-mj-write.md) 请求，驱动程序通过使用每个 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构中的标志来指定 i/o 方法。 有关详细信息，请参阅 [初始化设备对象](initializing-a-device-object.md)。

对于 [**irp \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 和 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求，i/o 方法由每个 IOCTL 值中包含的 *TransferType* 值确定。 有关详细信息，请参阅 [定义 I/o 控制代码](defining-i-o-control-codes.md)。

对于每个请求，驱动程序堆栈中的所有驱动程序都必须使用相同的缓冲区访问方法，但 (可能会使用 "不" 方法，而不考虑较低的驱动程序) 使用的方法。

 

