---
title: 单独 DispatchCreate 和 DispatchClose 例程
description: 单独 DispatchCreate 和 DispatchClose 例程
ms.assetid: b2e05555-c70d-4293-8622-51eea92091b1
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE I/O 函数代码
- IRP_MJ_CLOSE I/O 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cf1686cf8e32b28bf29b5987307440f8a883d8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547086"
---
# <a name="separate-dispatchcreate-and-dispatchclose-routines"></a>单独 DispatchCreate 和 DispatchClose 例程





驱动程序的*调度*例程[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)并[ **IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)请求可能不执行任何操作完成多个输入状态的 IRP\_成功。 有关详细信息，请参阅[完成 Irp](completing-irps.md)。

另一个驱动程序*调度*例程**IRP\_MJ\_创建**并**IRP\_MJ\_关闭**请求可能需要做更多的工作，具体取决于基础设备驱动程序或基础设备上。 请考虑以下方案：

- 类驱动程序可能会接收的创建请求时，初始化内部队列并发送[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)请求向相应端口驱动程序请求设备的配置信息或对控制器端口独占访问权限。

- 收据**IRP\_MJ\_关闭**指示已删除对与目标设备对象相关联的文件对象的最后一个引用。 这意味着文件对象的所有句柄已关闭，且已完成或取消所有未完成的 I/O 请求。

- 创建请求回执，不常使用的设备的驱动程序可能会调用[ **MmLockPagableCodeSection** ](https://msdn.microsoft.com/library/windows/hardware/ff554601)使驻留的一些处理其他驱动程序例程**IRP\_MJ\_* XXX*** 的请求。 接收到相应的关闭请求，该驱动程序可能会调用[ **MmUnlockPagableImageSection** ](https://msdn.microsoft.com/library/windows/hardware/ff556377)以节省通过使其可分页图像部分中调出所有文件的对象句柄时的系统内存此类的驱动程序的设备对象都将关闭。

某些驱动程序处理**IRP\_MJ\_关闭**请求仅对对称的因为，在其设备对象已打开受保护的子系统或更高级别的驱动程序，较低级别驱动程序的设备对象是未关闭，直到关闭系统本身。 例如，键盘和鼠标的驱动程序设置设备对象表示必须功能在运行时系统，因此，这些驱动程序可能具有最少的物理设备[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程对称性，或者它们可能会合并[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

如果由较低级驱动程序控制的设备必须可供系统以继续运行，驱动程序的*DispatchClose*例程通常不会调用。 例如，一些系统磁盘驱动程序没有*DispatchClose*例程，但这些驱动程序通常具有[ *DispatchFlushBuffers* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)和[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，从而在系统关闭之前完成所有未完成的文件 I/O 操作。

尽管可以实现单独的[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并*DispatchClose*例程，驱动程序有时必须[单一 DispatchCreateClose 例程](a-single-dispatchcreateclose-routine.md)处理同时创建并关闭请求。

 

 




