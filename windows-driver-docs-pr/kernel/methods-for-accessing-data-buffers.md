---
title: 访问数据缓冲区的方法
description: 访问数据缓冲区的方法
ms.assetid: f95a0aec-65f9-44c9-8ae5-11bb4d832752
keywords:
- I/O WDK 内核，数据缓冲区
- 数据缓冲 WDK I/O
- WDK I/O 的缓冲区
- 缓冲 WDK I/O 访问
- 数据缓冲 WDK I/O 访问
- 数据传输 WDK 内核，数据缓冲区的访问
- 传输数据 WDK 内核，数据缓冲区的访问
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a6a23ca1b45d98da0b0433006d18f17d0c4e4b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380367"
---
# <a name="methods-for-accessing-data-buffers"></a>访问数据缓冲区的方法


驱动程序堆栈的主要职责之一用户模式应用程序和系统的设备之间传输数据。 操作系统提供了用于访问数据缓冲区的以下三种方法：

<a href="" id="buffered-i-o"></a>*缓冲的 I/O*  
操作系统会创建应用程序的缓冲区大小等于的非分页的系统缓冲区。 对于写入操作，I/O 管理器用户将数据复制到系统缓冲区之前调用驱动程序堆栈。 对于读取操作，I/O 管理器将数据从复制系统缓冲区到应用程序的缓冲区后驱动程序堆栈完成请求的操作。

有关详细信息，请参阅[使用缓冲 I/O](using-buffered-i-o.md)。

<a href="" id="direct-i-o"></a>*直接 I/O*  
操作系统将在内存中锁定应用程序的缓冲区。 然后，创建描述符内存列表 (MDL)，用于标识锁定的内存页，并将 MDL 传递给驱动程序堆栈。 驱动程序通过 MDL 访问锁定的页。

有关详细信息，请参阅[使用直接 I/O](using-direct-i-o.md)。

<a href="" id="neither-buffered-nor-direct-i-o"></a>*既不缓冲，也不直接 I/O*  
操作系统将传递给驱动程序堆栈的应用程序缓冲区虚拟起始地址和大小。 缓冲区才可从应用程序的线程上下文中执行的驱动程序进行访问。

有关详细信息，请参阅[使用既不缓冲 Nor 直接 I/O](using-neither-buffered-nor-direct-i-o.md)。

有关[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)并[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求，驱动程序通过在每个使用标志来指定的 I/O 方法[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

有关[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)并[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766) I/O 方法由请求*留空，则*IOCTL 的每个值中包含的值。 有关详细信息，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

驱动程序堆栈中的所有驱动程序必须使用相同缓冲区访问的方法为每个请求，除可能是最高级别的驱动程序 （这可以使用"不"方法，而不考虑使用较低的驱动程序的方法）。

 

 




