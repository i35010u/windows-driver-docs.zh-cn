---
title: 使用内核堆栈
description: 使用内核堆栈
keywords:
- 内存管理 WDK 内核，内核堆栈
- 内核模式堆栈空间 WDK
- 内核堆栈空间 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc35fc77d7359a3b2eac96535e5f66f25711baee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840677"
---
# <a name="using-the-kernel-stack"></a>使用内核堆栈





内核模式堆栈的大小限制为大约三个页。 因此，在将数据传递到内部例程时，驱动程序不能在内核堆栈上传递大量的数据。

若要避免用尽内核模式堆栈空间，请使用以下设计准则：

-   如果每个例程在内核堆栈上传递数据，请避免在一个内部驱动程序例程之间进行深层嵌套的调用。

-   如果设计具有递归例程的驱动程序，请确保限制可能发生的递归调用的数量。

换句话说，驱动程序的调用树结构应相对平整。 可以调用 [**IoGetStackLimits**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetstacklimits) 和 [**IoGetRemainingStackSize**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetremainingstacksize) 例程来确定可用的内核堆栈空间，或使用 [**KeExpandKernelStackAndCallout**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keexpandkernelstackandcallout) 将其展开。 请注意，内核模式堆栈的大小在不同的硬件平台和不同版本的操作系统之间可能会有所不同。

内核堆栈空间不足会导致严重的系统错误。 因此，驱动程序 [分配的系统空间内存](allocating-system-space-memory.md) 要比用尽内核堆栈空间的更好。 但是，非分页池也是受限系统资源。

通常情况下，内核模式堆栈驻留在内存中，但如果线程进入指定用户模式的等待状态，则有时可能会将其分页。 有关如何暂时禁用当前线程的内核堆栈分页的信息，请参阅 [**KeSetKernelStackSwapEnable**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kesetkernelstackswapenable) 。 出于性能原因，不建议全局禁用内核堆栈分页，但如果想要在调试会话期间执行此操作，请参阅 [禁用内核堆栈分页](../debugger/disable-paging-of-kernel-stacks.md)

由于内核堆栈可能会分页，因此，传递基于堆栈的缓冲区 (例如，本地变量) 为 DMA 或在 DISPATCH_LEVEL 或更高版本中运行的任何例程。
