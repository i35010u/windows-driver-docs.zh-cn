---
title: 使驱动程序可分页
description: 使驱动程序可分页
ms.assetid: 0b3c1e00-2416-4534-9934-bb05f91c7482
keywords:
- 内存管理 WDK 内核，可分页驱动程序
- 可分页驱动程序 WDK 内核
- 可分页驱动程序 WDK 内核，关于可分页驱动程序
- 页面外的驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e67273ee76958a59df0c45c341a6e2afb7290a4
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403336"
---
# <a name="making-drivers-pageable"></a>使驱动程序可分页





默认情况下，链接器将名称（如 "text" 和 "data"）分配给驱动程序映像文件的 "代码" 和 "数据" 部分。 加载驱动程序时，i/o 管理器会将这些部分非分页。 非分页的部分始终驻留在内存中。

驱动程序开发人员可以选择使驱动程序的指定部分可以分页，以便 Windows 可以在未使用时将这些部件移动到页面文件中。 为了使代码或数据部分可分页，驱动程序开发人员将以 "PAGE" 开头的名称分配给部分。 在加载驱动程序时，i/o 管理器会检查部分的名称。 如果部分名称以 "PAGE" 开头，则 i/o 管理器会使该部分可分页。

以 IRQL &gt; = 调度级别运行的代码 \_ 必须驻留在内存中。 也就是说，此代码必须位于不可分页段或在内存中锁定的可分页段中。 如果以 IRQL &gt; = 调度级别运行的代码 \_ 导致页错误，则会发生 bug 检查。 驱动程序可以使用 [**分页 \_ 代码**](./mm-bad-pointer.md) 宏来验证是否只在适当的 IRQLs 调用了可分页函数。

如果代码或数据部分是可分页的，则驱动程序可以通过调用 [**MmLockPagableCodeSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) 或 [**MmLockPagableDataSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection) 例程来锁定内存中的部分。 该部分将保持锁定状态，直到驱动程序调用 [**MmUnlockPagableImageSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection) 例程对其进行解锁。 当可分页节被锁定时，它的行为与非分页节的行为相同。

有关如何为代码和数据部分分配名称的信息，请参阅 [**MmLockPagableCodeSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) 和 [**MmLockPagableDataSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection)。

本节包括下列主题：

[代码和数据何时应可分页？](when-should-code-and-data-be-pageable-.md)

[使驱动程序代码或数据可分页](detecting-code-that-can-be-pageable.md)

 

