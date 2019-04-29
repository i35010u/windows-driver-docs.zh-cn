---
title: 使驱动程序可分页
description: 使驱动程序可分页
ms.assetid: 0b3c1e00-2416-4534-9934-bb05f91c7482
keywords:
- 内存管理 WDK 内核，可分页的驱动程序
- 可分页的驱动程序 WDK 内核
- 可分页的驱动程序 WDK 内核，有关可分页的驱动程序
- 分页出驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7723e1cbf3e98586836b0b74d90f88952aa84abf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378729"
---
# <a name="making-drivers-pageable"></a>使驱动程序可分页





默认情况下，链接器将".text"和"查看"等名称分配给驱动程序图像文件的代码和数据部分。 加载驱动程序，则 I/O 管理器使这些部分非分页。 非分页的部分始终是驻留在内存中的。

驱动程序开发人员可以选择以使指定的驱动程序可分页，以便 Windows 可以将移动这些部件到分页文件时未使用。 若要使代码或数据部分可分页，驱动程序开发人员将分配一个名称以与"页"的部分。 加载驱动程序时，I/O 管理器检查节的名称。 如果"页"开头的部分名称，则 I/O 管理器会使部分可分页。

代码运行在 IRQL &gt;= 调度\_级别必须是驻留在内存中。 也就是说，此代码必须在分页段中，或在被锁定在内存中的可分页段中。 如果代码，正在运行的 IRQL &gt;= 调度\_级别会导致页错误，就会执行错误检查。 驱动程序可以使用[ **PAGED\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff558773)宏，以验证是否仅在适用于 Irql 调用可分页的函数。

如果代码或数据部分为可分页，驱动程序可以通过调用锁定在内存中的部分[ **MmLockPagableCodeSection** ](https://msdn.microsoft.com/library/windows/hardware/ff554601)或[ **MmLockPagableDataSection**](https://msdn.microsoft.com/library/windows/hardware/ff554607)例程。 部分驱动程序调用之前一直处于锁定[ **MmUnlockPagableImageSection** ](https://msdn.microsoft.com/library/windows/hardware/ff556377)例程对其进行解锁。 虽然可分页的部分被锁定，它的行为与非分页部分相同。

有关如何将名称分配给代码和数据部分的信息，请参阅[ **MmLockPagableCodeSection** ](https://msdn.microsoft.com/library/windows/hardware/ff554601)并[ **MmLockPagableDataSection** ](https://msdn.microsoft.com/library/windows/hardware/ff554607).

本部分包括以下主题：

[何时代码和数据应可分页？](when-should-code-and-data-be-pageable-.md)

[使驱动程序代码或数据可分页](making-driver-code-or-data-pageable.md)

 

 




