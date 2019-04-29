---
title: NDIS_STATUS_WAN_LINE_UP
description: NDIS_STATUS_WAN_LINE_UP 状态指示支持 WAN 的微型端口驱动程序已建立与远程节点的连接。
ms.assetid: 1eb9d934-871a-4d95-b04f-d0b174716c98
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_LINE_UP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5596820fc36c8b6ea790b8992db8916fd2ac9459
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392390"
---
# <a name="ndisstatuswanlineup"></a>NDIS\_状态\_WAN\_行\_向上


NDIS\_状态\_WAN\_行\_向上状态指示支持 WAN 的微型端口驱动程序已建立与远程节点的连接。

<a name="remarks"></a>备注
-------

NDIS 4。*x*和早期 NDIS WAN 的微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用的 CoNDIS WAN 接口。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)。

*StatusBuffer*的参数[ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)函数包含一个指向[ **NDIS\_MAC\_行\_向上**](https://msdn.microsoft.com/library/windows/hardware/ff557058)结构。

详细了解 NDIS\_状态\_WAN\_行\_，请参阅[Line-Up 指示 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff549189)和[，该值指示 NDIS WAN 微型端口驱动程序状态 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546867).

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


[**NDIS\_MAC\_LINE\_UP**](https://msdn.microsoft.com/library/windows/hardware/ff557058)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




