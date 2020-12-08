---
title: 锁定可分页代码或数据
description: 锁定可分页代码或数据
keywords:
- 可分页驱动程序 WDK 内核，锁定代码或数据
- 锁定 WDK 可分页驱动程序
- 还原可分页状态
- 居民代码 WDK 可分页驱动程序
- 隔离可分页代码
- 页关键字 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6f7b6f90c4e0a6e4023f81158e9c8449c3e9fcd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815073"
---
# <a name="locking-pageable-code-or-data"></a>锁定可分页代码或数据





某些内核模式驱动程序（例如串行和并行驱动程序）无需驻留在内存中，除非打开它们管理的设备。 但是，只要有活动的连接或端口，管理该端口的驱动程序代码的某些部分就必须驻留在设备上。 如果未使用端口或连接，则不需要驱动程序代码。 相反，包含系统代码、应用程序代码或系统分页文件的磁盘的驱动程序必须始终驻留在内存中，因为驱动程序会在其设备和系统之间持续传输数据。

偶尔使用的设备 (（例如调制) 解调器）的驱动程序在它管理的设备不处于活动状态时可以释放系统空间。 如果放置在一个部分中，这些代码必须位于一起才能为活动设备服务，并且当使用设备时，如果驱动程序在内存中锁定代码，则可以将此部分指定为可分页。 打开驱动程序的设备后，操作系统会将可分页部分引入内存，驱动程序会将其锁定，直到不再需要。

系统 CD 音频驱动程序代码使用此方法。 根据 CD 设备制造商的不同，驱动程序的代码已分组为可分页的部分。 某些品牌可能永远不会出现在给定的系统上。 此外，即使系统上存在 CD-ROM，也可能很少访问它，因此，按 CD 类型将代码分组到可分页部分可确保永远不会加载不在特定计算机上的设备代码。 但是，当访问设备时，系统会为相应的 CD 设备加载代码。 然后，该驱动程序调用 [**MmLockPagableCodeSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) 例程，如下所述，在使用其设备时将其代码锁定到内存。

若要将可分页代码隔离到一个命名部分，请使用以下编译器指令进行标记：

**\# pragma 分配 \_ 文本 (PAGE * Xxx**<em>， *RoutineName</em>* * )**

可分页代码部分的名称必须以四个字母 "PAGE" 开头，并可后跟四个字符， (在此处表示为 **_Xxx_**) 以唯一标识该部分。 节名 (的前四个字母为 "PAGE" ) 必须大写。 *RoutineName* 标识要包含在可分页节中的入口点。

驱动程序文件中的可分页代码部分的最短有效名称只是页面。 例如，下面的代码示例中的杂注指令在 `RdrCreateConnection` 名为 PAGE 的可分页代码部分中标识为入口点。

```cpp
#ifdef  ALLOC_PRAGMA 
#pragma alloc_text(PAGE, RdrCreateConnection) 
#endif 
```

若要在内存中驻留和锁定可分页的驱动程序代码，驱动程序将调用 [**MmLockPagableCodeSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection)，传递地址 (通常是可分页代码部分) 的驱动程序例程的入口点。 **MmLockPagableCodeSection** 会锁定包含调用中引用的例程的部分的全部内容。 换句话说，此调用会使每个与相同 PAGE *Xxx* 标识符关联的例程在内存中驻留和锁定。

**MmLockPagableCodeSection** 返回一个句柄，该句柄在 (通过调用 [**MmUnlockPagableImageSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection) 例程) 或驱动程序必须在其代码中的其他位置锁定节时使用。

驱动程序还可以将极少使用的数据视为可分页，以便在它支持的设备处于活动状态之前，也可以将其分页出去。 例如，系统混音器驱动程序使用可分页的数据。 混音器设备没有与其关联的异步 i/o，因此此驱动程序可以使其数据可分页。

可分页数据部分的名称必须以四个字母 "PAGE" 开头，可以后跟四个字符来唯一标识该部分。 节名 (的前四个字母为 "PAGE" ) 必须大写。

避免为代码和数据节指定相同的名称。 为了使源代码更具可读性，驱动程序开发人员通常会将 "名称" 页分配给可分页代码部分，因为此名称较短，可能会出现在大量的分配 \_ 文本杂注指令中。 然后，将更长的名称分配给任何可分页的数据节 (例如，PAGEDATA for data \_ seg、PAGEBSS for bss \_ seg 等，以及驱动程序可能需要的) 。

