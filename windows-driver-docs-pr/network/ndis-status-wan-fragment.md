---
title: NDIS_STATUS_WAN_FRAGMENT
description: NDIS_STATUS_WAN_FRAGMENT 状态指示支持 WAN 的微型端口驱动程序已收到来自远程节点的部分数据包。
ms.assetid: 1ac00110-8b97-4905-b409-454e3d9a09e0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_FRAGMENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 97cb2a741efb0c3b950a1afefe16148dcef3e06a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380911"
---
# <a name="ndisstatuswanfragment"></a>NDIS\_状态\_WAN\_片段


NDIS\_状态\_WAN\_片段状态指示支持 WAN 的微型端口驱动程序已收到来自远程节点的部分数据包。

<a name="remarks"></a>备注
-------

NDIS 4。*x*和早期 NDIS WAN 的微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的微型端口驱动程序应使用的 CoNDIS WAN 接口。 详细了解 NDIS\_状态\_WAN\_片段，请参阅[ **NDIS\_状态\_WAN\_共同\_片段**](ndis-status-wan-co-fragment.md).

*StatusBuffer*的参数[ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)函数包含一个指向[ **NDIS\_MAC\_片段**](https://msdn.microsoft.com/library/windows/hardware/ff557055)结构。 NDIS\_MAC\_片段标识特定的链接，并介绍了已接收到的部分数据包的原因。

详细了解 NDIS\_状态\_WAN\_片段，请参阅[，该值指示 NDIS WAN 微型端口驱动程序状态 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546867)。

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
<td><p>不支持 NDIS 6.0 驱动程序或 NDIS 5.1 在 Windows Vista 或 Windows XP 中的驱动程序。 支持 NDIS 4.x 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_MAC\_FRAGMENT**](https://msdn.microsoft.com/library/windows/hardware/ff557055)

[**NDIS\_状态\_WAN\_共同\_片段**](ndis-status-wan-co-fragment.md)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




