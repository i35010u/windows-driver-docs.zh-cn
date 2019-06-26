---
title: 保留应用程序的处理器
description: 保留应用程序的处理器
ms.assetid: e09790e9-29a7-4ff6-a122-b4bd99de8bc7
keywords:
- CPU 配置 WDK RSS
- 保留应用程序 WDK RSS 的处理器
- 处理器 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23fb0637dc6663d4e88821c2932d80f880550fc7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378653"
---
# <a name="reserving-processors-for-applications"></a>保留应用程序的处理器





接收方缩放 (RSS) 界面使管理员能够保留一组应用程序使用的处理器。 管理员可以保留一组逻辑 CPU 编号 0 开始和结束时间指定的 CPU 数目的处理器。 RSS*基于 CPU 数量*是可以使用 RSS 的第一个 CPU 的 CPU 数。 RSS 不能使用 Cpu 的如下 CPU 底数编号。 例如，在具有超线程，关闭状态的四核系统上为基的 CPU 数设置为 1，如果可以处理器 1、 2 和 3 用于 RSS。

NDIS 基 CPU 号码，使用默认值为 0，但管理员可以更改此值。 RSS 接口不允许管理员保留非连续的任意的应用程序使用的 Cpu 子集。

在 Microsoft Windows Server 2003 的可伸缩网络包，管理员可以设置基 CPU 带有**RssBaseCpu**中的注册表关键字**HKEY\_本地\_机\\\\系统\\CurrentControlSet\\Services\\Tcpip\\参数**。 **RssBaseCpu**值是 DWORD 类型，并且如果不存在，NDIS 将使用默认值为 0。

在 Windows Server 2008 中，管理员可以设置基 CPU 带有**RssBaseCpu**中的注册表关键字**HKEY\_本地\_机\\\\系统\\CurrentControlSet\\Services\\NDIS\\参数**。 **RssBaseCpu**值是 DWORD 类型，并且如果不存在，NDIS 将使用默认值为 0。 此注册表关键字也适用于更高版本的 Windows Server。

**请注意**从 Windows 8 和 Windows Server 2012 中，管理员可以控制许多方面的网络适配器使用 PowerShell cmdlet。 现在不建议直接编辑注册表。

PowerShell cmdlet 为保留 RSS Cpu [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss)。 使用的主要区别**Set-netadapterrss**并使用**RssBaseCpu**是针对每个网络适配器时运行 PowerShell cmdlet **RssBaseCpu**是全局的这意味着它将应用于所有网络适配器。 通常情况下，单独使用每个网络适配器的建议，因为它提供了更多的灵活性、 粒度和为每个网络适配器提供其自己的配置中的可理解性。 但是，管理员可能仍使用全局**RssBaseCpu**密钥如果他们想要在同一时间将配置应用于所有当前及未来的所有网络适配器。

网络适配器 cmdlet 的完整列表，请参阅[Windows PowerShell 中的网络适配器 Cmdlet](https://docs.microsoft.com/powershell/module/netadapter/)。

 

 





