---
title: OID_TCP4_OFFLOAD_STATS
description: 本主题介绍) OID_TCP4_OFFLOAD_STATS 对象标识符 (OID。
keywords:
- OID_TCP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: eacad2f6ed5d1a4c5731555e9d9bd2bbf18ff8bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832141"
---
# <a name="oid_tcp4_offload_stats"></a>OID_TCP4_OFFLOAD_STATS

宿主堆栈会查询 OID_TCP4_OFFLOAD_STATS OID，以获取在传输 IPv4 数据报的已卸载的 TCP 连接上对卸载目标处理的 TCP 段上的统计信息。 宿主堆栈设置此 OID，导致卸载目标将此类统计信息的计数器重置为零。

为了响应 OID_TCP4_OFFLOAD_STATS 的查询，卸载目标提供了一个已填充的 [TCP_OFFLOAD_STATS](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_tcp_offload_stats) 结构。

为响应一组 OID_TCP4_OFFLOAD_STATS，卸载目标应重置为传入 TCP 连接的所有 TCP 统计信息计数器，这些计数器用于传递 IPv4 数据报。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
