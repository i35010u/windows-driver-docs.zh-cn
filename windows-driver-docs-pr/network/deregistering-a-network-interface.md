---
title: 取消注册网络接口
description: 取消注册网络接口
ms.assetid: 8d290a6a-008d-434b-bcbf-c4efade3d017
keywords:
- NDIS 网络接口 WDK，注销
- 网络接口 WDK，注销
- 注销网络接口
- 正在删除网络接口
- 正在注销网络接口
- NdisIfDeregisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed4aad5b2de4aea32d523984a4f592f1e4466bcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838159"
---
# <a name="deregistering-a-network-interface"></a>取消注册网络接口





NDIS 接口提供程序会调用[**NdisIfDeregisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterinterface)函数，以指示应从计算机上已知接口的列表中删除指定的接口，例如，因为接口已卸载。 注销接口的其他原因是特定于应用程序的。 为了提升良好的资源管理，接口提供程序应始终取消注册不再有用的接口。

**NdisIfDeregisterInterface**释放与指定接口相关联的接口索引。 NDIS 可以将索引重新分配给以后注册的接口。 但是，不会回收与相应的 NET\_LUID 值相关联的[**net\_luid**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)索引（如有必要），接口提供程序可以通过调用[**NDISIFFREENETLUIDINDEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex)来释放 net\_LUID 索引。才能.

**请注意**，在卸载小型端口适配器时  NDIS 代理提供程序注销接口，并在分离时筛选模块。

 

 

 





