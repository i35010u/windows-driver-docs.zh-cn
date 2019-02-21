---
title: 注册和队列 CustomTimerDpc 例程
description: 注册和队列 CustomTimerDpc 例程
ms.assetid: 884bff8e-8437-44fb-acc0-f535d64ce900
keywords:
- 计时器对象 WDK 内核，CustomTimerDpc 例程
- CustomTimerDpc
- 队列计时器对象
- 注册计时器对象
- KeSetTimer
- KeSetTimerEx
- KeInitializeTimer
- KeInitializeTimerEx
- 重复调用 CustomTimerDpc 例程
- 重复调用 CustomTimerDpc 例程
- DueTime 值
- 计时器过期 WDK 内核
- 过期的计时器 WDK 内核
- 计时器对象 WDK 内核，队列
- 计时器对象 WDK 内核，注册
- 计时器对象 WDK 内核，过期时间
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d328e808a94225536cd8ef31216a86ecf8a477c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548194"
---
# <a name="registering-and-queuing-a-customtimerdpc-routine"></a>注册和队列 CustomTimerDpc 例程





驱动程序可以注册[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程通过调用以下例程通常从其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程：

1.  [**KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)注册其例程

2.  [**KeInitializeTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff552168)或[ **KeInitializeTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552173)设置计时器对象

随后，该驱动程序可以调用[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)或[ **KeSetTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff553292)指定到期时间并将添加到计时器对象系统的计时器队列。 系统达到过期时间后，该计时器对象并调用取消排队*CustomTimerDpc*例程。 下图说明了这些调用。

![说明 customtimerdpc 例程使用计时器和 dpc 对象的关系图](images/3ketmdpc.png)

如，如上图所示，该驱动程序必须提供存储 DPC 对象和计时器对象。 大多数驱动程序提供的存储中的这些对象[设备扩展](device-extensions.md)或其他驱动程序分配、 常驻内存中。

在调用**KeSetTimer**，驱动程序将传递指向*Dpc*并*计时器*对象，以及与*DueTime*单位表示100 纳秒上, 图中所示。 一个正值*DueTime*指定*绝对到期时间*（自 1601 年 1 月 1 日) 从该处*CustomTimerDpc*应调用例程。 负值*DueTime*指定*相对过期时间*。

绝对计时器将在特定的系统时间到期，因为系统时间更改之前在计时器过期时，也不会影响绝对计时器的等待持续时间。 另一方面，相对计时器始终指定的时间单位内重复，而不考虑的绝对系统时间更改数后过期。

若要调用*CustomTimerDpc*例程重复，使用**KeSetTimerEx**设置计时器并指定在重复间隔*期*参数。 **KeSetTimerEx**类似于**KeSetTimer**此额外参数除外。

上图中，对的调用中所示**KeSetTimer**或**KeSetTimerEx**队列计时器对象指定的间隔时间，如下所示：

1.  当*DueTime*到期时，取消排队的计时器对象并将其设置为用信号通知状态。

2.  如果每个处理器计算机中的当前正在运行的代码在 IRQL 大于或等于调度\_级别，请与计时器对象相关联的 DPC 对象置于 DPC 队列中。 否则为*CustomTimerDpc*调用例程。

3.  如果 DPC 对象已在队列中时*DueTime*间隔过期， *CustomTimerDpc*只要计算机的任何处理器上 IRQL 低于调度调用例程\_级别。

    **请注意**   *CustomTimerDpc*例程，如所有 DPC 例程，称为在 IRQL = 调度\_级别。 DPC 例程时，会阻止所有线程在同一个处理器上运行。 驱动程序开发人员应仔细设计其*CustomTimerDpc*例程 brief 尽可能时间运行的。

     

可以为指定的最小时间间隔**KeSetTimer**并**KeSetTimerEx**大约为 10 毫秒，因此驱动程序可以使用*CustomTimerDpc*例程当计时比更小的间隔[ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)例程，每秒一次运行时，可以处理。

可以在任意时刻排队的特定计时器对象只有一个实例化。 调用**KeSetTimer**或**KeSetTimerEx**再次具有相同*计时器*对象指针取消排队的计时器对象，并将其重置。

设置[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程是完全一样设置[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程，与其他步骤，以初始化计时器对象。 事实上，其原型是相同的但*CustomTimerDpc*例程不能使用这两个*SystemArgument*其原型中声明的指针。

 

 




