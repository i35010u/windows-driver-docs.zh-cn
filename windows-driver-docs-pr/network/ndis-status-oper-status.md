---
title: NDIS_STATUS_OPER_STATUS
description: NDIS_STATUS_OPER_STATUS 状态指示过量驱动程序的 NDIS 网络接口的当前操作状态。
ms.assetid: dbe7ce19-290d-4a48-a6c2-1b95e956c26c
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e81f990eed12f8de9ee1abe72ac8dd1df63ce461
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524790"
---
# <a name="ndisstatusoperstatus"></a>NDIS\_状态\_工序\_状态


NDIS\_状态\_工序\_状态状态指示过量驱动程序的 NDIS 网络接口的当前操作状态。

<a name="remarks"></a>备注
-------

NDIS 生成此状态指示;NDIS 微型端口驱动程序不应生成此状态指示。

NDIS 提供[ **NDIS\_工序\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566737)结构**StatusBuffer**隶属[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。

**StatusBufferSize**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构设置为 sizeof (NDIS\_运算符\_状态）。

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


[**NDIS\_工序\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566737)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




