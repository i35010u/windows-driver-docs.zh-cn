---
title: NET_LUID 值
description: NET_LUID 值
ms.assetid: 9b9c63c1-f8b4-4e26-afc1-a3e4910609e2
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d99c54808d8e6ca50005472a485a98db73df3306
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210717"
---
# <a name="net_luid-value"></a>NET \_ LUID 值





[**NET \_ LUID**](/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值是用于标识 NDIS 网络接口的64位值。 NET \_ luid 数据类型是一种联合，它可以将 net \_ luid 值作为单个64位值或包含 net \_ luid 索引和接口类型的结构提供访问。

NET luid 联合的 **NetLuidIndex** 成员 \_ 是一个24位 net \_ luid 索引，该索引是在接口提供程序调用 [**NdisIfAllocateNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex) 函数时 NDIS 分配的。 NDIS 和接口提供程序使用此索引来区分具有相同接口类型的多个接口。 因此，此索引在本地计算机中是唯一的。

[**NET \_ LUID**](/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)联合的**IfType**成员是一个16位值，其中包含 INTERNET 号码分配机构 (IANA) 定义的接口类型。 有关有效接口类型的列表，请参阅 [NDIS 接口类型](./ndis-interface-types.md)。

NET \_ luid 数据类型等效于 RFC 2863 中的 *ifName* 对象，因为 NDIS 从 NET LUID 值派生了 *ifName* 字符串 \_ 。

若要创建 NET \_ luid 值，接口提供程序会调用 [**NdisIfAllocateNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex) 函数来分配 net \_ luid 索引，然后调用 [**NDIS \_ MAKE \_ net \_ luid**](/windows-hardware/drivers/ddi/ntddndis/nf-ntddndis-ndis_make_net_luid) 宏来构建 net \_ luid 值。 有关创建 NET luid 值的详细信息 \_ ，请参阅 [使用 Net \_ luid 索引](using-a-net-luid-index.md)。

 

