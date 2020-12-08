---
title: OID_WDI_SET_RECEIVE_PACKET_FILTER
description: OID_WDI_SET_RECEIVE_PACKET_FILTER 为指定的虚拟化端口指定要显示的数据包的位掩码筛选器。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_RECEIVE_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a330483de444b1e58336e26a98804cc6fa8eb116
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829323"
---
# <a name="oid_wdi_set_receive_packet_filter"></a>OID \_ WDI \_ SET \_ 接收 \_ 数据包 \_ 筛选器


OID \_ WDI \_ SET \_ 接收 \_ 数据包 \_ 筛选器定义一个位掩码筛选器，用于指示给定虚拟化端口的数据包。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

如果设置此项，则该端口只应通知与提供的筛选器匹配的数据包的主机。 这些筛选器类似于为 [OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)提供的必需802.11 筛选器。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                   | 允许多个 TLV 实例 | 可选 | 说明                          |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI \_ TLV \_ 数据包 \_ 筛选器 \_ 参数**](./wdi-tlv-packet-filter-parameters.md) |                                |          | 数据包的位掩码筛选器。 |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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

 

