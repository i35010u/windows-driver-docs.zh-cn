---
title: DispatchCreate、DispatchClose 和 DispatchCreateClose 例程
description: DispatchCreate、DispatchClose 和 DispatchCreateClose 例程
ms.assetid: 5c1c0036-71b1-4410-b157-f9ebe3b6ecfc
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE I/O 函数代码
- IRP_MJ_CLOSE I/O 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b259a4c10bbb28a0d7acfd246ad2058afb9f93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381719"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose 和 DispatchCreateClose 例程





驱动程序的[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) I/O 函数代码的 Irp [ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)和[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)分别。 或者，组合[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以处理 Irp 为这两个这些 I/O 函数代码。

创建请求可能源自从用户模式下子系统的尝试获取一个表示设备 （可能是代表应用程序或子系统级驱动程序） 的文件对象的句柄或更高级别的驱动程序中调用[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)或[ **IoAttachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevice)。

相应的关闭请求所源自的驱动程序的设备对象与关联的文件对象句柄的用户模式下子系统的关闭。

每个请求是本质上是同步的。

 

 




