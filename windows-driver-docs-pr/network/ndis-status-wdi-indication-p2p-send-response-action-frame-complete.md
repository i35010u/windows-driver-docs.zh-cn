---
title: NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE 指示由 OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 发送的响应操作框架有关的信息。
ms.assetid: 0b330ad6-4a55-4a3e-951f-0e5a951a8cf1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 15e7ab711ad6c76bc17b8437086766933c20b94d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375216"
---
# <a name="ndisstatuswdiindicationp2psendresponseactionframecomplete"></a>NDIS\_状态\_WDI\_指示\_P2P\_发送\_响应\_操作\_帧\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_P2P\_发送\_响应\_操作\_帧\_完成以指示有关发送的响应操作帧的信息[OID\_WDI\_任务\_P2P\_发送\_响应\_操作\_帧](oid-wdi-task-p2p-send-response-action-frame.md).

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                                       | 允许多个 TLV 实例 | 可选                                            | 描述                                                            |
|------------------------------------------------------------------------------------------------------------|--------------------------------|-----------------------------------------------------|------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_SEND\_ACTION\_FRAME\_RESULT**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-send-action-frame-result-parameters) |                                | 此绑定的 TLV 处于仅需要状态是否成功。 | 有关对等方发送的响应操作帧的信息。 |

 

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

 

 




