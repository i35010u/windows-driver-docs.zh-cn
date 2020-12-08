---
title: 取消注册网络接口
description: 取消注册网络接口
keywords:
- NDIS 网络接口 WDK，注销
- 网络接口 WDK，注销
- 注销网络接口
- 正在删除网络接口
- 正在注销网络接口
- NdisIfDeregisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c60deec0f18b12fdc4d073205f622eceb8f31db1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822201"
---
# <a name="deregistering-a-network-interface"></a>取消注册网络接口





NDIS 接口提供程序会调用 [**NdisIfDeregisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterinterface) 函数，以指示应从计算机上已知接口的列表中删除指定的接口，例如，因为接口已卸载。 注销接口的其他原因是特定于应用程序的。 为了提升良好的资源管理，接口提供程序应始终取消注册不再有用的接口。

**NdisIfDeregisterInterface** 释放与指定接口相关联的接口索引。 NDIS 可以将索引重新分配给以后注册的接口。 但是，不会回收与相应的 NET luid 值相关联的 [**net \_ luid**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 索引（ \_ 如有必要），接口提供程序可以 \_ 通过调用 [**NdisIfFreeNetLuidIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex) 函数来释放 net luid 索引。

**注意**  当卸载微型端口适配器时，NDIS 代理提供程序注销接口，并在分离时筛选模块。

 

 

