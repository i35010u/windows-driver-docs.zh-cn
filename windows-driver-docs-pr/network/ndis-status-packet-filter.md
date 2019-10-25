---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER 状态表示对过量驱动程序的数据包筛选器更改。
ms.assetid: 7633772a-cd3d-4030-b97a-9d503341fdeb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PACKET_FILTER 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f5f58a7bc534c525334ca42a684d7117868f0574
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842773"
---
# <a name="ndis_status_packet_filter"></a>\_数据包\_筛选器的 NDIS\_状态


\_数据包\_筛选器状态的 NDIS\_状态表明对过量驱动程序的数据包筛选器更改。 NDIS 为微型端口适配器生成此状态指示，以通知过量驱动程序可能会更改微型端口适配器的数据包筛选器设置。

<a name="remarks"></a>备注
-------

当 NDIS\_筛选器状态指示生成 NDIS\_\_状态时，NDIS 不保证数据包筛选器已更改。

NDIS 筛选器驱动程序还可以生成 NDIS\_状态\_数据包\_筛选器状态指示。

NDIS 在[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员中提供筛选器类型标志的按位 "或"。 有关筛选器类型标志的列表，请参阅[OID\_GEN\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)OID。 有关数据包筛选器的其他信息，请参阅[OID\_GEN\_支持的\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)。

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBufferSize**成员设置为 sizeof （ULONG）。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)

[OID\_代\_支持\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)

 

 




