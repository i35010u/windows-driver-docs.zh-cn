---
title: NDIS 唤醒原因状态指示概述
description: NDIS 唤醒原因状态指示概述
ms.assetid: 94B54281-7A7E-4DBA-85AE-313EEF09E733
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f397d36b7ff08af8e5230957df2c6bae359d1296
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210617"
---
# <a name="overview-of-ndis-wake-reason-status-indications"></a>NDIS 唤醒原因状态指示概述


从 NDIS 6.30 开始，微型端口驱动程序发出 NDIS 唤醒原因状态指示 ([**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md)) 通知 ndis 和过量驱动程序有关系统唤醒事件的原因。 如果网络适配器生成唤醒事件，则当网络适配器恢复到完全电源状态时，微型端口驱动程序会立即发出 ndis 状态 ** \_ \_ PM \_ 唤醒 \_ 原因** 的 ndis 状态指示。

**注意**   支持 NDIS 唤醒原因状态指示对于移动宽带 (MB) 微型端口驱动程序是可选的。

 

微型端口驱动程序使用电源管理 (PM) 参数通过对象标识符 (OID) 设置 [oid \_ PM \_ 参数](./oid-pm-parameters.md)的请求。 此 OID 请求通过 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 结构指定 PM 参数。

[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构指定以下类型的唤醒事件的参数。

<a href="" id="received-packet-wake-up-events"></a>接收的数据包唤醒事件  
如果网络适配器接收到与 (LAN 唤醒) 模式相匹配的数据包，则会生成唤醒事件。 WOL 模式包括以下各项：

-   独立于介质的 WOL 模式，如数据包有效负载中的幻数据包或 TCP/IP 数据模式。 例如， [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 结构可以为 TCP SYN 帧指定 WOL 模式。

-   特定于媒体的 WOL 模式，如 EAPOL 请求标识符数据包或移动宽带 (MB) 短消息服务 (SMS) 消息。

-   通配符模式，与通过 OID 的 oid 集请求指定 [ \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)指定的接收筛选器匹配。

**注意**   对于这种类型的唤醒原因状态指示，网络适配器必须能够保存接收的数据包。 驱动程序必须在状态指示内返回接收的数据包。

 

WOL 模式由[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**EnabledWoLPacketPatterns**成员指定。

<a href="" id="media-specific-wake-up-events"></a>特定于媒体的唤醒事件  
网络适配器会生成唤醒事件，这是因为特定于媒体的原因，例如从802.11 接入点解除与 (AP) 或接收移动宽带 (MB) 短消息服务 (SMS) 消息。

此类型的唤醒事件通过[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**MediaSpecificWakeUpEvents**成员指定。

<a href="" id="media-independent-wake-up-events"></a>独立于媒体的唤醒事件  
由于与媒体无关的原因（例如，媒体连接或断开连接），网络适配器将生成唤醒事件。

此类型的唤醒事件通过[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**WakeUpFlags**成员指定。

对于 NDIS 唤醒原因，微型端口驱动程序必须遵循以下准则：

-   如果微型端口驱动程序支持发出唤醒数据包指示的功能，则当 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，它必须报告此功能。 有关详细信息，请参阅 [报表唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)。

    **注意**   微型端口驱动程序不必为与 WOL 数据包的接收相关的事件报告其发出 NDIS 唤醒原因状态指示的能力。

     

-   当微型端口驱动程序对 WOL 数据包发出唤醒数据包指示时，它必须包含引起唤醒事件的数据包。 有关详细信息，请参阅 [发出 NDIS 唤醒原因状态指示](issuing-ndis-wake-reason-indications.md)。

-   如果网络适配器生成了唤醒信号，则微型端口驱动程序必须发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示。 驱动程序会在处理 oid [ \_ PNP \_ 设置 \_ ](./oid-pnp-set-power.md) 的 oid 请求功能时执行此操作，以实现到全功能状态的过渡。

-   在发出与唤醒事件相关的状态指示之前，微型端口驱动程序必须发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示。 例如，如果唤醒事件是因为媒体连接状态发生了变化，则微型端口驱动程序必须在发出**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**状态指示之后发出[**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md)指示。

-   微型端口驱动程序必须 ssue [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示，只指示先前通过 oid [ \_ 参数 oid \_ 参数](./oid-pm-parameters.md)启用的电源管理事件。

-   微型端口驱动程序必须仅为基础网络适配器生成的唤醒事件发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示。

 

