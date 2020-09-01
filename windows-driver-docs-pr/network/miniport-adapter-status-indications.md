---
title: 微型端口适配器状态指示
description: 微型端口适配器状态指示
ms.assetid: feb5259f-ce9b-40eb-85d2-0064bce692fc
keywords:
- 状态指示 WDK 网络，微型端口适配器
- 微型端口适配器 WDK 网络，状态指示
- 适配器 WDK 网络，状态指示
- NdisMIndicateStatusEx
- NDIS_STATUS_INDICATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8799bba62dabc0dcdd6f22a15d424f2a121dfcad
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215570"
---
# <a name="miniport-adapter-status-indications"></a>微型端口适配器状态指示





微型端口驱动程序调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数来报告微型端口适配器的状态更改。 微型端口驱动程序将 **NdisMIndicateStatusEx** 传递到包含状态信息的 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构。

状态指示包含用于标识状态类型和状态更改原因的信息。

微型端口驱动程序应将**SourceHandle**成员设置为 NDIS 传递到[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的*MiniportAdapterHandle*参数的句柄。 如果状态指示与 OID 请求关联，微型端口驱动程序可以设置 **DestinationHandle** 和 **RequestId** 成员，使 NDIS 可以向特定协议绑定提供状态指示。

 

