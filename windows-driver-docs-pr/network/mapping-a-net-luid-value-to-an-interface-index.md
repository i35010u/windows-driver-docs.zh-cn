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
ms.openlocfilehash: 6b312b9f90eb9c01815d9f91db7be5fc365202b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564215"
---
# <a name="mapping-a-netluid-value-to-an-interface-index"></a>映射网络\_LUID 值到接口索引





NDIS 提供服务获取的接口索引的给定[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)值，反之亦然。 请注意，NET\_LUID 值是一个接口，并对应于特定网络的接口索引的持久性标识\_LUID 值可以更改，即使计算机不重新启动 （例如，当筛选器模块是附加和分离，因为关联的微型端口适配器已禁用和重新启用）。

NDIS 提供了以下函数映射：

-   [**NdisIfGetInterfaceIndexFromNetLuid**](https://msdn.microsoft.com/library/windows/hardware/ff562707)

-   [**NdisIfGetNetLuidFromInterfaceIndex**](https://msdn.microsoft.com/library/windows/hardware/ff562711)

这些函数将返回 NDIS\_状态\_界面\_不\_如果找到给定的 NET\_LUID 或接口索引中不存在的已注册的接口的列表。

 

 





