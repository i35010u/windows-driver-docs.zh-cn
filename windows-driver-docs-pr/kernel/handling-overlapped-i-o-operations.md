---
title: 处理重叠的 I/O 操作
description: 处理重叠的 I/O 操作
ms.assetid: d13a9fa2-9f68-4c35-af79-dd3f8cec2805
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
- 重叠的 I/O WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03845bea026b74a8ace7c98b56fc407a32f34e3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521160"
---
# <a name="handling-overlapped-io-operations"></a>处理重叠的 I/O 操作





[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程的重叠操作在其设备上的驱动程序不能依赖于一对一请求的输入之间的通信[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程和 ISR 调用[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)或[ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)。 此类的驱动程序的*DpcForIsr*或*CustomDpc*一定不能使用的 IRP 和 ISR 提供上下文中，输入的指向或**CurrentIrp**目标中的指针设备对象，若要完成仅该 IRP。

在任何给定时刻，不能两次排队相同 DPC 对象。 如果调用了 ISR **IoRequestDpc**或**KeInsertQueueDpc**多次在相应*DpcForIsr*或者*CustomDpc*执行DPC 例程只运行一次当处理器上的 IRQL 低于调度\_级别。 另一方面，如果调用 ISR **IoRequestDpc**或**KeInsertQueueDpc**而相应*DpcForIsr*或者*CustomDpc*是在另一个处理器上运行，DPC 例程可以在两个处理器上同时运行。

因此，任何重叠的 I/O 操作中断驱动其设备上的驱动程序必须具有以下：

-   一个*DpcForIsr*或*CustomDpc*例程可以完成一些驱动程序维护调用的每次未完成请求的计数

-   永远不会覆盖传递到的上下文信息 ISR *DpcForIsr*或*CustomDpc*例程，直到该例程已使用的上下文信息并完成到 IRP 上下文信息所属

-   一个*SynchCritSection*访问代表 ISR 的上下文区域的例程*DpcForIsr*或*CustomDpc*例程

 

 




