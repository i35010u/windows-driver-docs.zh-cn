---
title: CoNDIS 微型端口驱动程序状态指示
description: CoNDIS 微型端口驱动程序状态指示
ms.assetid: 1f1174ba-8b0a-4d43-96c9-2d92f50a22c4
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- NDIS 微型端口驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fe04999b873af395cdf8b382572bb6dc64a7a41
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209795"
---
# <a name="condis-miniport-driver-status-indications"></a>CoNDIS 微型端口驱动程序状态指示





微型端口驱动程序调用 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 函数来报告微型端口适配器的状态更改。 微型端口驱动程序将 **NdisMCoIndicateStatusEx** 传递到包含状态信息的 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构。

状态指示包含用于标识状态类型和状态更改原因的信息。

微型端口驱动程序应将 NDIS 状态指示结构的**SourceHandle**成员设置 \_ \_ 为 ndis 传递到[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的*MiniportAdapterHandle*参数的句柄。 如果状态指示与 OID 请求关联，微型端口驱动程序可以设置 NDIS 状态指示的 **DestinationHandle** 和 **RequestId** 成员， \_ \_ 使 ndis 能够向特定协议绑定提供状态指示。 有关 OID 请求的详细信息，请参阅 [CoNDIS 微型端口驱动程序 OID 请求](condis-miniport-driver-oid-requests.md)。

 

