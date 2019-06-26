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
ms.openlocfilehash: 2a0cabd3b8de4ffe4dea357b3f56ace763c8874f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360754"
---
# <a name="using-a-netluid-index"></a>使用 NET\_LUID 索引





NDIS 提供函数来分配和释放[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)创建 NET 所需的索引\_LUID 值。 NDIS 接口提供程序必须分配 NET\_LUID 值注册接口。

若要分配 NET\_LUID 索引接口提供程序调用[ **NdisIfAllocateNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex)函数。 接口提供程序分配的索引之后, 调用[ **NDIS\_使\_NET\_LUID** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)宏来构建 NET\_LUID 值。 若要释放 NET\_LUID 索引接口提供程序调用[ **NdisIfFreeNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiffreenetluidindex)函数。

**NdisIfAllocateNetLuidIndex**会尝试分配一个 24 位值，与在调用方指定的接口类型相关联*IfType*参数且是唯一的本地计算机。 如果索引分配成功， **NdisIfAllocateNetLuidIndex**返回 NDIS\_状态\_成功，并提供 NET\_LUID 的索引，在中提供的地址*pNetLuidIndex*参数。 如果 NDIS 不能够找到免费 NET\_LUID 索引**NdisIfAllocateNetLuidIndex**返回 NDIS\_状态\_资源。 **NdisIfAllocateNetLuidIndex**可以返回其他 NDIS 状态的值以指示 NDIS 内的内部错误。 NDIS 记录此索引的计算机随后重新启动时分配。 NDIS 不会将特定索引用于将来的调用方，即使计算机重新启动后，直到分配该索引的接口提供程序调用**NdisIfFreeNetLuidIndex**该索引的函数。

[**NdisIfFreeNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiffreenetluidindex)释放以前分配[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)编制索引，以便 NDIS 可能是可以重新分配到另一个接口的索引。 调用方必须传入相同的接口类型在*IfType*时调用它，将使用调用方[ **NdisIfAllocateNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex)分配 NET\_LUID 的索引。 如果释放操作成功， **NdisIfFreeNetLuidIndex**返回 NDIS\_状态\_成功。 如果在调用**NdisIfFreeNetLuidIndex**失败，接口提供程序应删除其与网络相关的持久存储中保存的任何信息\_LUID 索引。 删除信息将确保提供程序不会继续不尝试，以释放已释放的每台计算机重新启动后的索引。 在调用**NdisIfFreeNetLuidIndex**，调用方不能使用 NET\_LUID 试值，除非它调用**NdisIfAllocateNetLuidIndex**再次为同一个接口类型和接收同一 NET\_LUID 索引释放它。

若要注册的网络接口，接口提供程序必须通过有效 NET\_LUID 值赋给[ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)函数。 有关注册网络接口的详细信息，请参阅[注册网络接口](registering-a-network-interface.md)。

 

 





