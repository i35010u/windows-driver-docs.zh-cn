---
title: NDIS_STATUS_RING_STATUS
description: NDIS_STATUS_RING_STATUS 状态指示行的环状态。 支持 WAN 的微型端口驱动程序可以使用此状态报告环失败。
ms.assetid: 8971eeea-13ff-47d5-8167-83c061cad054
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RING_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9ea2cd06b4ab5d036b3a572d8420945cd6d03fb4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385074"
---
# <a name="ndisstatusringstatus"></a>NDIS\_状态\_环\_状态


NDIS\_状态\_环\_状态状态指示行的环状态。 支持 WAN 的微型端口驱动程序可以使用此状态报告环失败。

<a name="remarks"></a>备注
-------

NDIS 4。*x*和早期 NDIS WAN 的微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用的 CoNDIS WAN 接口。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546752(v=vs.85))。

*StatusBuffer*的参数[ **NdisMIndicateStatus** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数包含具有以下状态的值之一的 ULONG 值：

NDIS\_环\_凸\_线路\_容错

NDIS\_环\_硬盘\_错误

NDIS\_环\_信号\_丢失

这些值指定为状态可能的原因环条件。 详细了解 NDIS\_状态\_环\_状态，请参阅[Reporting 硬件状态 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564044(v=vs.85))。

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


[**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 

 




