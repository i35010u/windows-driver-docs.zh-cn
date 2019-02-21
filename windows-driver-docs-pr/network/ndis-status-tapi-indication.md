---
title: NDIS_STATUS_TAPI_INDICATION
description: NDIS_STATUS_TAPI_INDICATION 状态指示发生了 TAPI 事件。 支持 WAN 的微型端口驱动程序可以指示 TAPI 状态。
ms.assetid: b90c5524-2e03-45e1-9ec9-478112eba01b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TAPI_INDICATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6f587338985eedc6b1556c5795f07ac3caa0a3e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546643"
---
# <a name="ndisstatustapiindication"></a>NDIS\_状态\_TAPI\_指示


NDIS\_状态\_TAPI\_状态指示发生了 TAPI 事件的指示。 支持 WAN 的微型端口驱动程序可以指示 TAPI 状态。

<a name="remarks"></a>备注
-------

NDIS 4。*x*和早期 NDIS WAN 的微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用的 CoNDIS WAN 接口。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)。

*StatusBuffer*的参数[ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)函数包含一个指向[ **NDIS\_TAPI\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff558986)结构。NDIS\_TAPI\_事件结构描述 TAPI 行或调用时发生的事件 （例如，行并调用状态，到达的传入呼叫，并关闭远程节点或对现有的微型端口驱动程序中的更改调用或行）。

详细了解 NDIS\_状态\_TAPI\_指示，请参阅[，该值指示 NDIS WAN 微型端口驱动程序状态 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546867)。

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
<td><p>不支持 NDIS 6.0 驱动程序或 NDIS 5.1 在 Windows Vista 或 Windows XP 中的驱动程序。 支持 NDIS 4.x 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_TAPI\_EVENT**](https://msdn.microsoft.com/library/windows/hardware/ff558986)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




