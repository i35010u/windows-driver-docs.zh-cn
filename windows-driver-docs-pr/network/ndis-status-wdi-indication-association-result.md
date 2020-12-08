---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT 来指示关联结果。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7ec033f2f28991e1b00c22d014319034bbc0e4b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801425"
---
# <a name="ndis_status_wdi_indication_association_result"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 关联 \_ 结果


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 关联 \_ 结果来指示关联结果。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                     | 允许多个 TLV 实例 | 可选 | 说明                    |
|--------------------------------------------------------------------------|--------------------------------|----------|--------------------------------|
| [**WDI \_ TLV \_ 关联 \_ 结果**](./wdi-tlv-association-result.md) | X                              |          | 关联结果的列表。 |

 

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


[OID \_ WDI \_ 任务 \_ 连接](oid-wdi-task-connect.md)

[OID \_ WDI \_ 任务 \_ 漫游](oid-wdi-task-roam.md)

 

