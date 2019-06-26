---
title: NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED 来指示已收到 Wi-Fi Direct 操作帧。
ms.assetid: 16e8f61d-373b-49fb-a0c5-4505fa7e653d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 93a2e16bb88167afb0444ba76060fcc80ba35451
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380877"
---
# <a name="ndisstatuswdiindicationp2pactionframereceived"></a>NDIS\_状态\_WDI\_指示\_P2P\_操作\_帧\_接收时间


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_P2P\_操作\_帧\_接收时间以指示已收到 Wi-Fi Direct 操作帧。

| Object |
|--------|
| Port   |

 

主机可能会发出[OID\_WDI\_任务\_P2P\_发送\_响应\_操作\_帧](oid-wdi-task-p2p-send-response-action-frame.md)此请求。

端口必须指示在任何以下情况下这些数据包：

-   端口处于侦听状态。
-   端口已转到操作状态。
-   端口抛开远程侦听通道何时[OID\_WDI\_任务\_P2P\_发送\_请求\_操作\_帧](oid-wdi-task-p2p-send-request-action-frame.md)或[OID\_WDI\_任务\_P2P\_发送\_响应\_操作\_帧](oid-wdi-task-p2p-send-response-action-frame.md)最近发出。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_传入\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-incoming-frame-information) |                                |          | 传入的 Wi-Fi Direct 操作帧信息。 此信息转发回该端口，当主机发出[OID\_WDI\_任务\_P2P\_发送\_响应\_操作\_帧](oid-wdi-task-p2p-send-response-action-frame.md). |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_TASK\_P2P\_SEND\_REQUEST\_ACTION\_FRAME](oid-wdi-task-p2p-send-request-action-frame.md)

[OID\_WDI\_TASK\_P2P\_SEND\_RESPONSE\_ACTION\_FRAME](oid-wdi-task-p2p-send-response-action-frame.md)

 

 




