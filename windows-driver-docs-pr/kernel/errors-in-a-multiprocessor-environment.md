---
title: 在多处理器环境中的错误
description: 在多处理器环境中的错误
ms.assetid: 8a76b8d6-14d8-4709-8b15-e8b6b5094a1b
keywords:
- 可靠性 WDK 内核，争用条件
- 争用条件 WDK 内核
- 可靠性 WDK 内核，多处理器环境错误
- 多处理器环境错误 WDK 内核
- 锁定 WDK 内核
- 处理 WDK 内核的多个 I/O 请求
- I/O 请求 WDK 内核
- 线程冲突 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4b7866b7ef29c9e79336c2b228a25296a850ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523059"
---
# <a name="errors-in-a-multiprocessor-environment"></a>在多处理器环境中的错误





在基于 NT 的操作系统上驱动程序是多线程;它们可以在同一时间接收来自不同线程的多个 I/O 请求。 在设计时驱动程序，您必须假定它将是 SMP 系统上运行并采取适当的措施来确保数据完整性。

具体而言，每当一个驱动程序更改全局或对象的文件数据，它必须使用互锁的序列或锁以避免出现争用情况。

### <a name="encountering-a-race-condition-when-referencing-global-or-file-object-specific-data"></a>遇到争用条件时引用全局或文件特定于对象的数据

在下面的代码段中，驱动程序访问的全局数据时可能发生的争用条件**Data.LpcInfo**:

```cpp
   PLPC_INFO pLpcInfo = &Data.LpcInfo; //Pointer to global data
   ...
   ...
   // This saved pointer may be overwritten by another thread.
   pLpcInfo->LpcPortName.Buffer = ExAllocatePool(
                                     PagedPool,
                                     arg->PortName.Length);
```

输入此代码 IOCTL 调用后的多个线程可能会导致内存泄漏，如指针将被覆盖。 若要避免此问题，该驱动程序应使用**ExInterlocked * Xxx*** 例程或某种类型的锁的全局数据发生更改时。 驱动程序的要求确定锁的可接受的类型。 有关详细信息，请参阅[旋转锁](spin-locks.md)，[内核调度程序对象](kernel-dispatcher-objects.md)，并[ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)。

以下示例尝试重新分配特定于文件的缓冲区 (**终结点-&gt;LocalAddress**) 来保存终结点地址：

```cpp
   Endpoint = FileObject->FsContext;

    if ( Endpoint->LocalAddress != NULL &&
         Endpoint->LocalAddressLength <
                   ListenEndpoint->LocalAddressLength ) {

      FREE_POOL (Endpoint->LocalAddress,
                 LOCAL_ADDRESS_POOL_TAG
                 );
      Endpoint->LocalAddress  = NULL;
   }

    if ( Endpoint->LocalAddress == NULL ) {
       Endpoint->LocalAddress =
            ALLOCATE_POOL (NonPagedPool,
                           ListenEndpoint->LocalAddressLength,
                           LOCAL_ADDRESS_POOL_TAG);
   }
```

在此示例中，争用条件可能访问到导致文件对象。 该驱动程序不占用任何锁，因为相同的文件对象的两个请求可以输入此函数。 结果可能是对已释放内存，多次尝试释放的相同内存的引用或内存泄漏。 若要避免这些错误，这两个**如果**语句应括在旋转锁。








