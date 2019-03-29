---
title: 为自旋锁和受保护数据提供存储
description: 为自旋锁和受保护数据提供存储
ms.assetid: bde18474-10c3-4d9a-b120-6cbd5fc675cc
keywords:
- 存储 WDK 自旋锁
- 存储数值调节钮锁定受保护的数据
- 数值调节钮锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba56d78c33627e9b70feb5ec457f09ae97c01429
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562086"
---
# <a name="providing-storage-for-spin-locks-and-protected-data"></a>为自旋锁和受保护数据提供存储





作为设备启动时的一部分，驱动程序必须分配驻留的存储的任何数值调节钮锁定受保护的数据或资源并在以下位置之一中的相应自旋锁的：

-   该驱动程序通过调用来设置的设备对象的设备扩展[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)

-   该驱动程序通过调用来设置控制器对象的控制器扩展[ **IoCreateController**](https://msdn.microsoft.com/library/windows/hardware/ff548395)

-   非分页缓冲，驱动程序将获取通过调用的系统空间内存[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)

尝试访问可分页的数据，同时保留数值调节钮锁定会导致严重的页面错误，如果该页面不存在。 引用 （因为它已存储在可分页内存和当前换出时） 是无效的数值调节钮锁还会导致严重的页面错误。

驱动程序必须提供存储为每个 executive 自旋锁也可能会使用以下几种：

- 任何旋转锁的驱动程序显式获取和释放使用任一**Ke * Xxx*** 旋转锁例程。

- 任何旋转锁用作参数的任何**ExInterlocked * Xxx*** 例程。

尽管驱动程序可以调用**ExInterlocked * Xxx*** 从其 ISR 的例程或[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程，它不能使用任何**Ke * Xxx*** 例程来获取和释放调节锁大于调度任何 IRQL\_级别。 因此，重复使用旋转锁之间的任何驱动程序调用**Ke*Xxx*旋转锁**并**ExInterlocked * Xxx*** 例程必须使每次调用在 IRQL 运行时&lt;= 调度\_级别。

驱动程序可以将传递到同一个数值调节钮锁**ExInterlockedInsertHeadList**到另一个一样**ExInterlocked * Xxx*** 例程，只要这两个例程在相同的 IRQL 使用自旋锁。 有关数值调节钮锁使用情况如何影响性能的详细信息，请参阅[使用数值调节钮锁定：示例](using-spin-locks--an-example.md)。

除了其 executive 自旋锁的存储设备驱动程序必须提供另一个旋转锁，如果它具有 multivector ISR 或多个 ISR.要与它中断的对象相关联的存储

 

 




