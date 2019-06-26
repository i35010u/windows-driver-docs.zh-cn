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
ms.openlocfilehash: dffa1662f14e50c11416b3829c21ea484d53b609
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385843"
---
# <a name="netluid-value"></a>NET\_LUID 值





一个[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值是标识的 NDIS 网络接口的 64 位值。 NET\_LUID 数据类型是一个可提供对网络访问的联合\_LUID 值作为单个的 64 位值或结构，其中包含 NET\_LUID 索引和一个接口类型。

**NetLuidIndex** NET 成员\_LUID 联合是 24 位 NET\_NDIS 分配时调用的接口提供的 LUID 索引[ **NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex)函数。 NDIS 和接口提供程序使用此索引以区分具有相同的接口类型的多个接口。 因此，此索引是在本地计算机中是唯一的。

**IfType**的成员[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)联合是一个 16 位值，包含 Internet 号码分配机构 IANA 定义的接口类型。 有关有效的接口类型的列表，请参阅[NDIS 接口类型](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-interface-types)。

NET\_LUID 数据类型等效于*ifName*对象在 RFC 2863，因为 NDIS 派生*ifName*字符串从 NET\_LUID 值。

若要创建 NET\_LUID 值接口提供程序调用[ **NdisIfAllocateNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex)函数以分配 NET\_LUID 索引，然后调用[**NDIS\_使\_NET\_LUID** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)宏来构建 NET\_LUID 值。 有关创建 NET\_LUID 值，请参阅[使用 NET\_LUID 索引](using-a-net-luid-index.md)。

 

 





