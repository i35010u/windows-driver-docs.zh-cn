---
title: 注册网络接口
description: 注册网络接口
ms.assetid: 7e3c3b0f-2013-4133-8b52-fa9e66f963cb
keywords:
- NDIS 网络接口 WDK，注册
- 网络接口 WDK，注册
- 注册网络接口
- NdisIfRegisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d7b723dd4fc720198754c44ef486121e302e75e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548182"
---
# <a name="registering-a-network-interface"></a>注册网络接口





只要在计算机重新启动，NDIS 开头的已注册的网络接口的空列表。 接口提供程序调用[ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)函数每当启动或检测到一个接口并将其[ **NET\_LUID**](https://msdn.microsoft.com/library/windows/hardware/ff568747)已知值。 有关启动或检测接口的机制是特定于应用程序。

**NdisIfRegisterInterface**返回 NDIS\_状态\_成功才 NDIS 已成功将指定的接口添加到其计算机上的已知接口的列表。 在这种情况下， **NdisIfRegisterInterface**返回的接口索引*pIfIndex*参数。 但是，调用**NdisIfRegisterInterface**并不意味着接口处于活动状态; 此调用可确保仅存在接口。 **NdisIfRegisterInterface**返回 NDIS\_状态\_资源如果 NDIS 不具有足够的资源可用于注册接口。 **NdisIfRegisterInterface**还可以返回其他 NDIS 状态值。

*ProviderIfContext*的参数**NdisIfRegisterInterface**包含句柄到调用方的上下文区域的接口-此句柄是传递给调用方的 OID 查询和 set 函数。 *PIfInfo*参数包含一个指向[ **NET\_如果\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568743)结构，其中包含有关接口的信息。

以下主题提供有关网络的详细信息的接口**NdisIfRegisterInterface**成功注册：

[分配的接口索引](allocating-an-interface-index.md)

[网络接口信息](network-interface-information.md)

 

 





