---
title: 保留应用程序的处理器
description: 保留应用程序的处理器
keywords:
- CPU 配置 WDK RSS
- 保留应用程序的处理器 WDK RSS
- 处理器 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3277bd8b2bb6c790a56964fd310f756459ffd1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831247"
---
# <a name="reserving-processors-for-applications"></a>保留应用程序的处理器





接收方缩放 (RSS) 接口允许管理员为应用程序保留一组处理器以供使用。 管理员可以保留一组处理器，从逻辑 CPU 编号0开始，到指定 CPU 号结束。 RSS *基本 cpu 号* 是 rss 可使用的第一个 CPU 的 cpu 号。 RSS 不能使用数字低于基本 CPU 号的 Cpu。 例如，在启用超线程的四核系统上，如果 "基本 CPU 数量" 设置为1，则可以将处理器1、2和3用于 RSS。

对于基本 CPU 号，NDIS 使用默认值0，但管理员可以更改此值。 RSS 接口不允许管理员为要使用的应用程序保留一个不连续的任意 Cpu 子集。

在带有可伸缩网络包的 Microsoft Windows Server 2003 中，管理员可以在 **HKEY \_ 本地 \_ 计算机 \\ \\ 系统 \\ CurrentControlSet \\ Services \\ Tcpip \\ 参数** 中用 **RssBaseCpu** 注册表关键字设置基本 CPU 号。 **RssBaseCpu** 值是一个 DWORD 类型，如果不存在，NDIS 将使用默认值0。

在 Windows Server 2008 中，管理员可以在 **HKEY \_ 本地 \_ 计算机 \\ \\ 系统 \\ CurrentControlSet \\ Services \\ NDIS \\ 参数** 中用 **RssBaseCpu** 注册表关键字设置基本 CPU 号。 **RssBaseCpu** 值是一个 DWORD 类型，如果不存在，NDIS 将使用默认值0。 此注册表关键字还适用于 Windows Server 的更高版本。

**注意** 从 Windows 8 和 Windows Server 2012 开始，管理员可以使用 PowerShell cmdlet 控制网络适配器的许多方面。 现在不鼓励直接编辑注册表。

用于保留 RSS Cpu 的 PowerShell cmdlet 是 [get-netadapterrss](/powershell/module/netadapter/Set-NetAdapterRss)。 使用 **get-netadapterrss** 和 using **RssBaseCpu** 之间的主要区别是，PowerShell Cmdlet 在每个网络适配器基础上运行，而 **RssBaseCpu** 是全局性的，这意味着它适用于所有网络适配器。 通常，建议单独使用每个网络适配器，因为它在为每个网络适配器提供自己的配置时提供更大的灵活性、粒度和可理解性。 但是，如果他们想要同时对所有当前和未来的网络适配器应用配置，则管理员可能仍然使用 global **RssBaseCpu** 密钥。

有关网络适配器 cmdlet 的完整列表，请参阅 [Windows PowerShell 中的网络适配器 cmdlet](/powershell/module/netadapter/)。

 

