---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS 是包含 OID_WDI_SET_RECEIVE_PACKET_FILTER 的数据包筛选器参数的 TLV。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PACKET_FILTER_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: baa8387ef6ef853b44eace3e26497264bbeeeb9a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214260"
---
# <a name="wdi_tlv_packet_filter_parameters"></a>WDI \_ TLV \_ 数据包 \_ 筛选器 \_ 参数


WDI \_ tlv \_ 数据包 \_ 筛选器 \_ 参数是一个 Tlv，其中包含 [OID \_ WDI \_ 设置 \_ 接收 \_ 数据包 \_ 筛选器](./oid-wdi-set-receive-packet-filter.md)的数据包筛选器参数。

## <a name="tlv-type"></a>TLV 类型


0x47

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型                                                                      | 说明                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI \_数据包 \_ 筛选器 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_packet_filter_type) (UINT32)  | 指定所需的 Wi-fi 数据包筛选器。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

