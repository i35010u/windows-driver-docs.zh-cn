---
title: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION
description: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 状态指示特定于媒体的状态。
ms.assetid: 983ffff1-5157-46ae-b4ce-31ee1aa55955
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 719eaa093b2dc54db386ed7894aeb609a5809812
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373925"
---
# <a name="ndisstatusmediaspecificindication"></a>NDIS\_状态\_媒体\_特定\_指示


NDIS\_状态\_媒体\_特定\_指示状态指示特定于媒体的状态。

<a name="remarks"></a>备注
-------

微型端口驱动程序通过调用做出特定于媒体的状态指示[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)函数与**StatusCode**隶属[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构设置为 NDIS\_状态\_媒体\_特定\_指示。 **StatusBuffer**此结构的成员将指向驱动程序分配的缓冲区。 在缓冲区中包含特定于中标识的状态指示的格式中的数据**StatusCode**成员。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

 

 




