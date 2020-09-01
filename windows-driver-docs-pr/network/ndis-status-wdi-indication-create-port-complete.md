---
title: NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE 指示 OID_WDI_TASK_CREATE_PORT 完成。
ms.assetid: 8d3cdac1-06d3-4a21-ac13-e6d789c6922e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c9491a355f7034ffca6aacaa6b9e0f622fb88e84
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215508"
---
# <a name="ndis_status_wdi_indication_create_port_complete"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 创建 \_ 端口 \_ 完成


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 创建 \_ 端口 \_ 完成，以指示已完成 [OID \_ WDI \_ 任务 \_ 创建 \_ 端口](oid-wdi-task-create-port.md)。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                               | 允许多个 TLV 实例 | 可选 | 说明                         |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI \_ TLV \_ 端口 \_ 属性**](./wdi-tlv-port-attributes.md) |                                |          | 所创建端口的属性。 |

 

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

 

