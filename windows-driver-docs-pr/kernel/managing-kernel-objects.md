---
title: 管理内核对象
description: 管理内核对象
ms.assetid: d45aca94-67b7-444d-8585-713ec982e3bc
keywords:
- 内核模式驱动程序 WDK，对象管理
- 对象管理器 WDK 内核
- 对象管理 WDK 内核
- 引用对象
- 对象名称 WDK 用户模式
- 对象管理 WDK 用户模式
- 内核模式对象 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a108a775c65393344b991055583e13bb4f7b2a1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184431"
---
# <a name="managing-kernel-objects"></a>管理内核对象





Windows 对象管理器控制作为内核模式操作系统一部分的 *对象* 。 对象是操作系统所管理的数据的集合。

典型的内核模式对象包括以下对象：

-   设备对象 (参阅 [设备对象和设备堆栈](device-objects-and-device-stacks.md)。 ) 

-   文件对象。

-   符号链接。

-   注册表项。

-   线程和进程。

-   内核调度程序对象，如事件对象和 mutex 对象。  (参阅 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md)。 ) 

-   回调对象。  (参阅 [回叫对象](callback-objects.md)。 ) 

-   节对象。  (参阅 [部分对象和视图](section-objects-and-views.md)。 ) 

内核模式对象使你能够在与对象管理器的合作关系中操作对象，而不会损坏操作系统所需的对象部分。 此原则称为 *封装* ，是面向对象编程的核心概念之一。  (因为内核模式对象并不提供对象方向的其他方面，所以通常将内核模式编程称为 [*基于对象*](object-based.md)。 ) 内核模式对象不遵循 c + + 或 Microsoft COM 中的对象。

可以通过指针引用内核模式对象。 对象可以具有对象名称。 有关对象名称的详细信息，请参阅 [对象名称](object-names.md)。

用户模式程序员只能通过间接寻址使用 *句柄*来引用对象。 如果对象具有名称，您可以使用它来获取用户模式下的句柄。 有关句柄的详细信息，请参阅 [对象句柄](object-handles.md)。

内核模式对象具有非常具体的生命周期。 有关对象生命周期的详细信息，请参阅 [对象的生命周期](life-cycle-of-an-object.md)。

对于内核模式编程，对象安全性是一个主要考虑因素。 有关对象安全的详细信息，请参阅 [对象安全性](object-security.md)。

内核模式环境将对象存储在虚拟目录系统（也称为对象命名空间）中。 这允许使用父对象和子对象以分层方式访问对象。 此命名空间类似于文件系统目录集，但并不完全对应于计算机上的特定文件系统。 有关对象目录的详细信息，请参阅 [对象目录](object-directories.md)。

 

