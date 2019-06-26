---
title: 单个 DispatchCreateClose 例程
description: 单个 DispatchCreateClose 例程
ms.assetid: 6127d696-2409-49fc-9cbd-ba1b13c0c672
keywords:
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- IRP_MJ_CREATE I/O 函数代码
- IRP_MJ_CLOSE I/O 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d1442de58f98921bbad2140a998fbb3a1fea5f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363469"
---
# <a name="a-single-dispatchcreateclose-routine"></a>单个 DispatchCreateClose 例程





许多驱动程序，尤其是较低级别的链中的驱动程序分层驱动程序，只需建立在收到其是否存在*创建*请求并只需确认的接收*关闭*请求。

例如，端口驱动程序的设备控制器与一个或多个紧密耦合的类驱动程序调用[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)可能具有的精简[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 例程可能不执行任何操作多个完整 IRP，如下所示：

```cpp
    :    : 
{ 
    Irp->IoStatus.Status = STATUS_SUCCESS; 
 Irp->IoStatus.Information = 0; 
    IoCompleteRequest(Irp, IO_NO_INCREMENT); 
 return STATUS_SUCCESS; 
}
```

此最小*DispatchCreateClose*例程集**信息**为创建请求; 打开的 I/O 状态块为零，指示文件对象的成员**信息**关闭请求没有意义。 例程集**状态**成员添加到状态\_成功，此时也返回此状态的值，指示该驱动程序已准备好接受 I/O 请求。

此最小*DispatchCreateClose*例程完成创建 IRP，而无需提升的 IRP 发起方的优先级 (IO\_否\_增量)，因为发起方假定要等待的时间要完成的请求不确定，但非常小的间隔。

工作量*DispatchCreateClose*例程的执行取决于一定程度上驱动程序的设备或基础设备的性质和一定程度上的驱动程序的设计。 如果驱动程序执行创建和关闭请求非常不同的操作，应能处理这些请求中的[分隔 DispatchCreate 和 DispatchClose 例程](separate-dispatchcreate-and-dispatchclose-routines.md)。

若要处理的创建请求以打开文件对象，表示逻辑或物理设备，最高级别的驱动程序应执行以下操作：

1.  调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)以获得到 IRP 中其 I/O 堆栈位置的指针。

2.  检查**的文件对象**。**文件名**i/o 堆栈位置，并完成状态 IRP\_如果 Unicode 字符串在成功**FileName**长度为零; 否则，请完成状态 IRP\_无效\_参数。

按照前面的步骤可以确保不会尝试打开的设备上 pseudofile，可能会导致问题更高版本。 例如，这会阻止在尝试打开不存在\\\\设备\\parallel0\\temp.dat。

 

 




