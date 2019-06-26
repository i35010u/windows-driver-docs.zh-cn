---
title: NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE 来指示发送 OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 的 AP 关联响应有关的信息。
ms.assetid: c8bfa3b3-5d22-4831-9355-94c62fed7fd4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c910d0286cb18afaf7cea1773ce8c438f3e80684
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375213"
---
# <a name="ndisstatuswdiindicationsendapassociationresponsecomplete"></a>NDIS\_状态\_WDI\_指示\_发送\_AP\_关联\_响应\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_发送\_AP\_关联\_响应\_完成以指示有关的信息发送的 AP 关联响应[OID\_WDI\_任务\_发送\_AP\_关联\_响应](oid-wdi-task-send-ap-association-response.md)。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_关联\_响应\_结果\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-association-response-result-parameters) |   |   | 关联响应参数。 |
| [**WDI\_TLV\_关联\_响应\_帧**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-association-response-frame) |   |   | 接收到的关联的响应。 这不包括 802.11 MAC 报头。 |
| [**WDI\_TLV\_BEACON\_IES**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-beacon-ies) |   |   | 从关联信号导致浏览器。 |
| [**WDI\_TLV\_PHY\_TYPE\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-phy-type-list) |   |   | PHY 类型的列表。 |
 

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

 

 




