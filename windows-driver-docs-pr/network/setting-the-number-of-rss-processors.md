---
title: 设置 RSS 处理器数目
description: 设置 RSS 处理器数目
ms.assetid: c13db4a1-e345-4368-9bcd-afbd2fd8db7a
keywords:
- 处理器 WDK RSS
- CPU 配置 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5294ecead308a18e263383a484dba9f901f389de
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214424"
---
# <a name="setting-the-number-of-rss-processors"></a>设置 RSS 处理器数目





管理员应将接收方缩放 (RSS) 处理器数设置为有助于计算机的整体性能。 并行延迟的过程调用在多个 Cpu 上运行 (Dpc) 启用分布式接收处理并消除 CPU 瓶颈 (例如，在高速 Nic) 中。 但是，多个 Dpc 确实会产生额外的开销。 随着 RSS 的使用更多处理器，中断和 DPC 处理开销会增加。 因此，当 RSS 处于活动状态时，所有 Cpu 的总 CPU 使用率会增加。 管理员应选择用于 RSS 的 Cpu 数量，以避免出现以下情况：使用 RSS 会使应用程序使用的处理能力更少，并且不会提高网络吞吐量。

在带有可伸缩网络包的 Microsoft Windows Server 2003 中，管理员可以在**HKEY \_ 本地 \_ 计算机 \\ \\ 系统 \\ CurrentControlSet \\ Services \\ Tcpip \\ 参数**中设置包含**MaxNumRssCpus**注册表关键字的 RSS cpu 的最大数目。 **MaxNumRssCpus**值是一个 DWORD 类型，如果不存在，NDIS 将使用默认值4。

在 Windows Server 2008 中，管理员可在**HKEY \_ 本地 \_ 计算机 \\ \\ 系统 \\ CurrentControlSet \\ SERVICES \\ Ndis \\ 参数**中设置最大 RSS cpu 数量，其中包含**MaxNumRssCpus**注册表关键字。 **MaxNumRssCpus**值是一个 DWORD 类型，如果不存在，NDIS 将使用默认值4。 此注册表关键字还适用于 Windows Server 的更高版本。

若要避免复杂情况 (和未在实际硬件中实现的非现实情况) （其中可用硬件接收队列数量小于 RSS Cpu 数量），管理员不得将 **MaxNumRssCpus** 值设置为大于16的值。

用于 RSS 的 Cpu 的实际数量也受在配置 RSS 基本 CPU 号后保留的核心处理器总数限制。 例如，如果管理员将四核计算机系统上的最大 RSS Cpu 数设置为6，则网络驱动程序堆栈最多使用用于 RSS 的4个 Cpu。 如果管理员还将 RSS 基本 CPU 数设置为1，则网络驱动程序堆栈最多使用3个 cpu (CPU 号1、2和 3) 。

 计算机用于 RSS 的 Cpu 数量是静态的，并且在运行时不会更改。 因此，对 **MaxNumRssCpus** 注册表值所做的任何更改都需要重新启动才能生效。

**注意** 从 Windows 8 和 Windows Server 2012 开始，管理员可以使用 PowerShell cmdlet 控制网络适配器的许多方面。 现在不鼓励直接编辑注册表。 

用于设置 RSS Cpu 数量的 PowerShell cmdlet 是 [get-netadapterrss](/powershell/module/netadapter/Set-NetAdapterRss)。 使用 **get-netadapterrss** 和 using **MaxNumRssCpus** 之间的主要区别是，PowerShell Cmdlet 在每个网络适配器基础上运行，而 **MaxNumRssCpus** 是全局性的，这意味着它适用于所有网络适配器。 通常，建议单独使用每个网络适配器，因为它在为每个网络适配器提供自己的配置时提供更大的灵活性、粒度和可理解性。 但是，如果他们想要同时对所有当前和未来的网络适配器应用配置，则管理员可能仍然使用 global **MaxNumRssCpus** 密钥。

有关网络适配器 cmdlet 的完整列表，请参阅 [Windows PowerShell 中的网络适配器 cmdlet](/powershell/module/netadapter/)。