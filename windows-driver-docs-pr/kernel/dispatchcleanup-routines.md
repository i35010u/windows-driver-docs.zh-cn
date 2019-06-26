---
title: DispatchCleanup 例程
description: DispatchCleanup 例程
ms.assetid: 1ba001b8-92e0-453f-b9f6-6099cedf6439
keywords:
- 调度例程 WDK 内核，DispatchCleanup 例程
- DispatchCleanup 例程
- IRP_MJ_CLEANUP I/O 函数代码
- 正在解除分配资源 WDK 内核
- 正在取消映射硬件内存
- 正在取消映射用户模式内存
- 解锁用户模式内存
- 清理资源 WDK 内核
- 数值调节钮锁 WDK 内核
- 清理调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49d8ad0a9e60e5a551bc1f619ece598cb0ec86d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381734"
---
# <a name="dispatchcleanup-routines"></a>DispatchCleanup 例程





驱动程序的[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_清理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup) I/O函数代码。

驱动程序可以使用*DispatchCleanup*例程，以执行任何清理操作需要所有的文件对象的句柄已关闭的。 请注意， *DispatchCleanup*进程的进程上下文中调用关闭最后一个句柄; 此过程可能需要不同于最初打开句柄的过程。 (这种差异通常是因为另一个进程使用**DuplicateHandle**用户模式下的例程，以复制进程句柄。)必须在原始进程上下文中执行清除的驱动程序可以使用[ **PsSetCreateProcessNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)例程，以实现此目的，注册回调例程，但请记住，此类回调是有限的系统资源。

一般情况下， *DispatchCleanup*例程必须处理**IRP\_MJ\_清理**通过执行以下内容，目前设备队列中每个 IRP 的请求 (或在驱动程序的内部队列的 Irp），目标设备对象，并且与文件对象相关联：

-   调用[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)若要设置[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程的指针，指向**NULL**。

-   取消当前是在队列中的目标设备对象，如果在排队 IRP 的驱动程序的 I/O 堆栈位置中指定的文件对象与已接收的 I/O 堆栈位置中的文件对象相匹配的每个 IRP **IRP\_MJ\_清理**请求。

-   调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)完成 IRP，并返回状态\_成功。

在处理**IRP\_MJ\_清理**请求时，驱动程序可以接收的其他请求，如[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)。 因此，必须解除分配资源的驱动程序还必须同步执行其*DispatchCleanup*例程与其他调度例程，如[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)。

 

 




