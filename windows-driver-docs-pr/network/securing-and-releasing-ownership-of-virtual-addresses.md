---
title: 保护和释放虚拟地址所有权
description: 保护和释放虚拟地址所有权
ms.assetid: e7b31c8d-fed4-43e2-bcd2-295e3e17719e
keywords:
- 代理驱动程序 WDK San，虚拟地址
- SAN 代理驱动程序 WDK、虚拟地址
- 虚拟地址 WDK San
- 所有权 WDK 虚拟地址
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bf44c3b266cb5f73045768d850d94aeaf5b4ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841995"
---
# <a name="securing-and-releasing-ownership-of-virtual-addresses"></a>保护和释放虚拟地址所有权





每当代理驱动程序的 SAN 服务提供程序缓存这些缓冲区时，代理驱动程序必须保护用户模式缓冲区的虚拟地址的所有权。 有关缓存缓冲区的详细信息，请参阅[缓存已注册内存](caching-registered-memory.md)。 代理驱动程序保护用户模式缓冲区的所有权，以便在应用程序将缓冲区释放回操作系统时，操作系统将通知 Windows 套接交换机。 若要确保缓冲区的所有权，代理驱动程序必须调用[**MmSecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)函数。 在此调用中，代理驱动程序将指针传递到缓冲区的起始地址和缓冲区的大小（以字节为单位）。

如果计划更改缓存的缓冲区的虚拟到物理映射，则会通知交换机，并调用 SAN 服务提供程序的[**WSPMemoryRegistrationCacheCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))函数，以删除来自 san NIC 的缓冲区注册和来自 SAN 服务提供商缓存的缓冲区。 SAN 服务提供程序的代理驱动程序又必须调用[**MmUnsecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmunsecurevirtualmemory)函数来释放缓冲区的所有权。 在此调用中，代理驱动程序将句柄传递给之前从**MmSecureVirtualMemory**调用返回的缓冲区。

**请注意**  一个驱动程序，该驱动程序尝试访问通过调用**MmSecureVirtualMemory**而受到保护的用户模式缓冲区可能会关闭操作系统。 因此，当代理驱动程序访问此类用户模式缓冲区时，它还必须在访问缓冲区的代码周围使用**try/except**机制。 有关**try/except**的详细信息，请参阅 Visual C++文档。

 

SAN 服务提供程序可以将 i/o 控制（IOCTL）请求发送到代理驱动程序，以保护和释放缓冲区的所有权。 有关详细信息，请参阅为[SAN 服务提供商实现 IOCTLs](implementing-ioctls-for-a-san-service-provider.md)。

 

 





