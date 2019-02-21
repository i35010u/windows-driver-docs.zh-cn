---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状态指示通知 NDIS 和基础驱动程序已被封装设置中的更改。
ms.assetid: 2db2a42e-85a2-41a6-b6ab-13b493057648
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 11c0078f342297f19958da8cc173225fcd650b6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555306"
---
# <a name="ndisstatusoffloadencaspulationchange"></a>NDIS\_状态\_卸载\_ENCASPULATION\_更改


微型端口驱动程序使用 NDIS\_状态\_卸载\_ENCASPULATION\_更改状态指示通知 NDIS 和基础驱动程序已被封装设置中的更改。

<a name="remarks"></a>备注
-------

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含[ **NDIS\_卸载\_封装**](https://msdn.microsoft.com/library/windows/hardware/ff566702)结构。 NDIS\_卸载\_封装指定封装设置。

有关封装设置的详细信息，请参阅[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_卸载\_封装**](https://msdn.microsoft.com/library/windows/hardware/ff566702)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)

 

 




