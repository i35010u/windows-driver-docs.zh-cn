---
title: 保护和释放虚拟地址所有权
description: 保护和释放虚拟地址所有权
ms.assetid: e7b31c8d-fed4-43e2-bcd2-295e3e17719e
keywords:
- 代理驱动程序 WDK San，虚拟地址
- SAN 代理驱动程序 WDK，虚拟地址
- WDK San 的虚拟地址
- 所有权 WDK 虚拟地址
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a3de75034093139cc01b1caa180c150ea2ef4fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382122"
---
# <a name="securing-and-releasing-ownership-of-virtual-addresses"></a>保护和释放虚拟地址所有权





每当代理驱动程序的 SAN 服务提供程序将缓存这些缓冲区时，代理驱动程序必须保护用户模式缓冲区的虚拟地址的所有权。 有关缓存缓冲区的详细信息，请参阅[缓存注册内存](caching-registered-memory.md)。 代理驱动程序保护的用户模式缓冲区所有权，如果应用程序缓冲区释放回操作系统，以便操作系统通知切换 Windows 套接字。 代理驱动程序必须调用到安全的缓冲区的所有权[ **MmSecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmsecurevirtualmemory)函数。 在此调用中，代理驱动程序将指针传递到的缓冲区和大小，以字节为单位的缓冲区的起始地址。

如果缓存缓冲区的虚拟物理映射计划更改，交换机会收到通知，并调用 SAN 服务提供商[ **WSPMemoryRegistrationCacheCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))函数从 SAN NIC 中删除缓冲区注册和 SAN 中的缓冲区服务提供程序的缓存。 SAN 服务提供商的代理驱动程序，反过来，必须调用[ **MmUnsecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmunsecurevirtualmemory)函数，以释放缓冲区的所有权。 在此调用中，代理驱动程序将句柄传递到之前从返回的缓冲区**MmSecureVirtualMemory**调用。

**请注意**  的驱动程序，尝试通过调用访问受保护的用户模式缓冲区**MmSecureVirtualMemory**可能可以关闭操作系统。 因此，当代理驱动程序访问此类用户模式缓冲区时，它还必须使用**试用 / 除外**访问缓冲区的代码周围的机制。 有关详细信息**试用 / 除外**，请参阅视觉对象C++文档。

 

SAN 服务提供商可以 I/O 控制 (IOCTL) 将请求发送到代理驱动程序来保护和释放缓冲区的所有权。 有关详细信息，请参阅[SAN 服务提供程序实现 Ioctl](implementing-ioctls-for-a-san-service-provider.md)。

 

 





