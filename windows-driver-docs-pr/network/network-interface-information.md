---
title: 网络接口信息
description: 网络接口信息
ms.assetid: 4d8cd9c2-6f78-4c70-83bd-f36fffbf1c35
keywords:
- NDIS 网络接口 WDK，有关的信息
- 网络接口 WDK，有关的信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a3f4cd4e167badbb32513cd2604136fe912910
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543916"
---
# <a name="network-interface-information"></a>网络接口信息





接口提供程序提供有关每个已注册的接口的信息，使用以下数据结构。

-   [**NET\_如果\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568743)

-   [**NDIS\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565736)

若要注册一个接口，提供程序将指针传递到初始化 NET\_IF\_信息结构[ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)函数。

NDIS 接口提供程序提供[ **NDIS\_界面\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565736)中的查询响应的结构[OID\_常规\_界面\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569589)OID。

NDIS 还可以查询提供商提供了其他 Oid。 有关 NDIS 提供程序 Oid 的详细信息，请参阅[NDIS OID 映射的网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。 有关处理接口提供程序中的 OID 请求的详细信息，请参阅[处理 OID 查询和 NDIS 接口提供程序中设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)。

 

 





