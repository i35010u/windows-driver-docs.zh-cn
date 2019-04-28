---
title: 同步中断代码
description: 同步中断代码
ms.assetid: 5E2D0063-2251-40B3-8982-46001E67EB55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b7da0609d5fbc9c09ee229ecf410ba799a58c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350669"
---
# <a name="synchronizing-interrupt-code"></a>同步中断代码


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

必须同步访问中断数据缓冲区的所有驱动程序代码，以便只有一个例程一次访问数据。

您可以通过使用手动中断锁定或自动回调序列化同步中断代码。

## <a name="manual-interrupt-locking"></a>手动中断锁定


获取之前调用该中断锁，UMDF [ *OnInterruptIsr*](https://msdn.microsoft.com/library/windows/hardware/hh463902)， [ *OnInterruptDisable*](https://msdn.microsoft.com/library/windows/hardware/hh463895)，或[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)回调。

如果驱动程序需要同步使用中断锁的任何代码，它将调用[ **IWDFInterrupt::AcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh451289)并[ **IWDFInterrupt::ReleaseInterruptLock**](https://msdn.microsoft.com/library/windows/hardware/hh451319). 例如，驱动程序获取并释放中断锁中的其[ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905)通过使用这些方法的回调例程。 但是，在 I/O 调度回调 (例如[ **OnRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556875)并[ **OnWrite**](https://msdn.microsoft.com/library/windows/hardware/ff556885))，则驱动程序的第一个调用[ **IWDFInterrupt::TryToAcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh451332)来确定是否要将工作项排队或执行操作，以避免潜在的死锁的同一线程中的工作。 有关可以通过调用导致死锁方案的示例**IWDFInterrupt::AcquireInterruptLock**从任意线程上下文，请参阅备注部分[ **IWDFInterrupt::AcquireInterruptLock**](https://msdn.microsoft.com/library/windows/hardware/hh451289)。

如果[ **IWDFInterrupt::TryToAcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh451332)返回**TRUE**，驱动程序已获取同一线程中的中断锁。 在这种情况下，该驱动程序执行的工作，需要该锁，然后调用[ **ReleaseInterruptLock**](https://msdn.microsoft.com/library/windows/hardware/hh451319)。 如果**IWDFInterrupt::TryToAcquireInterruptLock**返回**FALSE**，该驱动程序的工作项进行排队并执行中的工作及其[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)回调。 在这种情况下，工作项必须不使用自动序列化。

## <a name="using-automatic-serialization"></a>使用自动序列化


UMDF 驱动程序可以通过调用请求自动回调同步[ **IWDFDeviceInitialize::SetLockingConstraint** ](https://msdn.microsoft.com/library/windows/hardware/ff556991)与*LockType*参数设置为**WdfDeviceLevel**。

然后，驱动程序设置**AutomaticSerialization**的成员及其[ **WUDF\_中断\_配置**](https://msdn.microsoft.com/library/windows/hardware/hh464084)结构 **，则返回 TRUE**之前调用[ **CreateInterrupt**](https://msdn.microsoft.com/library/windows/hardware/hh451208)。

因此，UMDF 序列化的驱动程序[ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905)回调与 I/O 队列请求取消，以及文件对象回调例程。 在此方案中，UMDF 使用回调锁，而不是每个中断对象锁。

 

 





