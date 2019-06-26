---
title: 使用缓冲 I/O 执行 DispatchReadWrite
description: 使用缓冲 I/O 执行 DispatchReadWrite
ms.assetid: bb8ce47d-5722-4050-9492-bec154744597
keywords:
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE I/O 函数代码
- IRP_MJ_READ I/O 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读/写调度例程
- 缓冲的 I/O WDK 内核
- I/O WDK 内核缓冲
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d501237309b86db5779d690dd82bbbe0f96c6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384974"
---
# <a name="dispatchreadwrite-using-buffered-io"></a>使用缓冲 I/O 执行 DispatchReadWrite





任何设置了其设备的最低级别的设备驱动程序对象的缓冲 I/O 通过返回从其设备传输到锁定下的数据满足读取的请求系统空间缓冲区**Irp-&gt;AssociatedIrp.SystemBuffer**. 它通过将数据从出同一缓冲区传输到其设备满足写入请求。

因此， *DispatchReadWrite*这样的设备驱动程序例程通常执行以下操作在收到的传输请求：

1.  调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)并确定该传输请求的方向。

2.  检查请求的参数的有效性。

    -   对于读取请求，该例程通常会检查驱动程序的*IoStackLocation*-&gt;**Parameters.Read.Length**值来确定缓冲区是否足够大，接收从设备传输的数据。

        例如，在系统键盘类驱动程序处理仅来自 Win32 用户输入线程的读取的请求。 此驱动程序定义的结构，键盘\_输入\_数据，要在其中存储击键从设备上，并在任何给定时间点，以便满足读取的请求和他们一起内部环缓冲区中保存一定数量的这些结构在中。

    -   对于写入请求，该例程通常会检查处的值**Parameters.Write.Length**，并检查在数据**Irp-&gt;AssociatedIrp.SystemBuffer**的有效性，如有必要： 即，如果其设备接受包含具有定义的值范围的成员的唯一的结构化的数据数据包。

3.  如果任何参数无效，则*DispatchReadWrite*例程完成立即，如前面所述 IRP[完成 Irp](completing-irps.md)。 否则，该例程将传递 IRP 上进行进一步处理由其他驱动程序例程，如中所述[驱动程序堆栈的下层传递 Irp](passing-irps-down-the-driver-stack.md)。

通常使用缓冲的 I/O 驱动程序必须满足的读取或写入大小的数据的传输请求指定的请求的发起最低级别的设备。 此类驱动程序很可能定义的数据结构来自或发送到其设备以及有可能在内部，缓冲结构化的数据，如系统键盘类驱动程序执行。

在内部缓冲的数据的驱动程序应支持[ **IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)请求，并且还可以支持[ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)请求。

在一个链中的最高级别的驱动程序是通常负责在将传递到较低的驱动程序的读/写请求之前检查输入的 IRP 的参数。 因此，许多较低级驱动程序可以假定在读/写 IRP 及其 I/O 堆栈位置具有有效的参数。 如果链中的最低级别驱动程序已注意到的数据传输的特定于设备的约束，该驱动程序需要检查其 I/O 堆栈位置中的参数的有效性。

 

 




