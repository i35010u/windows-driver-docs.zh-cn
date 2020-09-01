---
title: NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE 来指示 OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 发送的 AP 关联响应的相关信息。
ms.assetid: c8bfa3b3-5d22-4831-9355-94c62fed7fd4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3f3d920158fa390286bd154213f9c8d47c89ce46
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212861"
---
# <a name="ndis_status_wdi_indication_send_ap_association_response_complete"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 发送 \_ AP \_ 关联 \_ 响应 \_ 完成


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 发送 \_ ap \_ 关联 \_ 响应 \_ 完成，以指示由 [OID \_ WDI \_ TASK \_ 发送 \_ ap \_ 关联 \_ 响应](oid-wdi-task-send-ap-association-response.md)发送的 AP 关联响应的相关信息。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [**WDI \_ TLV \_ 关联 \_ 响应 \_ 结果 \_ 参数**](./wdi-tlv-association-response-result-parameters.md) |   |   | 关联响应参数。 |
| [**WDI \_ TLV \_ 关联 \_ 响应 \_ 帧**](./wdi-tlv-association-response-frame.md) |   |   | 收到的关联响应。 这不包括 802.11 MAC 标头。 |
| [**WDI \_ TLV \_ 信标 \_**](./wdi-tlv-beacon-ies.md) |   |   | 来自关联的信号。 |
| [**WDI \_ TLV \_ PHY \_ 类型 \_ 列表**](./wdi-tlv-phy-type-list.md) |   |   | PHY 类型的列表。 |
 

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

 

