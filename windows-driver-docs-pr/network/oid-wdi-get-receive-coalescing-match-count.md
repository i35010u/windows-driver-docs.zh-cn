---
title: OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT
description: OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT 请求网络端口上具有匹配接收筛选器的数据包数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6502a904a5b388c61b89f8f1dd9fb92527448b17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792132"
---
# <a name="oid_wdi_get_receive_coalescing_match_count"></a>OID \_ WDI \_ 获取 \_ 接收 \_ 合并 \_ 匹配 \_ 计数


OID \_ WDI \_ GET \_ RECEIVE \_ 合并 \_ 匹配 \_ 计数请求在网络端口上具有匹配的接收筛选器的数据包数。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

