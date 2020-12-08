---
title: x64 驱动程序的限制
description: x64 驱动程序的限制
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eaebe5a2c4cd1db775169301c8eda798fab451d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825889"
---
# <a name="driver-x64-restrictions"></a>x64 驱动程序的限制


在基于 x64 的系统上，将保护内核代码和某些内核数据结构不被修改。 任何试图修改此类代码或数据的驱动程序都将导致系统检查 \_) 严重结构 \_ 损坏 bug 检查 (。

基于 x64 的系统的驱动程序必须避免可能触发此错误检查的操作。 具体而言，驱动程序不能：

-   尝试在运行时修改内核代码。

-   实现并使用自己的堆栈。

-   修改硬件调度表，如中断调度表 (IDT) 或全局描述符表 (GDT) 。

-   修改未记录的内核数据结构。

即使前面的操作将不会在基于 x86 或基于 Itanium 的系统上触发 bug 检查，驱动程序也不应在任何平台上执行这些操作。 这些操作可能在 Microsoft Windows 操作系统的未来版本中不起作用。

有关修改内核代码和数据结构的详细信息，请参阅 [修补基于 x64 的系统的策略](https://go.microsoft.com/fwlink/p/?linkid=50719) 白皮书和 [64 位修补程序常见问题解答](https://go.microsoft.com/fwlink/p/?linkid=69534)。

有关使用64位编译器编程的常规信息，请参阅 [使用 Visual C++ 的64位编程](/cpp/build/configuring-programs-for-64-bit-visual-cpp)。

 

