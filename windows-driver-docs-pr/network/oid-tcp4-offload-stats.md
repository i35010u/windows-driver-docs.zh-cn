---
title: OID_TCP4_OFFLOAD_STATS
description: 本主题介绍 OID_TCP4_OFFLOAD_STATS 对象标识符 (OID)。
ms.assetid: e6933a86-0ff3-48ff-a0e3-3bfc32b19df3
keywords:
- OID_TCP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8f9809437d385555e02113006cced3145cf2e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353694"
---
# <a name="oidtcp4offloadstats"></a>OID_TCP4_OFFLOAD_STATS

主机堆栈查询 OID_TCP4_OFFLOAD_STATS OID，若要获得有关卸载目标已处理卸载传达 IPv4 数据报的 TCP 连接的 TCP 段统计信息。 主机堆栈设置会导致重置为零，此类统计信息计数器的卸载目标此 OID。

OID_TCP4_OFFLOAD_STATS 的查询响应，卸载目标提供填入[TCP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_tcp_offload_stats)结构。

OID_TCP4_OFFLOAD_STATS 一组响应，卸载目标应重置为零的所有卸载传达 IPv4 数据报的 TCP 连接其 TCP 统计信息计数器。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

