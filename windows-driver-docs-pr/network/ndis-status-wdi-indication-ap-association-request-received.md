---
title: NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED，以指示为操作 Wi-fi Direct 组所有者接收了 Wi-fi 关联请求帧。
ms.assetid: c207ada5-39fd-4326-9b62-4844d3bb01af
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 048f81bd6846cdfc44b2f5b540c1c005d86248b9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207441"
---
# <a name="ndis_status_wdi_indication_ap_association_request_received"></a>\_ \_ 已收到 NDIS 状态 WDI \_ 指示 \_ AP \_ 关联 \_ 请求 \_


微型端口驱动程序 \_ 使用 \_ \_ 已接收的 NDIS 状态 WDI 指示 \_ AP \_ 关联 \_ 请求 \_ ，以指示为操作 Wi-fi Direct 组所有者接收了 wi-fi 关联请求帧。 主机可能会为此请求发出 [OID \_ WDI \_ TASK \_ 发送 \_ AP \_ 关联 \_ 响应](oid-wdi-task-send-ap-association-response.md) 。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                                                     | 允许多个 TLV 实例 | 可选 | 说明                                   |
|----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI \_ TLV \_ 传入 \_ 关联 \_ 请求 \_ 信息**](./wdi-tlv-incoming-association-request-info.md) |                                |          | 传入关联请求信息。 |

 

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

 

