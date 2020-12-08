---
title: NDIS 6.20 后向兼容性
description: NDIS 6.20 后向兼容性
keywords:
- NDIS 6.20 WDK，向后兼容性
- 向后兼容性 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f45373bec84a6d004388391b1b536a17c70cf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798037"
---
# <a name="ndis-620-backward-compatibility"></a>NDIS 6.20 后向兼容性





NDIS 6.20 向向后兼容的功能添加了适用于 NDIS 6.0 驱动程序的功能。 有关 NDIS 6.0 兼容性问题的信息，请参阅 [ndis 6.0 向后兼容性](/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)。 除了 NDIS 6.0 提供的用于 NDIS 1.x 和更早驱动程序的翻译功能外，NDIS 6.20 还为电源管理接口提供翻译。 NDIS 6.20 驱动程序必须支持 NDIS 6.20 电源管理接口。

NDIS 6.20 支持为 NDIS 6.1 添加的功能的更新版本。 有关 NDIS 6.1 功能的更新的详细信息，请参阅 ndis [6.1 功能的 ndis 6.20 支持](ndis-6-20-updates-to-ndis-6-1-features.md)。

**注意**  NDIS 6.20 接口支持超过64个处理器。 在 x86 版本的操作系统) 中，以前的 NDIS 版本限制为不超过64处理器 (32。

 

若要保持与较旧的 NDIS 版本的向后兼容性，未更新为支持超过64处理器的驱动程序默认情况下为处理器组零。 有关处理器组的详细信息，请参阅处理器组的 Kernel-Mode 驱动程序体系结构设计文档。

一些 NDIS 6.1 和更早版本的函数已过时，不能与 NDIS 6.20 驱动程序一起使用。 请参阅特定函数的参考页的 "要求" 部分，以确定其 NDIS 版本兼容性。 有关过时接口的列表，请参阅 [NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

Windows 7 附带的 TCP/IP 协议驱动程序已更新为 NDIS 6.20。 TCP/IP 协议驱动程序与驱动程序堆栈中的 NDIS 6.1 和更早的驱动程序向后兼容。 但是，若要在 Windows 7 驱动程序堆栈上获得最佳性能，应将所有驱动程序更新为 NDIS 6.20。

Windows 7 之后，Microsoft Windows 版本中已弃用 NDIS 1.x 和更早版本的 NDIS 驱动程序。 不会对任何新的 NDIS 1.x 驱动程序进行 WHQL 认证。 所有新驱动程序都应为 NDIS 6.0 或更高版本的驱动程序。

Windows 7 之后的 Microsoft Windows 版本不支持 IrDA 微型端口驱动程序。

Windows 7 之后的 Microsoft Windows 版本不支持[IPsec 任务卸载版本 1](background-reading-on-ipsec.md) 。 应更新支持 IPsec 任务卸载的所有驱动程序，以支持 [ipsec 任务卸载版本 2](./introduction-to-ipsec-offload-version-2.md)。

Windows 7 之后的 Microsoft Windows 版本不支持筛选器中间驱动程序。 应使用 NDIS 6.0 筛选器驱动程序接口。 有关筛选器驱动程序的详细信息，请参阅 [NDIS 筛选器驱动程序](ndis-filter-drivers.md)。

802.11 在 Windows 7 之后的 Microsoft Windows 版本中将不支持模拟802.3 的驱动程序。 NDIS 802.11 驱动程序必须支持本机802.11 接口。 有关本机802.11 的详细信息，请参阅 [本机802.11 无线 LAN](/previous-versions/windows/hardware/wireless/ff560689(v=vs.85))。

Windows 7 之后的 Microsoft Windows 版本将不支持 NDIS WAN 驱动程序。 NDIS WAN 驱动程序必须移植到 NDIS 6.0 CoNDIS WAN 驱动程序模型。 有关 CoNDIS WAN 的详细信息，请参阅 WAN 微型端口驱动程序。

Windows 7 之后的 Microsoft Windows 版本不支持 ATM 和令牌环驱动程序。

 

