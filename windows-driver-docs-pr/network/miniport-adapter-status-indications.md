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
ms.openlocfilehash: cc8c3ff31694f309515acc15fd6b57976b108c4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373942"
---
# <a name="miniport-adapter-status-indications"></a>微型端口适配器状态指示





微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)函数报告的微型端口适配器状态中的更改。 微型端口驱动程序传递**NdisMIndicateStatusEx**指向的指针[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构，其中包含状态信息。

状态指示包括的信息来标识的类型的状态和状态更改的原因。

微型端口驱动程序应设置**SourceHandle**成员添加到 NDIS 传递给的句柄*MiniportAdapterHandle*参数[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 如果状态指示是使用 OID 请求相关联，可以设置微型端口驱动程序**DestinationHandle**并**RequestId**成员，因此该 NDIS 可以提供与特定的状态指示协议绑定。

 

 





