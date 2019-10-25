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
ms.openlocfilehash: ad3539cdd0b4d584bf4e0a8c955161d06a085616
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829032"
---
# <a name="net_luid-value"></a>NET\_LUID 值





[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值是用于标识 NDIS 网络接口的64位值。 NET\_LUID 数据类型是一种联合，它可以将 NET\_LUID 值作为单个64位值或包含 NET\_LUID 索引和接口类型的结构提供访问。

NET\_LUID 联合的**NetLuidIndex**成员是一个24位网络\_LUID 索引，NDIS 在接口提供程序调用[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)函数时分配。 NDIS 和接口提供程序使用此索引来区分具有相同接口类型的多个接口。 因此，此索引在本地计算机中是唯一的。

[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)联合的**IfType**成员是一个16位值，其中包含 Internet 号码分配机构（IANA）定义的接口类型。 有关有效接口类型的列表，请参阅[NDIS 接口类型](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-interface-types)。

NET\_LUID 数据类型等效于 RFC 2863 中的*ifName*对象，因为 NDIS 从 NET\_LUID 值派生了*ifName*字符串。

若要创建 NET\_LUID 值，接口提供程序会调用[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)函数来分配 NET\_LUID 索引，然后调用[**NDIS\_使\_net\_LUID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)宏生成 net\_LUID 值。 有关创建 NET\_LUID 值的详细信息，请参阅[使用 net\_Luid 索引](using-a-net-luid-index.md)。

 

 





