---
title: NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 指示主机应尝试查找更好的对等互连以连接到。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 30e7fab591a70152856e0dc78a538ca90548f73f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839479"
---
# <a name="ndis_status_wdi_indication_roaming_needed"></a>需要有 NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI 指示解除了连接， \_ \_ 以指示主机应尝试查找更好的对等连接。 当当前连接的对等节点的链接质量低于特定阈值时，将使用此通知。 发送此通知时，主机可能会触发漫游扫描和/或漫游操作。 Microsoft 组件在启动漫游操作之前不会执行断开连接。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                                    | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                         |
|-----------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ \_ 需要 \_ 参数**](./wdi-tlv-roaming-needed-parameters.md) |                                |          | 漫游触发器的原因。 当触发 [OID \_ WDI \_ 任务 \_ 漫游](oid-wdi-task-roam.md) 时，此原因将转发给它。 |

 

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


[OID \_ WDI \_ 任务 \_ 漫游](oid-wdi-task-roam.md)

 

