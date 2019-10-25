---
title: 单个 DispatchCreateClose 例程
description: 单个 DispatchCreateClose 例程
ms.assetid: 6127d696-2409-49fc-9cbd-ba1b13c0c672
keywords:
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- IRP_MJ_CREATE i/o 函数代码
- IRP_MJ_CLOSE i/o 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfc660f7559867878be33d568b2e87dbc8763f5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837334"
---
# <a name="a-single-dispatchcreateclose-routine"></a>单个 DispatchCreateClose 例程





许多驱动程序，特别是分层驱动程序链中较低级别的驱动程序，只需建立其在接收*创建*请求时的存在性，而只需确认是否收到*关闭*请求。

例如，如果设备控制器的端口驱动程序具有一个或多个与调用[**plxntb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)的紧密耦合的类驱动程序，则它可能具有最小[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。 例程除了完成 IRP 外，还可以执行任何操作，如下所示：

```cpp
    :    : 
{ 
    Irp->IoStatus.Status = STATUS_SUCCESS; 
 Irp->IoStatus.Information = 0; 
    IoCompleteRequest(Irp, IO_NO_INCREMENT); 
 return STATUS_SUCCESS; 
}
```

这一最小*DispatchCreateClose*例程将 i/o 状态块的**信息**成员设置为零，表示为创建请求打开文件对象;**信息**对于关闭请求没有意义。 例程将**状态**成员设置为 STATUS\_SUCCESS，并返回此状态值，指示驱动程序已准备好接受 i/o 请求。

这一最小的*DispatchCreateClose*例程完成 create irp，而不提升 IRP 的发起方的优先级（IO\_没有\_递增），因为假定发起方等待的是不确定的，而是非常小的时间间隔要完成的请求。

*DispatchCreateClose*例程所需的工作量部分取决于驱动程序的设备或基础设备的性质，并部分取决于驱动程序的设计。 如果驱动程序对创建和关闭请求执行的操作非常不同，则它应在[单独的 DispatchCreate 和 DispatchClose 例程](separate-dispatchcreate-and-dispatchclose-routines.md)中处理这些请求。

若要处理用于打开表示逻辑或物理设备的文件对象的 create 请求，最高级别的驱动程序应执行以下操作：

1.  调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)以获取指向 IRP 中其 i/o 堆栈位置的指针。

2.  检查**FileObject**。如果**文件名**的 Unicode 字符串的长度为零，则在 i/o 堆栈位置中输入**文件名**并完成 IRP，状态\_成功;否则，请完成 IRP，状态\_无效\_参数。

按照前面的步骤，可以确保不会尝试在设备上打开 pseudofile，这会导致以后出现问题。 例如，这会阻止尝试打开不存在的 \\\\设备\\parallel0\\。

 

 




