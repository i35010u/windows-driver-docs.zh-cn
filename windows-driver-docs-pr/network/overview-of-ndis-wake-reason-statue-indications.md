---
title: NDIS 唤醒原因状态指示概述
description: NDIS 唤醒原因状态指示概述
ms.assetid: 94B54281-7A7E-4DBA-85AE-313EEF09E733
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f174738bab9d6bbffdab9a28d29606be4c4921b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335346"
---
# <a name="overview-of-ndis-wake-reason-status-indications"></a>NDIS 唤醒原因状态指示概述


从开始 NDIS 6.30，微型端口驱动程序发出 NDIS 唤醒原因状态指示 ([**NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) 到通知 NDIS 和系统唤醒事件的原因有关的基础驱动程序。 如果网络适配器生成唤醒事件时，微型端口驱动程序会立即发出的 NDIS 状态指示**NDIS\_状态\_PM\_唤醒\_原因**时网络适配器将恢复到全功率状态。

**请注意**  支持 NDIS 唤醒原因状态指示是可选的移动宽带 (MB) 微型端口驱动程序。

 

微型端口驱动程序配置与电源管理 (PM) 参数的对象标识符 (OID) 组请求通过[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)。 此 OID 请求指定了 PM 参数通过[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构指定的唤醒事件的以下类型的参数。

<a href="" id="received-packet-wake-up-events"></a>接收的数据包唤醒事件  
如果收到与 LAN 唤醒 (WOL) 模式匹配的数据包将网络适配器生成唤醒事件。 WOL 模式包括：

-   独立于媒体的 WOL 模式，如魔幻数据包或数据包负载中的 TCP/IP 数据模式。 例如， [ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构可以指定 TCP SYN 帧的 WOL 模式。

-   特定于媒体的 WOL 模式，如 EAPOL 请求标识符数据包或移动宽带 (MB) 短消息服务 (SMS) 消息。

-   指定通过 OID 集请求的接收筛选器匹配的通配符模式[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

**请注意**  唤醒原因状态指示此类型，网络适配器必须能够保存所接收的数据包。 该驱动程序必须返回的状态指示在接收到的数据包。

 

通过指定 WOL 模式**EnabledWoLPacketPatterns**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

<a href="" id="media-specific-wake-up-events"></a>特定于媒体的唤醒事件  
网络适配器由于一个特定于媒体的原因，例如从 802.11 访问点 (AP) 或移动的宽带 (MB) 短消息服务 (SMS) 消息的接收解除关联生成唤醒事件。

通过指定此类型的唤醒事件**MediaSpecificWakeUpEvents**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

<a href="" id="media-independent-wake-up-events"></a>独立于媒体的唤醒事件  
由于一个独立于媒体的原因，例如媒体连接或断开连接，网络适配器生成唤醒事件。

通过指定此类型的唤醒事件**WakeUpFlags**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

有关 NDIS 唤醒原因状态指示，微型端口驱动程序必须遵循以下准则：

-   如果微型端口驱动程序支持能够发送唤醒数据包迹象，NDIS 调用的驱动程序时，它必须报告这一功能[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 有关详细信息，请参阅[报告唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)。

    **请注意**  微型端口驱动程序不需要报告其能够发出 NDIS 唤醒原因不相关的 WOL 数据包的接收到的事件的状态指示。

     

-   当微型端口驱动程序发出的 WOL 数据包的唤醒数据包指示时，它必须包括导致唤醒事件的数据包。 有关详细信息，请参阅[发出 NDIS 唤醒原因状态指示](issuing-ndis-wake-reason-indications.md)。

-   如果网络适配器生成唤醒信号，微型端口驱动程序必须发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示。 该驱动程序执行此时它正在处理的 OID 集请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)全功率状态转换。

-   微型端口驱动程序必须发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示才能发出的状态指示的是与唤醒事件相关。 例如，如果唤醒事件是由于媒体连接状态中的更改，微型端口驱动程序必须发出[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示已发出后**NDIS\_状态\_PM\_唤醒\_原因**状态指示。

-   微型端口驱动程序必须得出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)电源管理事件的状态指示以前通过 OID 集请求的已启用[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)。

-   微型端口驱动程序必须发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)唤醒事件生成状态指示由基础的网络适配器。

 

 





