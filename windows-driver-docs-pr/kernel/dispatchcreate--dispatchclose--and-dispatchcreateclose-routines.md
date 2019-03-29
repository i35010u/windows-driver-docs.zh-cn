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
ms.openlocfilehash: 539efa05a13f866c6aeb66b2af6a982cf6fda117
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565267"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose 和 DispatchCreateClose 例程





驱动程序的[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) I/O 函数代码的 Irp [ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)和[**IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)分别。 或者，组合[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以处理 Irp 为这两个这些 I/O 函数代码。

创建请求可能源自从用户模式下子系统的尝试获取一个表示设备 （可能是代表应用程序或子系统级驱动程序） 的文件对象的句柄或更高级别的驱动程序中调用[ **IoGetDeviceObjectPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff549198)或[ **IoAttachDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548294)。

相应的关闭请求所源自的驱动程序的设备对象与关联的文件对象句柄的用户模式下子系统的关闭。

每个请求是本质上是同步的。

 

 




