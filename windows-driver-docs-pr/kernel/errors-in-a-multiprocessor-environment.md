---
title: 多处理器环境出错
description: 多处理器环境出错
ms.assetid: 8a76b8d6-14d8-4709-8b15-e8b6b5094a1b
keywords:
- 可靠性 WDK 内核，争用条件
- 争用条件 WDK 内核
- 可靠性 WDK 内核，多处理器环境错误
- 多处理器环境错误，WDK 内核
- 锁定 WDK 内核
- 多个 i/o 请求处理 WDK 内核
- I/o 请求 WDK 内核
- 线程冲突 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a12469e12d5777864920a04d481b5f391ed76bf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192695"
---
# <a name="errors-in-a-multiprocessor-environment"></a>多处理器环境出错





在基于 NT 的操作系统上，驱动程序是多线程的;它们可以同时从不同的线程接收多个 i/o 请求。 设计驱动程序时，必须假定它将在 SMP 系统上运行，并采取相应的措施来确保数据完整性。

具体而言，每当驱动程序更改全局或文件对象数据时，都必须使用锁或互锁序列来防止争用条件。

### <a name="encountering-a-race-condition-when-referencing-global-or-file-object-specific-data"></a>引用全局或特定于对象的对象数据时遇到争用条件

在以下代码片段中，当驱动程序访问 **LpcInfo**中的全局数据时，可能会出现争用条件：

```cpp
   PLPC_INFO pLpcInfo = &Data.LpcInfo; //Pointer to global data
   ...
   ...
   // This saved pointer may be overwritten by another thread.
   pLpcInfo->LpcPortName.Buffer = ExAllocatePool(
                                     PagedPool,
                                     arg->PortName.Length);
```

由于 IOCTL 调用，多个线程输入此代码可能会导致内存泄漏，因为指针被覆盖。 若要避免此问题，驱动程序应使用 **ExInterlocked * Xxx*** 例程，或在更改全局数据时使用某种类型的锁。 驱动程序的要求确定可接受的锁类型。 有关详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md)、 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md)和 [**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))。

下面的示例尝试重新分配特定于文件的缓冲区 (** &gt; LocalAddress**) 以保存终结点地址：

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

在此示例中，可以通过访问文件对象出现争用情况。 由于驱动程序未持有任何锁，因此对同一文件对象的两个请求可以输入此函数。 结果可能是对已释放内存的引用、多次尝试释放相同的内存或内存泄漏。 若要避免这些错误，应将两个 **if** 语句包含在一个旋转锁中。