---
title: 锁定可分页代码或数据
description: 锁定可分页代码或数据
ms.assetid: b99b6af3-b4b1-4fd6-ac73-27c1068183a4
keywords:
- 锁定的代码或数据的可分页的驱动程序 WDK 内核
- 锁定 WDK 可分页的驱动程序
- 还原可分页的状态
- 常驻代码 WDK 可分页驱动程序
- 隔离可分页的代码
- 页关键字 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56313f85fa62f3e6aa160b609db56316af01e9fc
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716958"
---
# <a name="locking-pageable-code-or-data"></a>锁定可分页代码或数据





某些内核模式驱动程序，如串行和并行的驱动程序，无需为驻留在内存中的除非他们管理的设备已打开。 但是，只要没有活动连接或端口，驱动程序代码，用于管理该端口的某些部分必须在常驻设备提供服务。 当未正在使用的端口或连接时，则不需要的驱动程序代码。 与此相反，包含系统代码、 应用程序代码或系统分页文件的磁盘的驱动程序必须始终为驻留在内存中的因为驱动程序不断地在其设备与系统之间传输数据。

它所管理的设备不处于活动状态时，偶尔使用设备 （例如调制解调器） 的驱动程序可以释放系统空间。 本部分将放在单个部分必须是常驻活动设备，提供服务的代码和您的驱动程序在内存中锁定代码，使用该设备时，便可以将指定为可分页。 当打开驱动程序的设备时，操作系统将存入内存的可分页的部分中，驱动程序锁定它存在直到不再需要。

系统 CD 音频驱动程序代码使用此技术。 驱动程序的代码分为可分页几个部分根据制造商的 CD 设备。 某些品牌可能永远不会显示给定系统上。 此外，即使 CD-ROM 的系统上存在，它可能会访问很少，因此分组到可分页部分中，通过 CD 类型的代码可确保永远不会加载的设备的特定计算机上不存在的代码。 但是，当访问该设备，系统可加载相应的 CD 设备的代码。 然后驱动程序调用[ **MmLockPagableCodeSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagablecodesection)例程，如所述，要到其设备时的内存中锁定其代码正在使用。

若要隔离到命名的节的可分页的代码，请将其标记与以下编译器指令：

**\#杂注 alloc\_文本 (页\*Xxx**<em>, \*RoutineName</em>* *)

可分页的代码节的名称必须以"PAGE"由四个字母开头，并且可以后跟最多四个字符 (表示为此处 **_Xxx_** ) 来唯一地标识部分。 节名称 （即，"页"） 的前四个字母必须采用大写形式。 *RoutineName*标识包含的可分页的部分中的入口点。

驱动程序文件中的可分页的代码部分的最短有效名称只是页。 例如，下面的代码示例中的杂注指令标识`RdrCreateConnection`作为入口点在一个名为页的可分页的代码部分中。

```cpp
#ifdef  ALLOC_PRAGMA 
#pragma alloc_text(PAGE, RdrCreateConnection) 
#endif 
```

使可分页的驱动程序代码驻留在内存中锁定，驱动程序调用[ **MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagablecodesection)，传递 （通常在驱动程序例程的入口点） 的地址是可分页的代码中部分。 **MmLockPagableCodeSection**中包含在调用的例程的部分的全部内容的锁。 换而言之，此调用可与相同的页关联的每个例程*Xxx*标识符常驻和锁定在内存中。

**MmLockPagableCodeSection**返回的句柄时解锁部分使用 (通过调用[ **MmUnlockPagableImageSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpagableimagesection)例程) 或驱动程序时必须锁定中的节在其代码中的其他位置。

驱动程序还可以将很少使用数据视为作为可分页，以便它，也可以出页之前它所支持的设备处于活动状态。 例如，系统混音器驱动程序将使用可分页的数据。 Mixer 设备都有与之关联，因此此驱动程序可以使其数据可分页无异步 I/O。

可分页的数据部分的名称必须以"PAGE"由四个字母开头，可以后跟最多四个字符来唯一地标识部分。 节名称 （即，"页"） 的前四个字母必须采用大写形式。

避免将相同的名称分配给代码和数据部分。 若要提高源代码的可读性，驱动程序开发人员通常给页的名称的可分页的代码段，因为该名称是短，它可能会出现在大量分配\_文本杂注指令。 较长的名称会分配给任何可分页的数据部分 (例如，对于数据 PAGEDATA\_seg，bss 的 PAGEBSS\_seg，，等等) 驱动程序可能需要的。

