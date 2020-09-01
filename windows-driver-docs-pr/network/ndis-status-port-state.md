---
title: NDIS_STATUS_PORT_STATE
description: 支持 NDIS 端口的微型端口驱动程序使用 NDIS_STATUS_PORT_STATE 状态指示来指示 NDIS 端口状态的更改。
ms.assetid: 28e76963-af06-4a00-83ef-14e009cf35ec
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PORT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 57277e1e36bd7f3acbc56753278cb6b1e62bd0a6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215530"
---
# <a name="ndis_status_port_state"></a>NDIS \_ 状态 \_ 端口 \_ 状态


支持 NDIS 端口的微型端口驱动程序使用 NDIS \_ 状态 \_ 端口 \_ 状态指示来指示 ndis 端口状态的更改。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须在[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**PortNumber**成员中设置端口号。 此结构的 **StatusBuffer** 成员包含指向 [**NDIS \_ 端口 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state) 结构的指针。

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
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 端口 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

