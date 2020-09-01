---
title: NDIS_STATUS_WDI_INDICATION_CAN_SUSTAIN_AP
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_CAN_SUSTAIN_AP 指示端口在前面指示 NDIS_STATUS_WDI_INDICATION_STOP_AP 之前已准备好接收 OID_WDI_TASK_START_AP 请求。
ms.assetid: 638822A9-4CED-4564-86B3-8BC9DBA05DD3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CAN_SUSTAIN_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c8eabb0700ab47a391a304d1dc33da3d8184c2da
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207439"
---
# <a name="ndis_status_wdi_indication_can_sustain_ap"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 可以 \_ 承受 \_ AP


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI 指示 \_ \_ 可以 \_ 维持 \_ AP，以指示端口已准备好接收 [OID \_ WDI \_ 任务 \_ 启动 \_ AP](oid-wdi-task-start-ap.md) 请求，在前面指出 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 停止 \_ ap](ndis-status-wdi-indication-stop-ap.md)。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                                     | 允许多个 TLV 实例 | 可选 | 说明                                                     |
|------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------|
| [**WDI \_ TLV \_ 指示 \_ 可以 \_ 维持 \_ AP**](./wdi-tlv-indication-can-sustain-ap.md) |                                |          | 适配器现在可以承受 802.11 AP 功能的原因。 |

 

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

 

