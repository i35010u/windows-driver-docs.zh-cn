---
title: NDIS_STATUS_WAN_CO_MTULINKPARAMS
description: NDIS_STATUS_WAN_CO_MTULINKPARAMS 状态指示链接速度和发送窗口参数已发生了更改的 CoNDIS 微型端口适配器处于活动状态的特定 VC。
ms.assetid: 1ba67087-08aa-4359-9884-e47bf634fda5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_CO_MTULINKPARAMS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f5d08cd826ad4d166d18ef50e6d3af773637640f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554834"
---
# <a name="ndisstatuswancomtulinkparams"></a>NDIS\_状态\_WAN\_共同\_MTULINKPARAMS


NDIS\_状态\_WAN\_共同\_MTULINKPARAMS 状态指示链接速度和发送窗口参数已发生了更改的 CoNDIS 微型端口适配器处于活动状态的特定 VC。

<a name="remarks"></a>备注
-------

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含一个指向[ **WAN\_共同\_MTULINKPARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff565821)结构。 WAN\_CO\_MTULINKPARAMS 结构为 VC 描述新的参数。

详细了解 NDIS\_状态\_WAN\_共同\_MTULINKPARAMS，请参阅[，该值指示的 CoNDIS WAN 微型端口驱动程序状态](https://msdn.microsoft.com/library/windows/hardware/ff554825)。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff553805)。

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
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**WAN\_CO\_MTULINKPARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff565821)

 

 




