---
title: 提供 IoTimer 上下文信息
description: 提供 IoTimer 上下文信息
ms.assetid: a92a7c3d-1602-430b-8ae1-c79bfc9ac7f9
keywords:
- IoTimer
- IoInitializeTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9346742cfbafcbd3f2a0793f2356cb6986dbb96c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562567"
---
# <a name="providing-iotimer-context-information"></a>提供 IoTimer 上下文信息





*上下文*指针传递给[**最好**](https://msdn.microsoft.com/library/windows/hardware/ff549344)标识上下文区域的其他驱动程序例程，以及[ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)例程本身，可以维护有关定时操作的状态。 I/O 管理器传递*上下文*指针时它将调用*IoTimer*例程。

因为*IoTimer*例程运行在 IRQL = 调度\_级别，其上下文区域必须在常驻，系统空间内存中。 具有大多数驱动程序*IoTimer*例程使用[设备扩展](device-extensions.md)形式的关联的设备对象的*上下文*-访问区域中，但上下文可以改为是如果驱动程序使用的控制器扩展[控制器对象](using-controller-objects.md)或非分页缓冲池分配驱动程序中。

**请遵循以下准则，以便** *IoTimer * * * 例程的上下文区域：**

-   如果*IoTimer*例程与驱动程序的 ISR 共享其上下文区域，则必须使用[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)调用[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)以包含多个处理器安全的方式访问的上下文区域的例程。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

-   如果*IoTimer*例程不与 ISR 共享其上下文区域，但共享它与另一个驱动程序例程，驱动程序必须保护的共享的上下文区域初始化 executive 数值调节钮锁定后，若要访问上下文以包含多个处理器安全的方式的信息。 有关详细信息，请参阅[旋转锁](spin-locks.md)。

 

 