例如，下面的代码示例中的前两个杂注指令定义两个可分页的数据部分，PAGEDATA 和 PAGEBSS。 使用数据声明 PAGEDATA\_seg 杂注指令和包含已初始化的数据。 使用 bss 声明 PAGEBSS\_seg 杂注指令和包含未初始化的数据。

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

在此代码示例中，`Variable1`和`Array1`显式初始化，因此位于 PAGEDATA 部分。 `Variable2` 和`Array2`隐式初始化为零，并放入的 PAGEBSS 节。

隐式初始化为零的全局变量可以减少磁盘上的可执行文件的大小和孰优孰显式初始化为零。 除中，在其中它才可将变量放在特定的数据部分的情况下应避免使用显式的零初始化。

若要使驻留在内存中的数据部分，并将其锁定在内存中，驱动程序调用[ **MmLockPagableDataSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagabledatasection)，传递数据项的可分页的数据部分中显示。 **MmLockPagableDataSection**返回要在后续锁定或解锁请求中使用的句柄。

若要还原锁定的节的可分页状态，请调用[ **MmUnlockPagableImageSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpagableimagesection)，将返回的句柄值传递[ **MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagablecodesection)或[ **MmLockPagableDataSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagabledatasection)根据。 驱动程序的[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程必须调用**MmUnlockPagableImageSection**释放其所获得的可锁定的代码和数据节的每个句柄。

锁定节是代价高昂的操作，因为内存管理器锁定到内存中的页之前必须搜索其加载的模块列表。 如果驱动程序锁定在其代码中的多个位置中的部分，则应使用更高效[ **MmLockPagableSectionByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmlockpagablesectionbyhandle)其首次调用后**MmLockPagable*Xxx*部分**。

句柄传递给**MmLockPagableSectionByHandle**是对的早期调用返回的句柄**MmLockPagableCodeSection**或**MmLockPagableDataSection**。

内存管理器维护的每个部分句柄计数和驱动程序调用每次将递增此计数**MmLockPagable<em>Xxx</em>** 该节。 调用**MmUnlockPagableImageSection**递减计数。 在任一部分句柄的计数器为非零值，该部分会保持锁定在内存中。

只要加载其驱动程序部分的句柄无效。 因此，驱动程序应调用**MmLockPagable*Xxx*部分**仅一次。 如果驱动程序需要其他锁定调用，则应使用**MmLockPagableSectionByHandle**。

如果驱动程序调用任意**MmLockPagable<em>Xxx</em>** 例程的一个部分，其中已被锁定，内存管理器递增引用计数的部分。 如果部分换出时锁定例程调用时，内存管理器页的部分中和其引用计数设置为 1。

使用此方法对系统资源的驱动程序的影响降至最低。 该驱动程序运行时，它可以锁定到内存中，代码和数据，以便为驻留。 当其设备，（即，打开或关闭设备时在设备处于永远不会） 没有未完成 I/O 请求，该驱动程序可以解锁的相同代码或数据，使其可用于调出。

但是，驱动程序已连接中断后，可以在中断始终处理过程中调用任何驱动程序代码必须是内存驻留。 而某些设备驱动程序可以按需可分页或锁定到内存中进行，此类组某些核心驱动程序的代码和数据必须是永久驻留在系统空间中。

请考虑对锁定的代码或数据部分的以下实现准则。

- 主要用途**Mm (Un) 锁<em>Xxx</em>** 例程是启用通常非分页的代码或数据进行分页和的情况下通过非分页的代码或数据。 如串行驱动程序和并行驱动程序的驱动程序是很好的示例： 如果设备没有打开的句柄这样的驱动程序管理、 代码的部分不需要可以保留出分页。重定向程序和服务器也是可以使用此技术的驱动程序的很好的示例。 如果没有活动连接，这两个这些组件可以调出。

- 整个可分页的节被锁定到内存中。

- 有关代码的一个部分，另一个用于每个驱动程序数据都十分高效。 可分页的很多命名的部分是通常效率低下。

- 将完全可分页的部分和分页，但按需锁定部分分开。

- 请记住， **MmLockPagableCodeSection**并**MmLockPagableDataSection**不应频繁地调用。 内存管理器加载部分时，这些例程可能会导致大量的 I/O 活动。 如果驱动程序必须在其代码中的多个位置中的部分已锁定，则应使用**MmLockPagableSectionByHandle**。

 

 




