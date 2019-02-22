---
title: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION
description: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 状态指示特定于媒体的状态。
ms.assetid: 983ffff1-5157-46ae-b4ce-31ee1aa55955
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 865d64e7277b6a34f038df2291c043b4fabcef94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546203"
---
# <a name="ndisstatusmediaspecificindication"></a>NDIS\_状态\_媒体\_特定\_指示


NDIS\_状态\_媒体\_特定\_指示状态指示特定于媒体的状态。

<a name="remarks"></a>备注
-------

微型端口驱动程序通过调用做出特定于媒体的状态指示[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数与**StatusCode**隶属[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构设置为 NDIS\_状态\_媒体\_特定\_指示。 **StatusBuffer**此结构的成员将指向驱动程序分配的缓冲区。 在缓冲区中包含特定于中标识的状态指示的格式中的数据**StatusCode**成员。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




