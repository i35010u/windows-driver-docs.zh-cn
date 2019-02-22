---
title: 使用内核堆栈
description: 使用内核堆栈
ms.assetid: f1df01f4-f156-4267-a4a0-c548e16c02ea
keywords:
- 内存管理 WDK 内核，内核堆栈
- 内核模式堆栈空间 WDK
- 内核堆栈空间 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 714dce6251579ae4f1285fca3345ca7252c3bbf9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525183"
---
# <a name="using-the-kernel-stack"></a>使用内核堆栈





内核模式堆栈的大小被限制为大约三个页面。 因此时将数据传递给内部例程，, 驱动程序不能在内核堆栈上传递的大量数据。

若要避免内核模式堆栈空间不足，请使用以下设计指导原则：

-   避免深度嵌套调用一个内部驱动程序例程从另一种，如果每个例程将数据传递到内核堆栈上。

-   请确保限制的递归调用可能发生的次数，如果您设计的递归例程的驱动程序。

换而言之，驱动程序的调用关系树结构应为相对较平。 您可以调用[ **IoGetStackLimits** ](https://msdn.microsoft.com/library/windows/hardware/ff549299)并[ **IoGetRemainingStackSize** ](https://msdn.microsoft.com/library/windows/hardware/ff549286)例程来确定内核堆栈空间，它是可用，或[ **KeExpandKernelStackAndCallout** ](https://msdn.microsoft.com/library/windows/hardware/ff552030)以将其展开。 请注意，内核模式堆栈的大小会因不同的硬件平台和不同版本的操作系统。

内核堆栈空间不足会导致系统错误。 因此，它是到驱动程序的更好[分配系统空间内存](allocating-system-space-memory.md)比若要运行内核堆栈空间不足。 但是，非分页缓冲的池也是有限的系统资源。

通常情况下，内核模式堆栈驻留在内存中，但它可以偶尔出页如果线程进入等待状态，用于指定用户模式。 请参阅[ **KeSetKernelStackSwapEnable** ](https://msdn.microsoft.com/library/windows/hardware/ff553262)如何暂时禁用分页在当前线程的内核堆栈的信息。 出于性能原因，不建议禁用全局，分页的内核堆栈，但如果你想要在调试会话期间此，请参阅[禁用分页的内核堆栈](https://msdn.microsoft.com/library/windows/hardware/ff541920)

因为内核堆栈可能会换出，请谨慎将基于堆栈的缓冲区 （即本地变量） 传递给 DMA 或运行位于 DISPATCH_LEVEL 或更高的任何例程。

