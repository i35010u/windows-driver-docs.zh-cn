---
title: 发出 NDIS 唤醒原因状态指示
description: 发出 NDIS 唤醒原因状态指示
ms.assetid: F3DBE0DB-9787-4C3D-8DE3-AD47E5778B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ea8b9e3526a346cafafe919b52ef7e739761ecf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576337"
---
# <a name="issuing-ndis-wake-reason-status-indications"></a>发出 NDIS 唤醒原因状态指示


微型端口驱动程序是否支持 NDIS 唤醒原因状态指示 ([**NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808))，它必须生成此状态指示网络适配器生成唤醒事件和适配器后立即恢复全功率状态。

**请注意**支持 NDIS 唤醒原因状态指示是可选的移动宽带 (MB) 微型端口驱动程序。

微型端口驱动程序配置与电源管理 (PM) 参数的对象标识符 (OID) 组请求通过[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)。 此 OID 请求指定了 PM 参数通过[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构指定的唤醒事件的以下类型的参数。

<a href="" id="received-packet-wake-up-events"></a>接收的数据包唤醒事件  
如果收到与 LAN 唤醒 (WOL) 模式匹配的数据包将网络适配器生成唤醒事件。 WOL 模式包括：

-   独立于媒体的 WOL 模式，如魔幻数据包或数据包负载中的 TCP/IP 数据模式。 例如， [ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构可以指定 TCP SYN 帧的 WOL 模式。

-   特定于媒体的 WOL 模式，如 EAPOL 请求标识符数据包或移动宽带 (MB) 短消息服务 (SMS) 消息。

-   指定通过 OID 集请求的接收筛选器匹配的通配符模式[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

**请注意**唤醒原因状态指示此类型，网络适配器必须能够保存所接收的数据包。 该驱动程序必须返回的状态指示在接收到的数据包。

通过指定 WOL 模式**EnabledWoLPacketPatterns**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

<a href="" id="media-specific-wake-up-events"></a>特定于媒体的唤醒事件  
网络适配器由于一个特定于媒体的原因，例如从 802.11 访问点 (AP) 或移动的宽带 (MB) 短消息服务 (SMS) 消息的接收解除关联生成唤醒事件。

通过指定此类型的唤醒事件**MediaSpecificWakeUpEvents**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

<a href="" id="media-independent-wake-up-events"></a>独立于媒体的唤醒事件  
由于一个独立于媒体的原因，例如媒体连接或断开连接，网络适配器生成唤醒事件。

通过指定此类型的唤醒事件**WakeUpFlags**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

如果网络适配器生成唤醒信号，微型端口驱动程序必须发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示。 该驱动程序执行此时它正在处理的 OID 集请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)适配器到全功率状态的转换。

**请注意**微型端口驱动程序必须发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示才能发出与唤醒事件相关的状态指示。 例如，如果唤醒事件是由于媒体连接状态中的更改，微型端口驱动程序必须发出[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示已发出后**NDIS\_状态\_PM\_唤醒\_原因**状态指示。

当微型端口驱动程序发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示，它必须执行以下步骤：

1.  微型端口驱动程序必须分配缓冲区足够大，以包含以下信息：

    -   [ **NDIS\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh451605)结构。

    -   [ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)结构以及所接收的数据包 (*唤醒数据包*) 导致网络若要生成唤醒事件的适配器。

        **请注意**微型端口驱动程序不需要分配此缓冲区空间，如果它表示特定于媒体的或独立于媒体的唤醒事件。

2.  微型端口驱动程序初始化[ **NDIS\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh451605)的缓冲区开始处的结构。 驱动程序集**WakeReason**成员添加到[ **NDIS\_PM\_唤醒\_原因\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh451607)枚举定义唤醒事件的类型的值。

    例如，如果微型端口驱动程序指示接收的数据包唤醒事件，则必须设置**WakeReason**成员添加到**NdisWakeReasonPacket**。 否则，该驱动程序设置**WakeReason**最适当地描述特定于媒体的或独立于媒体的唤醒事件的枚举值的成员。

3.  如果颁发 miniportdriver [ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示对于接收的数据包唤醒事件，它必须执行以下步骤：

    1.  微型端口驱动程序集**InfoBufferOffset**成员的偏移量[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)结构后面[ **NDIS\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh451605)缓冲区中的结构。

        **请注意**微型端口驱动程序必须保持一致的开头[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603) 64 位边界上的结构。

    2.  微型端口驱动程序集**InfoBufferSize**成员添加到的大小[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)结构加号导致唤醒事件数据包的大小。

    3.  微型端口驱动程序初始化[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)结构以下[ **NDIS\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh451605)缓冲区中的结构。

        微型端口驱动程序设置的成员[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)结构，如下所示：

        -   **PatternId**成员设置为唤醒数据包匹配的 WOL 模式的标识符。 通过指定此标识符**PatternId**的成员[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)传递的结构为在 OID 的驱动程序设置的请求[OID\_PM\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569764)。

        -   **PatternFriendlyName**成员设置为唤醒模式所指定的用户可读说明**PatternId**成员。 通过指定此值**FriendlyName**的成员[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)结构。

            **请注意**微型端口驱动程序不需要初始化此成员。 NDIS 集**PatternFriendlyName**成员添加到正确的值将传递之前[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)过量驱动程序结构。

        -   **OriginalPacketSize**根据网络适配器接收到的成员被设置为数据包的长度。

        -   **SavedPacketSize**成员必须设置为通过正在报告的数据包长度[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示。

            **请注意**此成员的值不能大于微型端口驱动程序中设置的值**MaxWoLPacketSaveBuffer**的成员[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。 报告其唤醒数据包指示功能时，驱动程序将返回此结构。 有关详细信息，请参阅[报告唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)。

        -   **SavedPacketOffset**成员必须设置为的偏移量，以遵循唤醒数据包字节为单位[ **NDIS\_PM\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/hh451603)结构。

            **请注意**微型端口驱动程序必须保持一致的唤醒数据包缓冲区中的 64 位边界上开始。

    4.  微型端口将唤醒数据包复制到指定的偏移量处的缓冲区**SavedPacketOffset**成员。

4.  如果颁发的微型端口驱动程序[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)媒体特定的状态指示或设置独立于媒体的唤醒事件**InfoBufferOffset**并**InfoBufferSize**的成员[ **NDIS\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh451605)为零的结构。

5.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。 驱动程序集**StatusCode**成员添加到 NDIS\_状态\_PM\_唤醒\_原因。 驱动程序还设置**StatusBuffer**要指向的缓冲区和集成员**StatusBufferLength**到缓冲区的长度，以字节为单位。

6.  微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600) ，并将传递一个指向[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构中*StatusIndication*参数。

**请注意**微型端口驱动程序问题后[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)收到的状态指示数据包唤醒事件，则必须通过调用表示此接收的数据包[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)。