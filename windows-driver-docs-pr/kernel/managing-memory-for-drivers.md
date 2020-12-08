---
title: Windows 驱动程序的内存管理
description: 内核模式驱动程序出于某种目的分配内存，例如存储内部数据、在 i/o 操作过程中缓冲数据，以及与其他内核模式和用户模式组件共享内存。
keywords:
- 内存管理 WDK 内核
- 可用空间 WDK 内核
- 可用空间 WDK 内核
- 太空 WDK，请参阅内存 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3654aab0ff97fefab88fb02965abd53d5c9827
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793533"
---
# <a name="memory-management-for-windows-drivers"></a>Windows 驱动程序的内存管理


内核模式驱动程序出于某种目的分配内存，例如存储内部数据、在 i/o 操作过程中缓冲数据，以及与其他内核模式和用户模式组件共享内存。 驱动程序开发人员应了解 Windows 中的内存管理，以便它们可以正确有效地使用已分配的内存。 Windows 管理虚拟内存和物理内存，并将内存分割为单独的用户和系统地址空间。 驱动程序可以指定分配的内存是否支持需求分页、数据缓存和指令执行等功能。




*内存管理器* 是在 Windows 中执行内存管理操作的内核组件。 有关详细信息，请参阅 [Windows Kernel-Mode 内存管理器](windows-kernel-mode-memory-manager.md)。

内存管理器实现了多个内核模式支持例程，驱动程序调用来分配和管理内存。 有关详细信息，请参阅 [内存分配和缓冲区管理](/windows-hardware/drivers/ddi/_kernel/#memory-allocation-and-buffer-management)。

内核模式驱动程序的内存管理功能不同于用户模式应用程序的内存管理功能。 有关应用程序的内存管理的详细信息，请参阅 [内存管理](/windows/desktop/Memory/memory-management)。

## <a name="in-this-section"></a>在本节中


-   [Windows 内存空间概述](overview-of-windows-memory-space.md)
-   [分配系统空间内存](allocating-system-space-memory.md)
-   [映射寄存器](map-registers.md)
-   [将总线相对地址映射到虚拟地址](mapping-bus-relative-addresses-to-virtual-addresses.md)
-   [使用内核堆栈](using-the-kernel-stack.md)
-   [使用后备列表](using-lookaside-lists.md)
-   [使驱动程序可分页](making-drivers-pageable.md)
-   [访问只读的系统内存](accessing-read-only-system-memory.md)
-   [访问用户空间内存](accessing-user-space-memory.md)
-   [非执行 (NX) 非分页缓冲池](no-execute-nonpaged-pool.md)
-   [节对象和视图](section-objects-and-views.md)
-   [使用 MDL](using-mdls.md)

 

