---
title: NDIS 6.20 向后兼容性
description: NDIS 6.20 向后兼容性
ms.assetid: a2d71cae-aed2-4c23-9ad2-5c32d4ab2294
keywords:
- NDIS 6.20 WDK，向后兼容性
- 向后兼容性 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9c56a0c1522da4a934aef8160c95ec9802e09f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545142"
---
# <a name="ndis-620-backward-compatibility"></a>NDIS 6.20 向后兼容性





NDIS 6.20 将向后兼容性功能添加到那些适用于 NDIS 6.0 驱动程序。 有关 NDIS 6.0 兼容性问题的信息，请参阅[NDIS 6.0 向后兼容性](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)。 除了转换提供的功能的 NDIS 6.0 ndis 5.x 和早期版本的驱动程序，NDIS 6.20 还提供了电源管理接口对应的翻译。 NDIS 6.20 驱动程序必须支持 NDIS 6.20 电源管理接口。

NDIS 6.20 支持 NDIS 6.1 新增的功能的更新的版本。 有关 NDIS 6.1 功能的更新的详细信息，请参阅[NDIS 6.20 支持 NDIS 6.1 功能](ndis-6-20-updates-to-ndis-6-1-features.md)。

**请注意**  NDIS 6.20 接口支持超过 64 个处理器。 早期 NDIS 版本仅限于不超过 64 个处理器 (在 x86 的 32 版本的操作系统)。

 

若要保持与早期 NDIS 版本向后的兼容，尚未更新以支持 64 个以上处理器默认为处理器的驱动程序组零。 有关处理器组的详细信息，请参阅处理器组的内核模式驱动程序体系结构设计文档。

某些 NDIS 6.1 和更早的函数已过时，并不能用于 NDIS 6.20 驱动程序。 请参阅特定函数来确定其 NDIS 版本兼容性的参考页的要求部分。 已过时的接口的列表，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

附带了 Windows 7 的 TCP/IP 协议驱动程序已更新为 NDIS 6.20。 TCP/IP 协议驱动程序是使用 NDIS 6.1 和驱动程序堆栈中的早期驱动程序的向后兼容。 但是，若要获取 Windows 7 驱动程序堆栈的最佳性能，所有驱动程序应更新为 NDIS 6.20。

NDIS 5.x 和早期 NDIS 驱动程序在 Windows 7 后在 Microsoft Windows 版本中已弃用。 没有新的 NDIS 5.x 驱动程序将 WHQL 认证。 NDIS 6.0 或更高版本的驱动程序，应为所有新的驱动程序。

IrDA 微型端口驱动程序将不支持在 Microsoft Windows 版本后 Windows 7。

[IPsec 任务卸载版本 1](ipsec-offload-version-1.md)将不支持在 Microsoft Windows 版本后 Windows 7。 支持 IPsec 任务卸载的所有驱动程序应更新为支持[IPsec 任务卸载版本 2](ipsec-offload-version-2.md)。

筛选器中间驱动程序将不支持在 Microsoft Windows 版本后 Windows 7。 应使用 NDIS 6.0 筛选器驱动程序接口。 有关筛选器驱动程序的详细信息，请参阅[NDIS 筛选器驱动程序](ndis-filter-drivers.md)。

802.11 模拟 802.3 的驱动程序将不支持在 Microsoft Windows 版本后 Windows 7。 NDIS 802.11 驱动程序必须支持本机 802.11 接口。 有关本机 802.11 的详细信息，请参阅[本机 802.11 无线 LAN](https://msdn.microsoft.com/library/windows/hardware/ff560689)。

NDIS WAN 驱动程序将不支持在 Microsoft Windows 版本后 Windows 7。 NDIS WAN 驱动程序必须移植到 NDIS 6.0 的 CoNDIS WAN 的驱动程序模型。 有关的 CoNDIS WAN 的详细信息，请参阅 WAN 微型端口驱动程序。

ATM 和令牌环驱动程序将不支持在 Microsoft Windows 版本后 Windows 7。

 

 





