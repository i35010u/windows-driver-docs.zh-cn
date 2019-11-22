---
title: 发出 NDIS 唤醒原因状态指示
description: 发出 NDIS 唤醒原因状态指示
ms.assetid: F3DBE0DB-9787-4C3D-8DE3-AD47E5778B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5989c7469feb469662614271a5f4ace83cec5ef6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844156"
---
# <a name="issuing-ndis-wake-reason-status-indications"></a>发出 NDIS 唤醒原因状态指示


如果微型端口驱动程序支持 NDIS 唤醒原因状态指示（[**ndis\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)），则它必须在网络适配器生成唤醒事件之后立即生成此状态指示，适配器恢复到完全电源状态。

**注意** 支持 NDIS 唤醒原因状态指示对于移动宽带（MB）微型端口驱动程序是可选的。

微型端口驱动程序通过[oid\_pm\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)的对象标识符（oid）设置请求，使用电源管理（PM）参数配置。 此 OID 请求通过[**NDIS\_pm\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构来指定 pm 参数。

[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构指定以下类型的唤醒事件的参数。

<a href="" id="received-packet-wake-up-events"></a>接收的数据包唤醒事件  
如果网络适配器接收到与 LAN 唤醒（WOL）模式匹配的数据包，则会生成唤醒事件。 WOL 模式包括以下各项：

-   独立于介质的 WOL 模式，如数据包有效负载中的幻数据包或 TCP/IP 数据模式。 例如， [**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构可以为 TCP SYN 帧指定 WOL 模式。

-   特定于媒体的 WOL 模式，如 EAPOL 请求标识符数据包或移动宽带（MB）短消息服务（SMS）消息。

-   通配符模式匹配通过 OID 集 oid 指定的接收筛选器[\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)。

**注意** 对于这种类型的唤醒原因状态指示，网络适配器必须能够保存接收的数据包。 驱动程序必须在状态指示内返回接收的数据包。

WOL 模式通过[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**EnabledWoLPacketPatterns**成员指定。

<a href="" id="media-specific-wake-up-events"></a>特定于媒体的唤醒事件  
由于特定于媒体的原因（例如，从802.11 接入点（AP）解除相关或接收移动宽带（MB）短消息服务（SMS）消息），网络适配器将生成唤醒事件。

此类型的唤醒事件通过[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**MediaSpecificWakeUpEvents**成员指定。

<a href="" id="media-independent-wake-up-events"></a>独立于媒体的唤醒事件  
由于与媒体无关的原因（例如，媒体连接或断开连接），网络适配器将生成唤醒事件。

此类型的唤醒事件通过[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的**WakeUpFlags**成员指定。

如果网络适配器生成了唤醒信号，则微型端口驱动程序必须[ **\_PM\_唤醒\_原因状态指示发出 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)。 驱动程序在处理[oid\_PNP\_集](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)的 oid 集请求时执行此操作，\_电源将适配器转换为完全电源状态。

**注意** 在发出与唤醒事件相关的状态指示之前，微型端口驱动程序必须[ **\_PM 发出 NDIS\_状态\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示。 例如，如果唤醒事件是因为媒体连接状态发生了变化，则微型端口驱动程序必须[ **\_链接发出 ndis\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)，然后在其发出**NDIS\_\_状态之后\_状态状态指示\_唤醒\_原因**状态指示。

如果微型端口驱动程序发出[**NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示，则必须执行以下步骤：

1.  微型端口驱动程序必须分配一个足够大的缓冲区，以包含以下内容：

    -   [**NDIS\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构。

    -   [**NDIS\_PM\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构以及接收到的数据包（*唤醒数据包*），导致网络适配器生成唤醒事件。

        **注意** 如果小型端口驱动程序指示特定于媒体或与媒体无关的唤醒事件，则无需分配此缓冲区空间。

2.  微型端口驱动程序在缓冲区开头[ **\_唤醒\_原因结构初始化 NDIS\_PM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason) 。 驱动程序将**WakeReason**成员设置为[**NDIS\_PM\_唤醒\_原因\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_wake_reason_type)枚举值定义唤醒事件的类型。

    例如，如果微型端口驱动程序指示收到的数据包唤醒事件，则必须将**WakeReason**成员设置为**NdisWakeReasonPacket**。 否则，驱动程序将**WakeReason**成员设置为最能描述特定于媒体或与媒体无关的唤醒事件的枚举值。

3.  如果 miniportdriver 正在发出[**NDIS\_状态\_PM\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)收到的数据包唤醒事件的唤醒\_原因状态指示，则必须执行以下步骤：

    1.  微型端口驱动程序将**InfoBufferOffset**成员设置为[**ndis\_pm\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构的偏移量，该结构遵循[**ndis\_PM\_在缓冲区中唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构。

        **注意** 微型端口驱动程序必须在64位边界上将[**NDIS\_PM 的开头与\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构对齐。

    2.  微型端口驱动程序将**InfoBufferSize**成员设置为[**NDIS\_PM\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构的大小加上导致唤醒事件的数据包大小。

    3.  小型小型驱动程序在 Ndis\_PM 之后初始化[**ndis\_PM\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构，\_缓冲区中的[**唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)结构。

        微型端口驱动程序将[**NDIS\_PM 的成员设置\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构，如下所示：

        -   **PatternId**成员设置为与唤醒数据包匹配的 WOL 模式的标识符。 此标识符由 NDIS\_PM 的**PatternId**成员指定[ **\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构，该结构将在 OID\_PM 的 oid 集请求中传递给驱动程序[\_添加\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern).

        -   **PatternFriendlyName**成员设置为**PatternId**成员指定的唤醒模式的用户可读说明。 此值由[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的**FriendlyName**成员指定。

            **注意** 微型端口驱动程序无需初始化此成员。 NDIS 将**PatternFriendlyName**成员设置为正确的值，然后将[**NDIS\_PM\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构传递到过量驱动程序。

        -   **OriginalPacketSize**成员设置为网络适配器接收到的数据包的长度。

        -   必须将**SavedPacketSize**成员设置为通过[**NDIS\_状态\_PM**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)报告的数据包的长度\_唤醒\_原因状态指示。

            **注意** 此成员的值不能大于在[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**MaxWoLPacketSaveBuffer**成员中设置的微型端口驱动程序的值。 当驱动程序报告其唤醒数据包指示功能时，驱动程序将返回此结构。 有关详细信息，请参阅[报表唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)。

        -   必须将**SavedPacketOffset**成员设置为以字节为单位的偏移量（以字节为单位），以将[**NDIS\_PM 之后的唤醒数据包\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)结构。

            **注意** 微型端口驱动程序必须将唤醒数据包的开头与缓冲区中的64位边界对齐。

    4.  小型端口会将唤醒数据包复制到缓冲区中**SavedPacketOffset**成员指定的偏移量处。

4.  如果微型端口驱动程序正在发出[**NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示用于特定于媒体或媒体的唤醒事件，则会设置**InfoBufferOffset**和**InfoBufferSize**[**NDIS\_PM 的成员\_将\_原因结构唤醒**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)为零。

5.  微型端口驱动程序初始化[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构。 驱动程序将**StatusCode**成员设置为 NDIS\_状态\_PM\_唤醒\_原因。 驱动程序还将**StatusBuffer**成员设置为指向缓冲区，并将**StatusBufferLength**设置为缓冲区的长度（以字节为单位）。

6.  微型端口驱动程序调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) ，并将指向[**NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)的指针传递\_*StatusIndication*参数中的指示结构。

**注意** 在微型端口驱动程序发出[ **\_状态\_PM 的 NDIS 状态，\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)收到的数据包唤醒事件的 "唤醒\_原因状态指示"，则它必须通过调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)来指示收到的数据包。