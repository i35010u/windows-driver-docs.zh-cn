---
title: NDIS_STATUS_WAN_LINE_DOWN
description: NDIS_STATUS_WAN_LINE_DOWN 状态指示支持 WAN 的微型端口驱动程序已失去与远程节点建立的连接。
ms.assetid: 85904e2f-ae34-4cca-a5b9-2ec4b342672a
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WAN_LINE_DOWN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6ff9df73f5bb305ce6cbc2cf75e92d2c5f47d14a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372543"
---
# <a name="ndisstatuswanlinedown"></a>NDIS\_状态\_WAN\_行\_下


NDIS\_状态\_WAN\_行\_停机状态指示支持 WAN 的微型端口驱动程序已失去与远程节点建立的连接。

<a name="remarks"></a>备注
-------

NDIS 4。*x*和早期 NDIS WAN 的微型端口驱动程序使用此状态指示。 NDIS 5.0 和更高版本的 WAN 微型端口驱动程序必须使用的 CoNDIS WAN 接口。 有关的 CoNDIS WAN 接口的详细信息，请参阅[实现的 CoNDIS WAN 微型端口驱动程序 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546752(v=vs.85))。

*StatusBuffer*的参数[ **NdisMIndicateStatus** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数包含一个指向[ **NDIS\_MAC\_行\_向下**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557057(v=vs.85))结构。 **NdisLinkContext**成员的 NDIS\_MAC\_行\_列表标识将不再有效的链接。

详细了解 NDIS\_状态\_WAN\_行\_下，请参阅[，该值指示 NDIS WAN 微型端口驱动程序状态 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546867(v=vs.85))。

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


[**NDIS\_MAC\_LINE\_DOWN**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557057(v=vs.85))

[**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 

 




