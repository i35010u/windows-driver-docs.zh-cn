---
title: DispatchCleanup 例程
description: DispatchCleanup 例程
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
ms.openlocfilehash: 839226e3b9a04787bfd94d03eb044b7162a50f5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799469"
---
# <a name="dispatchcleanup-routines"></a>DispatchCleanup 例程





驱动程序的 [*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 清理**](./irp-mj-cleanup.md) i/o 函数代码处理 irp。

驱动程序可以使用 *DispatchCleanup* 例程来执行所有已关闭文件对象的句柄之后所需的任何清理操作。 请注意， *DispatchCleanup* 是在关闭最终句柄的进程的进程上下文中调用的;此过程可能与最初打开句柄的进程不同。  (通常会发生这种差异，因为另一个进程使用 **DuplicateHandle** 用户模式例程来复制进程句柄。必须在原始进程上下文中执行清理的 ) 驱动程序可以使用 [**PsSetCreateProcessNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine) 例程为该目的注册回调例程，但请记住，此类回调是一个有限的系统资源。

通常情况下， *DispatchCleanup* 例程必须处理 **irp \_ MJ \_ 清除** 请求，方法是对当前位于设备队列 (或驱动程序的) 中的每个 irp （对于目标设备对象）执行以下操作，并将其与 file 对象关联：

-   调用 [**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) 将 [*Cancel*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程指针设置为 **NULL**。

-   如果在排队 IRP 的驱动程序 i/o 堆栈位置中指定的文件对象与 **irp \_ MJ \_ 清除** 请求的 i/o 堆栈位置中所接收的文件对象匹配，则取消当前位于队列中的目标设备对象的所有 IRP。

-   调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 完成 IRP，并返回状态 " \_ 成功"。

处理 **irp \_ mj \_ 清除** 请求时，驱动程序可能会收到其他请求，如 [**IRP \_ mj \_ 读取**](./irp-mj-read.md) 或 [**irp \_ mj \_ 写入**](./irp-mj-write.md)。 因此，必须解除分配资源的驱动程序还必须使用其他调度例程（如 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)）同步其 *DispatchCleanup* 例程的执行。

 

