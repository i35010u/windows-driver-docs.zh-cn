---
title: 何时应对代码和数据进行分页
description: 何时应对代码和数据进行分页
ms.assetid: 2804f558-8c8c-43f4-b14e-8deaac9da286
keywords:
- 内存管理 WDK 内核，可分页驱动程序
- 可分页驱动程序 WDK 内核，何时应进行分页
- 已锁定的按需代码 WDK 内核
- 旋转锁定 WDK 内存
- 居民代码 WDK 可分页驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa8110999947455f4a2c6e2967cec4c9330eb3e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838320"
---
# <a name="when-should-code-and-data-be-pageable"></a>代码和数据何时应可分页？





可以使所有或部分驱动程序可分页。 寻呼驱动程序代码可以减小驱动程序加载映像的大小，从而释放系统空间用于其他用途。 最适用于偶尔使用的设备（例如调制解调器和 CD-ROM）的驱动程序，或者很少被称为的驱动程序部分。

执行以下任何一项的驱动程序代码都必须驻留在内存中。 也就是说，此代码必须位于非分页的部分或在代码运行时在内存中锁定的分页部分。

-   在 IRQL = 调度\_级别或更高版本上运行。

-   获取旋转锁。

-   调用任何内核的对象支持例程（如[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或[**KeReleaseSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)），其中*Wait*参数设置为**TRUE**。 如果在将*Wait*设置为**TRUE**的情况下调用内核，则在调度\_级别，调用将以 IRQL 返回。

当代码执行可能导致页错误的任何内容时，驱动程序代码必须以 IRQL 运行 &lt; 调度\_级别。 如果代码执行以下任一操作，则可能会导致页错误：

-   访问未在内存中锁定的分页池。

-   调用可分页的例程。

-   在用户线程的上下文中访问未锁定的用户缓冲区。

通常，如果所有可分页代码（或数据）的总大小至少为 4 kb，则应将某个部分分页。 应尽可能将纯可分页的代码（或数据）与代码（或数据）隔离在不同的节中，但有时还必须锁定。 例如，将纯粹的可分页代码和已锁定的按需代码组合起来会导致更多的系统空间被锁定，而不是必需的。 但是，如果驱动程序的可能可分页代码（或数据）少于 4 KB，则可以将该代码（或数据）与已锁定的按需代码（或数据）组合到一个部分，以节省系统空间。

 

 




