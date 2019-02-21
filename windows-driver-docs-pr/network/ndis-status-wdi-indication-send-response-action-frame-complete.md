---
title: NDIS_STATUS_WDI_INDICATION_SEND_RESPONSE_ACTION_FRAME_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_SEND_RESPONSE_ACTION_FRAME_COMPLETE 指示 OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME 完成。
ms.assetid: 9D07F05B-212F-403E-AD37-4AB537C25536
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_SEND_RESPONSE_ACTION_FRAME_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b16d065661a5391ffbb6767a7267e8ab901d3178
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523519"
---
# <a name="ndisstatuswdiindicationsendresponseactionframecomplete"></a>NDIS\_状态\_WDI\_指示\_发送\_响应\_操作\_帧\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_发送\_响应\_操作\_帧\_完成以指示完成[OID\_WDI\_任务\_发送\_响应\_操作\_帧](oid-wdi-task-send-response-action-frame.md)。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


此指示不包含任何其他数据。 标头中的数据就足够了。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WDI\_TASK\_SEND\_RESPONSE\_ACTION\_FRAME](oid-wdi-task-send-response-action-frame.md)

 

 




