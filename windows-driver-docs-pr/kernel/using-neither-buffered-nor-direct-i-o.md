---
title: 既不使用缓冲 I/O，也不使用直接 I/O
description: 既不使用缓冲 I/O，也不使用直接 I/O
ms.assetid: e85af2e0-e532-47ca-918e-087e7aff859e
keywords:
- 既不缓冲，也不直接 I/O 的缓冲区 WDK I/O
- 数据缓冲 WDK I/O，既不缓冲，也不直接 I/O
- 既不缓冲，也不直接 I/O WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8292956b71f46aec32185eab82eb8afa2a0af1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567757"
---
# <a name="using-neither-buffered-nor-direct-io"></a>既不使用缓冲 I/O，也不使用直接 I/O





如果驱动程序使用的既不缓冲，也不直接 I/O，然后在 I/O 管理器将传递原始用户空间虚拟地址 Irp 发送到该驱动程序中。 若要安全地访问这些缓冲区，必须在调用线程的上下文中执行该驱动程序。 通常情况下，因此，只有最高级别的驱动程序，例如 FSDs，可以使用此方法用于访问缓冲区。

中间或最低级别的驱动程序无法始终满足此条件。 例如，如果请求线程等待 I/O 请求完成或更高级别的驱动程序被上层的中间或最低级别的驱动程序，则较低级驱动程序的例程是不太可能在请求线程的上下文中调用。

I/O 管理器确定 I/O 操作使用既不缓冲，也不直接 I/O，如下所示：

-   有关[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)并[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求，都不执行操作\_缓冲\_IO 也不执行\_直接\_中设置 IO**标志**隶属[**设备\_对象** ](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

-   有关[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)并[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)请求时，IOCTL 代码的值包含方法\_都不一样*留空，则*IOCTL 值中的值。 有关详细信息，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

当驱动程序接收 IRP，指定使用既不缓冲，也不直接 I/O 的 I/O 操作时，它必须执行以下操作：

1.  检查用户缓冲区的地址范围的有效性，并检查是否适当读取或写入访问允许，则允许使用[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)并[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)支持例程。 该驱动程序必须将缓冲区的地址范围内的驱动程序提供的异常处理程序中，对其访问，以便用户线程不能更改缓冲区的访问权限，而该驱动程序正在访问的内存。 如果探测会引发异常，该驱动程序应返回错误。 该驱动程序必须调用这些例程发出 I/O 请求; 的线程的上下文中因此，更高级别的驱动程序可以执行此任务。

2.  通过以下方式之一管理缓冲区和内存操作：
    -   与 I/O 管理器为使用缓冲的 I/O 驱动程序执行其自身双缓冲的操作。 有关详细信息，请参阅[使用缓冲 I/O](using-buffered-i-o.md)。
    -   创建其自己 MDLs 和锁定缓冲区通过调用内存管理器的支持例程与 I/O 管理器为使用直接 I/O 驱动程序。 有关详细信息，请参阅[使用直接 I/O](using-direct-i-o.md)。
    -   直接在调用线程的上下文中执行所有必要的操作，对用户缓冲区。 在用户线程更改缓冲区的访问权限，或者在缓冲区中的数据驱动程序正在访问的内存的情况下，该驱动程序必须换行对驱动程序提供的异常处理程序内的缓冲区的访问权限。 有关详细信息，请参阅[处理异常](handling-exceptions.md)。

事实上，该驱动程序必须选择在每个 IRP 的基础上是在调用线程的上下文中执行缓冲的 I/O、 直接 I/O 或 I/O 操作，并且它必须处理可能发生在用户模式线程上下文中的任何异常。 该驱动程序必须管理自己用户缓冲区访问、 双缓冲操作和内存映射，根据需要，而不是让处理驱动程序的这些操作的 I/O 管理器。

 

 




