---
title: NDIS_STATUS_WDI_INDICATION_STOP_AP
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_STOP_AP 指示适配器无法在任何 PHYs 上维持802.11 接入点 (AP) 功能。
ms.assetid: EF129BD3-6AA2-4F38-BECD-E9D526314A27
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4b4663b1683ee90df1c1db9f40ac8339077f1eee
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213901"
---
# <a name="ndis_status_wdi_indication_stop_ap"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 停止 \_ AP


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 停止 \_ AP，指示适配器无法在任何 PHYs 上维持802.11 接入点 (AP) 功能。 仅当 NIC 停止了在可用 PHYs 上运行的任何 Ap 后，适配器才应发送此指示。 主机会阻止所有 [OID \_ WDI \_ 任务 \_ 启动 \_ AP](oid-wdi-task-start-ap.md) 请求，直到适配器发送 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 可以 \_ 维持 \_ ap](ndis-status-wdi-indication-can-sustain-ap.md)。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                      | 允许多个 TLV 实例 | 可选 | 说明                                                                       |
|---------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 指示 \_ 停止 \_ AP**](./wdi-tlv-indication-stop-ap.md) |                                |          | 适配器无法在任何 PHYs 上承受 802.11 AP 功能的原因。 |

 

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

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 任务 \_ 启动 \_ AP](oid-wdi-task-start-ap.md)

[NDIS \_ 状态 \_ WDI \_ 指示 \_ 可以 \_ 承受 \_ AP](ndis-status-wdi-indication-can-sustain-ap.md)

 

