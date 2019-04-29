---
title: NDIS_STATUS_WDI_INDICATION_P2P_SEND_REQUEST_ACTION_FRAME_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_SEND_REQUEST_ACTION_FRAME_COMPLETE 指示由 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 发送的请求操作框架有关的信息。
ms.assetid: 4c67b512-456f-48ed-bd1c-71a32bcf85f0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_SEND_REQUEST_ACTION_FRAME_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d4a8610da1562236a1a2c3a648b56b31c9da903e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360196"
---
# <a name="ndisstatuswdiindicationp2psendrequestactionframecomplete"></a>NDIS\_状态\_WDI\_指示\_P2P\_发送\_请求\_操作\_帧\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_P2P\_发送\_请求\_操作\_帧\_完成以指示有关发送的请求操作帧的信息[OID\_WDI\_任务\_P2P\_发送\_请求\_操作\_帧](oid-wdi-task-p2p-send-request-action-frame.md).

| Object |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                                       | 允许多个 TLV 实例 | 可选                                            | 描述                                                           |
|------------------------------------------------------------------------------------------------------------|--------------------------------|-----------------------------------------------------|-----------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_SEND\_ACTION\_FRAME\_RESULT**](https://msdn.microsoft.com/library/windows/hardware/dn897993) |                                | 此绑定的 TLV 处于仅需要状态是否成功。 | 有关对等方发送的请求操作帧的信息。 |

 

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

 

 




