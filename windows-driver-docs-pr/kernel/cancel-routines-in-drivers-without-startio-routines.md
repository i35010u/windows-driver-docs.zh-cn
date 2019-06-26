---
title: 不包含 StartIo 例程的驱动程序中的 Cancel 例程
description: 不包含 StartIo 例程的驱动程序中的 Cancel 例程
ms.assetid: c6e1a05e-28ed-4f42-8678-55f01303b312
keywords:
- 正在取消 Irp，StartIo 例程
- 取消例程，StartIo 例程
- StartIo 例程，取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce3e593a7f51e9614d4e11409b5f56bcc080b9ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377237"
---
# <a name="cancel-routines-in-drivers-without-startio-routines"></a>不包含 StartIo 例程的驱动程序中的 Cancel 例程





I/O 管理器维护**CurrentIrp**字段中的设备对象仅当 Irp 排列在关联的设备队列对象。

驱动程序不具有[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程管理 Irp 自己内部队列。 在此类驱动程序， [*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)可以与输入 IRP 既不是调用例程**CurrentIrp**为输入的目标设备对象，也不在驱动程序中的 IRP 的内部队列。 该驱动程序必须保留哪些 IRP，当前正在处理以及应具有其自己的状态*取消*其队列的每个例程。 驱动程序的内部队列应互锁的队列，因为必须通过执行旋转锁保护其内部队列。

当驱动程序的*取消*调用例程，它通常执行以下操作：

1.  调用[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))，并传递**Irp-&gt;CancelIrql**。

2.  获取数值调节钮锁，以保护其互锁的队列并指导该队列来查找与 IRP **Irp-&gt;取消**设置为**TRUE**。

    -   如果互锁的队列中找到此类 IRP，取消其排队、 释放自旋锁保护队列、 设置 IRP 的 I/O 状态块 w

        状态\_取消**状态**对于该值为零**信息**，启动下一步排队的 IRP，调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与已取消的 IRP 和返回控件

    -   如果未找到此类 IRP*取消*例程释放它持有并控制返回的任何数值调节钮锁。

        驱动程序通常假定 IRP 已经开始如果 IRP 未排队的输入该 I/O 处理。

具有驱动程序*取消*例程可以处理[ **IRP\_MJ\_清理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)也请求。 请参阅[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)有关详细信息**IRP\_MJ\_清理**请求。

 

 