例如，下面的代码示例中的前两个杂注指令定义了两个可分页数据节 PAGEDATA 和 PAGEBSS。 PAGEDATA 是使用数据 \_ seg 杂注指令声明的，其中包含已初始化的数据。 PAGEBSS 是使用 bss \_ seg 杂注指令声明的，其中包含未初始化的数据。

```cpp
#pragma data_seg("PAGEDATA")
#pragma bss_seg("PAGEBSS")

INT Variable1 = 1;
INT Variable2;

CHAR Array1[64*1024] = { 0 };
CHAR Array2[64*1024];

#pragma data_seg()
#pragma bss_seg()
```

在此代码示例中， `Variable1` 和 `Array1` 是显式初始化的，因此放置在 PAGEDATA 节中。 `Variable2` 和 `Array2` 隐式地初始化为零，并放置在 PAGEBSS 节中。

将全局变量隐式初始化为零可减少磁盘上的可执行文件的大小，并且优先于将显式初始化为零。 应避免使用显式的零初始化，除非在需要时才将变量放入特定数据部分。

为了使 data 部分驻留在内存中，驱动程序将调用 [**MmLockPagableDataSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection)，并传递一个显示在 "可分页数据" 部分的数据项。 **MmLockPagableDataSection** 返回一个句柄，以用于后续锁定或解锁请求。

若要还原锁定的节的可分页状态，请根据需要调用 [**MmUnlockPagableImageSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection)，传递 [**MmLockPagableCodeSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) 或 [**MmLockPagableDataSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection)返回的句柄值。 驱动程序的 [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程必须调用 **MmUnlockPagableImageSection** ，以释放为可锁定代码和数据部分获得的每个句柄。

锁定节是一种代价高昂的操作，因为在将页面锁定到内存之前，内存管理器必须搜索其已加载的模块列表。 如果驱动程序在其代码中的多个位置锁定某个部分，则应在其首次调用 **MmLockPagable *Xxx* 节** 后使用更有效的 [**MmLockPagableSectionByHandle**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmlockpagablesectionbyhandle) 。

传递给 **MmLockPagableSectionByHandle** 的句柄是先前调用 **MmLockPagableCodeSection** 或 **MmLockPagableDataSection** 时返回的句柄。

内存管理器维护每个节句柄的计数，并在每次驱动程序为该部分调用 **MmLockPagable <em>Xxx</em>** 时递增此计数。 对 **MmUnlockPagableImageSection** 的调用将减少计数。 当任何节句柄的计数器为非零值时，该部分将在内存中保持锁定状态。

只要加载了驱动程序的驱动程序，它的句柄就会有效。 因此，驱动程序只应调用一次 **MmLockPagable *Xxx* 部分** 。 如果驱动程序需要其他锁定调用，则应使用 **MmLockPagableSectionByHandle**。

如果驱动程序为已锁定的节调用了任何 **MmLockPagable <em>Xxx</em>** 例程，则内存管理器会递增此部分的引用计数。 如果调用锁例程时该部分已分页，则该部分中的内存管理器页会将其引用计数设置为1。

使用此技术可最大程度地减少驱动程序对系统资源的影响。 当驱动程序运行时，它可以锁定必须常驻的代码和数据。 如果设备没有未完成的 i/o 请求， (即关闭设备或设备从未打开) 时，驱动程序可以对相同的代码或数据进行解锁，使其可用于分页。

但是，在驱动程序连接中断后，任何在中断处理期间都可以调用的驱动程序代码都必须驻留在内存中。 尽管某些设备驱动程序可以进行分页或按需锁定到内存中，但某些核心的驱动程序代码和数据集必须永久驻留在系统空间中。

请考虑以下用于锁定代码或数据部分的实现准则。

- **Mm (未) 锁定 <em>Xxx</em>** 例程的主要用途是使通常非分页的代码或数据可以分页，并作为未分页的代码或数据进行分页。 诸如串行驱动程序和并行驱动程序之类的驱动程序都是很好的示例：如果驱动程序管理的设备没有打开的句柄，则不需要部分代码，也不需要将其打开。重定向程序和服务器也是可以使用此方法的驱动程序的好示例。 如果没有活动连接，则可以将这两个组件都调出。

- 整个可分页节被锁定在内存中。

- 每个驱动程序的代码部分和一个数据部分都有效。 许多命名的可分页部分通常效率低下。

- 保持纯可分页的部分和分页，但会单独进行锁定的按需部分。

- 请记住， **MmLockPagableCodeSection** 和 **MmLockPagableDataSection** 不应经常调用。 当内存管理器加载部分时，这些例程会导致大量 i/o 活动。 如果驱动程序必须锁定其代码中多个位置的部分，则应使用 **MmLockPagableSectionByHandle**。

 

