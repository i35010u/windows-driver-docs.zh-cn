---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER 状态指示对过量驱动程序的数据包筛选器更改。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7165b85b54e45f5829806206dafaf11a0cb100d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837182"
---
# <a name="ndis_status_packet_filter"></a>NDIS \_ 状态 \_ 数据包 \_ 筛选器


NDIS \_ 状态 \_ 数据包 \_ 筛选器状态指示对过量驱动程序的数据包筛选器更改。 NDIS 为微型端口适配器生成此状态指示，以通知过量驱动程序可能会更改微型端口适配器的数据包筛选器设置。

<a name="remarks"></a>备注
-------

当 NDIS 生成 NDIS \_ 状态 \_ 数据包 \_ 筛选器状态指示时，ndis 不保证数据包筛选器已更改。

NDIS 筛选器驱动程序还可以生成 NDIS \_ 状态 \_ 数据包 \_ 筛选器状态指示。

NDIS 在 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员中提供筛选器类型标志的按位 "或"。 有关筛选器类型标志的列表，请参阅 [OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md) oid。 有关数据包筛选器的其他信息，请参阅 [OID \_ GEN \_ 支持的 \_ 数据包 \_ 筛选器](./oid-gen-supported-packet-filters.md)。

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBufferSize** 成员设置为 sizeof (ULONG) 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)

[OID \_ 代 \_ 支持的 \_ 数据包 \_ 筛选器](./oid-gen-supported-packet-filters.md)

 

