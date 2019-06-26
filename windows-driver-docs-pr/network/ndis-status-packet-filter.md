---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER 状态指示过量驱动程序的数据包筛选器更改。
ms.assetid: 7633772a-cd3d-4030-b97a-9d503341fdeb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9b4575a2c0a3aadcf3e00e122f942c0925ff8856
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368548"
---
# <a name="ndisstatuspacketfilter"></a>NDIS\_状态\_数据包\_筛选器


NDIS\_状态\_数据包\_筛选器状态指示过量驱动程序的数据包筛选器更改。 NDIS 生成微型端口适配器，以通知基础驱动程序可能是微型端口适配器的数据包筛选器设置中更改此状态指示。

<a name="remarks"></a>备注
-------

NDIS 不保证数据包筛选器已更改时 NDIS 生成 NDIS\_状态\_数据包\_筛选器状态指示。

NDIS 筛选器驱动程序还可以生成 NDIS\_状态\_数据包\_筛选器状态指示。

NDIS 提供中的筛选器类型标志的按位 OR **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。 有关筛选器类型标志的列表，请参阅[OID\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)OID。 有关数据包筛选器的其他信息，请参阅[OID\_代\_支持\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)。

**StatusBufferSize**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构设置为 sizeof(ULONG)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_CURRENT\_PACKET\_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)

[OID\_GEN\_支持\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)

 

 




