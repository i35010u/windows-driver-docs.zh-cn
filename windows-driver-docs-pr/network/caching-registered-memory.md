---
title: 缓存已注册的内存
description: 缓存已注册的内存
ms.assetid: e1040f6a-6e65-462a-a79a-5d05d36787b0
keywords:
- SAN 连接设置 WDK，缓存已注册内存
- RDMA 缓冲区缓存 WDK San
- 缓存 RDMA 缓冲 WDK San
- 已注册内存 WDK San
- 本地访问注册的内存缓存 WDK San
- 远程访问注册的内存缓存 WDK San
- 内存 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c225e40ae2176d0530563767ecd7816fce7a3d00
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835270"
---
# <a name="caching-registered-memory"></a>缓存已注册的内存





SAN 服务提供程序可以缓存为本地或远程访问而公开的 RDMA 缓冲区以提高性能。

### <a name="caching-rdma-buffers-exposed-for-local-access"></a>缓存为本地访问公开的 RDMA 缓冲区

Windows 套接字开关代表应用程序调用 SAN 服务提供程序的[**WSPRegisterMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566311(v=vs.85)) extension 函数，以便在调用[**WSPRdmaWrite**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))扩展函数时，将充当本地接收 rdma 缓冲区的所有数据缓冲区注册到[**WSPRDMAREAD**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))扩展函数或本地 RDMA 源。 作为此注册过程的一部分，SAN 服务提供程序必须将这些缓冲区锁定到物理内存区域，并将其注册到 SAN NIC。 这两个操作都消耗大量资源。 因此，SAN 服务提供商应使用缓存来减少这些注册的开销。 如果 SAN 服务提供商使用缓存，则为数据传输重复使用缓冲区的应用程序的性能将提高。

SAN 服务提供商应缓存并释放为本地访问公开的 RDMA 缓冲区，如以下列表中所述：

1.  当开关调用[**WSPDeregisterMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566279(v=vs.85))扩展函数以释放缓冲区时，san 服务提供程序应将已向 san NIC 注册的缓冲区，并将其锁定到物理内存区域。 SAN 服务提供程序还应将缓冲区添加到已注册的缓冲区的缓存，以防在后续 RDMA 操作中再次使用该缓冲区，并按下一个列表项中所述的方式保护缓冲区。

2.  SAN 服务提供程序基于虚拟地址缓存内存注册。 当 SAN 服务提供程序缓存缓冲区的注册时，SAN 服务提供程序的代理驱动程序必须调用[**MmSecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)函数来保护已注册的缓冲区的所有权，使操作系统在缓冲区发布时通知开关（例如，如果应用程序调用**VirtualFree**函数将虚拟地址范围释放回操作系统）。

3.  当交换机随后调用**WSPRegisterMemory**来注册缓冲区时，SAN 服务提供程序应检查其缓存，以确定是否已注册了缓冲区。 如果 SAN 服务提供程序在其缓存中查找缓冲区，则 SAN 服务提供程序不应执行任何进一步的注册操作。

4.  在已注册的缓冲区的虚拟到物理映射随后更改之前，开关会调用每个 SAN 服务提供程序的[**WSPMemoryRegistrationCacheCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))扩展函数。 每个 SAN 服务提供商的代理驱动程序反过来，都必须调用[**MmUnsecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmunsecurevirtualmemory)函数来释放缓冲区的所有权。 此外，每个 SAN 服务提供程序必须从缓存中删除该缓冲区，并且必须从 SAN NIC 中删除该缓冲区注册。

5.  在本地 SAN 套接字与远程对等端之间的连接关闭之前，SAN 服务提供商应释放所有缓存的缓冲区。

**请注意**  代理驱动程序必须在代码上使用**try/except**机制，以访问通过对**MmSecureVirtualMemory**的调用来保护的用户模式缓冲区，以防操作系统崩溃。 有关代理驱动程序如何保护和释放缓冲区的详细信息，请参阅[保护和释放虚拟地址的所有权](securing-and-releasing-ownership-of-virtual-addresses.md)。 有关**try/except**的详细信息，请参阅 Visual C++文档。 有关**VirtualFree**的信息，请参阅 Microsoft Windows SDK 文档。

 

### <a name="caching-rdma-buffers-exposed-for-remote-access"></a>缓存公开用于远程访问的 RDMA 缓冲区

Windows 套接交换机调用 SAN 服务提供程序的[**WSPRegisterRdmaMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566313(v=vs.85))扩展函数来注册所有数据缓冲区，这些数据缓冲区充当远程**WSPRdmaWrite**调用的远程 Rdma 目标或远程**WSPRdmaRead**调用的远程 rdma 源。 也就是说，该开关公开了这些缓冲区以便远程对等方进行访问。 在这些缓冲区中的数据传输完成后，开关会调用 SAN 服务提供程序的[**WSPDeregisterRdmaMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566281(v=vs.85))扩展函数来释放这些缓冲区，以便不再从远程对等节点访问它们。

SAN 服务提供商应缓存为远程访问公开的 RDMA 缓冲区，如以下列表中所述：

1.  当开关调用**WSPDeregisterRdmaMemory**来释放缓冲区时，san 服务提供程序应将缓冲区锁定在物理内存中并向 san NIC 注册。 SAN 服务提供程序还应将缓冲区添加到已注册的缓冲区的缓存，以防在后续的 RDMA 操作中再次使用该缓冲区。 但是，SAN 服务提供商应采取相应的措施来确保远程对等方不能再访问该缓冲区。
    **请注意**  如果该缓冲区只能由 san 服务提供程序从 san NIC 删除缓冲区注册，则 san 服务提供程序必须这样做。 但是，SAN 服务提供商应将缓冲区锁定为物理内存区域。 此方案不能提供最佳性能，但最好是不提供缓存。

     

2.  为了缓存公开用于远程访问的 RDMA 缓冲区，SAN 服务提供程序及其代理驱动程序应使用为本地访问公开的 RDMA 缓冲区的前面列表中所述的缓存技术。

3.  当交换机随后调用**WSPRegisterRdmaMemory**来注册缓冲区时，SAN 服务提供程序应检查其缓存，以确定是否已注册了缓冲区。 如果 SAN 服务提供程序在其缓存中找到了缓冲区，则 SAN 服务提供程序只应公开用于远程访问的缓冲区，无需进一步注册操作。 但是，如果之前已从 SAN NIC 中删除了缓冲区注册，则 SAN 服务提供程序应再次注册该缓冲区。

4.  为了释放公开用于远程访问的 RDMA 缓冲区，SAN 服务提供程序及其代理驱动程序应使用上述列表中所述的方法。

 

 





