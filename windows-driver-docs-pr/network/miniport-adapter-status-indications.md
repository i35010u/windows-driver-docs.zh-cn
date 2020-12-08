---
title: 微型端口适配器状态指示
description: 微型端口适配器状态指示
keywords:
- 状态指示 WDK 网络，微型端口适配器
- 微型端口适配器 WDK 网络，状态指示
- 适配器 WDK 网络，状态指示
- NdisMIndicateStatusEx
- NDIS_STATUS_INDICATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf8b4dd97bdeb24dab3b72bfa3c9e2a45df009ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831329"
---
# <a name="miniport-adapter-status-indications"></a>微型端口适配器状态指示





微型端口驱动程序调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数来报告微型端口适配器的状态更改。 微型端口驱动程序将 **NdisMIndicateStatusEx** 传递到包含状态信息的 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构。

状态指示包含用于标识状态类型和状态更改原因的信息。

微型端口驱动程序应将 **SourceHandle** 成员设置为 NDIS 传递到 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的 *MiniportAdapterHandle* 参数的句柄。 如果状态指示与 OID 请求关联，微型端口驱动程序可以设置 **DestinationHandle** 和 **RequestId** 成员，使 NDIS 可以向特定协议绑定提供状态指示。

 

