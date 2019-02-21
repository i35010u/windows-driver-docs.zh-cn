---
title: OID_TCP6_OFFLOAD_STATS
description: 本主题介绍 OID_TCP6_OFFLOAD_STATS 对象标识符 (OID)。
ms.assetid: d7da8dd0-8de0-4283-9ecf-94e3d1503abe
keywords:
- OID_TCP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdfbe05f0f44c14d02d0b6abcb44961e28777cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554751"
---
# <a name="oidtcp6offloadstats"></a>OID_TCP6_OFFLOAD_STATS

主机堆栈查询 OID_TCP6_OFFLOAD_STATS OID，若要获得有关卸载目标已处理卸载传达 IPv6 数据报的 TCP 连接的 TCP 段统计信息。 主机堆栈设置会导致重置为零，此类统计信息计数器的卸载目标此 OID。

OID_TCP6_OFFLOAD_STATS 的查询响应，卸载目标提供填入[TCP_OFFLOAD_STATS](https://msdn.microsoft.com/library/windows/hardware/ff570940)结构。

OID_TCP6_OFFLOAD_STATS 一组响应，卸载目标应重置为零的所有卸载传达 IPv6 数据报的 TCP 连接其 TCP 统计信息计数器。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

