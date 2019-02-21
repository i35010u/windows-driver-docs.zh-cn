---
title: NDIS_STATUS_RING_STATUS
description: NDIS_STATUS_RING_STATUS 状态指示行的环状态。 支持 WAN 的微型端口驱动程序可以使用此状态报告环失败。
ms.assetid: 8971eeea-13ff-47d5-8167-83c061cad054
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RING_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4f3b2fecb835899e7f057453351ed3df87a71972
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555965"
---
# <a name="ndisstatusringstatus"></a>NDIS\_状态\_环\_状态


NDIS\_状态\_环\_状态状态指示行的环状态。 支持 WAN 的微型端口驱动程序可以使用此状态报告环失败。

<a name="remarks"></a>备注
-------

NDIS 4。*x*和早期 NDIS WAN 的微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用的 CoNDIS WAN 接口。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)。

*StatusBuffer*的参数[ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)函数包含具有以下状态的值之一的 ULONG 值：

NDIS\_环\_凸\_线路\_容错

NDIS\_环\_硬盘\_错误

NDIS\_环\_信号\_丢失

这些值指定为状态可能的原因环条件。 详细了解 NDIS\_状态\_环\_状态，请参阅[Reporting 硬件状态 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff564044)。

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


[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




