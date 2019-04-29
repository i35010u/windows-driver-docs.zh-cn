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
ms.openlocfilehash: 3883195353e59c1ed62819b03ed5af3dfb673d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380279"
---
# <a name="managing-kernel-objects"></a>管理内核对象





Windows 对象管理器控件*对象*是内核模式下操作系统的一部分。 一个对象是操作系统管理的数据的集合。

典型的内核模式对象包括以下对象：

-   设备对象 (请参阅[设备对象和设备堆栈](device-objects-and-device-stacks.md)。)

-   文件对象。

-   符号链接。

-   注册表项。

-   线程和进程。

-   内核调度程序对象，如事件对象和互斥体对象。 (请参阅[内核调度程序对象](kernel-dispatcher-objects.md)。)

-   回调对象。 (请参阅[回调对象](callback-objects.md)。)

-   部分对象。 (请参阅[部分对象和视图](section-objects-and-views.md)。)

内核模式的对象，可以使用对象管理器操作合作关系中的对象，而不损坏操作系统需要的对象的部分。 此原则称为*封装*，而是一个面向对象的编程的核心概念。 (因为内核模式的对象不提供的面向对象的其他方面，内核模式编程通常称为[*基于对象的*](object-based.md)。)内核模式的对象不遵循相同的规则中的对象C++或 Microsoft com。

可以通过指针引用内核模式对象。 对象可能包含的对象名称。 有关对象名称的详细信息，请参阅[对象名称](object-names.md)。

用户模式编程人员可以引用对象只能通过间接寻址，使用*处理*。 如果对象具有一个名称，可用于获取在用户模式下的句柄。 有关控点的详细信息，请参阅[对象句柄](object-handles.md)。

内核模式对象具有非常特定的生命周期。 有关对象生命周期的详细信息，请参阅[对象的生命周期](life-cycle-of-an-object.md)。

对象安全是内核模式编程首要关心的问题。 对象安全的详细信息，请参阅[对象安全](object-security.md)。

内核模式环境中的虚拟目录系统，也称为对象命名空间中存储对象。 这允许要进行访问以分层方式与父对象和子对象。 此命名空间类似于文件系统集的目录，但不完全对应您的计算机上的特定文件系统。 对象目录的详细信息，请参阅[对象目录](object-directories.md)。

 

 




