---
title: 发出 NDIS 唤醒原因状态指示
description: 发出 NDIS 唤醒原因状态指示
ms.assetid: F3DBE0DB-9787-4C3D-8DE3-AD47E5778B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 765a827e58d88af8de5189f07f264e9ec75ae772
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212165"
---
# <a name="issuing-ndis-wake-reason-status-indications"></a>发出 NDIS 唤醒原因状态指示


如果微型端口驱动程序支持 NDIS 唤醒原因状态指示 ([**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md)) ，则它必须在网络适配器生成唤醒事件之后立即生成此状态指示，并且适配器恢复到完全电源状态。

**注意**  支持 NDIS 唤醒原因状态指示对于移动宽带 (MB) 微型端口驱动程序是可选的。

微型端口驱动程序使用电源管理 (PM) 参数通过对象标识符 (OID) 设置 [oid \_ PM \_ 参数](./oid-pm-parameters.md)的请求。 此 OID 请求通过 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 结构指定 PM 参数。

[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构指定以下类型的唤醒事件的参数。

<a href="" id="received-packet-wake-up-events"></a>接收的数据包唤醒事件  
如果网络适配器接收到与 (LAN 唤醒) 模式相匹配的数据包，则会生成唤醒事件。 WOL 模式包括以下各项：

-   独立于介质的 WOL 模式，如数据包有效负载中的幻数据包或 TCP/IP 数据模式。 例如， [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 结构可以为 TCP SYN 帧指定 WOL 模式。

-   特定于媒体的 WOL 模式，如 EAPOL 请求标识符数据包或移动宽带 (MB) 短消息服务 (SMS) 消息。

-   通配符模式，与通过 OID 的 oid 集请求指定 [ \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)指定的接收筛选器匹配。

**注意**  对于这种类型的唤醒原因状态指示，网络适配器必须能够保存接收的数据包。 驱动程序必须在状态指示内返回接收的数据包。

WOL 模式由[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**EnabledWoLPacketPatterns**成员指定。

<a href="" id="media-specific-wake-up-events"></a>特定于媒体的唤醒事件  
网络适配器会生成唤醒事件，这是因为特定于媒体的原因，例如从802.11 接入点解除与 (AP) 或接收移动宽带 (MB) 短消息服务 (SMS) 消息。

此类型的唤醒事件通过[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**MediaSpecificWakeUpEvents**成员指定。

<a href="" id="media-independent-wake-up-events"></a>独立于媒体的唤醒事件  
由于与媒体无关的原因（例如，媒体连接或断开连接），网络适配器将生成唤醒事件。

此类型的唤醒事件通过[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**WakeUpFlags**成员指定。

如果网络适配器生成了唤醒信号，则微型端口驱动程序必须发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示。 驱动程序在处理 oid [ \_ PNP \_ 设置 \_ ](./oid-pnp-set-power.md) 的 oid 设置请求时执行此操作，以便将适配器转换为完全电源状态。

**注意**  在发出与唤醒事件相关的状态指示之前，微型端口驱动程序必须发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示。 例如，如果唤醒事件是因为媒体连接状态发生了变化，则微型端口驱动程序必须在发出**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**状态指示之后发出[**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md)指示。

当微型端口驱动程序发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示时，必须执行以下步骤：

1.  微型端口驱动程序必须分配一个足够大的缓冲区，以包含以下内容：

    -   [**NDIS \_ PM \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构。

    -   [**NDIS \_ PM \_ 唤醒 \_ 数据包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)的结构以及接收到的数据包 (*唤醒数据包*) 导致网络适配器生成唤醒事件。

        **注意**  如果小型端口驱动程序指示特定于媒体或与媒体无关的唤醒事件，则无需分配此缓冲区空间。

2.  微型端口驱动程序在缓冲区的开头初始化 [**NDIS \_ PM \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason) 结构。 驱动程序将 **WakeReason** 成员设置为定义唤醒事件类型的 [**NDIS \_ PM \_ 唤醒 \_ 原因 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_wake_reason_type) 枚举值。

    例如，如果微型端口驱动程序指示收到的数据包唤醒事件，则必须将 **WakeReason** 成员设置为 **NdisWakeReasonPacket**。 否则，驱动程序将 **WakeReason** 成员设置为最能描述特定于媒体或与媒体无关的唤醒事件的枚举值。

3.  如果 miniportdriver 对收到的数据包唤醒事件发出 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示，则必须执行以下步骤：

    1.  微型端口驱动程序将**InfoBufferOffset**成员设置为遵循缓冲区中[**ndis \_ pm \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构的[**ndis \_ pm \_ 唤醒 \_ 包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构的偏移量。

        **注意**  微型端口驱动程序必须将 [**NDIS \_ PM \_ 唤醒 \_ 包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet) 结构的开头与64位边界对齐。

    2.  微型端口驱动程序将 **InfoBufferSize** 成员设置为 [**NDIS \_ PM \_ 唤醒 \_ 包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet) 结构的大小加上导致唤醒事件的数据包大小。

    3.  小型小型驱动程序会按照缓冲区中的[**ndis \_ pm \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构初始化[**ndis \_ pm \_ 唤醒 \_ 数据包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构。

        微型端口驱动程序设置 [**NDIS \_ PM \_ 唤醒 \_ 包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet) 结构的成员，如下所示：

        -   **PatternId**成员设置为与唤醒数据包匹配的 WOL 模式的标识符。 此标识符由[**NDIS \_ pm \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的**PatternId**成员指定，该结构将在 oid pm 的 oid 集请求[ \_ \_ 添加 \_ WOL \_ 模式](./oid-pm-add-wol-pattern.md)期间传递给驱动程序。

        -   **PatternFriendlyName**成员设置为**PatternId**成员指定的唤醒模式的用户可读说明。 此值由[**NDIS \_ PM \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的**FriendlyName**成员指定。

            **注意**  微型端口驱动程序无需初始化此成员。 在将[**ndis \_ PM \_ 唤醒 \_ 数据包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构传递到过量驱动程序之前，NDIS 会将**PatternFriendlyName**成员设置为正确的值。

        -   **OriginalPacketSize**成员设置为网络适配器接收到的数据包的长度。

        -   必须将 **SavedPacketSize** 成员设置为通过 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示报告的数据包的长度。

            **注意** 此成员的值不能大于微端口驱动程序在[**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**MaxWoLPacketSaveBuffer**成员中设置的值。 当驱动程序报告其唤醒数据包指示功能时，驱动程序将返回此结构。 有关详细信息，请参阅 [报表唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)。

        -   **SavedPacketOffset**成员必须设置为采用[**NDIS \_ PM \_ 唤醒 \_ 包**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构的唤醒数据包的偏移量（以字节为单位）。

            **注意**  微型端口驱动程序必须将唤醒数据包的开头与缓冲区中的64位边界对齐。

    4.  小型端口会将唤醒数据包复制到缓冲区中 **SavedPacketOffset** 成员指定的偏移量处。

4.  如果微型端口驱动程序对特定于媒体或媒体的唤醒事件发出[**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md)状态指示，则会将[**ndis \_ PM \_ 唤醒 \_ 原因**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构的**InfoBufferOffset**和**InfoBufferSize**成员设置为零。

5.  微型端口驱动程序初始化 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构。 驱动程序将 **StatusCode** 成员设置为 NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因。 驱动程序还将 **StatusBuffer** 成员设置为指向缓冲区，并将 **StatusBufferLength** 设置为缓冲区的长度（以字节为单位）。

6.  微型端口驱动程序调用[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) ，并在*StatusIndication*参数中传递指向[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。

**注意**  在微型端口驱动程序发出接收的数据包唤醒事件的 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示后，它必须通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)来指示此接收的数据包。