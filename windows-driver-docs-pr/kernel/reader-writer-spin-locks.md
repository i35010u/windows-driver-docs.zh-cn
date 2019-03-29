---
title: 读取器/写入器自旋锁
description: 从 Windows Vista Service Pack 1 (SP1) 的一组相关的例程使用自旋锁来同步访问的共享的读取器和编写器的数据结构。
ms.assetid: E2853F35-590E-4EF5-8647-1261BC4B8D15
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9da891fc77c5a1f3a4bd17b36936cf2c9eab7035
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562585"
---
# <a name="readerwriter-spin-locks"></a>读取器/写入器自旋锁


从 Windows Vista Service Pack 1 (SP1) 的一组相关的例程使用自旋锁来同步访问的共享的读取器和编写器的数据结构。 只需要读取访问权限与数据结构的线程可以使用旋转锁与其他读取器线程共享此结构。 需要写入到共享的数据结构的线程必须使用数值调节钮锁获取的数据结构的独占访问权限之前它可以写入此结构。

如果读取器线程需要获取共享访问的自旋锁，并且已经持有锁的独占访问权限由编写器线程，读取器前必须等待要释放锁的编写器。 同样，如果编写器线程需要获取独占访问权限的自旋锁和锁已由一个或多个读取器线程保留的共享访问，编写器线程必须等待所有这些读取器线程释放锁。 让状态下等待编写器，则任何新的读取器线程可以不获取的锁。 相反，需要获取的锁的编写器正在等待的读取器必须先等待编写器来获取和释放锁。

一个线程可以切换读取器和编写器之间的角色。 已持有共享访问的自旋锁的线程可以尝试将旋转锁的访问模式从共享模式转换为排他模式。 如果没有读取器已拥有共享的访问，旋转锁，并且没有编写器已在等待获取独占访问权限的自旋锁，此尝试都会成功。

旋转锁的递归获得会导致死锁，并且不允许。

下面是一系列的例程，可用于管理从 Windows Vista SP1 的读取器/编写器自旋锁。

| 例程名称                                                                                | 描述                                                                                                           |
|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**ExAcquireSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451007)                         | 将获取调用方的独占访问权限的自旋锁并引发到调度 IRQL\_级别。                      |
| [**ExAcquireSpinLockExclusiveAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451009)    | 将获取在 IRQL 已运行的调用方的独占访问权限的自旋锁&gt;= 调度\_级别。          |
| [**ExAcquireSpinLockShared**](https://msdn.microsoft.com/library/windows/hardware/hh451053)                               | 获取共享访问由调用方，数值调节钮锁并引发到调度 IRQL\_级别。                         |
| [**ExAcquireSpinLockSharedAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451055)           | 获取由调用方已在 IRQL 上运行的共享访问的自旋锁&gt;= 调度\_级别。             |
| [**ExReleaseSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451061)                        | 释放调用方获取独占访问权限，而还原原始的 IRQL 自旋锁。                   |
| [**ExReleaseSpinLockExclusiveFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451058) | 释放调用方获取独占访问权限，而不小于 IRQL 自旋锁。                      |
| [**ExReleaseSpinLockShared**](https://msdn.microsoft.com/library/windows/hardware/hh451067)                              | 释放调用方为获取共享访问，旋转锁，并还原原始的 IRQL。                      |
| [**ExReleaseSpinLockSharedFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451064)      | 释放调用方为获取共享访问，旋转锁并不小于 IRQL。                         |
| [**ExTryConvertSharedSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451070)      | 尝试将转换的旋转锁的调用方已持有的共享访问对独占访问权限的访问状态。 |

 

所有采用作为其第一个参数，旋转锁，这是一个指向的读取器/编写器数值调节钮锁定例程**EX\_数值调节钮\_锁**结构。 此结构是不透明的驱动程序。 驱动程序应从非分页的系统内存的自旋锁分配的存储并初始化为零的锁。

 

 




