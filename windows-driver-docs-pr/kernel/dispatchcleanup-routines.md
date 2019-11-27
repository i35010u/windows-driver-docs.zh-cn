---
title: DispatchCleanup 例程
description: DispatchCleanup 例程
ms.assetid: 1ba001b8-92e0-453f-b9f6-6099cedf6439
keywords:
- 调度例程 WDK 内核，DispatchCleanup 例程
- DispatchCleanup 例程
- IRP_MJ_CLEANUP i/o 函数代码
- 解除分配资源 WDK 内核
- 取消映射硬件内存
- 取消映射用户模式内存
- 解锁用户模式内存
- 清理资源 WDK 内核
- 旋转锁定 WDK 内核
- 清理调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8217625e32b3d0b19fcd3a7ffe3c243df5b7492
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836894"
---
# <a name="dispatchcleanup-routines"></a>DispatchCleanup 例程





驱动程序的[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程为[**irp\_MJ\_清理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)I/o 函数代码处理 irp。

驱动程序可以使用*DispatchCleanup*例程来执行所有已关闭文件对象的句柄之后所需的任何清理操作。 请注意， *DispatchCleanup*是在关闭最终句柄的进程的进程上下文中调用的;此过程可能与最初打开句柄的进程不同。 （通常会发生这种差异，因为另一个进程使用**DuplicateHandle**用户模式例程来复制进程句柄。）必须在原始进程上下文中执行清理的驱动程序可以使用[**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)例程为此目的注册回调例程，但请记住，此类回调是一个有限的系统资源。

通常， *DispatchCleanup*例程必须通过对目标设备对象的设备队列（或驱动程序的内部队列）中的每个 irp 执行以下操作来处理**irp\_MJ\_清理**请求：和与文件对象关联：

-   调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)将[*Cancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程指针设置为**NULL**。

-   如果已排队 IRP 的驱动程序 i/o 堆栈位置中指定的文件对象与 IRP\_MJ 的 i/o 堆栈位置中接收的文件对象匹配，则取消当前位于队列中的目标设备对象的所有 IRP **\_清理**请求。

-   调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成 IRP，并返回状态\_SUCCESS。

在处理**irp\_MJ\_清理**请求时，驱动程序可能会收到其他请求，如[**IRP\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read) [](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)\_ 因此，必须解除分配资源的驱动程序还必须使用其他调度例程（如[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)）同步其*DispatchCleanup*例程的执行。

 

 




