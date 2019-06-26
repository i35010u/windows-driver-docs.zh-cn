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
ms.openlocfilehash: 3f644d6b79b92dfa120579efcec9eec14d1e37f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386332"
---
# <a name="mapping-a-netluid-value-to-an-interface-index"></a>映射网络\_LUID 值到接口索引





NDIS 提供服务获取的接口索引的给定[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值，反之亦然。 请注意，NET\_LUID 值是一个接口，并对应于特定网络的接口索引的持久性标识\_LUID 值可以更改，即使计算机不重新启动 （例如，当筛选器模块是附加和分离，因为关联的微型端口适配器已禁用和重新启用）。

NDIS 提供了以下函数映射：

-   [**NdisIfGetInterfaceIndexFromNetLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifgetinterfaceindexfromnetluid)

-   [**NdisIfGetNetLuidFromInterfaceIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifgetnetluidfrominterfaceindex)

这些函数将返回 NDIS\_状态\_界面\_不\_如果找到给定的 NET\_LUID 或接口索引中不存在的已注册的接口的列表。

 

 





