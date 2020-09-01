---
title: WDI 低延迟连接质量
description: 本部分介绍如何在 WDI 中保持低延迟连接的质量
ms.assetid: 194A26DA-A138-4967-9A09-5843A38007E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8eeb6248d690d89589e447041398142f68e38b4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211533"
---
# <a name="wdi-low-latency-connection-quality"></a>WDI 低延迟连接质量


如果在系统上运行的应用程序需要低延迟数据流量，则可以为低延迟模式操作配置端口， (例如，VoIP 应用程序) 。 在此操作模式下，驱动程序应修改任何行为 (如扫描或更好的 AP 漫游) ，这将导致其从配置为低延迟模式的端口通道移出。 它还应遵循 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 链接 \_ 状态 \_ 更改](./ndis-status-wdi-indication-link-state-change.md) 指示的指定指南。 主机提供在此模式下端口应使用的 [**WDI \_ TLV \_ 低 \_ 延迟 \_ 连接 \_ 质量 \_ 参数**](./wdi-tlv-low-latency-connection-quality-parameters.md) 。 此值指定端口应为 off 通道的最长时间，以及连接在启动低延迟漫游之前必须下降到的最小链接质量值 (包括发送 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_ 所需](./ndis-status-wdi-indication-roaming-needed.md)) 。

对于扫描，主机会提供最大通道停留时间， (主动和被动通道) 有不同的值，并且适配器不应超过最大时间。 主机还会限制不必要的扫描。 但是，如果 [**WDI \_ Scan \_ 触发器**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_trigger) **WDI \_ scan \_ trigger \_ BACKGROUND** 或 **WDI \_ scan \_ trigger \_ 漫游**，则适配器可以进一步限制扫描。 如果适配器在此模式下执行其自己的扫描，则建议将其包含在查找 (的 SSID，除非它在从睡眠状态恢复之后) ，以减少频道上的停留时间。 此外，它应避免在单通道扫描中扫描多个通道，使其低于总体的非通道时间限制。

主机将 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_ 需要](./ndis-status-wdi-indication-roaming-needed.md) 适配器的强请求进行漫游，因此，在此模式下，适配器应小心发送此指示的频率。 如果适配器执行其自己的漫游/AP 选择决定，则必须使用适当的机制 (如 "邻居报告" 或 "PMKIDs) " 以查找和选择/分级 Ap。

若要优化关联进程，在可能的情况下，适配器应使用缓存的 BSS 条目进行 TSF 计时器同步。 缓存的条目应该足以应对 TSF 计时器同步，这是最新的，因为它是从最近的探测请求获取的。 即使驱动程序决定选择不具有最新缓存探测响应的 AP，TSF 同步也可以在以后进行。 驱动程序可以在接收到下一个信标之前禁用 Wi-fi 节能，这通常出现在100ms 中。

当在多通道并发模式下操作时，建议适配器使用 ECSA 或其他机制来实现通道多路复用时无缝/无抖动体验。

 

