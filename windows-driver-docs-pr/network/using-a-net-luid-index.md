---
title: 使用 NET_LUID 索引
description: 使用 NET_LUID 索引
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a11d42c3ce404082f5e74aa1ad92780141a03ef6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790407"
---
# <a name="using-a-net_luid-index"></a>使用 NET \_ LUID 索引





NDIS 提供函数来分配和释放创建 NET luid 值所需的 [**net \_ luid**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 索引 \_ 。 NDIS 接口提供程序必须分配 NET \_ LUID 值才能注册接口。

若要分配 NET \_ LUID 索引，接口提供程序会调用 [**NdisIfAllocateNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex) 函数。 分配索引后，接口提供程序会调用 [**NDIS \_ MAKE \_ net \_ LUID**](/windows-hardware/drivers/ddi/ntddndis/nf-ntddndis-ndis_make_net_luid) 宏来生成 net \_ luid 值。 若要释放 NET \_ LUID 索引，接口提供程序将调用 [**NdisIfFreeNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex) 函数。

**NdisIfAllocateNetLuidIndex** 尝试分配一个24位值，此值与调用方在 *IfType* 参数指定的接口类型相关联，并且对于本地计算机是唯一的。 如果索引分配成功， **NdisIfAllocateNetLuidIndex** 将返回 NDIS \_ 状态 \_ SUCCESS，并在 \_ *pNetLuidIndex* 参数中提供的地址提供 NET LUID 索引。 如果 NDIS 无法找到 free NET \_ LUID 索引， **NdisIfAllocateNetLuidIndex** 将返回 NDIS \_ 状态 \_ 资源。 **NdisIfAllocateNetLuidIndex** 可以返回其他 ndis 状态值，以指明 NDIS 内的内部错误。 当计算机以后重新启动时，NDIS 记录此索引的分配。 即使在计算机重新启动之后，NDIS 也不会将特定索引用于以后的调用方，除非该索引的接口提供程序调用了该索引的 **NdisIfFreeNetLuidIndex** 函数。

[**NdisIfFreeNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex) 释放以前分配的 [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 索引，使 NDIS 可能将该索引重新分配给另一个接口。 调用方必须在调用 [**NdisIfAllocateNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)时所使用的同一接口类型中传递 *IfType* ，以分配 NET \_ LUID 索引。 如果免费操作成功， **NdisIfFreeNetLuidIndex** 将返回 NDIS \_ 状态 \_ 成功。 如果对 **NdisIfFreeNetLuidIndex** 的调用失败，接口提供程序应删除其保存在与 NET LUID 索引相关的永久性存储中的所有信息 \_ 。 删除信息将确保提供程序不会继续尝试释放已在每次重新启动计算机后释放的索引。 调用 **NdisIfFreeNetLuidIndex** 后，调用方不得再次使用 NET \_ LUID 值，除非它再次为同一接口类型调用 **NdisIfAllocateNetLuidIndex** ，并接收它所释放的相同 NET \_ luid 索引。

若要注册网络接口，接口提供程序必须将有效的 NET \_ LUID 值传递到 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数。 有关注册网络接口的详细信息，请参阅 [注册网络接口](registering-a-network-interface.md)。

 

