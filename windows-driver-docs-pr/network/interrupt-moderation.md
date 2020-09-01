---
title: 中断调解
description: 中断调解
ms.assetid: 291f9606-6379-4b78-b388-ba663f84b431
keywords:
- 中断裁决 WDK 网络
- 中断 WDK 网络，减少
- OID_GEN_INTERRUPT_MODERATION
- NDIS_INTERRUPT_MODERATION_PARAMETERS
- 中断 WDK 网络，裁决
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8681db468b3ecc5aa6bd86c89344411b781d4ab7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212899"
---
# <a name="interrupt-moderation"></a>中断调解





为了减少中断数，许多 Nic 都使用 *中断裁决*。 使用中断裁决，NIC 硬件在收到数据包后将不会立即产生中断。 相反，硬件会等待更多数据包到达，或在生成中断之前超时。 硬件供应商指定数据包、超时间隔或其他中断裁决算法的最大数目。

数据包的测量往返时间是最常用的一种方法，用于确定两个终结点之间的网络带宽。 但是，当启用中断裁决后，接收数据包并不会立即产生中断，因此，特定数据包的被察觉往返时间将大于平均时间。 为了使数据包的往返时间精确度量，NDIS 提供按需禁用和启用中断审核的功能。

所有 NDIS 6.0 和更高版本的微型端口驱动程序都必须支持 [oid \_ GEN \_ 中断 \_ 裁决](./oid-gen-interrupt-moderation.md) oid。 如果微型端口驱动程序不支持中断裁决，则驱动程序必须在[**NDIS \_ 中断 \_ 裁决 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构的**InterruptModeration**成员中指定**NdisInterruptModerationNotSupported** 。

NDIS 6.0 和更高版本的微型端口驱动程序必须同时支持 [oid \_ GEN \_ 中断 \_ 裁决](./oid-gen-interrupt-moderation.md) oid 集和查询请求。 Set 请求指示微型端口驱动程序启用或禁用中断裁决，查询请求报告中断裁决的当前状态。

默认情况下，支持中断裁决的微型端口驱动程序应默认启用此功能，除非注册表中的 **InterruptModeration** standard 关键字禁用了此功能。 有关标准关键字的详细信息，请参阅 [网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

