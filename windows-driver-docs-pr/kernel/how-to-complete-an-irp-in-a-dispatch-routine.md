---
title: 如何在 Dispatch 例程中完成 IRP
description: 如何在 Dispatch 例程中完成 IRP
ms.assetid: b29da791-e768-4f67-8e85-6cfbeca97220
keywords:
- 完成 Irp WDK 内核，调度例程
- 完成 Irp 的调度例程 WDK 内核
- WDK Irp 的状态信息
- I/O 状态块 WDK 内核
- 状态块 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a6dbd1f49848deab86b69555a43806ea11459ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364269"
---
# <a name="how-to-complete-an-irp-in-a-dispatch-routine"></a>如何在 Dispatch 例程中完成 IRP





如果可以立即完成输入的 IRP，调度例程执行以下任务：

1.  集**状态**并**信息**IRP 的 I/O 状态的成员使用适当的值，通常情况下阻止：

    -   调度例程集**状态**到状态\_成功或相应的错误 (状态\_*XXX*)，可以是对支持例程的调用返回的值或，对于某些同步请求，较低的驱动程序。

        如果较低级驱动程序将返回状态\_挂起状态，更高级别的驱动程序不应调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)的 IRP，有一个例外：更高级别的驱动程序可以使用某个事件之间的同步其[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程和中这种情况下其调度例程*IoCompletion*例程信号事件并返回状态\_更多\_处理\_必需。 调度例程等待事件，然后调用**IoCompleteRequest**完成 IRP。

    -   它会设置**信息**到的字节数已成功传输的请求来传输数据，如读取或写入请求，已满足。

    -   它会设置**信息**状态完成其他 Irp 的特定请求而异的值\_成功。

    -   它会设置**信息**Irp 完成但出现警告状态的特定请求而异的值\_*XXX*。 例如，它将设置**信息**到的字节数与状态这样的警告的传输\_缓冲区\_溢出。

    -   通常情况下，它会设置**信息**为零的请求，它完成并显示错误状态\_*XXX*。

2.  调用**IoCompleteRequest** IRP 和*PriorityBoost* = IO\_否\_增量。

3.  返回的相应状态\_*XXX*它已将设置 I/O 状态块中。 请注意，调用**IoCompleteRequest**使给定的 IRP，调用方，不可访问，因此不能从已完成的 IRP 的 I/O 状态块设置的调度例程的返回值。

**请按照用于调用与 IRP IoCompleteRequest 本实现原则：**

请务必发布之前，先在持有任何数值调节钮锁定**IoCompleteRequest**。

需要确定的时间才能完成 IRP，尤其是在一个链分层驱动程序的进度。 此外，可能发生死锁，如果更高级别的驱动程序的*IoCompletion*例程发送 IRP 到较低的驱动程序持有自旋锁。

 

 




