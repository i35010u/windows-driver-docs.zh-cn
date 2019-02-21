---
title: 若要重命名一个分配的请求
description: 若要重命名一个分配的请求
ms.assetid: f22e19ba-9ff3-4aa1-a3f0-103f67ea7c60
keywords:
- 命令缓冲区 WDK 显示分配重命名
- DMA 缓冲区 WDK 显示分配重命名
- 重命名 WDK 显示的分配
- 重命名 WDK 显示的分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c04a5b8d554b360919776b269c4a75a89a020173
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533015"
---
# <a name="requesting-to-rename-an-allocation"></a>若要重命名一个分配的请求


用户模式显示驱动程序应请求视频内存管理器重命名应用程序指示放弃图面的内容作为请求以锁定的图面 （例如，顶点缓冲区） 的一部分时图面与相关联的分配。 Microsoft Direct3D 运行时将传递**放弃**位域标志以指示它不再需要当前图面的内容。 该驱动程序可以请求的视频内存管理器分配新的分配，以处理锁定请求，如果保存图面的内容的当前分配处于繁忙状态，而不是当前分配之前停止应用程序线程进入空闲状态。

用户模式显示驱动程序请求的视频内存管理器时重命名分配驱动程序设置**放弃**的成员[ **D3DDDICB\_LOCKFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544214)对的调用中的结构[ **pfnLockCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568914)函数。 视频内存管理器确定它应重命名分配还是应导致应用程序分配处于空闲状态之前停止正在基于分配是否当前正忙和上的当前内存状态。 要重命名每个分配时，视频内存管理器维护一系列连续用于锁定分配的分配。 视频内存管理器进行应用程序将放弃的分配内容每次循环列表。 该列表的长度根据应用程序要求和内存不足的情况。 视频内存管理器尝试保留列表足够长，以避免阻塞锁请求上的应用程序线程。 但是，内存压力下的视频内存管理器可以修整的列表，以避免导致额外的内存压力。

若要对施加了限制为分配的重命名列表的长度，驱动程序设置**MaximumRenamingListLength**的成员[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)结构，当创建分配。 如果驱动程序设置**MaximumRenamingListLength**为非零值，然后视频内存管理器确定适当的重命名列表的长度不超过限制规定，驱动程序。 如果驱动程序设置**MaximumRenamingListLength**为 0，则内存管理器可以提高重命名列表到适当的大小是需要为提高性能的大小。

请注意，当用户模式显示驱动程序设置**放弃**的成员[ **D3DDDICB\_LOCKFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff544214)，视频内存管理器不会调用显示若要为原始分配分配额外的分配的微型端口驱动程序。 视频内存管理器创建所有额外的分配使用原始分配的创建参数。 从显示微型端口驱动程序的角度来看，相同的分配是收到呼叫，结果中可能使用多个同时进行的段位置。

 

 





