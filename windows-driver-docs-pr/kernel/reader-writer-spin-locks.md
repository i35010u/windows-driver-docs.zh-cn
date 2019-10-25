---
title: 读取器/写入器自旋锁
description: 从带有 Service Pack 1 （SP1）的 Windows Vista 开始，一组相关的例程使用自旋锁来支持对读取器和编写器共享的数据结构的同步访问。
ms.assetid: E2853F35-590E-4EF5-8647-1261BC4B8D15
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c0fac2388e801faae9f874989c534233fcf672bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827573"
---
# <a name="readerwriter-spin-locks"></a>读取器/写入器自旋锁


从带有 Service Pack 1 （SP1）的 Windows Vista 开始，一组相关的例程使用自旋锁来支持对读取器和编写器共享的数据结构的同步访问。 只需要对数据结构进行读取访问的线程可以使用旋转锁与其他读取器线程共享此结构。 需要写入共享数据结构的线程必须使用旋转锁来获取对数据结构的独占访问权限，然后才能将其写入到此结构中。

如果读取器线程需要获取共享访问的自旋锁，并且已持有一个写入器线程独占访问的锁，则读取器必须首先等待编写器释放该锁。 同样，如果编写器线程需要获取用于独占访问的自旋锁，并且一个或多个读取器线程已经持有锁用于共享访问，则编写器线程必须等待所有这些读取器线程释放该锁。 编写器等待时，没有新的读取器线程可以获取锁。 需要获取编写器等待的锁的读取器必须首先等待编写器获取并释放锁。

线程可以在读取器和编写器之间切换角色。 已经持有共享访问的旋转锁定的线程可以尝试将自旋锁的访问模式从共享模式转换为排他模式。 如果没有读者持有共享访问的自旋锁，并且没有任何编写器正在等待获取用于独占访问的旋转锁定，则此尝试将成功。

对自旋锁的递归获取会导致死锁，不允许这样做。

下面列出了可用于管理读取器/编写器自旋锁（从 Windows Vista SP1 开始）的例程列表。

| 例程名称                                                                                | 描述                                                                                                           |
|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**ExAcquireSpinLockExclusive**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451007(v=vs.85))                         | 获取用于调用方进行独占访问的自旋锁，并引发 IRQL 以调度\_级别。                      |
| [**ExAcquireSpinLockExclusiveAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451009(v=vs.85))    | 获取一个自旋锁，该锁用于通过已在 IRQL &gt;= 调度\_级别上运行的调用方进行独占访问。          |
| [**ExAcquireSpinLockShared**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451053(v=vs.85))                               | 获取调用方对共享访问的自旋锁，并引发 IRQL 以调度\_级别。                         |
| [**ExAcquireSpinLockSharedAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451055(v=vs.85))           | 获取调用方的用于共享访问的自旋锁，该调用方已运行的调用方 &gt;= 调度\_级别。             |
| [**ExReleaseSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451061)                        | 释放调用方为独占访问而获取的旋转锁，并还原原始 IRQL。                   |
| [**ExReleaseSpinLockExclusiveFromDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451058(v=vs.85)) | 释放调用方为独占访问而获取的旋转锁，并且不会降低 IRQL。                      |
| [**ExReleaseSpinLockShared**](https://msdn.microsoft.com/library/windows/hardware/hh451067)                              | 释放调用方为共享访问获取的旋转锁，并还原原始 IRQL。                      |
| [**ExReleaseSpinLockSharedFromDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451064(v=vs.85))      | 释放调用方为共享访问获取的旋转锁，并且不会降低 IRQL。                         |
| [**ExTryConvertSharedSpinLockExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-extryconvertsharedspinlockexclusive)      | 尝试将调用方已持有的自旋锁的访问状态转换为独占访问的共享访问。 |

 

读取器/写入器自旋锁例程全部采用，作为第一个参数，指向旋转锁的指针，这是一个**EX\_自旋\_锁**结构。 此结构对于驱动程序是不透明的。 驱动程序应为从未分页的系统内存分配旋转锁定的存储，并将锁定初始化为零。

 

 




