---
title: 取消注册网络接口
description: 取消注册网络接口
ms.assetid: 8d290a6a-008d-434b-bcbf-c4efade3d017
keywords:
- NDIS 网络接口 WDK，取消注册
- 网络接口 WDK，取消注册
- 取消注册网络接口
- 删除网络接口
- 正在注销的网络接口
- NdisIfDeregisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70384152e71bfb216320abf95643941aff1f6fd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347441"
---
# <a name="deregistering-a-network-interface"></a>取消注册网络接口





NDIS 接口提供程序调用[ **NdisIfDeregisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562700)函数来指示，指定的接口应从列表中删除的已知接口的计算机上，例如，因为该接口已卸载。 其他理由取消接口是特定于应用程序。 若要提升很好的资源管理，接口提供程序应始终取消注册，将不再有用的接口。

**NdisIfDeregisterInterface**释放与指定的接口相关联的接口索引。 NDIS 可以重新分配到已注册在将来的接口的索引。 但是， [ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)与相应的网络相关联的索引\_不回收 LUID 值-如有必要，接口提供程序可以发布 NET\_LUID 索引通过调用[ **NdisIfFreeNetLuidIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562706)函数。

**请注意**  NDIS 代理提供程序注销微型端口适配器的接口，它们都会被卸载并分离时筛选模块时。

 

 

 





