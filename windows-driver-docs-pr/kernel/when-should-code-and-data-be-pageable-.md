---
title: 何时应对代码和数据进行分页
description: 何时应对代码和数据进行分页
keywords:
- 内存管理 WDK 内核，可分页驱动程序
- 可分页驱动程序 WDK 内核，何时应进行分页
- 已锁定的按需代码 WDK 内核
- 旋转锁定 WDK 内存
- 居民代码 WDK 可分页驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee13088c9c7e38703720ddb9ccf70e13c04780b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789789"
---
# <a name="when-should-code-and-data-be-pageable"></a>代码和数据何时应可分页？





可以使所有或部分驱动程序可分页。 寻呼驱动程序代码可以减小驱动程序加载映像的大小，从而释放系统空间用于其他用途。 最适用于偶尔使用的设备（例如调制解调器和 CD-ROM）的驱动程序，或者很少被称为的驱动程序部分。

执行以下任何一项的驱动程序代码都必须驻留在内存中。 也就是说，此代码必须位于非分页的部分或在代码运行时在内存中锁定的分页部分。

-   运行时间为 IRQL = 调度 \_ 级别。

-   获取旋转锁。

-   调用任何内核的对象支持例程（如 [**KeReleaseMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) 或 [**KeReleaseSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)），其中 *Wait* 参数设置为 **TRUE**。 如果在 " *等待* " 设置为 " **TRUE**" 的情况下调用内核，则调用将在调度级别以 IRQL 返回 \_ 。

&lt; \_ 当代码执行可能导致页错误的任何内容时，驱动程序代码必须在 IRQL 调度级别运行。 如果代码执行以下任一操作，则可能会导致页错误：

-   访问未在内存中锁定的分页池。

-   调用可分页的例程。

-   在用户线程的上下文中访问未锁定的用户缓冲区。

通常情况下，如果所有可分页代码 (或数据) 的总大小至少为 4 kb () KB，则应进行分页。 应尽可能将纯可分页的代码 (或数据) 隔离到不同于代码 (或数据) 的单独节中，但有时必须锁定。 例如，将纯粹的可分页代码和已锁定的按需代码组合起来会导致更多的系统空间被锁定，而不是必需的。 但是，如果驱动程序的可分页代码 (或数据) 的大小不能超过 4 KB，则可以将该代码 (或数据) 与已锁定的按需代码 (或数据) 合并到一个部分，从而节省系统空间。

 

