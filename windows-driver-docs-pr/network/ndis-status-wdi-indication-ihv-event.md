---
title: NDIS_STATUS_WDI_INDICATION_IHV_EVENT
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_IHV_EVENT 将 IHV 特定信息传递到 IHV 扩展性模块。
ms.assetid: 767f15cd-456f-4d91-9b78-58f8f8b7a465
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_IHV_EVENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5235f6403e7235e9b632e00c4135466d5f398646
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217020"
---
# <a name="ndis_status_wdi_indication_ihv_event"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ IHV \_ 事件


微型端口驱动程序使用 NDIS \_ STATUS \_ WDI \_ 指示 \_ ihv \_ 事件将 IHV 特定信息传递到 ihv 扩展性模块。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                 | 允许多个 TLV 实例 | 可选 | 说明                                           |
|------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI \_ TLV \_ IHV \_ 数据**](./wdi-tlv-ihv-data.md) |                                | X        | 要发送到 IHV 扩展性模块的事件。 |

 

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

 

