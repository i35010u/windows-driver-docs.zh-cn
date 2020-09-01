---
title: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION
description: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 状态指示特定于介质的状态。
ms.assetid: 983ffff1-5157-46ae-b4ce-31ee1aa55955
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a604e00b408f977a868d3339ceb3e7ff36f3d45b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214706"
---
# <a name="ndis_status_media_specific_indication"></a>NDIS \_ 状态 \_ 媒体 \_ 特定 \_ 指示


NDIS \_ 状态 \_ 媒体特定 \_ 的 \_ 指示状态指示特定于媒体的状态。

<a name="remarks"></a>备注
-------

微型端口驱动程序通过调用[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数，并将[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusCode**成员设置为 ndis \_ 状态 \_ 媒体 \_ 特定 \_ 指示，来做出特定于媒体的状态指示。 此结构的 **StatusBuffer** 成员指向驱动程序分配的缓冲区。 该缓冲区包含的数据采用特定于 **StatusCode** 成员中标识的状态指示的格式。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

