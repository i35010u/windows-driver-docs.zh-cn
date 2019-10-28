---
title: 使用 NET_LUID 索引
description: 使用 NET_LUID 索引
ms.assetid: 21e0a73b-a02c-4ab4-b7c2-efcb8bfc806d
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12ee658713e52918ffb996c01e74e3066ffa287f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842996"
---
# <a name="using-a-net_luid-index"></a>使用 NET\_LUID 索引





NDIS 提供函数来分配和释放创建 NET\_LUID 值所需的[**net\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)索引。 NDIS 接口提供程序必须分配 NET\_LUID 值才能注册接口。

若要分配 NET\_LUID 索引，接口提供程序会调用[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)函数。 分配索引后，接口提供程序会调用[**NDIS\_使\_net\_luid**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)宏生成 NET\_LUID 值。 若要释放 NET\_LUID 索引，接口提供程序会调用[**NdisIfFreeNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex)函数。

**NdisIfAllocateNetLuidIndex**尝试分配一个24位值，此值与调用方在*IfType*参数指定的接口类型相关联，并且对于本地计算机是唯一的。 如果索引分配成功， **NdisIfAllocateNetLuidIndex**将返回 NDIS\_状态\_SUCCESS，并在*pNetLuidIndex*参数中提供的地址提供 NET\_LUID 索引。 如果 NDIS 无法找到免费的 NET\_LUID 索引， **NdisIfAllocateNetLuidIndex**将返回 NDIS\_状态\_资源。 **NdisIfAllocateNetLuidIndex**可以返回其他 ndis 状态值，以指明 NDIS 内的内部错误。 当计算机以后重新启动时，NDIS 记录此索引的分配。 即使在计算机重新启动之后，NDIS 也不会将特定索引用于以后的调用方，除非该索引的接口提供程序调用了该索引的**NdisIfFreeNetLuidIndex**函数。

[**NdisIfFreeNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex)释放以前分配的[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)索引，使 NDIS 可能将该索引重新分配给另一个接口。 调用方必须在调用[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)时使用的同一接口类型传入*IfType* ，以分配 NET\_LUID 索引。 如果免费操作成功， **NdisIfFreeNetLuidIndex**将\_SUCCESS 返回 NDIS\_状态。 如果对**NdisIfFreeNetLuidIndex**的调用失败，接口提供程序应删除其保存在与 NET\_LUID 索引相关的永久性存储中的所有信息。 删除信息将确保提供程序不会继续尝试释放已在每次重新启动计算机后释放的索引。 调用**NdisIfFreeNetLuidIndex**后，调用方不能再次使用 NET\_LUID 值，除非它再次为同一接口类型调用**NdisIfAllocateNetLuidIndex** ，并接收它所释放的同一网络\_LUID 索引。

若要注册网络接口，接口提供程序必须将有效的 NET\_LUID 值传递到[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数。 有关注册网络接口的详细信息，请参阅[注册网络接口](registering-a-network-interface.md)。

 

 





