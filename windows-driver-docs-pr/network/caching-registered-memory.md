---
title: 缓存已注册的内存
description: 缓存已注册的内存
ms.assetid: e1040f6a-6e65-462a-a79a-5d05d36787b0
keywords:
- SAN 连接安装 WDK，缓存已注册的内存
- RDMA 缓冲区缓存 WDK San
- 缓存 RDMA 缓冲区 WDK San
- 已注册的内存 WDK San
- 本地访问注册内存缓存，WDK San
- 远程访问注册内存缓存，WDK San
- 内存 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f15e5ffdbc9593ae680d504b751d8887d63475c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386354"
---
# <a name="caching-registered-memory"></a>缓存已注册的内存





SAN 服务提供商可以缓存以提高性能的本地或远程访问公开的 RDMA 缓冲区。

### <a name="caching-rdma-buffers-exposed-for-local-access"></a>缓存以进行本地访问公开的 RDMA 缓冲区

Windows 套接字开关调用 SAN 服务提供商[ **WSPRegisterMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566311(v=vs.85))代表应用程序注册充当本地接收 RDMA 的所有数据缓冲区的扩展函数对的调用中的缓冲区[ **WSPRdmaRead** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))扩展函数或调用中的本地 RDMA 源[ **WSPRdmaWrite** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))扩展函数。 作为此注册过程的一部分，SAN 服务提供商必须锁定的物理内存区域这些缓冲区并注册到 SAN nic。 这些操作都需要消耗大量资源。 因此，SAN 服务提供程序应使用缓存来降低这些注册的开销。 如果 SAN 服务提供程序使用缓存，提高了重复的缓冲区使用的数据传输的应用程序的性能。

SAN 服务提供商应缓存并发布以下列表中所述为本地访问公开的 RDMA 缓冲区：

1.  当此开关调用[ **WSPDeregisterMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566279(v=vs.85))扩展函数来释放缓冲区，SAN 服务提供商应原样保留缓冲区 SAN NIC 中注册并且锁定的区域物理内存。 SAN 服务提供商还应到已注册的缓冲区缓存添加缓冲区，以防在后续的 RDMA 操作和安全拥有缓冲区的下一步的列表项中所述再次使用该缓冲区。

2.  SAN 服务提供商将缓存内存注册基于虚拟地址。 SAN 服务提供商的代理驱动程序时的 SAN 服务提供程序缓存缓冲区的注册，必须调用[ **MmSecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmsecurevirtualmemory)函数来保护拥有该注册缓冲区操作操作系统通知开关，如果释放缓冲区 (例如，如果应用程序调用**VirtualFree**函数，以释放回操作系统是虚拟的地址范围)。

3.  当此开关随后调用**WSPRegisterMemory**若要注册一个缓冲区，SAN 服务提供程序应检查其缓存，以确定是否已注册的缓冲区。 如果 SAN 服务提供商在其缓存中找到缓冲区，SAN 服务提供程序不应执行任何进一步的注册操作。

4.  开关随后更改已注册的缓冲区的虚拟物理映射之前，调用每个 SAN 服务提供商[ **WSPMemoryRegistrationCacheCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))扩展函数。 每个 SAN 服务提供商的代理驱动程序，反过来，必须调用[ **MmUnsecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmunsecurevirtualmemory)函数，以释放缓冲区的所有权。 此外，每个 SAN 服务提供商必须从其缓存删除缓冲区，必须从 SAN NIC 中删除缓冲区注册

5.  关闭本地 SAN 套接字与远程对等方之间的连接之前，SAN 服务提供商应释放任何缓存的缓冲区。

**请注意**  代理驱动程序必须使用**尝试 / except**机制的访问受保护的用户模式缓冲区通过调用代码周围**MmSecureVirtualMemory**到防止操作系统崩溃。 有关代理驱动程序如何保护和释放缓冲区的详细信息，请参阅[保护和虚拟地址的释放所有权](securing-and-releasing-ownership-of-virtual-addresses.md)。 有关详细信息**试用 / 除外**，请参阅视觉对象C++文档。 璝惠**VirtualFree**，请参阅 Microsoft Windows SDK 文档。

 

### <a name="caching-rdma-buffers-exposed-for-remote-access"></a>缓存用于远程访问公开的 RDMA 缓冲区

Windows 套接字开关调用 SAN 服务提供商[ **WSPRegisterRdmaMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566313(v=vs.85))扩展函数来注册充当远程远程RDMA目标的所有数据缓冲区**WSPRdmaWrite**调用或远程的远程 RDMA 源**WSPRdmaRead**调用。 也就是说，该交换机公开远程对等方访问这些缓冲区。 开关从这些缓冲区的数据传输完成后，调用 SAN 服务提供商[ **WSPDeregisterRdmaMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566281(v=vs.85))扩展函数来释放这些缓冲区，使它们不再可从远程对等方访问。

SAN 服务提供商应缓存在以下列表中所述为远程访问公开的 RDMA 缓冲区：

1.  当此开关调用**WSPDeregisterRdmaMemory**来释放缓冲区，SAN 服务提供商应保留在物理内存中锁定，并使用 SAN NIC 注册的缓冲区 SAN 服务提供商还应到已注册的缓冲区缓存添加缓冲区，以防在后续的 RDMA 操作中再次使用该缓冲区。 但是，SAN 服务提供程序应采取适当措施以确保远程对等方不再可以访问缓冲区。
    **请注意**  如果缓冲区仅可访问 SAN 服务提供商从 SAN NIC 中删除缓冲区注册，SAN 服务提供商必须这样做。 但是，SAN 服务提供商应保留的物理内存的区域锁定的缓冲区。 这种情况下并不提供尽可能最佳的性能，但不缓存更好。

     

2.  若要缓存用于远程访问公开的 RDMA 缓冲区，SAN 服务提供商和其代理驱动程序应使用的缓存技术，用于为本地访问公开的 RDMA 缓冲区前面的列表中所述。

3.  当此开关随后调用**WSPRegisterRdmaMemory**若要注册一个缓冲区，SAN 服务提供程序应检查其缓存，以确定是否已注册的缓冲区。 如果 SAN 服务提供商在其缓存中找到缓冲区，SAN 服务提供程序应只公开的远程访问的缓冲区，不需要任何进一步的注册操作。 但是，如果缓冲区注册以前已删除从 SAN NIC，SAN 服务提供商应重新注册缓冲区。

4.  若要释放用于远程访问公开的 RDMA 缓冲区，SAN 服务提供商和其代理驱动程序应使用技术，如上面的列表中所述。

 

 





