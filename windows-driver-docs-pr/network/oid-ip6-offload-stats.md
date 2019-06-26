---
title: OID_IP6_OFFLOAD_STATS
description: 本主题介绍 OID_IP6_OFFLOAD_STATS 对象标识符 (OID)。
ms.assetid: 94bfc254-bc83-481f-a2d7-46c1e31e23a7
keywords:
- OID_IP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f57c3fa2f8ef5d4a592e8e3796ea86d021e2b0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371819"
---
# <a name="oidip6offloadstats"></a>OID_IP6_OFFLOAD_STATS

主机堆栈查询 OID_IP6_OFFLOAD_STATS OID，若要获取 IPv6 数据报的卸载目标已处理卸载 TCP 连接上的统计信息。 主机堆栈设置会导致重置为零，此类统计信息计数器的卸载目标此 OID。

OID_IP6_OFFLOAD_STATS 的查询响应，卸载目标提供填入[IP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ip_offload_stats)结构。 IP_OFFLOAD_STATS 结构包含 IPv6 数据报处理卸载 TCP 连接上的统计信息。

OID_IP6_OFFLOAD_STATS 一组响应，卸载目标应重置所有卸载 TCP 连接为零，其 IPv6 统计信息计数器。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

