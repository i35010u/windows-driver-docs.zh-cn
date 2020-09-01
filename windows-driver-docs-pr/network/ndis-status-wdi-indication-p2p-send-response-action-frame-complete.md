---
title: NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE 来指示有关 OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 发送的响应操作帧的信息。
ms.assetid: 0b330ad6-4a55-4a3e-951f-0e5a951a8cf1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 22ce0510b547c84ecb6c0f71776424e4861d3e17
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209703"
---
# <a name="ndis_status_wdi_indication_p2p_send_response_action_frame_complete"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧 \_ 完成


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧 \_ 完成，以指示由 [OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 框架](oid-wdi-task-p2p-send-response-action-frame.md)发送的响应操作帧的相关信息。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                                                       | 允许多个 TLV 实例 | 可选                                            | 说明                                                            |
|------------------------------------------------------------------------------------------------------------|--------------------------------|-----------------------------------------------------|------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果**](./wdi-tlv-p2p-send-action-frame-result-parameters.md) |                                | 仅当状态为 "成功" 时才需要此 TLV。 | 有关发送到对等方的响应操作帧的信息。 |

 

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
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

