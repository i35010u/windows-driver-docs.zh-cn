---
title: NDIS_STATUS_WAN_CO_FRAGMENT
description: NDIS_STATUS_WAN_CO_FRAGMENT 状态指示的 CoNDIS WAN 的微型端口驱动程序已收到来自 VC 的终结点的部分数据包。
ms.assetid: 5a534364-d528-45f8-a2e0-3c745b3b5ad0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_FRAGMENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d625f22f6cd7e617606140be6778dedb0596088e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523525"
---
# <a name="ndisstatuswancofragment"></a>NDIS\_状态\_WAN\_共同\_片段


NDIS\_状态\_WAN\_共同\_片段状态指示的 CoNDIS WAN 的微型端口驱动程序已收到部分数据包从 VC 的终结点。

<a name="remarks"></a>备注
-------

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含一个指向[ **NDIS\_WAN\_共同\_片段**](https://msdn.microsoft.com/library/windows/hardware/ff559030)结构。 NDIS\_WAN\_共同\_片段结构介绍了已接收到的部分数据包的原因。

详细了解 NDIS\_状态\_WAN\_共同\_片段，请参阅[，该值指示的 CoNDIS WAN 微型端口驱动程序状态](https://msdn.microsoft.com/library/windows/hardware/ff554825)。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff553805)。

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

[**NDIS\_WAN\_CO\_FRAGMENT**](https://msdn.microsoft.com/library/windows/hardware/ff559030)

 

 




