---
title: 设置 RSS 处理器数目
description: 设置 RSS 处理器数目
ms.assetid: c13db4a1-e345-4368-9bcd-afbd2fd8db7a
keywords:
- 处理器 WDK RSS
- CPU 配置 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7840da0e5762459d68484df363d0821ea3013f8a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368913"
---
# <a name="setting-the-number-of-rss-processors"></a>设置 RSS 处理器数目





管理员应将数设置接收方缩放 (RSS) 处理器，帮助计算机的总体性能。 并发延缓的过程调用 (Dpc) 上分布的多个 Cpu 启用运行的接收处理，并删除 （例如，在高速 Nic) 的 CPU 瓶颈。 但是，多个 Dpc 创建其他开销。 中断和 DPC 处理开销将增大，因为多个处理器用于 RSS。 因此，当 RSS 处于活动状态，所有 cpu 的总 CPU 使用率增加。 管理员应选择使用的 RSS 中以避免使用 RSS 离开应用程序以使用更少处理能力且不能提高网络吞吐量的 Cpu 数。

在 Microsoft Windows Server 2003 的可伸缩网络包，管理员可以设置与 RSS Cpu 的最大数目**MaxNumRssCpus**中的注册表关键字**HKEY\_本地\_机器\\\\系统\\CurrentControlSet\\Services\\Tcpip\\参数**。 **MaxNumRssCpus**值是 DWORD 类型，并 NDIS 不存在，如果使用的默认值为 4。

在 Windows Server 2008 中，管理员可以设置与 RSS Cpu 的最大数目**MaxNumRssCpus**中的注册表关键字**HKEY\_本地\_机\\\\系统\\CurrentControlSet\\Services\\Ndis\\参数**。 **MaxNumRssCpus**值是 DWORD 类型，并 NDIS 不存在，如果使用的默认值为 4。 此注册表关键字也适用于更高版本的 Windows Server。

若要避免复杂的情况下 （和不现实中实际的硬件不实现的情况下） 队列接收可用的硬件的数小于 RSS Cpu 的数量，管理员必须未设置**MaxNumRssCpus**大于 16 的值的值。

用于 RSS Cpu 的实际数目也受到配置 RSS 基 CPU 数后保留的核心处理器的总数。 例如，如果管理员将 RSS Cpu 的最大数目设置为 6 的四核计算机系统上，网络驱动程序堆栈使用，最多 4 个 rss Cpu。 管理员还可以设置 RSS CPU 底数为 1，如果网络驱动程序堆栈使用最多 3 个 Cpu （CPU 号 1、 2 和 3）。

 在计算机使用 RSS 的 Cpu 数是静态的且不会更改在运行时。 因此，对任何更改**MaxNumRssCpus**注册表值需要重新启动才能生效。

**请注意**从 Windows 8 和 Windows Server 2012 中，管理员可以控制许多方面的网络适配器使用 PowerShell cmdlet。 现在不建议直接编辑注册表。 

用于设置 RSS Cpu 数的 PowerShell cmdlet 是[Set-netadapterrss](https://technet.microsoft.com/library/jj130863)。 使用的主要区别**Set-netadapterrss**并使用**MaxNumRssCpus**是针对每个网络适配器时运行 PowerShell cmdlet **MaxNumRssCpus**是全局的这意味着它将应用于所有网络适配器。 通常情况下，单独使用每个网络适配器的建议，因为它提供了更多的灵活性、 粒度和为每个网络适配器提供其自己的配置中的可理解性。 但是，管理员可能仍使用全局**MaxNumRssCpus**密钥如果他们想要在同一时间将配置应用于所有当前及未来的所有网络适配器。

网络适配器 cmdlet 的完整列表，请参阅[Windows PowerShell 中的网络适配器 Cmdlet](https://technet.microsoft.com/library/jj134956)。
