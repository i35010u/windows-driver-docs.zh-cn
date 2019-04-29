---
title: x64 驱动程序的限制
description: x64 驱动程序的限制
ms.assetid: 717ca559-93aa-48d6-8347-bfdf223f1aa4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c16389945a5b6b96fcc2b87c7cf73b92ce730289
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372702"
---
# <a name="driver-x64-restrictions"></a>x64 驱动程序的限制


在基于 x64 的系统中，从修改保护内核代码和某些内核数据结构。 任何尝试修改此类代码或数据的驱动程序将会导致 bug 检查系统 (与严重\_结构\_损坏错误检查)。

对于基于 x64 的系统驱动程序必须避免可能会触发此 bug 检查的操作。 具体而言，驱动程序不可以：

-   尝试在运行时修改内核代码。

-   实现和使用自己的堆栈。

-   修改硬件调度表，例如中断调度表 (IDT) 或全局描述符表 (GDT)。

-   修改未记录的内核数据结构。

尽管上述操作不会触发 bug 检查在基于 x86 或基于 Itanium 的系统中，驱动程序不应执行任何一种在任何平台上的操作。 这些操作可能无法在将来版本的 Microsoft Windows 操作系统。

有关修改内核代码和数据结构的详细信息，请参阅[针对基于 x64 的系统的修补策略](https://go.microsoft.com/fwlink/p/?linkid=50719)白皮书并[64-Bit 修补常见问题解答](https://go.microsoft.com/fwlink/p/?linkid=69534)。

有关使用 64 位编译器的编程的常规信息，请参阅[64 位编程与视觉对象C++ ](https://go.microsoft.com/fwlink/p/?linkid=165521)。

 

 




