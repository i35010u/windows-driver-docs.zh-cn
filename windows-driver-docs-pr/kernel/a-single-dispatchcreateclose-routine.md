---
title: 单个 DispatchCreateClose 例程
description: 单个 DispatchCreateClose 例程
keywords:
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- IRP_MJ_CREATE i/o 函数代码
- IRP_MJ_CLOSE i/o 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44b6a9e5fb34dcb803c28afcf0bea621793aae90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840917"
---
# <a name="a-single-dispatchcreateclose-routine"></a>单个 DispatchCreateClose 例程





许多驱动程序，特别是分层驱动程序链中较低级别的驱动程序，只需建立其在接收 *创建* 请求时的存在性，而只需确认是否收到 *关闭* 请求。

例如，如果设备控制器的端口驱动程序具有一个或多个与调用 [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) 的紧密耦合的类驱动程序，则它可能具有最小 [*DispatchCreateClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程。 例程除了完成 IRP 外，还可以执行任何操作，如下所示：

```cpp
    :    : 
{ 
    Irp->IoStatus.Status = STATUS_SUCCESS; 
 Irp->IoStatus.Information = 0; 
    IoCompleteRequest(Irp, IO_NO_INCREMENT); 
 return STATUS_SUCCESS; 
}
```

这一最小 *DispatchCreateClose* 例程将 i/o 状态块的 **信息** 成员设置为零，表示为创建请求打开文件对象; **信息** 对于关闭请求没有意义。 例程将 **状态** 成员设置为状态 \_ "成功"，同时返回此状态值，指示驱动程序已准备好接受 i/o 请求。

这一最小的 *DispatchCreateClose* 例程将完成 create irp，而不会提升 irp 的发起方的优先级 (IO \_ 无 \_ 增量) ，因为假定发起方等待请求的不确定状态，但间隔时间非常短，请求才能完成。

*DispatchCreateClose* 例程所需的工作量部分取决于驱动程序的设备或基础设备的性质，并部分取决于驱动程序的设计。 如果驱动程序对创建和关闭请求执行的操作非常不同，则它应在 [单独的 DispatchCreate 和 DispatchClose 例程](separate-dispatchcreate-and-dispatchclose-routines.md)中处理这些请求。

若要处理用于打开表示逻辑或物理设备的文件对象的 create 请求，最高级别的驱动程序应执行以下操作：

1.  调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) 以获取指向 IRP 中其 i/o 堆栈位置的指针。

2.  检查 **FileObject**。如果文件名的 Unicode 字符串的长度为零，则 i/o 堆栈位置中的 **文件名** 并完成 IRP，状态 \_ 为 "成功"; 否则，请使用 " **FileName** 状态 \_ 无效" 参数完成 irp \_ 。

按照前面的步骤，可以确保不会尝试在设备上打开 pseudofile，这会导致以后出现问题。 例如，这会阻止尝试打开不存在的 \\ \\ 设备 \\ parallel0 \\ 。

 

