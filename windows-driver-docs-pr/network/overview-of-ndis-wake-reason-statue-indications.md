---
title: NDIS 唤醒原因状态指示概述
description: NDIS 唤醒原因状态指示概述
ms.assetid: 94B54281-7A7E-4DBA-85AE-313EEF09E733
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a158811f25caaba74fa0a62bfcee61f5fa1bc064
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843732"
---
# <a name="overview-of-ndis-wake-reason-status-indications"></a>NDIS 唤醒原因状态指示概述


从 NDIS 6.30 开始，微型端口驱动程序发出 NDIS 唤醒原因状态指示（[**ndis\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)），通知 NDIS 和过量驱动程序有关系统唤醒事件的原因。 如果网络适配器生成唤醒事件，则当网络适配器恢复到完全电源状态时，微型端口驱动程序会立即发出 ndis 状态指示， **\_状态\_PM\_唤醒\_原因**。

**注意**  支持 NDIS 唤醒原因状态指示对于移动宽带（MB）微型端口驱动程序是可选的。

 

微型端口驱动程序通过[oid\_pm\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)的对象标识符（oid）设置请求，使用电源管理（PM）参数配置。 此 OID 请求通过[**NDIS\_pm\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构来指定 pm 参数。

[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构指定以下类型的唤醒事件的参数。

<a href="" id="received-packet-wake-up-events"></a>接收的数据包唤醒事件  
如果网络适配器接收到与 LAN 唤醒（WOL）模式匹配的数据包，则会生成唤醒事件。 WOL 模式包括以下各项：

-   独立于介质的 WOL 模式，如数据包有效负载中的幻数据包或 TCP/IP 数据模式。 例如， [**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构可以为 TCP SYN 帧指定 WOL 模式。

-   特定于媒体的 WOL 模式，如 EAPOL 请求标识符数据包或移动宽带（MB）短消息服务（SMS）消息。

-   通配符模式匹配通过 OID 集 oid 指定的接收筛选器[\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)。

**注意**  此类型的唤醒原因状态指示，网络适配器必须能够保存接收的数据包。 驱动程序必须在状态指示内返回接收的数据包。

 

WOL 模式通过[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**EnabledWoLPacketPatterns**成员指定。

<a href="" id="media-specific-wake-up-events"></a>特定于媒体的唤醒事件  
由于特定于媒体的原因（例如，从802.11 接入点（AP）解除相关或接收移动宽带（MB）短消息服务（SMS）消息），网络适配器将生成唤醒事件。

此类型的唤醒事件通过[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**MediaSpecificWakeUpEvents**成员指定。

<a href="" id="media-independent-wake-up-events"></a>独立于媒体的唤醒事件  
由于与媒体无关的原因（例如，媒体连接或断开连接），网络适配器将生成唤醒事件。

此类型的唤醒事件通过[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**WakeUpFlags**成员指定。

对于 NDIS 唤醒原因，微型端口驱动程序必须遵循以下准则：

-   如果微型端口驱动程序支持发出唤醒数据包指示的功能，则当 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，它必须报告此功能。 有关详细信息，请参阅[报表唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)。

    **请注意**  微型端口驱动程序不必为与 WOL 数据包的接收相关的事件报告其发出 NDIS 唤醒原因状态指示的能力。

     

-   当微型端口驱动程序对 WOL 数据包发出唤醒数据包指示时，它必须包含引起唤醒事件的数据包。 有关详细信息，请参阅[发出 NDIS 唤醒原因状态指示](issuing-ndis-wake-reason-indications.md)。

-   如果网络适配器生成了唤醒信号，则微型端口驱动程序必须[ **\_PM\_唤醒\_原因状态指示发出 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)。 驱动程序在处理 oid\_PNP\_集的 OID 集请求时执行此操作，[集\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)转换为完全电源状态。

-   在发出与唤醒事件相关的状态指示之前，微型端口驱动程序必须[ **\_PM 发出 NDIS\_状态\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示。 例如，如果唤醒事件是因为媒体连接状态发生了变化，则微型端口驱动程序必须[ **\_链接发出 ndis\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)，然后在其发出**NDIS\_\_状态之后\_状态状态指示\_唤醒\_原因**状态指示。

-   微型端口驱动程序必须将[**NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示仅用于先前通过 OID 的 oid 集请求启用的电源管理事件\_[PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters).

-   微型端口驱动程序必须将[**NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示仅用于基础网络适配器生成的唤醒事件。

 

 





