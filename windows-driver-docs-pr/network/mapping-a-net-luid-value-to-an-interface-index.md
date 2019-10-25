---
title: 将 NET_LUID 值映射到接口索引
description: 将 NET_LUID 值映射到接口索引
ms.assetid: a535d886-186e-4abe-9ca0-ebef262614b3
keywords:
- NDIS 网络接口 WDK，NET_LUID
- 网络接口 WDK，NET_LUID
- NET_LUID
- 映射 NET_LUID 值
- 接口索引 WDK 网络
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b441ac12360acbbf19516bd2a586932f8023baa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844308"
---
# <a name="mapping-a-net_luid-value-to-an-interface-index"></a>将 NET\_LUID 值映射到接口索引





NDIS 提供服务来获取给定[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值的接口索引，反之亦然。 请注意，NET\_LUID 值是接口的持久标识，与特定 NET\_LUID 值相对应的接口索引即使计算机不重新启动（例如，附加了筛选器模块时也可能会更改）并分离，因为已禁用和重新启用关联的微型端口适配器。

NDIS 提供以下映射函数：

-   [**NdisIfGetInterfaceIndexFromNetLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetinterfaceindexfromnetluid)

-   [**NdisIfGetNetLuidFromInterfaceIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetnetluidfrominterfaceindex)

如果已注册的接口列表中不存在给定的 NET\_LUID 或接口索引，则这些函数将返回 NDIS\_状态\_接口\_未\_。

 

 





