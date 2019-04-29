---
title: KS 分配器
description: KS 分配器
ms.assetid: 07812703-a66f-450a-b28e-4cf765267c4a
keywords:
- 流式处理 WDK，分配器的内核
- KS WDK，分配器
- 流式处理的分配器 WDK 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa0de06382e2095502390e76e7eff11bb2e5dae4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380645"
---
# <a name="ks-allocators"></a>KS 分配器





*Allocator*称为实例化数据缓冲区的 KS 对象*帧*的 I/O 请求。 框架是连续的内存，它的大小是通过供应商指定的区块**AllocatorFraming**的成员[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534).

微型驱动程序可以支持分配器的多个缓冲区类型，例如板载 RAM 中的视频卡。 但是，大多数微型驱动程序使用*默认分配器*来分配系统内存。 帧大小、 最大数量的帧和对齐要求，可以指定微型驱动程序。 默认分配器负责满足要求，并可能通过重复使用已丢弃的帧来优化性能。

微型驱动程序通过调用创建一个分配器[ **KsCreateAllocator** ](https://msdn.microsoft.com/library/windows/hardware/ff561633)例程或相关的函数。 在此调用，微型驱动程序将传递一个指向[ **KSALLOCATOR\_组帧**](https://msdn.microsoft.com/library/windows/hardware/ff560979)结构。 此结构包含描述所请求的分配器参数。

在流类模型中，创建的分配器的微型驱动程序支持[ **KSPROPERTY\_连接\_ALLOCATORFRAMING** ](https://msdn.microsoft.com/library/windows/hardware/ff565099)属性。 这是只读的请求返回一个指向相关[ **KSALLOCATOR\_组帧**](https://msdn.microsoft.com/library/windows/hardware/ff560979)为指定的接收器句柄的结构。

提供的分配器的微型驱动程序还应支持[ **KSPROPERTY\_流\_分配器**](https://msdn.microsoft.com/library/windows/hardware/ff565684)属性。 此属性提供对当前已分配给流连接点的分配器的句柄的读/写访问。

AVStream 下运行的微型驱动程序可能包括实现其自己的分配器的 pin。 执行此操作通过设置[ **KSALLOCATOR\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff560976)隶属[ **KSPIN\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff563535)结构. 指定**NULL**为此成员，如果不想指定此 pin 的分配器。

此外，使用 AVStream 微型驱动程序[ **KSALLOCATOR\_组帧\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff560982)结构，以指定分配器要求。 然后使用客户端[ **KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff565101)属性来检索组帧 pin 的要求。 请参阅[AVStream 分配器](avstream-allocators.md)有关详细信息。

本部分包含以下附加信息：

[默认分配器](default-allocators.md)

[筛选器特定分配器](filter-specific-allocators.md)

[分配方案](allocation-schemes.md)

 

 




