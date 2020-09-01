---
title: OID_IP4_OFFLOAD_STATS
description: 本主题介绍) OID_IP4_OFFLOAD_STATS 对象标识符 (OID。
ms.assetid: 7ffe9703-5370-410f-bccd-4a430835edd0
keywords:
- OID_IP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b3b6331e6da441b17f9ab25203908c19b84d91f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209683"
---
# <a name="oid_ip4_offload_stats"></a>OID_IP4_OFFLOAD_STATS

宿主堆栈会查询 OID_IP4_OFFLOAD_STATS OID，以获取卸载目标已在卸载的 TCP 连接上处理的 IPv4 数据报的统计信息。 宿主堆栈设置此 OID，导致卸载目标将此类统计信息的计数器重置为零。

为了响应 OID_IP4_OFFLOAD_STATS 的查询，卸载目标提供了一个已填充的 [IP_OFFLOAD_STATS](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ip_offload_stats) 结构。 IP_OFFLOAD_STATS 结构包含在卸载的 TCP 连接上处理的 IPv4 数据报的统计信息。

为了响应一组 OID_IP4_OFFLOAD_STATS，卸载目标应将其所有已卸载 TCP 连接的 IPv4 统计信息计数器重置为零。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 