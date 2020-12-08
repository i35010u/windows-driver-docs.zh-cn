---
title: NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED 指示已收到 Wi-Fi 直接操作帧。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f89a4e2e5576f4fe33c525200a5b457b0c7c213a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837123"
---
# <a name="ndis_status_wdi_indication_p2p_action_frame_received"></a>\_ \_ 已收到 NDIS 状态 WDI \_ 指示 \_ P2P \_ 操作 \_ 帧 \_


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 操作 \_ 帧 \_ 接收到指示已收到 Wi-Fi 直接操作帧。

| 对象 |
|--------|
| 端口   |

 

主机可能会为此请求颁发 [OID \_ WDI \_ TASK \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧](oid-wdi-task-p2p-send-response-action-frame.md) 。

在以下任何情况下，该端口都必须指示这些数据包：

-   端口处于侦听状态。
-   端口处于操作状态。
-   在最近发出了 [oid \_ WDI \_ 任务 \_ p2p \_ 发送 \_ 请求 \_ 操作 \_ 框](oid-wdi-task-p2p-send-request-action-frame.md) 或 [OID \_ WDI \_ 任务 \_ p2p 发送 \_ \_ 响应 \_ 操作 \_ ](oid-wdi-task-p2p-send-response-action-frame.md) 帧时，此端口 dwelling 在远程侦听通道上。

## <a name="payload-data"></a>负载数据


| 类型                                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 传入 \_ 帧 \_ 信息**](./wdi-tlv-p2p-incoming-frame-information.md) |                                |          | 传入的 Wi-Fi 直接操作帧信息。 当主机发出 [OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧](oid-wdi-task-p2p-send-response-action-frame.md)时，此信息将转发回端口。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 请求 \_ 操作 \_ 帧](oid-wdi-task-p2p-send-request-action-frame.md)

[OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧](oid-wdi-task-p2p-send-response-action-frame.md)

 

