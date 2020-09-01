---
title: OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT
description: OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT 请求网络端口上具有匹配接收筛选器的数据包数。
ms.assetid: 45b68057-d62a-4b77-9634-dfbed2817f23
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 567c9be9da13160bc359a35eca88afb7f727ce6d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215843"
---
# <a name="oid_wdi_get_receive_coalescing_match_count"></a>OID \_ WDI \_ 获取 \_ 接收 \_ 合并 \_ 匹配 \_ 计数


OID \_ WDI \_ GET \_ RECEIVE \_ 合并 \_ 匹配 \_ 计数请求在网络端口上具有匹配的接收筛选器的数据包数。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


无其他参数。 标头中的数据足够了。
## <a name="get-property-results"></a>获取属性结果


| TLV                                                                                              | 允许多个 TLV 实例 | 可选 | 说明                                                                  |
|--------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数**](./wdi-tlv-coalescing-filter-match-count.md) |                                |          | 与网络端口上的接收筛选器匹配的数据包数。 |

 

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

 

