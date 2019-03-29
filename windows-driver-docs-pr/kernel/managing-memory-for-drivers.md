---
title: Windows 驱动程序的内存管理
description: 内核模式驱动程序为目的，例如将内部数据存储、 I/O 操作过程中将缓存数据和与其他内核模式和用户模式组件共享内存分配内存。
ms.assetid: e030a37c-26ab-4177-9980-4336928975e1
keywords:
- 内存管理 WDK 内核
- 可用空间 WDK 内核
- 可用空间 WDK 内核
- 请参阅 WDK 内存 WDK 的空间
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 796ec13ccedf25e4c2ae2b48bd457087a9b3afc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567598"
---
# <a name="memory-management-for-windows-drivers"></a>Windows 驱动程序的内存管理


内核模式驱动程序为目的，例如将内部数据存储、 I/O 操作过程中将缓存数据和与其他内核模式和用户模式组件共享内存分配内存。 驱动程序开发人员应了解在 Windows 中的内存管理，以便他们使用已分配内存，正确而高效地。 Windows 管理虚拟和物理内存，并将内存划分为单独的用户和系统地址空间。 驱动程序可以指定已分配的内存是否支持按需分页、 数据缓存和指令执行等功能。




*内存管理器*是内核组件，它在 Windows 中执行的内存管理操作。 有关详细信息，请参阅[Windows 内核模式内存管理器](windows-kernel-mode-memory-manager.md)。

内存管理器实现多个内核模式驱动程序调用来分配和管理内存的支持例程。 有关详细信息，请参阅[内存分配数据和缓冲区管理](https://msdn.microsoft.com/library/windows/hardware/ff554422)。

内核模式驱动程序的内存管理功能是不同的用户模式应用程序。 有关应用程序的内存管理的详细信息，请参阅[内存管理](https://msdn.microsoft.com/library/windows/desktop/aa366779)。

## <a name="in-this-section"></a>本节内容


-   [Windows 内存空间的概述](overview-of-windows-memory-space.md)
-   [分配系统空间内存](allocating-system-space-memory.md)
-   [映射寄存器](map-registers.md)
-   [总线相对地址映射到的虚拟地址](mapping-bus-relative-addresses-to-virtual-addresses.md)
-   [使用内核堆栈](using-the-kernel-stack.md)
-   [使用后备链列表](using-lookaside-lists.md)
-   [使驱动程序可分页](making-drivers-pageable.md)
-   [访问只读的系统内存](accessing-read-only-system-memory.md)
-   [访问用户空间内存](accessing-user-space-memory.md)
-   [无执行 (NX) 非分页缓冲的池](no-execute-nonpaged-pool.md)
-   [部分对象和视图](section-objects-and-views.md)
-   [使用 MDLs](using-mdls.md)

 

 




