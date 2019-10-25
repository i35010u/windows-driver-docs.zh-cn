---
title: WDI 低延迟连接质量
description: 本部分介绍如何在 WDI 中保持低延迟连接的质量
ms.assetid: 194A26DA-A138-4967-9A09-5843A38007E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a9d01cbe64e6c0d16169c2cba2715d3e0cf1bef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842922"
---
# <a name="wdi-low-latency-connection-quality"></a>WDI 低延迟连接质量


如果在系统上运行的应用程序需要低延迟数据流量（例如，VoIP 应用程序），则可以为低延迟模式操作配置端口。 在此操作模式下，驱动程序应修改任何行为（如扫描或更好的 AP 漫游），这会导致其移出配置为低延迟模式的端口通道。 它还应遵循[NDIS\_状态的指定指南\_WDI\_指示\_链接\_状态\_更改](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-link-state-change)指示。 主机提供[**WDI\_TLV\_低\_延迟\_连接\_质量\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-low-latency-connection-quality-parameters)在此模式下端口应使用的参数。 此值指定端口应为 off 通道的最长时间，以及在启动低延迟漫游之前连接必须下降到的最小链接质量值（包括发送[NDIS\_状态\_WDI\_指示\_漫游\_需要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)）。

对于扫描，主机提供最大通道停留时间（主动和被动通道有不同的值），并且适配器不应超过最大时间。 主机还会限制不必要的扫描。 但是，如果[**WDI\_扫描\_触发器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_trigger) **WDI\_scan\_触发器\_后台**或**WDI\_scan\_trigger\_漫游**，则适配器可以进一步限制扫描。 如果适配器在此模式下执行其自己的扫描，则建议包含它所查找的 SSID （除非它在从睡眠状态恢复之后），以减少通道上的停留时间。 此外，它应避免在单通道扫描中扫描多个通道，使其低于总体的非通道时间限制。

主机将[NDIS\_状态视为\_WDI\_指示\_漫游\_需要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)适配器的强请求进行漫游，因此在此模式下，适配器应小心发送此指示的频率。 如果适配器执行其自己的漫游/AP 选择决定，则必须使用适当的机制（如邻居报告或 PMKIDs）来查找并选择/分级 Ap。

若要优化关联进程，在可能的情况下，适配器应使用缓存的 BSS 条目进行 TSF 计时器同步。 缓存的条目应该足以应对 TSF 计时器同步，这是最新的，因为它是从最近的探测请求获取的。 即使驱动程序决定选择不具有最新缓存探测响应的 AP，TSF 同步也可以在以后进行。 驱动程序可以在接收到下一个信标之前禁用 Wi-fi 节能，这通常出现在100ms 中。

当在多通道并发模式下操作时，建议适配器使用 ECSA 或其他机制来实现通道多路复用时无缝/无抖动体验。

 

 





