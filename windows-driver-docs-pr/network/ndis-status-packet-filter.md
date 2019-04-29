---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER 状态指示过量驱动程序的数据包筛选器更改。
ms.assetid: 7633772a-cd3d-4030-b97a-9d503341fdeb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f5d9922ba3eab75edcfab51dcc1ac9203987b45d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386222"
---
# <a name="ndisstatuspacketfilter"></a>NDIS\_状态\_数据包\_筛选器


NDIS\_状态\_数据包\_筛选器状态指示过量驱动程序的数据包筛选器更改。 NDIS 生成微型端口适配器，以通知基础驱动程序可能是微型端口适配器的数据包筛选器设置中更改此状态指示。

<a name="remarks"></a>备注
-------

NDIS 不保证数据包筛选器已更改时 NDIS 生成 NDIS\_状态\_数据包\_筛选器状态指示。

NDIS 筛选器驱动程序还可以生成 NDIS\_状态\_数据包\_筛选器状态指示。

NDIS 提供中的筛选器类型标志的按位 OR **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。 有关筛选器类型标志的列表，请参阅[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)OID。 有关数据包筛选器的其他信息，请参阅[OID\_代\_支持\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569643)。

**StatusBufferSize**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构设置为 sizeof(ULONG)。

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


[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_GEN\_CURRENT\_PACKET\_FILTER](https://msdn.microsoft.com/library/windows/hardware/ff569575)

[OID\_GEN\_支持\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569643)

 

 




