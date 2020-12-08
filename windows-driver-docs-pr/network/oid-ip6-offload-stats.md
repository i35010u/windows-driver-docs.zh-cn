---
title: OID_IP6_OFFLOAD_STATS
description: 本主题介绍) OID_IP6_OFFLOAD_STATS 对象标识符 (OID。
keywords:
- OID_IP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a99daf9b1e15b5794285f179488f6aa4469c0f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806157"
---
# <a name="oid_ip6_offload_stats"></a>OID_IP6_OFFLOAD_STATS

宿主堆栈会查询 OID_IP6_OFFLOAD_STATS OID，以获取卸载目标已在卸载的 TCP 连接上处理的 IPv6 数据报的统计信息。 宿主堆栈设置此 OID，导致卸载目标将此类统计信息的计数器重置为零。

为了响应 OID_IP6_OFFLOAD_STATS 的查询，卸载目标提供了一个已填充的 [IP_OFFLOAD_STATS](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ip_offload_stats) 结构。 IP_OFFLOAD_STATS 结构包含在卸载的 TCP 连接上处理的 IPv6 数据报的统计信息。

为了响应一组 OID_IP6_OFFLOAD_STATS，卸载目标应将其所有已卸载的 TCP 连接的 IPv6 统计信息计数器重置为零。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
