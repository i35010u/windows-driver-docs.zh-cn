---
title: 微型端口适配器状态指示
description: 微型端口适配器状态指示
ms.assetid: feb5259f-ce9b-40eb-85d2-0064bce692fc
keywords:
- 状态指示 WDK 网络，微型端口适配器
- 微型端口适配器 WDK 网络状态指示
- 状态指示适配器 WDK 网络
- NdisMIndicateStatusEx
- NDIS_STATUS_INDICATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ddead5af15fc7a1527fc3cd1cb65acd58105d1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533697"
---
# <a name="miniport-adapter-status-indications"></a>微型端口适配器状态指示





微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数报告的微型端口适配器状态中的更改。 微型端口驱动程序传递**NdisMIndicateStatusEx**指向的指针[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构，其中包含状态信息。

状态指示包括的信息来标识的类型的状态和状态更改的原因。

微型端口驱动程序应设置**SourceHandle**成员添加到 NDIS 传递给的句柄*MiniportAdapterHandle*参数[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 如果状态指示是使用 OID 请求相关联，可以设置微型端口驱动程序**DestinationHandle**并**RequestId**成员，因此该 NDIS 可以提供与特定的状态指示协议绑定。

 

 





